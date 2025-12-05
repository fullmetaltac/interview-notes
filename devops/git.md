# Table of Contents
- [Table of Contents](#table-of-contents)
  - [Lab 1-2: Setup](#lab-1-2-setup)
  - [Lab 3: Create a Project](#lab-3-create-a-project)
  - [Lab 4: Checking Status](#lab-4-checking-status)
  - [Lab 5: Making Changes](#lab-5-making-changes)
  - [Lab 6: Staging Changes](#lab-6-staging-changes)
  - [Lab 7: Staging and Committing](#lab-7-staging-and-committing)
  - [Lab 8: Committing Changes](#lab-8-committing-changes)
  - [Lab 9: Changes, not Files](#lab-9-changes-not-files)
  - [Lab 10: History](#lab-10-history)
  - [Lab 11: Aliases](#lab-11-aliases)
  - [Lab 12: Getting Old Versions](#lab-12-getting-old-versions)
  - [Lab 13: Tagging versions](#lab-13-tagging-versions)
  - [Lab 14: Undoing Local Changes (before staging)](#lab-14-undoing-local-changes-before-staging)
  - [Lab 15: Undoing Staged Changes (before committing)](#lab-15-undoing-staged-changes-before-committing)
  - [Lab 16: Undoing Committed Changes](#lab-16-undoing-committed-changes)
  - [Lab 17: Removing Commits from a Branch](#lab-17-removing-commits-from-a-branch)
  - [Lab 18: Remove the oops tag](#lab-18-remove-the-oops-tag)
  - [Lab 19: Amending Commits](#lab-19-amending-commits)
  - [Lab 20: Moving Files](#lab-20-moving-files)
  - [Lab 21: More Structure](#lab-21-more-structure)
  - [Lab 22: Git Internals: The .git directory](#lab-22-git-internals-the-git-directory)
  - [Lab 23: Git Internals: Working directly with Git Objects](#lab-23-git-internals-working-directly-with-git-objects)
  - [Lab 24: Creating a Branch](#lab-24-creating-a-branch)
  - [Lab 25: Navigating Branches](#lab-25-navigating-branches)
  - [Lab 26: Changes in Main](#lab-26-changes-in-main)
  - [Lab 27: Viewing Diverging Branches](#lab-27-viewing-diverging-branches)
  - [Lab 28: Merging](#lab-28-merging)
  - [Lab 29: Creating a Conflict](#lab-29-creating-a-conflict)
  - [Lab 30: Resolving Conflicts](#lab-30-resolving-conflicts)
  - [Lab 31: Rebasing VS Merging](#lab-31-rebasing-vs-merging)
  - [Lab 32: Resetting the Greet Branch](#lab-32-resetting-the-greet-branch)
  - [Lab 33: Resetting the Main Branch](#lab-33-resetting-the-main-branch)
  - [Lab 34: Rebasing](#lab-34-rebasing)
  - [Lab 35: Merging Back to Main](#lab-35-merging-back-to-main)
  - [Lab 36: Multiple Repositories](#lab-36-multiple-repositories)
  - [Lab 37: Cloning Repositories](#lab-37-cloning-repositories)
  - [Lab 38: Review the Cloned Repository](#lab-38-review-the-cloned-repository)
  - [Lab 39: What is Origin?](#lab-39-what-is-origin)
  - [Lab 40: Remote Branches](#lab-40-remote-branches)
  - [Lab 41: Change the Original Repository](#lab-41-change-the-original-repository)
  - [Lab 42: Fetching Changes](#lab-42-fetching-changes)
  - [Lab 43: Merging Pulled Changes](#lab-43-merging-pulled-changes)
  - [Lab 44: Pulling Changes](#lab-44-pulling-changes)
  - [Lab 45: Adding a Tracking Branch](#lab-45-adding-a-tracking-branch)
  - [Lab 46: Bare Repositories](#lab-46-bare-repositories)
  - [Lab 47: Adding a Remote Repository](#lab-47-adding-a-remote-repository)
  - [Lab 48: Pushing a Change](#lab-48-pushing-a-change)
  - [Lab 49: Pulling Shared Changes](#lab-49-pulling-shared-changes)
  - [Lab 50: Hosting your Git Repositories](#lab-50-hosting-your-git-repositories)
  - [References](#references)

## Lab 1-2: Setup

**Setup Name and Email**

Run the following commands so that git knows your name and email.

```shell
git config --global user.name "Your Name"
git config --global user.email "your_email@whatever.com"
```

**Setup Line Ending Preferences**

Also, for Unix/Mac users:

```shell
git config --global core.autocrlf input
git config --global core.safecrlf true
```

And for Windows users:

```shell
git config --global core.autocrlf true
git config --global core.safecrlf true
```

## Lab 3: Create a Project

**Create a "Hello, World" program**

Starting in the empty working directory, create an empty directory named "hello", then create a file named `hello.rb` with the contents below.

```shell
mkdir hello
cd hello
```

```ruby
# hello.rb
puts "Hello, World"
```

**Create the Repository**

You now have a directory with a single file. To create a git repository from that directory, run the git init command.

```shell
$ git init
Initialized empty Git repository in /Users/jim/Downloads/git_tutorial/work/hello/.git/
```

**Add the program to the repository**

Now let's add the "Hello, World" program to the repository.

```shell
$ git add hello.rb
$ git commit -m "First Commit"
[main (root-commit) f7c41d3] First Commit
 1 file changed, 1 insertion(+)
 create mode 100644 hello.rb
```

## Lab 4: Checking Status

**Check the status of the repository**

Use the `git status` command to check the current status of the repository.

```shell
$ git status
On branch main
nothing to commit, working tree clean
```

The status command reports that there is nothing to commit. This means that the repository has all the current state of the working directory. There are no outstanding changes to record.

We will use the `git status` command to continue to monitor the state between the repository and the working directory.

## Lab 5: Making Changes

**Change the "Hello, World" program**

It's time to change our hello program to take an argument from the command line. Change the file to be:

```ruby
# hello.rb
puts "Hello, #{ARGV.first}!"
```

**Check the status**

Now check the status of the working directory.

```shell
$ git status
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   hello.rb

no changes added to commit (use "git add" and/or "git commit -a")
```

The first thing to notice is that git knows that the `hello.rb` file has been modified, but git has not yet been notified of these changes.

Also notice that the status message gives you hints about what you need to do next. If you want to add these changes to the repository, then use the `git add` command. Otherwise the `git checkout` command can be used to discard the changes.

## Lab 6: Staging Changes

**Add Changes**

Now tell git to stage the changes. Check the status

```shell
$ git add hello.rb
$ git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   hello.rb
```

The change to the `hello.rb` file has been staged. This means that git now knows about the change, but the change hasn't been permanently recorded in the repository yet. The next commit operation will include the staged changes.

If you decide you don't want to commit that change after all, the status command reminds you that the `git restore` command can be used to unstage that change.


## Lab 7: Staging and Committing

A separate staging step in git is in line with the philosophy of getting out of the way until you need to deal with source control. You can continue to make changes to your working directory, and then at the point you want to interact with source control, git allows you to record your changes in small commits that record exactly what you did.

For example, suppose you edited three files (`a.rb`, `b.rb`, and `c.rb`). Now you want to commit all the changes, but you want the changes in `a.rb` and `b.rb` to be a single commit, while the changes to `c.rb` are not logically related to the first two files and should be a separate commit.

```shell
git add a.rb
git add b.rb
git commit -m "Changes for a and b"
git add c.rb
git commit -m "Unrelated change to c"
```

## Lab 8: Committing Changes

**Commit the change**

Ok, enough about staging. Let's commit what we have staged to the repository.

When you used `git commit` previously to commit the initial version of the `hello.rb` file to the repository, you included the `-m` flag that gave a comment on the command line. The commit command will allow you to interactively edit a comment for the commit. Let's try that now.

If you omit the `-m` flag from the command line, git will pop you into the editor of your choice. The editor is chosen from the following list (in priority order):

- GIT_EDITOR environment variable
- core.editor configuration setting
- VISUAL environment variable
- EDITOR environment variable

I have the EDITOR variable set to `emacsclient`.

```shell
git commit
```

You should see the following in your editor:

```shell
|
# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
# On branch main
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#
#	modified:   hello.rb
#
```

On the first line, enter the comment: "Using ARGV". Save the file and exit the editor. You should see …

```shell
git commit
Waiting for Emacs...
[main 569aa96] Using ARGV
 1 files changed, 1 insertions(+), 1 deletions(-)
```

**Check the status**

```shell
$ git status
On branch main
nothing to commit, working tree clean
```
The working directory is clean and ready for you to continue.

## Lab 9: Changes, not Files

Most source control systems work with files. You add a file to source control and the system will track changes to the file from that point on.

Git focuses on the changes to a file rather than the file itself. When you say `git add file`, you are not telling git to add the file to the repository. Rather you are saying that git should make note of the current state of that file to be committed later.

**First Change: Allow a default name**

Change the "Hello, World" program to have a default value if a command line argument is not supplied.

```ruby
# hello.rb
name = ARGV.first || "World"

puts "Hello, #{name}!"
```

**Add this Change**

```shell
git add hello.rb
```

**Second change: Add a comment**

Now add a comment to the "Hello, World" program.

```ruby
# hello.rb
# Default is "World"
name = ARGV.first || "World"

puts "Hello, #{name}!"
```

**Check the current status**

```shell
$ git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   hello.rb

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   hello.rb
```
Notice how `hello.rb` is listed twice in the status. The first change (adding a default) is staged and is ready to be committed. The second change (adding a comment) is unstaged. If you were to commit right now, the comment would not be saved in the repository.

**Committing**

Commit the staged change (the default value), and then recheck the status.

```shell
$ git commit -m "Added a default value"
[main a6b268e] Added a default value
 1 file changed, 3 insertions(+), 1 deletion(-)
$ git status
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   hello.rb

no changes added to commit (use "git add" and/or "git commit -a")
```
The status command is telling you that `hello.rb` has unrecorded changes, but is no longer in the staging area.

**Add the Second Change**

Now add the second change to staging area, then run git status.

```shell
git add .
git status
```

We used the current directory ('.') as the file to add. This is a really convenient shortcut for adding in all the changes to the files in the current directory and below. But since it adds everything, it is a really good idea to check the status before doing an add ., just to make sure you don't add any file that is not intended.

```shell
$ git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   hello.rb
```

**Commit the Second Change**

```shell
git commit -m "Added a comment"
```

## Lab 10: History

Getting a listing of what changes have been made is the function of the `git log` command.

```shell
$ git log
commit e4e3645637546103e72f0deb9abdd22dd256601e
Author: Jim Weirich <jim (at) edgecase.com>
Date:   Sat Jun 10 03:49:13 2023 -0400

    Added a comment

commit a6b268ebc6a47068474bd6dfb638eb06896a6057
Author: Jim Weirich <jim (at) edgecase.com>
Date:   Sat Jun 10 03:49:13 2023 -0400

    Added a default value

commit 174dfabb62e6588c0e3c40867295da073204eb01
Author: Jim Weirich <jim (at) edgecase.com>
Date:   Sat Jun 10 03:49:13 2023 -0400

    Using ARGV

commit f7c41d3ce80ca44e2c586434cbf90fea3a9009a5
Author: Jim Weirich <jim (at) edgecase.com>
Date:   Sat Jun 10 03:49:13 2023 -0400

    First Commit
```

**One Line Histories**

You have a great deal of control over exactly what the `log` command displays. I like the one line format:

```shell
$ git log --pretty=oneline
e4e3645637546103e72f0deb9abdd22dd256601e Added a comment
a6b268ebc6a47068474bd6dfb638eb06896a6057 Added a default value
174dfabb62e6588c0e3c40867295da073204eb01 Using ARGV
f7c41d3ce80ca44e2c586434cbf90fea3a9009a5 First Commit
```

**Controlling Which Entries are Displayed**

There are a lot of options for selecting which entries are displayed in the log.

```shell
git log --pretty=oneline --max-count=2
git log --pretty=oneline --since='5 minutes ago'
git log --pretty=oneline --until='5 minutes ago'
git log --pretty=oneline --author=<your name>
git log --pretty=oneline --all
```

**Getting Fancy**

Here's what I use to review the changes made in the last week. I'll add `--author=jim` if I only want to see changes I made.

```shell
git log --all --pretty=format:'%h %cd %s (%an)' --since='7 days ago'
```

**The Ultimate Log Format**

Over time, I've decided that I like the following log format for most of my work.

```shell
$ git log --pretty=format:'%h %ad | %s%d [%an]' --graph --date=short
* e4e3645 2023-06-10 | Added a comment (HEAD -> main) [Jim Weirich]
* a6b268e 2023-06-10 | Added a default value [Jim Weirich]
* 174dfab 2023-06-10 | Using ARGV [Jim Weirich]
* f7c41d3 2023-06-10 | First Commit [Jim Weirich]
```

Let's look at it in detail:

- `--pretty="..."` defines the format of the output.
- `%h` is the abbreviated hash of the commit
- `%d` are any decorations on that commit (e.g. branch heads or tags)
- `%ad` is the author date
- `%s` is the comment
- `%an` is the author name
- `--graph` informs git to display the commit tree in an ASCII graph layout
- `--date=short` keeps the date format nice and short

**Other Tools**

Both `gitx` (for Macs) and `gitk` (any platform) are useful in exploring log history.

## Lab 11: Aliases

**Common Aliases**

`git status`, `git add`, `git commit`, and `git checkout` are such common commands that it is useful to have abbreviations for them.

Add the following to the .gitconfig file in your $HOME directory.

```conf
.gitconfig
[alias]
  co = checkout
  ci = commit
  st = status
  br = branch
  hist = log --pretty=format:'%h %ad | %s%d [%an]' --graph --date=short
  type = cat-file -t
  dump = cat-file -p
```

With these aliases defined in the `.gitconfig` file you can type `git co` wherever you used to have to type git checkout. Likewise with `git st` for `git status` and `git ci` for `git commit`. And best of all, `git hist` will allow you to avoid the really long log command.

## Lab 12: Getting Old Versions

Going back in history is very easy. The checkout command will copy any snapshot from the repository to the working directory.

**Get the hashes for previous versions**

```shell
$ git hist
* e4e3645 2023-06-10 | Added a comment (HEAD -> main) [Jim Weirich]
* a6b268e 2023-06-10 | Added a default value [Jim Weirich]
* 174dfab 2023-06-10 | Using ARGV [Jim Weirich]
* f7c41d3 2023-06-10 | First Commit [Jim Weirich]
```

Examine the log output and find the hash for the first commit. It should be the last line of the `git hist` output. Use that hash code (the first 7 characters are enough) in the command below. Then check the contents of the hello.rb file.

```shell
$ git checkout f7c41d3
Note: switching to 'f7c41d3'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at f7c41d3 First Commit
$ cat hello.rb
puts "Hello, World"
```
**Return the latest version in the main branch**

```shell
$ git checkout main
Previous HEAD position was f7c41d3 First Commit
Switched to branch 'main'
$ cat hello.rb
# Default is "World"
name = ARGV.first || "World"

puts "Hello, #{name}!"
```

'main' is the name of the default branch. By checking out a branch by name, you go to the latest version of that branch.

## Lab 13: Tagging versions

**Tagging version 1**

```shell
git tag v1
```

Now you can refer to the current version of the program as v1.

**Tagging Previous Versions**

Let's tag the version immediately prior to the current version v1-beta. First we need to checkout the previous version. Rather than look up the hash, we will use the `^` notation to indicate "the parent of v1".

If the `v1`^ notation gives you any trouble, you can also try `v1~1`, which will reference the same version. This notation means "the first ancestor of v1".

```shell
$ git checkout v1^
Note: switching to 'v1^'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at a6b268e Added a default value
$ cat hello.rb
name = ARGV.first || "World"

puts "Hello, #{name}!"
```

See, this is the version with the default value before we added the comment. Let's make this v1-beta.

```shell
git tag v1-beta
```

**Checking Out by Tag Name**

Now try going back and forth between the two tagged versions.

```shell
$ git checkout v1
Previous HEAD position was a6b268e Added a default value
HEAD is now at e4e3645 Added a comment
$ git checkout v1-beta
Previous HEAD position was e4e3645 Added a comment
HEAD is now at a6b268e Added a default value
```

**Viewing Tags using the tag command**

You can see what tags are available using the `git tag` command.

```shell
$ git tag
v1
v1-beta
```

**Viewing Tags in the Logs**

You can also check for tags in the log.

```shell
$ git hist main --all
* e4e3645 2023-06-10 | Added a comment (tag: v1, main) [Jim Weirich]
* a6b268e 2023-06-10 | Added a default value (HEAD, tag: v1-beta) [Jim Weirich]
* 174dfab 2023-06-10 | Using ARGV [Jim Weirich]
* f7c41d3 2023-06-10 | First Commit [Jim Weirich]
```

You can see both tags (`v1` and `v1-beta`) listed in the log output, along with the branch name (`main`). Also `HEAD` shows you the currently checked out commit (which is `v1-beta` at the moment).

## Lab 14: Undoing Local Changes (before staging)

**Checkout main**
Make sure you are on the latest commit in main before proceeding.

```shell
git checkout main
```

**Change hello.rb**

Sometimes you have modified a file in your local working directory and you wish to just revert to what has already been committed. The checkout command will handle that.

Change hello.rb to have a bad comment.

```ruby
# hello.rb
# This is a bad comment.  We want to revert it.
name = ARGV.first || "World"

puts "Hello, #{name}!"
```

**Check the Status**

First, check the status of the working directory.

```shell
$ git status
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   hello.rb

no changes added to commit (use "git add" and/or "git commit -a")
```
We see that the `hello.rb` file has been modified, but hasn't been staged yet.

**Revert the changes in the working directory**

Use the `checkout` command to checkout the repository's version of the `hello.rb` file.

```shell
$ git checkout hello.rb
Updated 1 path from the index
$ git status
On branch main
nothing to commit, working tree clean
$ cat hello.rb
# Default is "World"
name = ARGV.first || "World"

puts "Hello, #{name}!"
```

The status command shows us that there are no outstanding changes in the working directory. And the "bad comment" is no longer part of the file contents.

## Lab 15: Undoing Staged Changes (before committing)

**Change the file and stage the change**
Modify the hello.rb file to have a bad comment

```ruby
# hello.rb
# This is an unwanted but staged comment
name = ARGV.first || "World"

puts "Hello, #{name}!"
And then go ahead and stage it.
```

```shell
git add hello.rb
```

**Check the Status**

```shell
$ git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   hello.rb
```

The status output shows that the change has been staged and is ready to be committed.

**Reset the Staging Area**

The `reset` command resets the staging area to be whatever is in HEAD. This clears the staging area of the change we just staged.

```shell
$ git reset HEAD hello.rb
Unstaged changes after reset:
M	hello.rb
```

The `reset` command (by default) doesn't change the working directory. So the working directory still has the unwanted comment in it. We can use the `checkout` command of the previous lab to remove the unwanted change from the working directory.

**Note**: You could also have used the `git restore` command to restore just the single file.

**Checkout the Committed Version**

```shell
$ git status
On branch main
nothing to commit, working tree clean
```
And our working directory is clean once again.

## Lab 16: Undoing Committed Changes

**Undoing Commits**

Sometimes you realized that a change that you have already committed was not correct and you wish to undo that commit. There are several ways of handling that issue, and the way we are going to use in this lab is always safe.

Essentially we will undo the commit by creating a new commit that reverses the unwanted changes.

**Change the file and commit it.**

Change the `hello.rb` file to the following.

```ruby
# hello.rb
# This is an unwanted but committed change
name = ARGV.first || "World"

puts "Hello, #{name}!"
```

```shell
git add hello.rb
git commit -m "Oops, we didn't want this commit"
```

**Create a Reverting Commit**

To undo a committed change, we need to generate a commit that removes the changes introduced by our unwanted commit.

```shell
git revert HEAD
```

This will pop you into the editor. You can edit the default commit message or leave it as is. Save and close the file. You should see ...

```shell
$ git revert HEAD --no-edit
[main 8b71812] Revert "Oops, we didn't want this commit"
 Date: Sat Jun 10 03:49:14 2023 -0400
 1 file changed, 1 insertion(+), 1 deletion(-)
```

Since we were undoing the very last commit we made, we were able to use `HEAD` as the argument to revert. We can revert any arbitrary commit earlier in history by simply specifying its hash value.

**Note**: The `--no-edit` in the output can be ignored. It was necessary to generate the output without opening the editor.

**Check the log**

Checking the log shows both the unwanted and the reverting commits in our repository.

```shell
$ git hist
* 8b71812 2023-06-10 | Revert "Oops, we didn't want this commit" (HEAD -> main) [Jim Weirich]
* 146fb71 2023-06-10 | Oops, we didn't want this commit [Jim Weirich]
* e4e3645 2023-06-10 | Added a comment (tag: v1) [Jim Weirich]
* a6b268e 2023-06-10 | Added a default value (tag: v1-beta) [Jim Weirich]
* 174dfab 2023-06-10 | Using ARGV [Jim Weirich]
* f7c41d3 2023-06-10 | First Commit [Jim Weirich]
```

This technique will work with any commit (although you may have to resolve conflicts). It is safe to use even on branches that are publicly shared on remote repositories.

## Lab 17: Removing Commits from a Branch

The `revert` command of the previous section is a powerful command that lets us undo the effects of any commit in the repository. However, both the original commit and the "undoing" commit are visible in the branch history (using the `git log` command).

Often we make a commit and immediately realize that it was a mistake. It would be nice to have a "take back" command that would allow us to pretend that the incorrect commit never happened. The "take back" command would even prevent the bad commit from showing up the `git log` history. It would be as if the bad commit never happened.

**The reset command**

We've already seen the `reset` command and have used it to set the staging area to be consistent with a given commit (we used the HEAD commit in our previous lab).

When given a commit reference (i.e. a hash, branch or tag name), the `reset` command will ...

- Rewrite the current branch to point to the specified commit
- Optionally reset the staging area to match the specified commit
- Optionally reset the working directory to match the specified commit

**Check Our History**

```shell
$ git hist
* 8b71812 2023-06-10 | Revert "Oops, we didn't want this commit" (HEAD -> main) [Jim Weirich]
* 146fb71 2023-06-10 | Oops, we didn't want this commit [Jim Weirich]
* e4e3645 2023-06-10 | Added a comment (tag: v1) [Jim Weirich]
* a6b268e 2023-06-10 | Added a default value (tag: v1-beta) [Jim Weirich]
* 174dfab 2023-06-10 | Using ARGV [Jim Weirich]
* f7c41d3 2023-06-10 | First Commit [Jim Weirich]
```

We see that we have an "Oops" commit and a "Revert Oops" commit as the last two commits made in this branch. Let's remove them using reset.

**First, Mark this Branch**
But before we remove the commits, let's mark the latest commit with a tag so we can find it again.

```shell
git tag oops
```

**Reset to Before Oops**

Looking at the log history (above), we see that the commit tagged 'v1' is the commit right before the bad commit. Let's reset the branch to that point. Since that branch is tagged, we can use the tag name in the reset command (if it wasn't tagged, we could just use the hash value).

```shell
$ git reset --hard v1
HEAD is now at e4e3645 Added a comment
$ git hist
* e4e3645 2023-06-10 | Added a comment (HEAD -> main, tag: v1) [Jim Weirich]
* a6b268e 2023-06-10 | Added a default value (tag: v1-beta) [Jim Weirich]
* 174dfab 2023-06-10 | Using ARGV [Jim Weirich]
* f7c41d3 2023-06-10 | First Commit [Jim Weirich]
```

Our main branch now points to the v1 commit and the Oops commit and the Revert Oops commit are no longer in the branch. The `--hard` parameter indicates that the working directory should be updated to be consistent with the new branch head.

**Nothing is Ever Lost**

But what happened to the bad commits? It turns out that the commits are still in the repository. In fact, we can still reference them. Remember that at the beginning of this lab we tagged the reverting commit with the tag "oops". Let's look at all the commits.

```shell
$ git hist --all
* 8b71812 2023-06-10 | Revert "Oops, we didn't want this commit" (tag: oops) [Jim Weirich]
* 146fb71 2023-06-10 | Oops, we didn't want this commit [Jim Weirich]
* e4e3645 2023-06-10 | Added a comment (HEAD -> main, tag: v1) [Jim Weirich]
* a6b268e 2023-06-10 | Added a default value (tag: v1-beta) [Jim Weirich]
* 174dfab 2023-06-10 | Using ARGV [Jim Weirich]
* f7c41d3 2023-06-10 | First Commit [Jim Weirich]
```

Here we see that the bad commits haven't disappeared. They are still in the repository. It's just that they are no longer listed in the main branch. If we hadn't tagged them, they would still be in the repository, but there would be no way to reference them other than using their hash names. Commits that are unreferenced remain in the repository until the system runs the garbage collection software.

**Dangers of Reset**

Resets on local branches are generally safe. Any "accidents" can usually be recovered from by just resetting again with the desired commit.

However, if the branch is shared on remote repositories, resetting can confuse other users sharing the branch.

---

## Lab 18: Remove the oops tag

The oops tag has served its purpose. Let's remove it and allow the commits it referenced to be garbage collected.

```shell
$ git tag -d oops
Deleted tag 'oops' (was 8b71812)
$ git hist --all
* e4e3645 2023-06-10 | Added a comment (HEAD -> main, tag: v1) [Jim Weirich]
* a6b268e 2023-06-10 | Added a default value (tag: v1-beta) [Jim Weirich]
* 174dfab 2023-06-10 | Using ARGV [Jim Weirich]
* f7c41d3 2023-06-10 | First Commit [Jim Weirich]
```

## Lab 19: Amending Commits

**Change the program then commit**

Add an author comment to the program.

```ruby
# hello.rb
# Default is World
# Author: Jim Weirich
name = ARGV.first || "World"

puts "Hello, #{name}!"
```

```shell
git add hello.rb
git commit -m "Add an author comment"
```

**Amend the Previous Commit**

We really don't want a separate commit for just the email. Let's amend the previous commit to include the email change.

```shell
$ git add hello.rb
$ git commit --amend -m "Add an author/email comment"
[main 186488e] Add an author/email comment
 Date: Sat Jun 10 03:49:14 2023 -0400
 1 file changed, 2 insertions(+), 1 deletion(-)
```

**Review the History**

```shell
$ git hist
* 186488e 2023-06-10 | Add an author/email comment (HEAD -> main) [Jim Weirich]
* e4e3645 2023-06-10 | Added a comment (tag: v1) [Jim Weirich]
* a6b268e 2023-06-10 | Added a default value (tag: v1-beta) [Jim Weirich]
* 174dfab 2023-06-10 | Using ARGV [Jim Weirich]
* f7c41d3 2023-06-10 | First Commit [Jim Weirich]
```

We can see the original "author" commit is now gone, and it is replaced by the "author/email" commit. You can achieve the same effect by resetting the branch back one commit and then recommitting the new changes.


## Lab 20: Moving Files

**Move the hello.rb file into a lib directory.**

We are now going to build up the structure of our little repository. Let's move the program into a lib directory.

```shell
$ mkdir lib
$ git mv hello.rb lib
$ git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	renamed:    hello.rb -> lib/hello.rb
```

By using git to do the move, we inform git of 2 things
1. That the file `hello.rb` has been deleted.
1. The file `lib/hello.rb` has been created.

Both of these bits of information are immediately staged and ready to be committed. The git status command reports that the file has been moved.

**Another way of moving files**

One of the nice things about git is that you can forget about source control until the point you are ready to start committing code. What would happen if we used the operating system command to move the file instead of the git command?

It turns out the following set of commands is identical to what we just did. It's a bit more work, but the result is the same.

We could have done:

```shell
mkdir lib
mv hello.rb lib
git add lib/hello.rb
git rm hello.rb
```

**Commit the new directory**

Let's commit this move.

```shell
git commit -m "Moved hello.rb to lib"
```

## Lab 21: More Structure

**Now add a Rakefile**

```shell
gem install rake
```
Let's add a Rakefile to our repository. The following one will do nicely.

```ruby
# Rakefile
#!/usr/bin/ruby -wKU

task :default => :run

task :run do
  require './lib/hello'
end
```

Add and commit the change.

```shell
git add Rakefile
git commit -m "Added a Rakefile."
```

You should be able to use Rake to run your hello program now.

```shell
$ rake
Hello, World!
```

## Lab 22: Git Internals: The .git directory

**The .git Directory**

Time to do some exploring. First, from the root of your project directory…

```shell
$ ls -C .git
COMMIT_EDITMSG	config		index		objects
HEAD		description	info		packed-refs
ORIG_HEAD	hooks		logs		refs
```

This is the magic directory where all the git "stuff" is stored. Let's peek in the objects directory.

**The Object Store**

```shell
$ ls -C .git/objects
09	17	24	43	6b	97	af	c4	e7	pack
11	18	27	59	78	9c	b0	cd	f7
14	22	28	69	8b	a6	b5	e4	info
```

You should see a bunch of directories with 2 letter names. The directory names are the first two letters of the sha1 hash of the object stored in git.  

**Deeper into the Object Store**

```shell
$ ls -C .git/objects/09
6b74c56bfc6b40e754fc0725b8c70b2038b91e	9fb6f9d3a104feb32fcac22354c4d0e8a182c1
```

Look in one of the two-letter directories. You should see some files with 38-character names. These are the files that contain the objects stored in git. These files are compressed and encoded, so looking at their contents directly won't be very helpful, but we will take a closer look in a bit.


**Config File**

```shell
$ cat .git/config
[core]
	repositoryformatversion = 0
	filemode = true
	bare = false
	logallrefupdates = true
	ignorecase = true
	precomposeunicode = true
[user]
	name = Jim Weirich
	email = jim (at) edgecase.com
```

This is a project-specific configuration file. Config entries in here will override the config entries in the .gitconfig file in your home directory, at least for this project.

**Branches and Tags**

```shell
$ ls .git/refs
heads
tags
$ ls .git/refs/heads
main
$ ls .git/refs/tags
v1
v1-beta
$ cat .git/refs/tags/v1
e4e3645637546103e72f0deb9abdd22dd256601e
```

You should recognize the files in the tags subdirectory. Each file corresponds to a tag you created with the git tag command earlier. Its content is just the hash of the commit tied to the tag.

The heads directory is similar, but is used for branches rather than tags. We only have one branch at the moment, so all you will see is main in this directory.

**The HEAD File**

```shell
$ cat .git/HEAD
ref: refs/heads/main
```

The HEAD file contains a reference to the current branch. It should be a reference to main at this point.

## Lab 23: Git Internals: Working directly with Git Objects

**Finding the Latest Commit**

This should show the latest commit made in the repository. The SHA1 hash on your system is probably different from what is on mine, but you should see something like this.

```shell
$ git hist --max-count=1
* cdceefa 2023-06-10 | Added a Rakefile. (HEAD -> main) [Jim Weirich]
```

**Dumping the Latest Commit**

Using the SHA1 hash from the commit listed above ...

```shell
$ git cat-file -t cdceefa
commit
$ git cat-file -p cdceefa
tree 096b74c56bfc6b40e754fc0725b8c70b2038b91e
parent 22273f2a02983d905df7b4154b00447934034338
author Jim Weirich <jim (at) edgecase.com> 1686383357 -0400
committer Jim Weirich <jim (at) edgecase.com> 1686383357 -0400

Added a Rakefile.
```

This is the dump of the commit object that is at the head of the main branch. It looks a lot like the commit object from the presentation earlier.

**Finding the Tree**

We can dump the directory tree referenced in the commit. This should be a description of the (top level) files in our project (for that commit). Use the SHA1 hash from the "tree" line listed above.

```shell
$ git cat-file -p 096b74c
100644 blob 28e0e9d6ea7e25f35ec64a43f569b550e8386f90	Rakefile
040000 tree e46f374f5b36c6f02fb3e9e922b79044f754d795	lib
```

**Dumping the lib directory**

```shell
$ git cat-file -p e46f374
100644 blob c45f26b6fdc7db6ba779fc4c385d9d24fc12cf72	hello.rb
```

There's the hello.rb file.

**Dumping the hello.rb file**

```shell
$ git cat-file -p c45f26b
# Default is World
# Author: Jim Weirich (jim@somewhere.com)
name = ARGV.first || "World"

puts "Hello, #{name}!"
```

There you have it. We've dumped commit objects, tree objects and blob objects directly from the git repository. That's all there is to it, blobs, trees and commits.

## Lab 24: Creating a Branch

Let's call our new branch 'greet'.

```shell
git checkout -b greet
git status
```

`git checkout -b <branchname>` is a shortcut for `git branch <branchname>` followed by a `git checkout <branchname>`.

**Changes for Greet: Add a Greeter class.**

```ruby
# lib/greeter.rb
class Greeter
  def initialize(who)
    @who = who
  end
  def greet
    "Hello, #{@who}"
  end
end
```

```shell
git add lib/greeter.rb
git commit -m "Added greeter class"
```

**Changes for Greet: Modify the main program**

Update the hello.rb file to use greeter

```ruby
# lib/hello.rb
require 'greeter'

# Default is World
name = ARGV.first || "World"

greeter = Greeter.new(name)
puts greeter.greet
```

```shell
git add lib/hello.rb
git commit -m "Hello uses Greeter"
```

**Changes for Greet: Update the Rakefile**

Update the Rakefile to use an external ruby process

```ruby
# Rakefile
#!/usr/bin/ruby -wKU

task :default => :run

task :run do
  ruby '-Ilib', 'lib/hello.rb'
end
```

```shell
git add Rakefile
git commit -m "Updated Rakefile"
```

## Lab 25: Navigating Branches

You now have two branches in your project:

```shell
$ git hist --all
* c1a7120 2023-06-10 | Updated Rakefile (HEAD -> greet) [Jim Weirich]
* 959a7cb 2023-06-10 | Hello uses Greeter [Jim Weirich]
* cab1837 2023-06-10 | Added greeter class [Jim Weirich]
* cdceefa 2023-06-10 | Added a Rakefile. (main) [Jim Weirich]
* 22273f2 2023-06-10 | Moved hello.rb to lib [Jim Weirich]
* 186488e 2023-06-10 | Add an author/email comment [Jim Weirich]
* e4e3645 2023-06-10 | Added a comment (tag: v1) [Jim Weirich]
* a6b268e 2023-06-10 | Added a default value (tag: v1-beta) [Jim Weirich]
* 174dfab 2023-06-10 | Using ARGV [Jim Weirich]
* f7c41d3 2023-06-10 | First Commit [Jim Weirich]
```

**Switch to the Main Branch**

Just use the `git checkout` command to switch between branches.

```shell
$ git checkout main
Switched to branch 'main'
$ cat lib/hello.rb
# Default is World
# Author: Jim Weirich (jim@somewhere.com)
name = ARGV.first || "World"

puts "Hello, #{name}!"
```
You are now on the main branch. You can tell because the hello.rb file doesn't use the `Greeter` class.

**Switch Back to the Greet Branch.**

```shell
$ git checkout greet
Switched to branch 'greet'
$ cat lib/hello.rb
require 'greeter'

# Default is World
name = ARGV.first || "World"

greeter = Greeter.new(name)
puts greeter.greet
```

The contents of the `lib/hello.rb` confirms we are back on the **greet** branch.

## Lab 26: Changes in Main

**Switch to the main branch.**

```shell
git checkout main
```

**Create the README.**

```shell
# README
This is the Hello World example from the git tutorial.
```

**Commit the README to main.**

```shell
git add README
git commit -m "Added README"
```

## Lab 27: Viewing Diverging Branches

**View the Current Branches**

We now have two diverging branches in the repository. Use the following log command to view the branches and how they diverge.

```shell
$ git hist --all
* 976950b 2023-06-10 | Added README (HEAD -> main) [Jim Weirich]
| * c1a7120 2023-06-10 | Updated Rakefile (greet) [Jim Weirich]
| * 959a7cb 2023-06-10 | Hello uses Greeter [Jim Weirich]
| * cab1837 2023-06-10 | Added greeter class [Jim Weirich]
|/  
* cdceefa 2023-06-10 | Added a Rakefile. [Jim Weirich]
* 22273f2 2023-06-10 | Moved hello.rb to lib [Jim Weirich]
* 186488e 2023-06-10 | Add an author/email comment [Jim Weirich]
* e4e3645 2023-06-10 | Added a comment (tag: v1) [Jim Weirich]
* a6b268e 2023-06-10 | Added a default value (tag: v1-beta) [Jim Weirich]
* 174dfab 2023-06-10 | Using ARGV [Jim Weirich]
* f7c41d3 2023-06-10 | First Commit [Jim Weirich]
```

Here is our first chance to see the `--graph` option on `git hist` in action. Adding the `--graph` option to `git log` causes it to draw the commit tree using simple ASCII characters. We can see both branches (greet and main), and that the main branch is the current HEAD. The common ancestor to both branches is the "Added a Rakefile" branch.

The `--all` flag makes sure that we see all the branches. The default is to show only the current branch.

## Lab 28: Merging

**Merge the branches**

Merging brings the changes in two branches together. Let's go back to the greet branch and merge main onto greet.

```shell
$ git checkout greet
Switched to branch 'greet'
$ git merge main
Merge made by the 'recursive' strategy.
 README | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 README
$ git hist --all
*   82a2988 2023-06-10 | Merge branch 'main' into greet (HEAD -> greet) [Jim Weirich]
|\  
| * 976950b 2023-06-10 | Added README (main) [Jim Weirich]
* | c1a7120 2023-06-10 | Updated Rakefile [Jim Weirich]
* | 959a7cb 2023-06-10 | Hello uses Greeter [Jim Weirich]
* | cab1837 2023-06-10 | Added greeter class [Jim Weirich]
|/  
* cdceefa 2023-06-10 | Added a Rakefile. [Jim Weirich]
* 22273f2 2023-06-10 | Moved hello.rb to lib [Jim Weirich]
* 186488e 2023-06-10 | Add an author/email comment [Jim Weirich]
* e4e3645 2023-06-10 | Added a comment (tag: v1) [Jim Weirich]
* a6b268e 2023-06-10 | Added a default value (tag: v1-beta) [Jim Weirich]
* 174dfab 2023-06-10 | Using ARGV [Jim Weirich]
* f7c41d3 2023-06-10 | First Commit [Jim Weirich]
```

By merging main into your greet branch periodically, you can pick up any changes to main and keep your changes in greet compatible with changes in the mainline.

However, it does produce ugly commit graphs. Later we will look at the option of rebasing rather than merging.

## Lab 29: Creating a Conflict

**Switch back to main and create a conflict**

Switch back to the main branch and make this change:

```shell
git checkout main
```

```ruby
# lib/hello.rb
puts "What's your name"
my_name = gets.strip

puts "Hello, #{my_name}!"
```

```shell
git add lib/hello.rb
git commit -m "Made interactive"
```

**View the Branches**
```shell
$ git hist --all
*   82a2988 2023-06-10 | Merge branch 'main' into greet (greet) [Jim Weirich]
|\  
* | c1a7120 2023-06-10 | Updated Rakefile [Jim Weirich]
* | 959a7cb 2023-06-10 | Hello uses Greeter [Jim Weirich]
* | cab1837 2023-06-10 | Added greeter class [Jim Weirich]
| | * 3787562 2023-06-10 | Made interactive (HEAD -> main) [Jim Weirich]
| |/  
| * 976950b 2023-06-10 | Added README [Jim Weirich]
|/  
* cdceefa 2023-06-10 | Added a Rakefile. [Jim Weirich]
* 22273f2 2023-06-10 | Moved hello.rb to lib [Jim Weirich]
* 186488e 2023-06-10 | Add an author/email comment [Jim Weirich]
* e4e3645 2023-06-10 | Added a comment (tag: v1) [Jim Weirich]
* a6b268e 2023-06-10 | Added a default value (tag: v1-beta) [Jim Weirich]
* 174dfab 2023-06-10 | Using ARGV [Jim Weirich]
* f7c41d3 2023-06-10 | First Commit [Jim Weirich]
```

main at commit "Added README" has been merged to the greet branch, but there is now an additional commit on main that has not been merged back to greet.

## Lab 30: Resolving Conflicts

**Merge main to greet**

Now go back to the greet branch and try to merge the new main.

```shell
$ git checkout greet
Switched to branch 'greet'
$ git merge main
Auto-merging lib/hello.rb
CONFLICT (content): Merge conflict in lib/hello.rb
Automatic merge failed; fix conflicts and then commit the result.
```

If you open lib/hello.rb, you will see:

```ruby
# lib/hello.rb
<<<<<<< HEAD
require 'greeter'

# Default is World
name = ARGV.first || "World"

greeter = Greeter.new(name)
puts greeter.greet
=======
# Default is World

puts "What's your name"
my_name = gets.strip

puts "Hello, #{my_name}!"
>>>>>>> main
```

The first section is the version on the head of the current branch (greet). The second section is the version on the main branch.

**Fix the Conflict**

You need to manually resolve the conflict. Modify lib/hello.rb to be the following.

```ruby
# lib/hello.rb
require 'greeter'

puts "What's your name"
my_name = gets.strip

greeter = Greeter.new(my_name)
puts greeter.greet
```

**Commit the Conflict Resolution**

```shell
$ git add lib/hello.rb
$ git commit -m "Merged main fixed conflict."
[greet 73db54b] Merged main fixed conflict.
```

**Advanced Merging**

git doesn't provide any graphical merge tools, but it will gladly work with any third party merge tool you wish to use. See [External Merge and Diff Tools](http://git-scm.com/book/en/v2/Customizing-Git-Git-Configuration#External-Merge-and-Diff-Tools) for a description of using the Perforce merge tool with git.

## Lab 31: Rebasing VS Merging

Let's explore the differences between merging and rebasing. In order to do so, we need to rewind the repository back in time before the first merge, and then redo the same steps, but using rebasing rather than merging.

We will make use the of the `reset` command to wind the branches back in time.

## Lab 32: Resetting the Greet Branch

**Reset the greet branch**

Let's go back in time on the greet branch to the point *before* we merged main onto it. We can **reset** a branch to any commit we want. Essentially this is modifying the branch pointer to point to anywhere in the commit tree.

In this case we want to back greet up to the point prior to the merge with main. We need to find the last commit before the merge.

```shell
$ git checkout greet
Already on 'greet'
$ git hist
*   73db54b 2023-06-10 | Merged main fixed conflict. (HEAD -> greet) [Jim Weirich]
|\  
| * 3787562 2023-06-10 | Made interactive (main) [Jim Weirich]
* | 82a2988 2023-06-10 | Merge branch 'main' into greet [Jim Weirich]
|\| 
| * 976950b 2023-06-10 | Added README [Jim Weirich]
* | c1a7120 2023-06-10 | Updated Rakefile [Jim Weirich]
* | 959a7cb 2023-06-10 | Hello uses Greeter [Jim Weirich]
* | cab1837 2023-06-10 | Added greeter class [Jim Weirich]
|/  
* cdceefa 2023-06-10 | Added a Rakefile. [Jim Weirich]
* 22273f2 2023-06-10 | Moved hello.rb to lib [Jim Weirich]
* 186488e 2023-06-10 | Add an author/email comment [Jim Weirich]
* e4e3645 2023-06-10 | Added a comment (tag: v1) [Jim Weirich]
* a6b268e 2023-06-10 | Added a default value (tag: v1-beta) [Jim Weirich]
* 174dfab 2023-06-10 | Using ARGV [Jim Weirich]
* f7c41d3 2023-06-10 | First Commit [Jim Weirich]
```

That's a bit hard to read, but looking at the data we see that the "Updated Rakefile" commit was the last commit on the greet branch before merging. Let's reset the greet branch to that commit.

```shell
$ git reset --hard c1a7120
HEAD is now at c1a7120 Updated Rakefile
```

**Check the branch.**

Look at the log for the greet branch. We no longer have the merge commits in its history.

```shell
$ git hist --all
* 3787562 2023-06-10 | Made interactive (main) [Jim Weirich]
* 976950b 2023-06-10 | Added README [Jim Weirich]
| * c1a7120 2023-06-10 | Updated Rakefile (HEAD -> greet) [Jim Weirich]
| * 959a7cb 2023-06-10 | Hello uses Greeter [Jim Weirich]
| * cab1837 2023-06-10 | Added greeter class [Jim Weirich]
|/  
* cdceefa 2023-06-10 | Added a Rakefile. [Jim Weirich]
* 22273f2 2023-06-10 | Moved hello.rb to lib [Jim Weirich]
* 186488e 2023-06-10 | Add an author/email comment [Jim Weirich]
* e4e3645 2023-06-10 | Added a comment (tag: v1) [Jim Weirich]
* a6b268e 2023-06-10 | Added a default value (tag: v1-beta) [Jim Weirich]
* 174dfab 2023-06-10 | Using ARGV [Jim Weirich]
* f7c41d3 2023-06-10 | First Commit [Jim Weirich]
```
## Lab 33: Resetting the Main Branch

**Reset the main branch**

When we added the interactive mode to the main branch, we made a change that conflicted with changes in the greet branch. Let's rewind the main branch to a point before the conflicting change. This allows us to demonstrate the rebase command without worrying about conflicts.

```shell
$ git checkout main
$ git hist
* 3787562 2023-06-10 | Made interactive (HEAD -> main) [Jim Weirich]
* 976950b 2023-06-10 | Added README [Jim Weirich]
* cdceefa 2023-06-10 | Added a Rakefile. [Jim Weirich]
* 22273f2 2023-06-10 | Moved hello.rb to lib [Jim Weirich]
* 186488e 2023-06-10 | Add an author/email comment [Jim Weirich]
* e4e3645 2023-06-10 | Added a comment (tag: v1) [Jim Weirich]
* a6b268e 2023-06-10 | Added a default value (tag: v1-beta) [Jim Weirich]
* 174dfab 2023-06-10 | Using ARGV [Jim Weirich]
* f7c41d3 2023-06-10 | First Commit [Jim Weirich]
```

The 'Added README' commit is the one directly before the conflicting interactive mode. We will reset the main branch to 'Added README' commit.

```shell
git reset --hard <hash>
git hist --all
```

Review the log. It should look like the repository has been wound back in time to the point before we merged anything.

```shell
$ git hist --all
* 976950b 2023-06-10 | Added README (HEAD -> main) [Jim Weirich]
| * c1a7120 2023-06-10 | Updated Rakefile (greet) [Jim Weirich]
| * 959a7cb 2023-06-10 | Hello uses Greeter [Jim Weirich]
| * cab1837 2023-06-10 | Added greeter class [Jim Weirich]
|/  
* cdceefa 2023-06-10 | Added a Rakefile. [Jim Weirich]
* 22273f2 2023-06-10 | Moved hello.rb to lib [Jim Weirich]
* 186488e 2023-06-10 | Add an author/email comment [Jim Weirich]
* e4e3645 2023-06-10 | Added a comment (tag: v1) [Jim Weirich]
* a6b268e 2023-06-10 | Added a default value (tag: v1-beta) [Jim Weirich]
* 174dfab 2023-06-10 | Using ARGV [Jim Weirich]
* f7c41d3 2023-06-10 | First Commit [Jim Weirich]
```

## Lab 34: Rebasing

Ok, we are back in time before the first merge and we want to get the changes in main into our greet branch.

This time we will use the rebase command instead of the merge command to bring in the changes from the main branch.

```shell
$ go greet
Switched to branch 'greet'
$
$ git rebase main
First, rewinding head to replay your work on top of it...
Applying: added Greeter class
Applying: hello uses Greeter
Applying: updated Rakefile
$
$ git hist
* 5f626c6 2023-06-10 | Updated Rakefile (HEAD -> greet) [Jim Weirich]
* 24d82d4 2023-06-10 | Hello uses Greeter [Jim Weirich]
* 619f552 2023-06-10 | Added greeter class [Jim Weirich]
* 976950b 2023-06-10 | Added README (main) [Jim Weirich]
* cdceefa 2023-06-10 | Added a Rakefile. [Jim Weirich]
* 22273f2 2023-06-10 | Moved hello.rb to lib [Jim Weirich]
* 186488e 2023-06-10 | Add an author/email comment [Jim Weirich]
* e4e3645 2023-06-10 | Added a comment (tag: v1) [Jim Weirich]
* a6b268e 2023-06-10 | Added a default value (tag: v1-beta) [Jim Weirich]
* 174dfab 2023-06-10 | Using ARGV [Jim Weirich]
* f7c41d3 2023-06-10 | First Commit [Jim Weirich]
```

**Merge VS Rebase**

The final result of the rebase is very similar to the merge. The greet branch now contains all of its changes, as well as all the changes from the main branch. However, the commit tree is quite different. The commit tree for the greet branch has been rewritten so that the main branch is a part of the commit history. This leaves the chain of commits linear and much easier to read.

**When to Rebase, When to Merge?**

Don't use rebase …

1. If the branch is public and shared with others. Rewriting publicly shared branches will tend to screw up other members of the team.
1. When the exact history of the commit branch is important (since rebase rewrites the commit history).

Given the above guidelines, I tend to use rebase for short-lived, local branches and merge for branches in the public repository.

## Lab 35: Merging Back to Main

We've kept our greet branch up to date with main (via rebase), now let's merge the greet changes back into the main branch.

**Merge greet into main**

```shell
$ git checkout main
Switched to branch 'main'
$
$ git merge greet
Updating 976950b..5f626c6
Fast-forward
 Rakefile       | 2 +-
 lib/greeter.rb | 8 ++++++++
 lib/hello.rb   | 6 ++++--
 3 files changed, 13 insertions(+), 3 deletions(-)
 create mode 100644 lib/greeter.rb
```

Because the head of main is a direct ancestor of the head of the greet branch, git is able to do a fast-forward merge. When fast-forwarding, the branch pointer is simply moved forward to point to the same commit as the greeter branch.

There will never be conflicts in a fast-forward merge.

**Review the logs**

```shell
$ git hist
* 5f626c6 2023-06-10 | Updated Rakefile (HEAD -> main, greet) [Jim Weirich]
* 24d82d4 2023-06-10 | Hello uses Greeter [Jim Weirich]
* 619f552 2023-06-10 | Added greeter class [Jim Weirich]
* 976950b 2023-06-10 | Added README [Jim Weirich]
* cdceefa 2023-06-10 | Added a Rakefile. [Jim Weirich]
* 22273f2 2023-06-10 | Moved hello.rb to lib [Jim Weirich]
* 186488e 2023-06-10 | Add an author/email comment [Jim Weirich]
* e4e3645 2023-06-10 | Added a comment (tag: v1) [Jim Weirich]
* a6b268e 2023-06-10 | Added a default value (tag: v1-beta) [Jim Weirich]
* 174dfab 2023-06-10 | Using ARGV [Jim Weirich]
* f7c41d3 2023-06-10 | First Commit [Jim Weirich]
```

The greet and main branches are now identical.

## Lab 36: Multiple Repositories

Up to this point we have been working with a single git repository. However, git excels at working with multiple repositories. These extra repositories may be stored locally, or may be accessed across a network connection.

In the next section we will create a new repository called "cloned_hello". We will show how to move changes from one repository to another, and how to handle conflicts when they arise between two repositories.

<p align="center">
    <img src="images/git_clone.png" width="50%"> 
</p>

For now, we will be working with local repositories (i.e. repositories stored on your local hard disk), however most of the things learned in this section will apply to multiple repositories whether they are stored locally or remotely over a network.

**NOTE**: We are going be making changes to both copies of our repositories. Make sure you pay attention to which repository you are in at each step of the following labs.

## Lab 37: Cloning Repositories

Go to the work directory
Go to the working directory and make a clone of your hello repository.

```shell
$ cd ..
$ pwd
/Users/jim/Downloads/git_tutorial/work
$ ls
hello
```

At this point you should be in your "work" directory. There should be a single repository here named "hello".

**Create a clone of the hello repository**

Let's make a clone of the repository.

```shell
$ git clone hello cloned_hello
Cloning into 'cloned_hello'...
done.
$ ls
cloned_hello
hello
```

There should now be two repositories in your work directory: the original "hello" repository and the newly cloned "cloned_hello" repository.

## Lab 38: Review the Cloned Repository

**Look at the cloned repository**

Let's take a look at the cloned repository.

```shell
$ cd cloned_hello
$ ls
README
Rakefile
lib
```
You should see a list of all the files in the top level of the original repository (`README`, `Rakefile` and `lib`).

**Review the Repository History**

```shell
$ git hist --all
* 5f626c6 2023-06-10 | Updated Rakefile (HEAD -> main, origin/main, origin/greet, origin/HEAD) [Jim Weirich]
* 24d82d4 2023-06-10 | Hello uses Greeter [Jim Weirich]
* 619f552 2023-06-10 | Added greeter class [Jim Weirich]
* 976950b 2023-06-10 | Added README [Jim Weirich]
* cdceefa 2023-06-10 | Added a Rakefile. [Jim Weirich]
* 22273f2 2023-06-10 | Moved hello.rb to lib [Jim Weirich]
* 186488e 2023-06-10 | Add an author/email comment [Jim Weirich]
* e4e3645 2023-06-10 | Added a comment (tag: v1) [Jim Weirich]
* a6b268e 2023-06-10 | Added a default value (tag: v1-beta) [Jim Weirich]
* 174dfab 2023-06-10 | Using ARGV [Jim Weirich]
* f7c41d3 2023-06-10 | First Commit [Jim Weirich]
```

You should now see a list of all the commits in the new repository, and it should (more or less) match the history of commits in the original repository. The only difference should be in the names of the branches.

**Remote branches**

You should see a **main** branch (along with **HEAD**) in the history list. But you will also have a number of strangely named branches (**origin/main**, **origin/greet** and **origin/HEAD**). We'll talk about them in a bit.

## Lab 39: What is Origin?

```shell
$ git remote
origin
```

We see that the cloned repository knows about a remote repository named origin. Let's see if we can get more information about origin:

```shell
$ git remote show origin
warning: more than one branch.main.remote
* remote origin
  Fetch URL: /Users/jim/Downloads/git_tutorial/work/hello
  Push  URL: /Users/jim/Downloads/git_tutorial/work/hello
  HEAD branch: main
  Remote branches:
    greet tracked
    main  tracked
  Local branches configured for 'git pull':
    main   merges with remote main
              and with remote main
    master merges with remote master
  Local ref configured for 'git push':
    main pushes to main (up to date)
```

Now we see that the remote repository "origin" is simply the original hello repository. Remote repositories typically live on a separate machine, possibly a centralized server. As we can see here, however, they can just as well point to a repository on the same machine. There is nothing particularly special about the name "origin", however the convention is to use the name "origin" for the primary centralized repository (if there is one).

## Lab 40: Remote Branches

Let's look at the branches available in our cloned repository.

```shell
$ git branch
* main
```

That's it, only the main branch is listed. Where is the greet branch? The **git branch** command only lists the local branches by default.

**List Remote Branches**

```shell
$ git branch -a
* main
  remotes/origin/HEAD -> origin/main
  remotes/origin/greet
  remotes/origin/main
```

Git has all the commits from the original repository, but branches in the remote repository are not treated as local branches here. If we want our own **greet** branch, we need to create it ourselves. We will see how to do that in a minute.

## Lab 41: Change the Original Repository

**Make a change in the original hello repository**

```shell
cd ../hello
# (You should be in the original hello repository now)
```

**NOTE**: Now in the hello repo

Make the following changes to README:

```
#README
This is the Hello World example from the git tutorial.
(changed in original)
```

Now add and commit this change

```shell
git add README
git commit -m "Changed README in original repo"
```

## Lab 42: Fetching Changes

Learn how to pull changes from a remote repository.

```shell
$ cd ../cloned_hello
$ git fetch
From /Users/jim/Downloads/git_tutorial/work/hello
   5f626c6..5e2d55e  main       -> origin/main
$ git hist --all
* 5e2d55e 2023-06-10 | Changed README in original repo (origin/main, origin/HEAD) [Jim Weirich]
* 5f626c6 2023-06-10 | Updated Rakefile (HEAD -> main, origin/greet) [Jim Weirich]
* 24d82d4 2023-06-10 | Hello uses Greeter [Jim Weirich]
* 619f552 2023-06-10 | Added greeter class [Jim Weirich]
* 976950b 2023-06-10 | Added README [Jim Weirich]
* cdceefa 2023-06-10 | Added a Rakefile. [Jim Weirich]
* 22273f2 2023-06-10 | Moved hello.rb to lib [Jim Weirich]
* 186488e 2023-06-10 | Add an author/email comment [Jim Weirich]
* e4e3645 2023-06-10 | Added a comment (tag: v1) [Jim Weirich]
* a6b268e 2023-06-10 | Added a default value (tag: v1-beta) [Jim Weirich]
* 174dfab 2023-06-10 | Using ARGV [Jim Weirich]
* f7c41d3 2023-06-10 | First Commit [Jim Weirich]
```

At this point the repository has all the commits from the original repository, but they are not integrated into the cloned repository's local branches.

Find the "Changed README in original repo" commit in the history above. Notice that the commit includes "origin/main" and "origin/HEAD".

Now look at the "Updated Rakefile" commit. You will see that the local main branch points to this commit, not to the new commit that we just fetched.

The upshot of this is that the "git fetch" command will fetch new commits from the remote repository, but it will not merge these commits into the local branches.

**Check the README**

We can demonstrate that the cloned README is unchanged.

```shell
$ cat README
This is the Hello World example from the git tutorial.
```

## Lab 43: Merging Pulled Changes

**Merge the fetched changes into local main**

```shell
$ git merge origin/main
Updating 5f626c6..5e2d55e
Fast-forward
 README | 1 +
 1 file changed, 1 insertion(+)
```

**Check the README again**

We should see the changes now.

```shell
$ cat README
This is the Hello World example from the git tutorial.
(changed in original)
```

There are the changes. Even though "git fetch" does not merge the changes, we can still manually merge the changes from the remote repository.

## Lab 44: Pulling Changes

We're not going to go through the process of creating another change and pulling it again, but we do want you to know that doing:

```shell
git pull
```

is indeed equivalent to the two steps:

```shell
git fetch
git merge origin/main
```

## Lab 45: Adding a Tracking Branch

The branches starting with remotes/origin are branches from the original repo. Notice that you don't have a branch called greet anymore, but it knows that the original repo had a greet branch.

**Add a local branch that tracks a remote branch.**

```shell
$ git branch --track greet origin/greet
Branch 'greet' set up to track remote branch 'greet' from 'origin'.
$ git branch -a
  greet
* main
  remotes/origin/HEAD -> origin/main
  remotes/origin/greet
  remotes/origin/main
$ git hist --max-count=2
* 5e2d55e 2023-06-10 | Changed README in original repo (HEAD -> main, origin/main, origin/HEAD) [Jim Weirich]
* 5f626c6 2023-06-10 | Updated Rakefile (origin/greet, greet) [Jim Weirich]
```

We can now see the greet branch in the branch list and in the log.

## Lab 46: Bare Repositories

Bare repositories (without working directories) are usually used for sharing.

**Create a bare repository.**

```shell
$ git clone --bare hello hello.git
Cloning into bare repository 'hello.git'...
done.
$ ls hello.git
HEAD
config
description
hooks
info
objects
packed-refs
refs
```

The convention is that repositories ending in '.git' are bare repositories. We can see that there is no working directory in the hello.git repo. Essentially it is nothing but the .git directory of a non-bare repo.

## Lab 47: Adding a Remote Repository

Add the bare repository as a remote to our original repository.
Let's add the hello.git repo to our original repo.

```shell
cd hello
git remote add shared ../hello.git
```

**NOTE**: Now in the hello repository.

## Lab 48: Pushing a Change

Since bare repositories are usually shared on some sort of network server, it is usually difficult to cd into the repo and pull changes. So we need to push our changes into other repositories.

Let's start by creating a change to be pushed. Edit the README and commit it

```
# README
This is the Hello World example from the git tutorial.
(Changed in the original and pushed to shared)
```

```shell
git checkout main
git add README
git commit -m "Added shared comment to readme"
```

Now push the change to the shared repo.

```shell
git push shared main
```

*shared* is the name of the repository receiving the changes we are pushing. (Remember, we added it as a remote in the previous lab.)

```shell
$ git push shared main
To ../hello.git
   5e2d55e..7b4a53a  main -> main
```

**NOTE**: We had to explicitly name the branch main that was receiving the push. It is possible to set it up automatically, but I never remember the commands to do that. Check out the "Git Remote Branch" gem for easy management of remote branches.

## Lab 49: Pulling Shared Changes

Quick hop over to the clone repository and let's pull down the changes just pushed to the shared repo.

```shell
cd ../cloned_hello
git remote add shared ../hello.git
git branch --track shared main
git pull shared main
cat README
```

## Lab 50: Hosting your Git Repositories

There are many ways to share git repositories over the network. Here is a quick and dirty way.

**Start up the git server**


```shell
# (From the work directory)
git daemon --verbose --export-all --base-path=.
```

Now, in a separate terminal window, go to your work directory

```shell
# (From the work directory)
git clone git://localhost/hello.git network_hello
cd network_hello
ls
```

You should see a copy of hello project.

**Pushing to the Git Daemon**

If you want to push to the git daemon repository, add `--enable=receive-pack` to the git daemon command. Be careful because there is no authentication on this server, anyone could push to your repository.

## References
 - https://gitimmersion.com