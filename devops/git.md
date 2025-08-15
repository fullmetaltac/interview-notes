# Table of Contents
- [Table of Contents](#table-of-contents)
  - [Setup](#setup)
  - [Create a Project](#create-a-project)
  - [Checking Status](#checking-status)
  - [Making Changes](#making-changes)
  - [Staging Changes](#staging-changes)
  - [Staging and Committing](#staging-and-committing)
  - [Committing Changes](#committing-changes)
  - [Changes, not Files](#changes-not-files)
  - [History](#history)
  - [Aliases](#aliases)
  - [Getting Old Versions](#getting-old-versions)
  - [Tagging versions](#tagging-versions)
  - [Undoing Local Changes (before staging)](#undoing-local-changes-before-staging)
  - [Undoing Staged Changes (before committing)](#undoing-staged-changes-before-committing)
  - [Undoing Committed Changes](#undoing-committed-changes)
  - [Removing Commits from a Branch](#removing-commits-from-a-branch)
  - [Remove the oops tag](#remove-the-oops-tag)
  - [References](#references)

## Setup

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

## Create a Project

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

## Checking Status

**Check the status of the repository**

Use the `git status` command to check the current status of the repository.

```shell
$ git status
On branch main
nothing to commit, working tree clean
```

The status command reports that there is nothing to commit. This means that the repository has all the current state of the working directory. There are no outstanding changes to record.

We will use the `git status` command to continue to monitor the state between the repository and the working directory.

## Making Changes

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

## Staging Changes

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


## Staging and Committing

A separate staging step in git is in line with the philosophy of getting out of the way until you need to deal with source control. You can continue to make changes to your working directory, and then at the point you want to interact with source control, git allows you to record your changes in small commits that record exactly what you did.

For example, suppose you edited three files (`a.rb`, `b.rb`, and `c.rb`). Now you want to commit all the changes, but you want the changes in `a.rb` and `b.rb` to be a single commit, while the changes to `c.rb` are not logically related to the first two files and should be a separate commit.

```shell
git add a.rb
git add b.rb
git commit -m "Changes for a and b"
git add c.rb
git commit -m "Unrelated change to c"
```

## Committing Changes

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

## Changes, not Files

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

## History

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

## Aliases

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

## Getting Old Versions

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

## Tagging versions

**Tagging version 1**

```shell
git tag v1
```

Now you can refer to the current version of the program as v1.

**Tagging Previous Versions**

Let’s tag the version immediately prior to the current version v1-beta. First we need to checkout the previous version. Rather than look up the hash, we will use the `^` notation to indicate "the parent of v1".

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

## Undoing Local Changes (before staging)

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
We see that the `hello.rb` file has been modified, but hasn’t been staged yet.

**Revert the changes in the working directory**

Use the `checkout` command to checkout the repository’s version of the `hello.rb` file.

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

## Undoing Staged Changes (before committing)

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

The `reset` command (by default) doesn’t change the working directory. So the working directory still has the unwanted comment in it. We can use the `checkout` command of the previous lab to remove the unwanted change from the working directory.

**Note**: You could also have used the `git restore` command to restore just the single file.

**Checkout the Committed Version**

```shell
$ git status
On branch main
nothing to commit, working tree clean
```
And our working directory is clean once again.

## Undoing Committed Changes

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

## Removing Commits from a Branch

The `revert` command of the previous section is a powerful command that lets us undo the effects of any commit in the repository. However, both the original commit and the "undoing" commit are visible in the branch history (using the `git log` command).

Often we make a commit and immediately realize that it was a mistake. It would be nice to have a “take back” command that would allow us to pretend that the incorrect commit never happened. The "take back" command would even prevent the bad commit from showing up the `git log` history. It would be as if the bad commit never happened.

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

We see that we have an "Oops" commit and a "Revert Oops" commit as the last two commits made in this branch. Let’s remove them using reset.

**First, Mark this Branch**
But before we remove the commits, let’s mark the latest commit with a tag so we can find it again.

```shell
git tag oops
```

**Reset to Before Oops**

Looking at the log history (above), we see that the commit tagged ‘v1’ is the commit right before the bad commit. Let’s reset the branch to that point. Since that branch is tagged, we can use the tag name in the reset command (if it wasn’t tagged, we could just use the hash value).

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

But what happened to the bad commits? It turns out that the commits are still in the repository. In fact, we can still reference them. Remember that at the beginning of this lab we tagged the reverting commit with the tag "oops". Let’s look at all the commits.

```shell
$ git hist --all
* 8b71812 2023-06-10 | Revert "Oops, we didn't want this commit" (tag: oops) [Jim Weirich]
* 146fb71 2023-06-10 | Oops, we didn't want this commit [Jim Weirich]
* e4e3645 2023-06-10 | Added a comment (HEAD -> main, tag: v1) [Jim Weirich]
* a6b268e 2023-06-10 | Added a default value (tag: v1-beta) [Jim Weirich]
* 174dfab 2023-06-10 | Using ARGV [Jim Weirich]
* f7c41d3 2023-06-10 | First Commit [Jim Weirich]
```

Here we see that the bad commits haven’t disappeared. They are still in the repository. It’s just that they are no longer listed in the main branch. If we hadn’t tagged them, they would still be in the repository, but there would be no way to reference them other than using their hash names. Commits that are unreferenced remain in the repository until the system runs the garbage collection software.

**Dangers of Reset**

Resets on local branches are generally safe. Any "accidents" can usually be recovered from by just resetting again with the desired commit.

However, if the branch is shared on remote repositories, resetting can confuse other users sharing the branch.

---

## Remove the oops tag

## References
 - https://gitimmersion.com