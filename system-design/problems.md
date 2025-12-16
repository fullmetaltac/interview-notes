# Table of Contents
- [Table of Contents](#table-of-contents)
  - [Design Pastebin.com](#design-pastebincom)
  - [Design the Twitter timeline and search](#design-the-twitter-timeline-and-search)
  - [Design a web crawler](#design-a-web-crawler)
  - [Design Mint.com](#design-mintcom)
  - [Design the data structures for a social network](#design-the-data-structures-for-a-social-network)
  - [Design a key-value cache](#design-a-key-value-cache)
  - [Design Amazon's sales rank by category feature](#design-amazons-sales-rank-by-category-feature)
  - [References](#references)

## Design Pastebin.com

Design **Bit.ly** - is a similar question, except pastebin requires storing the paste contents instead of the original unshortened url.

<h2>Step 1: Outline use cases and constraints</h2>

<h3>Use cases</h3>

- **User** enters a block of text and gets a randomly generated link
  - Expiration
    - Default setting does not expire
    - Can optionally set a timed expiration
- **User** enters a paste's url and views the contents
- **User** is anonymous
- **Service** tracks analytics of pages
  - Monthly visit stats
- **Service** deletes expired pastes
- **Service** has high availability

**Out of scope**

- User registers for an account
  - User verifies email
- User logs into a registered account
  - User edits the document
- User can set visibility
- User can set the shortlink

<h3>Constraints and assumptions</h3>

**State assumptions**
- Traffic is not evenly distributed
- Following a short link should be fast
- Pastes are text only
- Page view analytics do not need to be realtime
- 10 million users
- 10 million paste writes per month
- 100 million paste reads per month
- 10:1 read to write ratio

**Calculate usage**

- Size per paste
  - 1 KB content per paste
  - `shortlink` - 7 bytes
  - `expiration_length_in_minutes` - 4 bytes
  - `created_at` - 5 bytes
  - `paste_path` - 255 bytes
  - total = ~1.27 KB
- 12.7 GB of new paste content per month
  - 1.27 KB per paste * 10 million pastes per month
  - ~450 GB of new paste content in 3 years
  - 360 million shortlinks in 3 years
  - Assume most are new pastes instead of updates to existing ones
- 4 paste writes per second on average
- 40 read requests per second on average

Handy conversion guide:
- 2.5 million seconds per month
- 1 request per second = 2.5 million requests per month
- 40 requests per second = 100 million requests per month
- 400 requests per second = 1 billion requests per month

<h2>Step 2: Create a high level design</h2>

<p align="center">
    <img src="images/pastebin1.png" width="50%"> 
</p>

<h2>Step 3: Design core components</h2>

<h3> Use case: User enters a block of text and gets a randomly generated link</h3>

We could use a relational database as a large hash table, mapping the generated url to a file server and path containing the paste file.

Instead of managing a file server, we could use a managed **Object Store** such as Amazon S3 or a NoSQL document store.

An alternative to a relational database acting as a large hash table, we could use a NoSQL key-value store. We should discuss the tradeoffs between choosing SQL or NoSQL. The following discussion uses the relational database approach.

- The **Client** sends a create paste request to the **Web Server**, running as a reverse proxy
- The **Web Server** forwards the request to the Write API server
- The Write API server does the following:
  - Generates a unique url
    - Checks if the url is unique by looking at the **SQL Database** for a duplicate
    - If the url is not unique, it generates another url
    - If we supported a custom url, we could use the user-supplied (also check for a duplicate)
  - Saves to the **SQL Database** `pastes` table
  - Saves the paste data to the **Object Store**
  - Returns the url

The `pastes` table could have the following structure:

```sql
shortlink char(7) NOT NULL
expiration_length_in_minutes int NOT NULL
created_at datetime NOT NULL
paste_path varchar(255) NOT NULL
PRIMARY KEY(shortlink)
```

Setting the primary key to be based on the `shortlink` column creates an index that the database uses to enforce uniqueness. We'll create an additional index on `created_at` to speed up lookups (log-time instead of scanning the entire table) and to keep the data in memory. Reading 1 MB sequentially from memory takes about 250 microseconds, while reading from SSD takes 4x and from disk takes 80x longer.

- Take the MD5 hash of the user's ip_address + timestamp
  - MD5 is a widely used hashing function that produces a 128-bit hash value
  - MD5 is uniformly distributed
  - Alternatively, we could also take the MD5 hash of randomly-generated data

- Base 62 encode the MD5 hash
  - Base 62 encodes to `[a-zA-Z0-9]` which works well for urls, eliminating the need for escaping special characters
  - There is only one hash result for the original input and Base 62 is deterministic (no randomness involved)
  - Base 64 is another popular encoding but provides issues for urls because of the additional `+` and `/` characters
  - The following Base 62 pseudocode runs in $O(k)$ time where k is the number of digits = 7:

```python
def base_encode(num, base=62):
    digits = []
    while num > 0
      remainder = modulo(num, base)
      digits.push(remainder)
      num = divide(num, base)
    digits = digits.reverse
```

- Take the first 7 characters of the output, which results in 62^7 possible values and should be sufficient to handle our constraint of 360 million shortlinks in 3 years:

```python
url = base_encode(md5(ip_address+timestamp))[:URL_LENGTH]
```

We'll use a public REST API:

```shell
$ curl -X POST --data '{ "expiration_length_in_minutes": "60", \
    "paste_contents": "Hello World!" }' https://pastebin.com/api/v1/paste
```

Response:

```json
{
    "shortlink": "foobar"
}
```

For internal communications, we could use Remote Procedure Calls.


<h3> Use case: User enters a paste's url and views the contents</h3>

- The **Client** sends a get paste request to the **Web Server**
- The **Web Server** forwards the request to the **Read API** server
- The **Read API** server does the following:
  - Checks the **SQL Database** for the generated url
    - If the url is in the **SQL Database**, fetch the paste contents from the **Object Store**
    - Else, return an error message for the user

REST API:

```shell
$ curl https://pastebin.com/api/v1/paste?shortlink=foobar
```
Response:

```json
{
    "paste_contents": "Hello World"
    "created_at": "YYYY-MM-DD HH:MM:SS"
    "expiration_length_in_minutes": "60"
}
```

<h3> Use case: Service tracks analytics of pages</h3>

Since realtime analytics are not a requirement, we could simply MapReduce the Web Server logs to generate hit counts.

```python
class HitCounts(MRJob):

    def extract_url(self, line):
        """Extract the generated url from the log line."""
        ...

    def extract_year_month(self, line):
        """Return the year and month portions of the timestamp."""
        ...

    def mapper(self, _, line):
        """Parse each log line, extract and transform relevant lines.

        Emit key value pairs of the form:

        (2016-01, url0), 1
        (2016-01, url0), 1
        (2016-01, url1), 1
        """
        url = self.extract_url(line)
        period = self.extract_year_month(line)
        yield (period, url), 1

    def reducer(self, key, values):
        """Sum values for each key.

        (2016-01, url0), 2
        (2016-01, url1), 1
        """
        yield key, sum(values)
```

<h3> Use case: Service deletes expired pastes</h3>

To delete expired pastes, we could just scan the **SQL Database** for all entries whose expiration timestamp are older than the current timestamp. All expired entries would then be deleted (or marked as expired) from the table.

<h2>Step 4: Scale the design</h2>

<p align="center">
    <img src="images/pastebin2.png" width="50%"> 
</p>

## Design the Twitter timeline and search

**Design the Facebook feed** and **Design Facebook search** are similar questions.

<h2>Step 1: Outline use cases and constraints</h2>

<h3>Use cases</h3>

- **User** posts a tweet
  - **Service** pushes tweets to followers, sending push notifications and emails
- **User** views the user timeline (activity from the user)
- **User** views the home timeline (activity from people the user is following)
- **User** searches keywords
- **Service** has high availability

**Out of scope**

- Service pushes tweets to the Twitter Firehose and other streams
- Service strips out tweets based on users' visibility settings
  - Hide @reply if the user is not also following the person being replied to
  - Respect 'hide retweets' setting
- Analytics

<h3>Constraints and assumptions</h3>

**State assumptions**

General

- Traffic is not evenly distributed
- Posting a tweet should be fast
  - Fanning out a tweet to all of your followers should be fast, unless you have millions of followers
- 100 million active users
- 500 million tweets per day or 15 billion tweets per month
  - Each tweet averages a fanout of 10 deliveries
  - 5 billion total tweets delivered on fanout per day
  - 150 billion tweets delivered on fanout per month
- 250 billion read requests per month
- 10 billion searches per month

Timeline

- Viewing the timeline should be fast
- Twitter is more read heavy than write heavy
  - Optimize for fast reads of tweets
- Ingesting tweets is write heavy

Search

- Searching should be fast
- Search is read-heavy

<h3>Calculate usage</h3>

- Size per tweet:
  - `tweet_id` - 8 bytes
  - `user_id` - 32 bytes
  - `text` - 140 bytes
  - `media` - 10 KB average
  - Total: ~10 KB
- 150 TB of new tweet content per month
  - 10 KB per tweet * 500 million tweets per day * 30 days per month
  - 5.4 PB of new tweet content in 3 years
- 100 thousand read requests per second
  - 250 billion read requests per month * (400 requests per second / 1 billion requests per month)
- 6,000 tweets per second
  - 15 billion tweets per month * (400 requests per second / 1 billion requests per month)
- 60 thousand tweets delivered on fanout per second
  - 150 billion tweets delivered on fanout per month * (400 requests per second / 1 billion requests per month)
- 4,000 search requests per second
  - 10 billion searches per month * (400 requests per second / 1 billion requests per month)

Handy conversion guide:

- 2.5 million seconds per month
- 1 request per second = 2.5 million requests per month
- 40 requests per second = 100 million requests per month
- 400 requests per second = 1 billion requests per month

<h2>Step 2: Create a high level design</h2>

<p align="center">
    <img src="images/twitter1.png" width="80%"> 
</p>

<h2>Step 3: Design core components</h2>

<h3>Use case: User posts a tweet</h3>

We could store the user's own tweets to populate the user timeline (activity from the user) in a relational database.

Delivering tweets and building the home timeline (activity from people the user is following) is trickier. Fanning out tweets to all followers (60 thousand tweets delivered on fanout per second) will overload a traditional relational database. We'll probably want to choose a data store with fast writes such as a **NoSQL database** or **Memory Cache**. Reading 1 MB sequentially from memory takes about 250 microseconds, while reading from SSD takes 4x and from disk takes 80x longer.

We could store media such as photos or videos on an Object Store.

- The **Client** posts a tweet to the **Web Server**, running as a reverse proxy
- The **Web Server** forwards the request to the **Write API** server
- The **Write API** stores the tweet in the user's timeline on a SQL database
- The **Write API** contacts the **Fan Out Service**, which does the following:
  - Queries the **User Graph Service** to find the user's followers stored in the **Memory Cache**
  - Stores the tweet in the home timeline of the user's followers in a **Memory Cache**
    - $O(n)$ operation: 1,000 followers = 1,000 lookups and inserts
  - Stores the tweet in the **Search Index Service** to enable fast searching
  - Stores media in the **Object Store**
  - Uses the **Notification Service** to send out push notifications to followers:
    - Uses a **Queue** (not pictured) to asynchronously send out notifications

If our **Memory Cache** is Redis, we could use a native Redis list with the following structure:

```
           tweet n+2                   tweet n+1                   tweet n
| 8 bytes   8 bytes  1 byte | 8 bytes   8 bytes  1 byte | 8 bytes   8 bytes  1 byte |
| tweet_id  user_id  meta   | tweet_id  user_id  meta   | tweet_id  user_id  meta   |
```

The new tweet would be placed in the **Memory Cache**, which populates the user's home timeline (activity from people the user is following).

We'll use a public REST API:

```shell
$ curl -X POST --data '{ "user_id": "123", "auth_token": "ABC123", \
    "status": "hello world!", "media_ids": "ABC987" }' \
    https://twitter.com/api/v1/tweet
```

Response:

```json
{
    "created_at": "Wed Sep 05 00:37:15 +0000 2012",
    "status": "hello world!",
    "tweet_id": "987",
    "user_id": "123",
    ...
}
```

For internal communications, we could use Remote Procedure Calls.

<h3>Use case: User views the home timeline</h3>

- The **Client** posts a home timeline request to the **Web Server**
- The **Web Server** forwards the request to the **Read API** server
- The **Read API** server contacts the **Timeline Service**, which does the following:
  - Gets the timeline data stored in the **Memory Cache**, containing tweet ids and user ids - $O(1)$
  - Queries the **Tweet Info Service** with a multiget to obtain additional info about the tweet ids - $O(n)$
  - Queries the **User Info Service** with a multiget to obtain additional info about the user ids - $O(n)$

REST API:

```shell
$ curl https://twitter.com/api/v1/home_timeline?user_id=123
```

Response:

```json
{
    "user_id": "456",
    "tweet_id": "123",
    "status": "foo"
},
{
    "user_id": "789",
    "tweet_id": "456",
    "status": "bar"
},
{
    "user_id": "789",
    "tweet_id": "579",
    "status": "baz"
},
```

<h3>Use case: User views the user timeline</h3>

- The **Client** posts a user timeline request to the **Web Server**
- The **Web Server** forwards the request to the **Read API** server
- The **Read API** retrieves the user timeline from the **SQL Database**

The REST API would be similar to the home timeline, except all tweets would come from the user as opposed to the people the user is following.

<h3>Use case: User searches keywords</h3>

- The **Client** sends a search request to the **Web Server**
- The **Web Server** forwards the request to the **Search API** server
- The **Search API** contacts the **Search Service**, which does the following:
  - Parses/tokenizes the input query, determining what needs to be searched
    - Removes markup
    - Breaks up the text into terms
    - Fixes typos
    - Normalizes capitalization
    - Converts the query to use boolean operations
  - Queries the **Search Cluster** (ie Lucene) for the results:
    - Scatter gathers each server in the cluster to determine if there are any results for the query
    - Merges, ranks, sorts, and returns the results

REST API:

```shell
$ curl https://twitter.com/api/v1/search?query=hello+world
```

The response would be similar to that of the home timeline, except for tweets matching the given query.

<h2>Step 4: Scale the design</h2>

<p align="center">
    <img src="images/twitter2.png" width="50%"> 
</p>

## Design a web crawler

<h2>Step 1: Outline use cases and constraints</h2>

<h3>Use cases</h3>

- **Service** crawls a list of urls:
  - Generates reverse index of words to pages containing the search terms
  - Generates titles and snippets for pages
    - Title and snippets are static, they do not change based on search query
- **User** inputs a search term and sees a list of relevant pages with titles and snippets the crawler generated
  - Only sketch high level components and interactions for this use case, no need to go into depth
- **Service** has high availability

**Out of scope**
- Search analytics
- Personalized search results
- Page rank

<h3>Constraints and assumptions</h3>

**State assumptions**

- Traffic is not evenly distributed
  - Some searches are very popular, while others are only executed once
- Support only anonymous users
- Generating search results should be fast
- The web crawler should not get stuck in an infinite loop
  - We get stuck in an infinite loop if the graph contains a cycle
- 1 billion links to crawl
  - Pages need to be crawled regularly to ensure freshness
  - Average refresh rate of about once per week, more frequent for popular sites
    - 4 billion links crawled each month
  - Average stored size per web page: 500 KB
    - For simplicity, count changes the same as new pages
- 100 billion searches per month

**Calculate usage**

- 2 PB of stored page content per month
  - 500 KB per page * 4 billion links crawled per month
  - 72 PB of stored page content in 3 years
- 1,600 write requests per second
- 40,000 search requests per second

Handy conversion guide:

- 2.5 million seconds per month
- 1 request per second = 2.5 million requests per month
- 40 requests per second = 100 million requests per month
- 400 requests per second = 1 billion requests per month

<h2>Step 2: Create a high level design</h2>

<p align="center">
    <img src="images/web_crawler.png" width="50%"> 
</p>

<h2>Step 3: Design core components</h2>

We'll assume we have an initial list of `links_to_crawl` ranked initially based on overall site popularity. If this is not a reasonable assumption, we can seed the crawler with popular sites that link to outside content such as Yahoo, DMOZ, etc.

We'll use a table `crawled_links` to store processed links and their page signatures.

We could store `links_to_crawl` and `crawled_links` in a key-value **NoSQL Database**. For the ranked links in `links_to_crawl`, we could use Redis with sorted sets to maintain a ranking of page links.

- The **Crawler Service** processes each page link by doing the following in a loop:
  - Takes the top ranked page link to crawl
    - Checks `crawled_links` in the **NoSQL Database** for an entry with a similar page signature
      - If we have a similar page, reduces the priority of the page link
        - This prevents us from getting into a cycle
        - Continue
      - Else, crawls the link
        - Adds a job to the **Reverse Index Service** queue to generate a reverse index
        - Adds a job to the **Document Service** queue to generate a static title and snippet
        - Generates the page signature
        - Removes the link from `links_to_crawl` in the **NoSQL Database**
        - Inserts the page link and signature to `crawled_links` in the **NoSQL Database**

`PagesDataStore` is an abstraction within the **Crawler Service** that uses the **NoSQL Database**:

```python
class PagesDataStore(object):

    def __init__(self, db);
        self.db = db
        ...

    def add_link_to_crawl(self, url):
        """Add the given link to `links_to_crawl`."""
        ...

    def remove_link_to_crawl(self, url):
        """Remove the given link from `links_to_crawl`."""
        ...

    def reduce_priority_link_to_crawl(self, url)
        """Reduce the priority of a link in `links_to_crawl` to avoid cycles."""
        ...

    def extract_max_priority_page(self):
        """Return the highest priority link in `links_to_crawl`."""
        ...

    def insert_crawled_link(self, url, signature):
        """Add the given link to `crawled_links`."""
        ...

    def crawled_similar(self, signature):
        """Determine if we've already crawled a page matching the given signature"""
        ...
```

`Page` is an abstraction within the **Crawler Service** that encapsulates a page, its contents, child urls, and signature:

```python
class Page(object):

    def __init__(self, url, contents, child_urls, signature):
        self.url = url
        self.contents = contents
        self.child_urls = child_urls
        self.signature = signature
```

`Crawler` is the main class within **Crawler Service**, composed of `Page` and `PagesDataStore`.

```python
class Crawler(object):

    def __init__(self, data_store, reverse_index_queue, doc_index_queue):
        self.data_store = data_store
        self.reverse_index_queue = reverse_index_queue
        self.doc_index_queue = doc_index_queue

    def create_signature(self, page):
        """Create signature based on url and contents."""
        ...

    def crawl_page(self, page):
        for url in page.child_urls:
            self.data_store.add_link_to_crawl(url)
        page.signature = self.create_signature(page)
        self.data_store.remove_link_to_crawl(page.url)
        self.data_store.insert_crawled_link(page.url, page.signature)

    def crawl(self):
        while True:
            page = self.data_store.extract_max_priority_page()
            if page is None:
                break
            if self.data_store.crawled_similar(page.signature):
                self.data_store.reduce_priority_link_to_crawl(page.url)
            else:
                self.crawl_page(page)
```

<h3>Handling duplicates</h3>

We need to be careful the web crawler doesn't get stuck in an infinite loop, which happens when the graph contains a cycle.

We'll want to remove duplicate urls:

  - For smaller lists we could use something like `sort | unique`
- With 1 billion links to crawl, we could use **MapReduce** to output only entries that have a frequency of 1

```python
class RemoveDuplicateUrls(MRJob):

    def mapper(self, _, line):
        yield line, 1

    def reducer(self, key, values):
        total = sum(values)
        if total == 1:
            yield key, total
```

Detecting duplicate content is more complex. We could generate a signature based on the contents of the page and compare those two signatures for similarity. Some potential algorithms are Jaccard index and cosine similarity.

<h3>Determining when to update the crawl results</h3>

Pages need to be crawled regularly to ensure freshness. Crawl results could have a `timestamp` field that indicates the last time a page was crawled. After a default time period, say one week, all pages should be refreshed. Frequently updated or more popular sites could be refreshed in shorter intervals.

Although we won't dive into details on analytics, we could do some data mining to determine the mean time before a particular page is updated, and use that statistic to determine how often to re-crawl the page.

We might also choose to support a `Robots.txt` file that gives webmasters control of crawl frequency.

<h3>Use case: User inputs a search term and sees a list of relevant pages with titles and snippets</h3>

- The **Client** sends a request to the **Web Server**, running as a reverse proxy
- The **Web Server** forwards the request to the **Query API** server
- The **Query API** server does the following:
  - Parses the query
      - Removes markup
      - Breaks up the text into terms
      - Fixes typos
      - Normalizes capitalization
      - Converts the query to use boolean operations
  - Uses the **Reverse Index Service** to find documents matching the query
    - The **Reverse Index Service** ranks the matching results and returns the top ones
  - Uses the **Document Service** to return titles and snippets

We'll use a public REST API:

```shell
$ curl https://search.com/api/v1/search?query=hello+world
```

Response:

```json
{
    "title": "foo's title",
    "snippet": "foo's snippet",
    "link": "https://foo.com",
},
{
    "title": "bar's title",
    "snippet": "bar's snippet",
    "link": "https://bar.com",
},
{
    "title": "baz's title",
    "snippet": "baz's snippet",
    "link": "https://baz.com",
},
```
For internal communications, we could use Remote Procedure Calls.

<h2>Step 4: Scale the design</h2>

<p align="center">
    <img src="images/web_crawler2.png" width="50%"> 
</p>

## Design Mint.com

<h2>Step 1: Outline use cases and constraints</h2>

<h3>Use cases</h3>

- **User** connects to a financial account
- **Service** extracts transactions from the account
  - Updates daily
  - Categorizes transactions
    - Allows manual category override by the user
    - No automatic re-categorization
  - Analyzes monthly spending, by category
- **Service** recommends a budget
  - Allows users to manually set a budget
  - Sends notifications when approaching or exceeding budget
- **Service** has high availability

**Out of scope**
- **Service** performs additional logging and analytics

<h3>Constraints and assumptions</h3>

**State assumptions**
- Traffic is not evenly distributed
- Automatic daily update of accounts applies only to users active in the past 30 days
- Adding or removing financial accounts is relatively rare
- Budget notifications don't need to be instant
- 10 million users
  - 10 budget categories per user = 100 million budget items
  - Example categories:
    - Housing = $1,000
    - Food = $200
    - Gas = $100
  - Sellers are used to determine transaction category
    - 50,000 sellers
- 30 million financial accounts
- 5 billion transactions per month
- 500 million read requests per month
- 10:1 write to read ratio
  - Write-heavy, users make transactions daily, but few visit the site daily

**Calculate usage**

- Size per transaction:
  - `user_id` - 8 bytes
  - `created_at` - 5 bytes
  - `seller` - 32 bytes
  - `amount` - 5 bytes
  - Total: ~50 bytes
- 250 GB of new transaction content per month
  - 50 bytes per transaction * 5 billion transactions per month
  - 9 TB of new transaction content in 3 years
  - Assume most are new transactions instead of updates to existing ones
- 2,000 transactions per second on average
- 200 read requests per second on average

Handy conversion guide:
- 2.5 million seconds per month
- 1 request per second = 2.5 million requests per month
- 40 requests per second = 100 million requests per month
- 400 requests per second = 1 billion requests per month

<h3>Step 2: Create a high level design</h3>

<p align="center">
    <img src="images/mint.png" width="50%"> 
</p>

<h2>Step 3: Design core components</h2>

<h3>Use case: User connects to a financial account</h3>

We could store info on the 10 million users in a relational database.

The **Client** sends a request to the **Web Server**, running as a reverse proxy
The **Web Server** forwards the request to the **Accounts API** server
The **Accounts API** server updates the **SQL Database** `accounts` table with the newly entered account info

The `accounts` table could have the following structure:

```sql
id int NOT NULL AUTO_INCREMENT
created_at datetime NOT NULL
last_update datetime NOT NULL
account_url varchar(255) NOT NULL
account_login varchar(32) NOT NULL
account_password_hash char(64) NOT NULL
user_id int NOT NULL
PRIMARY KEY(id)
FOREIGN KEY(user_id) REFERENCES users(id)
```

We'll create an index on `id`, `user_id` , and `created_at` to speed up lookups (log-time instead of scanning the entire table) and to keep the data in memory. Reading 1 MB sequentially from memory takes about 250 microseconds, while reading from SSD takes 4x and from disk takes 80x longer.1

We'll use a public REST API:

```shell
$ curl -X POST --data '{ "user_id": "foo", "account_url": "bar", \
    "account_login": "baz", "account_password": "qux" }' \
    https://mint.com/api/v1/account
```
For internal communications, we could use Remote Procedure Calls.

Next, the service extracts transactions from the account.

<h3>Use case: Service extracts transactions from the account</h3>

We'll want to extract information from an account in these cases:

- The user first links the account
- The user manually refreshes the account
- Automatically each day for users who have been active in the past 30 days

Data flow:

- The **Client** sends a request to the **Web Server**
- The **Web Server** forwards the request to the **Accounts API** server
- The **Accounts API** server places a job on a **Queue** such as Amazon SQS or RabbitMQ
  - Extracting transactions could take awhile, we'd probably want to do this - asynchronously with a queue, although this introduces additional complexity
- The **Transaction Extraction Service** does the following:
  - Pulls from the **Queue** and extracts transactions for the given account from the - financial institution, storing the results as raw log files in the **Object Store**
  - Uses the **Category Service** to categorize each transaction
  - Uses the **Budget Service** to calculate aggregate monthly spending by category
    - The **Budget Service** uses the **Notification Service** to let users know if they are - nearing or have exceeded their budget
  - Updates the **SQL Database** `transactions` table with categorized transactions
  - Updates the **SQL Database** `monthly_spending` table with aggregate monthly spending by - category
  - Notifies the user the transactions have completed through the Notification Service:
    - Uses a **Queue** (not pictured) to asynchronously send out notifications

The `transactions` table could have the following structure:

```sql
id int NOT NULL AUTO_INCREMENT
created_at datetime NOT NULL
seller varchar(32) NOT NULL
amount decimal NOT NULL
user_id int NOT NULL
PRIMARY KEY(id)
FOREIGN KEY(user_id) REFERENCES users(id)
```

We'll create an index on `id`, `user_id` , and `created_at`.

The `monthly_spending` table could have the following structure:

```sql
id int NOT NULL AUTO_INCREMENT
month_year date NOT NULL
category varchar(32)
amount decimal NOT NULL
user_id int NOT NULL
PRIMARY KEY(id)
FOREIGN KEY(user_id) REFERENCES users(id)
```

We'll create an index on `id` and `user_id`.

**Category service**

For the **Category Service**, we can seed a seller-to-category dictionary with the most popular sellers. If we estimate 50,000 sellers and estimate each entry to take less than 255 bytes, the dictionary would only take about 12 MB of memory.

```python
class DefaultCategories(Enum):

    HOUSING = 0
    FOOD = 1
    GAS = 2
    SHOPPING = 3
    ...

seller_category_map = {}
seller_category_map['Exxon'] = DefaultCategories.GAS
seller_category_map['Target'] = DefaultCategories.SHOPPING
...
```

For sellers not initially seeded in the map, we could use a crowdsourcing effort by evaluating the manual category overrides our users provide. We could use a heap to quickly lookup the top manual override per seller in $O(1)$ time.

```python
class Categorizer(object):

    def __init__(self, seller_category_map, seller_category_crowd_overrides_map):
        self.seller_category_map = seller_category_map
        self.seller_category_crowd_overrides_map = \
            seller_category_crowd_overrides_map

    def categorize(self, transaction):
        if transaction.seller in self.seller_category_map:
            return self.seller_category_map[transaction.seller]
        elif transaction.seller in self.seller_category_crowd_overrides_map:
            self.seller_category_map[transaction.seller] = \
                self.seller_category_crowd_overrides_map[transaction.seller].peek_min()
            return self.seller_category_map[transaction.seller]
        return None
```

Transaction implementation:

```python
class Transaction(object):

    def __init__(self, created_at, seller, amount):
        self.created_at = created_at
        self.seller = seller
        self.amount = amount
```

<h3>Use case: Service recommends a budget</h3>

To start, we could use a generic budget template that allocates category amounts based on income tiers. Using this approach, we would not have to store the 100 million budget items identified in the constraints, only those that the user overrides. If a user overrides a budget category, which we could store the override in the `TABLE budget_overrides`.

```python
class Budget(object):

    def __init__(self, income):
        self.income = income
        self.categories_to_budget_map = self.create_budget_template()

    def create_budget_template(self):
        return {
            DefaultCategories.HOUSING: self.income * .4,
            DefaultCategories.FOOD: self.income * .2,
            DefaultCategories.GAS: self.income * .1,
            DefaultCategories.SHOPPING: self.income * .2,
            ...
        }

    def override_category_budget(self, category, amount):
        self.categories_to_budget_map[category] = amount
```

For the **Budget Service**, we can potentially run SQL queries on the `transactions` table to generate the `monthly_spending` aggregate table. The `monthly_spending` table would likely have much fewer rows than the total 5 billion `transactions`, since users typically have many `transactions` per month.

As an alternative, we can run **MapReduce** jobs on the raw transaction files to:

- Categorize each transaction
- Generate aggregate monthly spending by category

Running analyses on the transaction files could significantly reduce the load on the database.

We could call the **Budget Service** to re-run the analysis if the user updates a category.

Sample log file format, tab delimited:

```
user_id   timestamp   seller  amount
```

MapReduce implementation:

```python
class SpendingByCategory(MRJob):

    def __init__(self, categorizer):
        self.categorizer = categorizer
        self.current_year_month = calc_current_year_month()
        ...

    def calc_current_year_month(self):
        """Return the current year and month."""
        ...

    def extract_year_month(self, timestamp):
        """Return the year and month portions of the timestamp."""
        ...

    def handle_budget_notifications(self, key, total):
        """Call notification API if nearing or exceeded budget."""
        ...

    def mapper(self, _, line):
        """Parse each log line, extract and transform relevant lines.

        Argument line will be of the form:

        user_id   timestamp   seller  amount

        Using the categorizer to convert seller to category,
        emit key value pairs of the form:

        (user_id, 2016-01, shopping), 25
        (user_id, 2016-01, shopping), 100
        (user_id, 2016-01, gas), 50
        """
        user_id, timestamp, seller, amount = line.split('\t')
        category = self.categorizer.categorize(seller)
        period = self.extract_year_month(timestamp)
        if period == self.current_year_month:
            yield (user_id, period, category), amount

    def reducer(self, key, value):
        """Sum values for each key.

        (user_id, 2016-01, shopping), 125
        (user_id, 2016-01, gas), 50
        """
        total = sum(values)
        yield key, sum(values)
```

<h2>Step 4: Scale the design</h2>

<p align="center">
    <img src="images/mint2.png" width="50%"> 
</p>

## Design the data structures for a social network

<h2>Step 1: Outline use cases and constraints</h2>

**Use cases**

- **User** searches for someone and sees the shortest path to the searched person
- **Service** has high availability

<h3>Constraints and assumptions</h3>

- Traffic is not evenly distributed
  - Some searches are more popular than others, while others are only executed once
- Graph data won't fit on a single machine
- Graph edges are unweighted
- 100 million users
- 50 friends per user average
- 1 billion friend searches per month

Exercise the use of more traditional systems - don't use graph-specific solutions such as GraphQL or a graph database like Neo4j.

**Calculate usage**

- 5 billion friend relationships
  - 100 million users * 50 friends per user average
- 400 search requests per second

Handy conversion guide:
- 2.5 million seconds per month
- 1 request per second = 2.5 million requests per month
- 40 requests per second = 100 million requests per month
- 400 requests per second = 1 billion requests per month

<h2>Step 2: Create a high level design</h2>

<p align="center">
    <img src="images/social_graph.png" width="50%"> 
</p>

<h2>Step 3: Design core components</h2>

<h3>Use case: User searches for someone and sees the shortest path to the searched person</h3>

Without the constraint of millions of users (vertices) and billions of friend relationships (edges), we could solve this unweighted shortest path task with a general BFS approach:

```python
class Graph(Graph):

    def shortest_path(self, source, dest):
        if source is None or dest is None:
            return None
        if source is dest:
            return [source.key]
        prev_node_keys = self._shortest_path(source, dest)
        if prev_node_keys is None:
            return None
        else:
            path_ids = [dest.key]
            prev_node_key = prev_node_keys[dest.key]
            while prev_node_key is not None:
                path_ids.append(prev_node_key)
                prev_node_key = prev_node_keys[prev_node_key]
            return path_ids[::-1]

    def _shortest_path(self, source, dest):
        queue = deque()
        queue.append(source)
        prev_node_keys = {source.key: None}
        source.visit_state = State.visited
        while queue:
            node = queue.popleft()
            if node is dest:
                return prev_node_keys
            prev_node = node
            for adj_node in node.adj_nodes.values():
                if adj_node.visit_state == State.unvisited:
                    queue.append(adj_node)
                    prev_node_keys[adj_node.key] = prev_node.key
                    adj_node.visit_state = State.visited
        return None
```

We won't be able to fit all users on the same machine, we'll need to shard users across **Person Servers** and access them with a **Lookup Service**.

- The **Client** sends a request to the **Web Server**, running as a reverse proxy
- The **Web Server** forwards the request to the **Search API** server
- The **Search API** server forwards the request to the **User Graph Service**
- The **User Graph Service** does the following:
  - Uses the **Lookup Service** to find the **Person Server** where the current user's info is stored
  - Finds the appropriate **Person Server** to retrieve the current user's list of `friend_ids`
  - Runs a BFS search using the current user as the `source` and the current user's `friend_ids` as the ids for - each `adjacent_node`
  - To get the `adjacent_node` from a given id:
    - The **User Graph Service** will again need to communicate with the **Lookup Service** to determine which **Person - Server** stores the `adjacent_node` matching the given id (potential for optimization)

**Note**: Error handling is excluded below for simplicity.

**Lookup Service** implementation:

```python
class LookupService(object):

    def __init__(self):
        self.lookup = self._init_lookup()  # key: person_id, value: person_server

    def _init_lookup(self):
        ...

    def lookup_person_server(self, person_id):
        return self.lookup[person_id]
```

**Person Server** implementation:

```python
class PersonServer(object):

    def __init__(self):
        self.people = {}  # key: person_id, value: person

    def add_person(self, person):
        ...

    def people(self, ids):
        results = []
        for id in ids:
            if id in self.people:
                results.append(self.people[id])
        return results
```

**Person** implementation:

```python
class Person(object):

    def __init__(self, id, name, friend_ids):
        self.id = id
        self.name = name
        self.friend_ids = friend_ids
```

**User Graph Service** implementation:

```python
class UserGraphService(object):

    def __init__(self, lookup_service):
        self.lookup_service = lookup_service

    def person(self, person_id):
        person_server = self.lookup_service.lookup_person_server(person_id)
        return person_server.people([person_id])

    def shortest_path(self, source_key, dest_key):
        if source_key is None or dest_key is None:
            return None
        if source_key is dest_key:
            return [source_key]
        prev_node_keys = self._shortest_path(source_key, dest_key)
        if prev_node_keys is None:
            return None
        else:
            # Iterate through the path_ids backwards, starting at dest_key
            path_ids = [dest_key]
            prev_node_key = prev_node_keys[dest_key]
            while prev_node_key is not None:
                path_ids.append(prev_node_key)
                prev_node_key = prev_node_keys[prev_node_key]
            # Reverse the list since we iterated backwards
            return path_ids[::-1]

    def _shortest_path(self, source_key, dest_key, path):
        # Use the id to get the Person
        source = self.person(source_key)
        # Update our bfs queue
        queue = deque()
        queue.append(source)
        # prev_node_keys keeps track of each hop from
        # the source_key to the dest_key
        prev_node_keys = {source_key: None}
        # We'll use visited_ids to keep track of which nodes we've
        # visited, which can be different from a typical bfs where
        # this can be stored in the node itself
        visited_ids = set()
        visited_ids.add(source.id)
        while queue:
            node = queue.popleft()
            if node.key is dest_key:
                return prev_node_keys
            prev_node = node
            for friend_id in node.friend_ids:
                if friend_id not in visited_ids:
                    friend_node = self.person(friend_id)
                    queue.append(friend_node)
                    prev_node_keys[friend_id] = prev_node.key
                    visited_ids.add(friend_id)
        return None
```

We'll use a public REST API:

```shell
$ curl https://social.com/api/v1/friend_search?person_id=1234
```

Response:

```json
{
    "person_id": "100",
    "name": "foo",
    "link": "https://social.com/foo",
},
{
    "person_id": "53",
    "name": "bar",
    "link": "https://social.com/bar",
},
{
    "person_id": "1234",
    "name": "baz",
    "link": "https://social.com/baz",
},
```

For internal communications, we could use Remote Procedure Calls.

<h2>Step 4: Scale the design</h2>

<p align="center">
    <img src="images/social_graph2.png" width="50%"> 
</p>


## Design a key-value cache

<h2>Step 1: Outline use cases and constraints</h2>

**Use cases**

- **User** sends a search request resulting in a cache hit
- **User** sends a search request resulting in a cache miss
- **Service** has high availability

**Constraints and assumptions**

**State assumptions**

- Traffic is not evenly distributed
  - Popular queries should almost always be in the cache
  - Need to determine how to expire/refresh
- Serving from cache requires fast lookups
- Low latency between machines
- Limited memory in cache
  - Need to determine what to keep/remove
  - Need to cache millions of queries
- 10 million users
- 10 billion queries per month

**Calculate usage**

- Cache stores ordered list of key: query, value: results
  - `query` - 50 bytes
  - `title` - 20 bytes
  - `snippet` - 200 bytes
  - Total: 270 bytes
- 2.7 TB of cache data per month if all 10 billion queries are unique and all are stored
  - 270 bytes per search * 10 billion searches per month
  - Assumptions state limited memory, need to determine how to expire contents
- 4,000 requests per second

Handy conversion guide:

- 2.5 million seconds per month
- 1 request per second = 2.5 million requests per month
- 40 requests per second = 100 million requests per month
- 400 requests per second = 1 billion requests per month

<h2>Step 2: Create a high level design</h2>

<p align="center">
    <img src="images/query_cache.png" width="40%"> 
</p>

<h2>Step 3: Design core components</h2>

<h3>Use case: User sends a request resulting in a cache hit</h3>

Popular queries can be served from a **Memory Cache** such as Redis or Memcached to reduce read latency and to avoid overloading the **Reverse Index Service** and **Document Service**. Reading 1 MB sequentially from memory takes about 250 microseconds, while reading from SSD takes 4x and from disk takes 80x longer.

Since the cache has limited capacity, we'll use a least recently used (LRU) approach to expire older entries.

- The **Client** sends a request to the **Web Server**, running as a reverse proxy
- The **Web Server** forwards the request to the **Query API** server
- The **Query API** server does the following:
  - Parses the query
    - Removes markup
    - Breaks up the text into terms
    - Fixes typos
    - Normalizes capitalization
    - Converts the query to use boolean operations
  - Checks the **Memory Cache** for the content matching the query
    - If there's a hit in the **Memory Cache**, the **Memory Cache** does the following:
      - Updates the cached entry's position to the front of the LRU list
      - Returns the cached contents
    - Else, the **Query API** does the following:
      - Uses the **Reverse Index Service** to find documents matching the query
        - The **Reverse Index Service** ranks the matching results and returns the top ones
      - Uses the **Document Service** to return titles and snippets
      - Updates the **Memory Cache** with the contents, placing the entry at the front of the LRU list

**Cache implementation**

The cache can use a doubly-linked list: new items will be added to the head while items to expire will be removed from the tail. We'll use a hash table for fast lookups to each linked list node.

**Query API Server** implementation:

```python
class QueryApi(object):

    def __init__(self, memory_cache, reverse_index_service):
        self.memory_cache = memory_cache
        self.reverse_index_service = reverse_index_service

    def parse_query(self, query):
        """Remove markup, break text into terms, deal with typos,
        normalize capitalization, convert to use boolean operations.
        """
        ...

    def process_query(self, query):
        query = self.parse_query(query)
        results = self.memory_cache.get(query)
        if results is None:
            results = self.reverse_index_service.process_search(query)
            self.memory_cache.set(query, results)
        return results
```

**Node** implementation:

```python
class Node(object):

    def __init__(self, query, results):
        self.query = query
        self.results = results
```

**LinkedList** implementation:

```python
class LinkedList(object):

    def __init__(self):
        self.head = None
        self.tail = None

    def move_to_front(self, node):
        ...

    def append_to_front(self, node):
        ...

    def remove_from_tail(self):
        ...
```

**Cache** implementation:

```python
class Cache(object):

    def __init__(self, MAX_SIZE):
        self.MAX_SIZE = MAX_SIZE
        self.size = 0
        self.lookup = {}  # key: query, value: node
        self.linked_list = LinkedList()

    def get(self, query)
        """Get the stored query result from the cache.

        Accessing a node updates its position to the front of the LRU list.
        """
        node = self.lookup[query]
        if node is None:
            return None
        self.linked_list.move_to_front(node)
        return node.results

    def set(self, results, query):
        """Set the result for the given query key in the cache.

        When updating an entry, updates its position to the front of the LRU list.
        If the entry is new and the cache is at capacity, removes the oldest entry
        before the new entry is added.
        """
        node = self.lookup[query]
        if node is not None:
            # Key exists in cache, update the value
            node.results = results
            self.linked_list.move_to_front(node)
        else:
            # Key does not exist in cache
            if self.size == self.MAX_SIZE:
                # Remove the oldest entry from the linked list and lookup
                self.lookup.pop(self.linked_list.tail.query, None)
                self.linked_list.remove_from_tail()
            else:
                self.size += 1
            # Add the new key and value
            new_node = Node(query, results)
            self.linked_list.append_to_front(new_node)
            self.lookup[query] = new_node
```

**When to update the cache**

The cache should be updated when:

- The page contents change
- The page is removed or a new page is added
- The page rank changes

The most straightforward way to handle these cases is to simply set a max time that a cached entry can stay in the cache before it is updated, usually referred to as time to live (TTL).

<h2>Step 4: Scale the design</h2>

<p align="center">
    <img src="images/query_cache2.png" width="40%"> 
</p>

## Design Amazon's sales rank by category feature

<h2>Step 1: Outline use cases and constraints</h2>

**Use cases**
- **Service** calculates the past week's most popular products by category
- **User** views the past week's most popular products by category
- **Service** has high availability

**Out of scope**

- The general e-commerce site
  - Design components only for calculating sales rank

**Constraints and assumptions**

**State assumptions**

- Traffic is not evenly distributed
- Items can be in multiple categories
- Items cannot change categories
- There are no subcategories ie foo/bar/baz
- Results must be updated hourly
  - More popular products might need to be updated more frequently
- 10 million products
- 1000 categories
- 1 billion transactions per month
- 100 billion read requests per month
- 100:1 read to write ratio

**Calculate usage**

- Size per transaction:
  - `created_at` - 5 bytes
  - `product_id` - 8 bytes
  - `category_id` - 4 bytes
  - `seller_id` - 8 bytes
  - `buyer_id` - 8 bytes
  - `quantity` - 4 bytes
  - `total_price` - 5 bytes
  - Total: ~40 bytes
- 40 GB of new transaction content per month
  - 40 bytes per transaction * 1 billion transactions per month
  - 1.44 TB of new transaction content in 3 years
  - Assume most are new transactions instead of updates to existing ones
- 400 transactions per second on average
- 40,000 read requests per second on average

**Handy conversion guide:**

- 2.5 million seconds per month
- 1 request per second = 2.5 million requests per month
- 40 requests per second = 100 million requests per month
- 400 requests per second = 1 billion requests per month

<h2>Step 2: Create a high level design</h2>

<p align="center">
    <img src="images/sales_rank.png" width="50%"> 
</p>

<h2>Step 3: Design core components</h2>

<h3>Use case: Service calculates the past week's most popular products by category</h3>

We could store the raw **Sales API** server log files on a managed **Object Store** such as Amazon S3, rather than managing our own distributed file system.

We'll assume this is a sample log entry, tab delimited:

```
timestamp   product_id  category_id    qty     total_price   seller_id    buyer_id
t1          product1    category1      2       20.00         1            1
t2          product1    category2      2       20.00         2            2
t2          product1    category2      1       10.00         2            3
t3          product2    category1      3        7.00         3            4
t4          product3    category2      7        2.00         4            5
t5          product4    category1      1        5.00         5            6
...
```

The **Sales Rank Service** could use **MapReduce**, using the **Sales API** server log files as input and writing the results to an aggregate table `sales_rank` in a **SQL Database**. We should discuss the use cases and tradeoffs between choosing SQL or NoSQL.

We'll use a multi-step MapReduce:

- **Step 1** - Transform the data to (`category`, `product_id`), `sum(quantity)`
- **Step 2** - Perform a distributed sort

```python
class SalesRanker(MRJob):

    def within_past_week(self, timestamp):
        """Return True if timestamp is within past week, False otherwise."""
        ...

    def mapper(self, _ line):
        """Parse each log line, extract and transform relevant lines.

        Emit key value pairs of the form:

        (category1, product1), 2
        (category2, product1), 2
        (category2, product1), 1
        (category1, product2), 3
        (category2, product3), 7
        (category1, product4), 1
        """
        timestamp, product_id, category_id, quantity, total_price, seller_id, \
            buyer_id = line.split('\t')
        if self.within_past_week(timestamp):
            yield (category_id, product_id), quantity

    def reducer(self, key, value):
        """Sum values for each key.

        (category1, product1), 2
        (category2, product1), 3
        (category1, product2), 3
        (category2, product3), 7
        (category1, product4), 1
        """
        yield key, sum(values)

    def mapper_sort(self, key, value):
        """Construct key to ensure proper sorting.

        Transform key and value to the form:

        (category1, 2), product1
        (category2, 3), product1
        (category1, 3), product2
        (category2, 7), product3
        (category1, 1), product4

        The shuffle/sort step of MapReduce will then do a
        distributed sort on the keys, resulting in:

        (category1, 1), product4
        (category1, 2), product1
        (category1, 3), product2
        (category2, 3), product1
        (category2, 7), product3
        """
        category_id, product_id = key
        quantity = value
        yield (category_id, quantity), product_id

    def reducer_identity(self, key, value):
        yield key, value

    def steps(self):
        """Run the map and reduce steps."""
        return [
            self.mr(mapper=self.mapper,
                    reducer=self.reducer),
            self.mr(mapper=self.mapper_sort,
                    reducer=self.reducer_identity),
        ]
```

The result would be the following sorted list, which we could insert into the `sales_rank` table:

```python
(category1, 1), product4
(category1, 2), product1
(category1, 3), product2
(category2, 3), product1
(category2, 7), product3
```
The `sales_rank` table could have the following structure:

```sql
id int NOT NULL AUTO_INCREMENT
category_id int NOT NULL
total_sold int NOT NULL
product_id int NOT NULL
PRIMARY KEY(id)
FOREIGN KEY(category_id) REFERENCES Categories(id)
FOREIGN KEY(product_id) REFERENCES Products(id)
```

We'll create an index on `id` , `category_id`, and `product_id` to speed up lookups (log-time instead of scanning the entire table) and to keep the data in memory. Reading 1 MB sequentially from memory takes about 250 microseconds, while reading from SSD takes 4x and from disk takes 80x longer.

<h3>Use case: User views the past week's most popular products by category</h3>

The **Client** sends a request to the **Web Server**, running as a reverse proxy
The **Web Server** forwards the request to the **Read API** server
The **Read API** server reads from the **SQL Database** `sales_rank` table

We'll use a public REST API:

```shell
$ curl https://amazon.com/api/v1/popular?category_id=1234
```
Response:

```json
{
    "id": "100",
    "category_id": "1234",
    "total_sold": "100000",
    "product_id": "50",
},
{
    "id": "53",
    "category_id": "1234",
    "total_sold": "90000",
    "product_id": "200",
},
{
    "id": "75",
    "category_id": "1234",
    "total_sold": "80000",
    "product_id": "3",
},
```
For internal communications, we could use Remote Procedure Calls.

<h2>Step 4: Scale the design</h2>

<p align="center">
    <img src="images/sales_rank2.png" width="50%"> 
</p>

## References
- https://github.com/donnemartin/system-design-primer