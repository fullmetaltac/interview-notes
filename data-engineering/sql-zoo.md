# Table of Contents
- [Table of Contents](#table-of-contents)
  - [0 SELECT basics](#0-select-basics)
  - [1 SELECT name](#1-select-name)
  - [2 SELECT from World](#2-select-from-world)
  - [3 SELECT from Nobel](#3-select-from-nobel)
  - [4 SELECT within SELECT](#4-select-within-select)
  - [5 SUM and COUNT](#5-sum-and-count)
  - [6 JOIN](#6-join)
  - [7 More JOIN operations](#7-more-join-operations)
  - [*8 Using Null*](#8-using-null)
  - [*8+ Numeric Examples*](#8-numeric-examples)
  - [*9- Window function*](#9--window-function)
  - [*9+ COVID 19*](#9-covid-19)
  - [*9 Self join*](#9-self-join)
  - [References](#references)



## 0 SELECT basics

**Introducing the world table of countries**

```sql
SELECT population
FROM world
WHERE name = 'Germany'
```

**Scandinavia**

```sql
SELECT name, population
FROM world
WHERE name IN ('Sweden', 'Norway', 'Denmark')
```

**Just the right size**

```sql
SELECT name, area
FROM world
WHERE area BETWEEN 200000 AND 250000
```

## 1 SELECT name

**Find the country that start with Y**

```sql
SELECT name
FROM world
WHERE name LIKE 'Y%'
```

**Find the countries that end with y**

```sql
SELECT name
FROM world
WHERE name LIKE '%y'
```

**Find the countries that contain the letter x**

```sql
SELECT name
FROM world
WHERE name LIKE '%x%'
```

**Find the countries that end with land**

```sql
SELECT name
FROM world
WHERE name LIKE '%land'
```

**Find the countries that start with C and end with ia**

```sql
SELECT name
FROM world
WHERE name LIKE 'C%ia'
```

**Find the country that has oo in the name**

```sql
SELECT name
FROM world
WHERE name LIKE '%oo%'
```

**Find the countries that have three or more a in the name**

```sql
SELECT name
FROM world
WHERE name LIKE '%a%a%a%'
```

**Find the countries that have "t" as the second character**

```sql
SELECT name
FROM world
WHERE name LIKE '_t%'
ORDER BY name
```

**Find the countries that have two "o" characters separated by two others**

```sql
SELECT name
FROM world
WHERE name LIKE '%o__o%'
```

**Find the countries that have exactly four characters**

```sql
SELECT name
FROM world
WHERE name LIKE '____'
```

**Find the country where the name is the capital city**

```sql
SELECT name
FROM world
WHERE name = capital
```

**Find the country where the capital is the country plus "City"**

```sql
SELECT name
FROM world
WHERE capital LIKE concat(name, ' City')
```


**Find the capital and the name where the capital includes the name of the country**

```sql
SELECT capital, name
FROM world
WHERE capital LIKE concat(name, ' %') OR capital = name
```

**Find the capital and the name where the capital is an extension of name of the country**

```sql
SELECT capital, name
FROM world
WHERE capital LIKE concat(name, ' %')
```

**Show the name and the extension where the capital is a proper (non-empty) extension of name of the country**

```sql
SELECT name, REPLACE(capital, name, '')
FROM world
WHERE capital LIKE concat(name, ' %')
```

## 2 SELECT from World

**Large Countries**

```sql
SELECT name
FROM world
WHERE population >= 200000000
```

**Per capita GDP**

```sql
SELECT name, gdp / population FROM world
WHERE population >= 200000000
```

**South America In millions**

```sql
SELECT name, population / 1000000
FROM world
WHERE continent = 'South America'
```

**France, Germany, Italy**

```sql
SELECT name, population
FROM world
WHERE name = 'France' OR name = 'Germany' OR name = 'Italy'
```

**United**

```sql
SELECT name FROM world
WHERE name LIKE '%United%'
```

**Two ways to be big**

```sql
SELECT name, population, area FROM world
WHERE population > 250000000 OR area > 3000000
```

**One or the other (but not both)**

```sql
SELECT name, population, area FROM world
WHERE (area > 3000000 AND population <= 250000000)
OR (area <= 3000000 AND population > 250000000)
```

**Rounding**

```sql
SELECT name,
ROUND(population / 1000000.0, 2),
ROUND(gdp / 1000000000.0, 2)
FROM world
WHERE continent = 'South America'
```

**Trillion dollar economies**

```sql
SELECT name, ROUND(gdp / population, -3)
FROM world
WHERE gdp > 1000000000000
```

**Name and capital have the same length**

```sql
SELECT name, capital
FROM world
WHERE LENGTH(name) = LENGTH(capital)
```

**Matching name and capital**

```sql
SELECT name, capital
FROM world
WHERE LEFT(name, 1) = LEFT(capital, 1) AND name <> capital
```

**All the vowels**

```sql
SELECT name
FROM world
WHERE name LIKE '%a%' 
AND name LIKE '%e%'
AND name LIKE '%i%'
AND name LIKE '%o%'
AND name LIKE '%u%'
AND name NOT LIKE '% %'
```

## 3 SELECT from Nobel

**Winners from 1950**

```sql
SELECT yr, subject, winner
FROM nobel
WHERE yr = 1950
```

**1962 Literature**

```sql
SELECT winner
FROM nobel
WHERE yr = 1962 AND subject = 'literature'
```

**Albert Einstein**

```sql
SELECT yr, subject
FROM nobel
WHERE winner = 'Albert Einstein'
```

**Recent Peace Prizes**

```sql
SELECT winner
FROM   nobel
WHERE  subject = 'peace' AND yr >= 2000 
```

**Literature in the 1980's**

```sql
SELECT yr, subject, winner
FROM   nobel
WHERE  subject = 'literature'
       AND yr >= 1980
       AND yr <= 1989 
```

**Only Presidents**

```sql
SELECT *
FROM nobel
WHERE winner IN ('Theodore Roosevelt',
                 'Thomas Woodrow Wilson',
                 'Jimmy Carter',
                 'Barack Obama')
```

**John**

```sql
SELECT winner
FROM nobel
WHERE winner like 'John %'
```

**Chemistry and Physics from different years**

```sql
SELECT yr, subject, winner
FROM nobel
WHERE (yr = 1984 AND subject = 'chemistry')
  OR (yr = 1980 AND subject = 'physics')
```

**Exclude Chemists and Medics**

```sql
SELECT yr, subject, winner
FROM nobel
WHERE yr = 1980
  AND subject != 'chemistry'
  AND subject != 'medicine'
```

**Early Medicine, Late Literature**

```sql
SELECT yr, subject, winner
FROM nobel 
WHERE (subject = 'medicine' AND yr < 1910)
       OR (subject ='literature' AND yr >= 2004)
```

**Umlaut**

```sql
SELECT *
FROM nobel
WHERE winner = 'PETER GRÜNBERG'
```

**Apostrophe**

```sql
SELECT *
FROM nobel
WHERE winner = 'EUGENE O\'NEILL'
```

**Knights of the realm**

```sql
SELECT winner, yr, subject
FROM nobel
WHERE winner like 'Sir%'
ORDER BY yr DESC, winner
```

**Chemistry and Physics last**

```sql
SELECT winner, subject
FROM nobel
WHERE yr=1984
ORDER BY subject IN ('physics', 'chemistry'), subject, winner
```

## 4 SELECT within SELECT

**Bigger than Russia**

```sql
SELECT NAME
FROM   world
WHERE  population > (SELECT population
                     FROM   world
                     WHERE  NAME = 'Russia') 
```

**Richer than UK**

```sql
SELECT NAME
FROM   world
WHERE  gdp / population > (SELECT gdp / population
                           FROM   world
                           WHERE  NAME = 'United Kingdom')
       AND continent = 'Europe' 
```

**Neighbours of Argentina and Australia**

```sql
SELECT NAME, continent
FROM   world
WHERE  continent IN (SELECT continent
                     FROM   world
                     WHERE  NAME IN ( 'Argentina', 'Australia' ))
ORDER  BY NAME
```

**Between Canada and Poland**

```sql
SELECT NAME, population
FROM   world
WHERE  population < (SELECT population
                     FROM   world
                     WHERE  NAME = 'Germany')
       AND population > (SELECT population
                         FROM   world
                         WHERE  NAME = 'United Kingdom') 
```

**Percentages of Germany**

```sql
SELECT NAME,
       CONCAT(ROUND(population / (SELECT population
                                  FROM   world
                                  WHERE  NAME = 'Germany') * 100), "%") percentage
FROM   world
WHERE  continent = 'Europe' 
```

**Bigger than every country in Europe**

```sql
SELECT NAME
FROM   world
WHERE  gdp > (SELECT MAX(gdp)
              FROM   world
              WHERE  continent = 'Europe' AND gdp > 0) 
```

**Largest in each continent**

```sql
SELECT w1.continent, w1.name, w1.area
FROM world w1
WHERE w1.area = (
  SELECT MAX(w2.area)
  FROM world w2
  WHERE w1.continent = w2.continent
  )
```

**First country of each continent (alphabetically)**

```sql
SELECT w1.continent, w1.NAME
FROM   world w1
WHERE  w1.NAME = (SELECT MIN(w2.NAME)
                  FROM   world w2
                  WHERE  w1.continent = w2.continent)
```

**Difficult Questions That Utilize Techniques Not Covered In Prior Sections**

```sql
SELECT NAME, continent, population
FROM   world
WHERE  continent IN (SELECT continent
                     FROM   world
                     GROUP  BY continent
                     HAVING MAX(population) <= 25000000)
```

**Three time bigger**

```sql
SELECT w1.name, w1.continent
FROM world w1
WHERE w1.population / 3 > ALL (
  SELECT w2.population
  FROM world w2
  WHERE w1.continent = w2.continent AND w1.name <> w2.name
)
```

## 5 SUM and COUNT

**Total world population**

```sql
SELECT SUM(population)
FROM world
```

**List of continents**

```sql
SELECT DISTINCT continent
FROM   world 
```

**GDP of Africa**

```sql
SELECT SUM(gdp)
FROM   world
WHERE  continent = 'Africa' 
```

**Count the big countries**

```sql
SELECT COUNT(*)
FROM   world
WHERE  area >= 1000000 
```

**Baltic states population**

```sql
SELECT SUM(population)
FROM   world
WHERE  NAME IN ( 'Estonia', 'Latvia', 'Lithuania' ) 
```

**Counting the countries of each continent**
```sql
SELECT continent, COUNT(NAME)
FROM   world
GROUP  BY continent
```

**Counting big countries in each continent**

```sql
SELECT continent, COUNT(NAME)
FROM   world
WHERE  population >= 10000000
GROUP  BY continent 
```

**Counting big continents**

```sql
SELECT continent
FROM   world
GROUP  BY continent
HAVING SUM(population) >= 100000000 
```

## 6 JOIN

**Show the matchid and player name for all goals scored by Germany. To identify German players, check for: teamid = 'GER'**

```sql
SELECT matchid, player
FROM   goal
WHERE  teamid = 'GER' 
```

**Show id, stadium, team1, team2 for just game 1012**

```sql
SELECT id, stadium, team1, team2
FROM   game
WHERE  id = 1012 
```

**Show the player, teamid, stadium and mdate for every German goal**

```sql
SELECT player, teamid, stadium, mdate
FROM   game
       JOIN goal ON id = matchid
WHERE  teamid = 'GER' 
```

**Show the team1, team2 and player for every goal scored by a player called Mario player LIKE 'Mario%'**

```sql
SELECT team1, team2, player
FROM   game
       JOIN goal ON id = matchid
WHERE  player LIKE 'Mario%' 
```


**Show player, teamid, coach, gtime for all goals scored in the first 10 minutes gtime<=10**

```sql
SELECT player, teamid, coach, gtime
FROM   goal
       JOIN eteam ON teamid = id
WHERE  gtime <= 10 
```

**List the dates of the matches and the name of the team in which 'Fernando Santos' was the team1 coach**

```sql
SELECT mdate, teamname
FROM   game
       JOIN eteam ON team1 = eteam.id
WHERE  eteam .coach = 'Fernando Santos' 
```

**List the player for every goal scored in a game where the stadium was 'National Stadium, Warsaw'**

```sql
SELECT player
FROM   game
       JOIN goal ON id = matchid
WHERE  stadium = 'National Stadium, Warsaw' 
```

**Show the name of all players who scored a goal against Germany**

```sql
SELECT DISTINCT player
FROM   game
       JOIN goal ON matchid = id
WHERE  teamid <> 'GER' AND ( team1 = 'GER' OR team2 = 'GER' ) 
```

**Show teamname and the total number of goals scored**

```sql
SELECT eteam.teamname, COUNT(*) goals
FROM   eteam
       JOIN goal ON id = teamid
GROUP  BY eteam.teamname 
```

**Show the stadium and the number of goals scored in each stadium**

```sql
SELECT stadium, COUNT(*) goals
FROM   game
       JOIN goal ON id = matchid
GROUP  BY stadium 
```

**For every match involving 'POL', show the matchid, date and the number of goals scored**

```sql
SELECT matchid, mdate, COUNT(*) goals
FROM   game
       JOIN goal ON matchid = id
WHERE  team1 = 'POL' OR team2 = 'POL'
GROUP  BY matchid, mdate 
```

**For every match where 'GER' scored, show matchid, match date and the number of goals scored by 'GER'**

```sql
SELECT matchid, mdate, COUNT(*) goals
FROM   game
       JOIN goal ON matchid = id
WHERE  ( team1 = 'GER' OR team2 = 'GER' ) AND teamid = 'GER'
GROUP  BY matchid, mdate 
```

**List every match with the goals scored by each team as shown. Sort your result by mdate, matchid, team1 and team2**

```sql
SELECT game.mdate,
       game.team1,
       SUM(CASE WHEN goal.teamid = game.team1 THEN 1 ELSE 0 END) score1,
       game.team2,
       SUM(CASE WHEN goal.teamid = game.team2 THEN 1 ELSE 0 END) score2
FROM   game
       LEFT JOIN goal ON matchid = id
GROUP  BY game.id, game.mdate, game.team1, game.team2
ORDER  BY mdate, matchid, team1, team2 
```

## 7 More JOIN operations

**1962 movies**

```sql
SELECT id, title
FROM   movie
WHERE  yr = 1962 AND budget > 2000000 
```

**When was Citizen Kane released?**

```sql
SELECT yr
FROM   movie
WHERE  title = 'Citizen Kane' 
```

**Star Trek movies**
```sql
SELECT id,
       title,
       yr
FROM   movie
WHERE  title LIKE 'Star Trek%'
ORDER  BY yr 
```


**id for actor Glenn Close**

```sql
SELECT id
FROM actor
WHERE name = 'Glenn Close'
```

**id for Casablanca**

```sql
SELECT id 
FROM movie
WHERE title= 'Casablanca' and yr = 1942
```

**Cast list for Casablanca**

```sql
SELECT NAME
FROM   casting
       JOIN actor ON id = actorid
WHERE  movieid = 132689
```

**Alien cast list**

```sql
SELECT NAME
FROM   casting
       JOIN actor ON id = actorid
WHERE  movieid = (SELECT id
                  FROM   movie
                  WHERE  title = 'Alien') 
```

**Harrison Ford movies**

```sql
SELECT title
FROM   actor a
       JOIN casting c ON a.id = c.actorid
       JOIN movie m ON m.id = c.movieid
WHERE  NAME = 'Harrison Ford' 
```

**Harrison Ford as a supporting actor**
```sql
SELECT title
FROM   actor a
       JOIN casting c ON a.id = c.actorid
       JOIN movie m ON m.id = c.movieid
WHERE  NAME = 'Harrison Ford'
       AND ord <> 1 
```

**Lead actors in 1962 movies**
```sql
SELECT title,
       NAME
FROM   actor a
       JOIN casting c ON a.id = c.actorid
       JOIN movie m ON m.id = c.movieid
WHERE  yr = 1962
       AND ord = 1 
```

**Busy years for Rock Hudson**

```sql
SELECT yr,
       COUNT(title) count
FROM   movie
       JOIN casting ON movie.id = movieid
       JOIN actor ON actorid = actor.id
WHERE  NAME = 'Rock Hudson'
GROUP  BY yr
HAVING COUNT(title) > 2 
```

**Lead actor in Julie Andrews movies**
```sql
SELECT title,
       NAME
FROM   casting c
       JOIN movie m ON c.movieid = m.id
       JOIN actor a ON a.id = c.actorid
WHERE  ord = 1
       AND m.id IN (SELECT movieid
                    FROM   casting c
                    JOIN actor a ON a.id = c.actorid
                    WHERE  actorid = (SELECT id
                                      FROM   actor
                                      WHERE  NAME = 'Julie Andrews')) 
```


**Actors with 15 leading roles**

```sql
SELECT NAME
FROM   actor a
WHERE  a.id IN (SELECT actorid
                FROM   casting
                WHERE  ord = 1
                GROUP  BY actorid
                HAVING COUNT(*) > 14)
ORDER  BY NAME ASC 
```

**Released in the year 1978**

```sql
SELECT m.title,
       COUNT(actorid) actors
FROM   movie m
JOIN casting c ON m.id = c.movieid
WHERE  m.yr = 1978
GROUP  BY m.title
ORDER  BY actors DESC,
          m.title 
```

**With Art Garfunkel**

```sql
SELECT DISTINCT NAME
FROM   casting
JOIN actor ON actorid = id
WHERE  movieid IN (SELECT movieid
                   FROM   actor a
                   JOIN casting c ON a.id = c.actorid
                   WHERE  a.NAME = 'Art Garfunkel')
       AND NAME <> 'Art Garfunkel' 
```

## *8 Using Null*

**List the teachers who have NULL for their department**

```sql
SELECT NAME
FROM   teacher
WHERE  dept IS NULL 
```

**Note the INNER JOIN misses the teachers with no department and the departments with no teacher**

```sql
SELECT teacher.NAME,
       dept.NAME
FROM   teacher
INNER JOIN dept ON teacher.dept = dept.id
```

**Use a different JOIN so that all teachers are listed**

```sql
SELECT teacher.NAME,
       dept.NAME
FROM   teacher
LEFT JOIN dept ON teacher.dept = dept.id 
```


**Use a different JOIN so that all departments are listed**

```sql
SELECT teacher.NAME,
       dept.NAME
FROM   teacher
RIGHT JOIN dept ON teacher.dept = dept.id 
```

**Show teacher name and mobile number or '07986 444 2266'**

```sql
SELECT NAME,
       COALESCE(mobile, '07986 444 2266') mobileNumber
FROM   teacher  
```

**Use the COALESCE function and a LEFT JOIN to print the teacher name and department name. Use the string 'None' where there is no department**

```sql
SELECT teacher.NAME,
       COALESCE(dept.NAME, 'None') dept
FROM   teacher
LEFT JOIN dept ON teacher.dept = dept.id
```

**Use COUNT to show the number of teachers and the number of mobile phones**

```sql
SELECT COUNT(NAME),
       COUNT(mobile)
FROM   teacher 
```

**Use COUNT and GROUP BY dept.name to show each department and the number of staff. Use a RIGHT JOIN to ensure that the Engineering department is listed**

```sql
SELECT dept.NAME,
       COUNT(teacher.NAME)
FROM   teacher
RIGHT JOIN dept ON dept.id = teacher.dept
GROUP  BY dept.NAME 
```

**Use CASE to show the name of each teacher followed by 'Sci' if the teacher is in dept 1 or 2 and 'Art' otherwise**

```sql
SELECT teacher.NAME,
       CASE
         WHEN teacher.dept = 1 OR teacher.dept = 2 THEN 'Sci'
         ELSE 'Art'
       END 'department'
FROM   teacher 
```

**Use CASE to show the name of each teacher followed by 'Sci' if the teacher is in dept 1 or 2, show 'Art' if the teacher's dept is 3 and 'None' otherwise**

```sql
SELECT NAME,
       CASE
         WHEN dept = 1 OR dept = 2 THEN 'Sci'
         WHEN dept = 3 THEN 'Art'
         ELSE 'None'
       END 'department'
FROM   teacher 
```

## *8+ Numeric Examples*

**Check out one row**

```sql
SELECT a_strongly_agree
FROM   nss
WHERE  question = 'Q01'
       AND institution = 'Edinburgh Napier University'
       AND subject = '(8) Computer Science'
```

**Calculate how many agree or strongly agree**
```sql
SELECT institution, subject
FROM nss
WHERE score >= 100 AND question = 'Q15'
```

**Unhappy Computer Students**

```sql
SELECT institution, score
FROM nss
WHERE question = 'Q15'
  AND score < 50
  AND subject = '(8) Computer Science'
```

**More Computing or Creative Students?**

```sql
SELECT subject,
       SUM(response)
FROM   nss
WHERE  question = 'Q22'
       AND subject IN ( '(8) Computer Science', '(H) Creative Arts and Design' )
GROUP  BY subject
```

**Strongly Agree Numbers**

```sql
SELECT subject,
       SUM(response * a_strongly_agree / 100)
FROM   nss
WHERE  question = 'Q22'
       AND subject IN ( '(8) Computer Science', '(H) Creative Arts and Design' )
GROUP  BY subject
```

**Strongly Agree, Percentage**

```sql
SELECT subject,
       ROUND(SUM(response * a_strongly_agree) / Sum(response), 0)
FROM   nss
WHERE  question = 'Q22'
       AND subject IN ( '(8) Computer Science', '(H) Creative Arts and Design' )
GROUP  BY subject
```

**Scores for Institutions in Manchester**

```sql
SELECT institution,
       ROUND(SUM(response * score) / SUM(response), 0)
FROM   nss
WHERE  question = 'Q22'
       AND institution LIKE '%Manchester%'
GROUP  BY institution
```

**Number of Computing Students in Manchester**

```sql
SELECT institution,
       SUM(sample),
       SUM(CASE WHEN subject = '(8) Computer Science' THEN sample ELSE 0 END)
FROM   nss
WHERE  question = 'Q01' AND institution LIKE '%Manchester%'
GROUP  BY institution
```

## *9- Window function*

**Warming up**
```sql
SELECT lastname,
       party,
       votes
FROM   ge
WHERE  constituency = 'S14000024'
       AND yr = 2017
ORDER  BY votes DESC
```

**Who won?**
```sql
SELECT party,
       votes,
       RANK() OVER (ORDER BY votes DESC) posn
FROM   ge
WHERE  constituency = 'S14000024 ' AND yr = 2017
ORDER  BY party
```

**PARTITION BY**

```sql
SELECT yr,
       party,
       votes,
       RANK() OVER (PARTITION BY yr ORDER BY votes DESC) posn
FROM   ge
WHERE  constituency = 'S14000021'
ORDER  BY party, yr
```

**Edinburgh Constituency**
```sql
SELECT constituency,
       party,
       votes,
       RANK() OVER (PARTITION BY constituency ORDER BY votes DESC) posn
FROM   ge
WHERE  constituency BETWEEN 'S14000021' AND 'S14000026' AND yr = 2017
ORDER  BY posn, constituency
```

**Winners Only**
```sql
SELECT constituency,
       party
FROM   (SELECT constituency,
               party,
               votes,
               RANK() OVER (PARTITION BY constituency ORDER BY votes DESC) posn
        FROM   ge
        WHERE  constituency BETWEEN 'S14000021' AND 'S14000026' AND yr = 2017) x
WHERE  x.posn = 1
```

**Scottish seats**

```sql
SELECT party,
       COUNT(*)
FROM   (SELECT constituency,
               party,
               votes,
               RANK() OVER (PARTITION BY constituency ORDER BY votes DESC) posn
        FROM   ge
        WHERE  constituency LIKE 'S%' AND yr = 2017) x
WHERE  x.posn = 1
GROUP  BY x.party
```

## *9+ COVID 19*

**Introducing the covid table**

```sql
SELECT NAME,
       DAY (whn),
       confirmed,
       deaths,
       recovered
FROM   covid
WHERE  NAME = 'Spain'
       AND Month (whn) = 3
ORDER  BY whn
```

**Introducing the LAG function**

```sql
SELECT NAME,
       DAY(whn),
       confirmed,
       LAG(confirmed, 1) OVER (PARTITION BY NAME ORDER BY whn)
FROM   covid
WHERE  NAME = 'Italy'
       AND Month(whn) = 3
ORDER  BY whn 
```

**Number of new cases**

```sql
SELECT NAME,
       DAY(whn),
       confirmed - LAG(confirmed, 1) OVER (partition BY NAME ORDER BY whn)
FROM   covid
WHERE  NAME = 'Italy'
       AND MONTH(whn) = 3
ORDER  BY whn 
```

**Weekly changes**

```sql
SELECT NAME,
       DATE_FORMAT(whn, '%Y-%m-%d'),
       confirmed - LAG(confirmed, 1) OVER (PARTITION BY NAME ORDER BY whn)
FROM   covid
WHERE  NAME = 'Italy'
       AND Weekday(whn) = 0
ORDER  BY whn 
```

**LAG using a JOIN**

```sql
SELECT tw.name,
       DATE_FORMAT(tw.whn, '%Y-%m-%d'),
       tw.confirmed - lw.confirmed
FROM   covid tw
       LEFT JOIN covid lw ON
       DATE_ADD(lw.whn, INTERVAL 1 week) = tw.whn
       AND tw.name = lw.name
WHERE  tw.name = 'Italy'
       AND Weekday(tw.whn) = 0
ORDER  BY tw.whn 
```

**RANK()**

```sql
SELECT NAME,
       confirmed,
       RANK() OVER ( ORDER BY confirmed DESC) rc,
       deaths,
       RANK() OVER ( ORDER BY deaths DESC) rd
FROM   covid
WHERE  whn = '2020-04-20'
ORDER  BY confirmed DESC
```

**Infection rate**

```sql
SELECT world.NAME,
       ROUND(100000 * confirmed / population, 0) infect_rate,
       RANK() OVER( ORDER BY infect_rate)
FROM   covid
       JOIN world ON covid.NAME = world.NAME
WHERE  whn = '2020-04-20' AND population > 10000000
ORDER  BY population DESC 
```

**Turning the corner**

```sql
SELECT table1.name, DATE_FORMAT(table1.whn,'%Y-%m-%d'), table1.c1 FROM
  (SELECT newcases.name,newcases.whn,
          RANK() OVER(PARTITION BY NAME ORDER BY c1 DESC) rk, newcases.c1 FROM 
          (SELECT name, whn,
                  (confirmed-lag(confirmed,1) OVER (PARTITION BY NAME ORDER BY whn)) c1
          FROM covid
          ) newcases
  ) table1
WHERE table1.rk = 1 AND table1.c1 >= 1000
ORDER BY table1.whn
```

## *9 Self join*

**How many stops are in the database**

```sql
SELECT COUNT(name) FROM stops
```

**Find the id value for the stop 'Craiglockhart'**

```sql
SELECT id
FROM   stops
WHERE  NAME = 'Craiglockhart' 
```

**Give the id and the name for the stops on the '4' 'LRT' service**

```sql
SELECT id, NAME
FROM   stops
       JOIN route ON route.stop = stops.id
WHERE  route.num = '4'AND route.company = 'LRT' 
```

**Add a HAVING clause to restrict the output to two routes**

```sql
SELECT company, num, COUNT(*)
FROM   route
WHERE  stop = 149 OR stop = 53
GROUP  BY company, num
HAVING COUNT(*) = 2 
```

**Change the query so that it shows the services from Craiglockhart to London Road**

```sql
SELECT a.company, a.num, a.stop, b.stop
FROM   route a
       JOIN route b ON a.company = b.company AND a.num = b.num
WHERE  a.stop = 53 AND b.stop = 149 
```

**Change the query so that the services between 'Craiglockhart' and 'London Road' are shown**

```sql
SELECT a.company, a.num, stopa.NAME, stopb.NAME
FROM   route a JOIN route b ON a.company = b.company AND a.num = b.num
       JOIN stops stopa ON a.stop = stopa.id
       JOIN stops stopb ON b.stop = stopb.id
WHERE  stopa.NAME = 'Craiglockhart' AND stopb.NAME = 'London Road' 
```

**Give a list of all the services which connect stops**

```sql
SELECT DISTINCT a.company, a.num
FROM   route a JOIN route b ON a.company = b.company AND a.num = b.num
WHERE  a.stop = 115 AND b.stop = 137 
```

**Give a list of the services which connect the stops**

```sql
SELECT DISTINCT a.company, a.num
FROM   route a
       JOIN route b ON a.company = b.company AND a.num = b.num
       JOIN stops stopa ON a.stop = stopa.id
       JOIN stops stopb ON b.stop = stopb.id
WHERE  stopa.NAME = 'Craiglockhart' AND stopb.NAME = 'Tollcross'
```

**Give a distinct list of the stops**

```sql
SELECT DISTINCT stopb.NAME, a.company, a.num
FROM   route a
       JOIN route b ON a.company = b.company AND a.num = b.num
       JOIN stops stopa ON a.stop = stopa.id
       JOIN stops stopb ON b.stop = stopb.id
WHERE  a.company = 'LRT' AND stopa.NAME = 'Craiglockhart' 
```

**Find the routes involving two buses that can go from Craiglockhart to Lochend**

```sql
SELECT a.num, a.company, stops.NAME, d.num, d.company
FROM   route a
       JOIN route b ON a.company = b.company AND a.num = b.num
       JOIN stops ON b.stop = stops.id
       JOIN route c ON c.stop = stops.id
       JOIN route d ON c.company = d.company AND c.num = d.num
WHERE  a.stop = (SELECT id FROM stops WHERE  NAME = 'Craiglockhart')
       AND
       d.stop = (SELECT id FROM stops WHERE  NAME = 'Lochend')
ORDER  BY a.num, stops.NAME, d.num 
```

## References
- https://sqlzoo.net/wiki/SQL_Tutorial