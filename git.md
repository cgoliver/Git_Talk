-------------------------------------------------

-> +-+-+-+-+-+ +-+-+-+
-> |C|M|G|S|:| |g|i|t|
-> +-+-+-+-+-+ +-+-+-+

-> Carlos G. Oliver
-> cgoliver@protonmail.com
-> www.cgoliver.com

-> October 23, 2017

-> # Learning git from the bottom up. <-

## Outline:
^
* What/why is git?
^
* git vs [GitHub](www.github.com)
^
* git quick start 
^
* From the bottom: piping
^
* GitHub collaborations

-------------------------------------------------

-> # What is git? 

git is a **local** version control system for tracking changes in files.
^

Created by Linus Torvalds (inventor of Linux) in 2005
^

Wanted something fast, free and *decentralized*
^

git is *distributed*: everyone has a full *independent* history and copy of the files.

-------------------------------------------------

-> # Fun facts about git

git is British slang for 'unpleasant person'
^

> "I'm an egotistical bastard, and I name all my projects after myself. First 'Linux', now 'git'." - Linus Torvalds
^

git is now the most widely used VCS in the world.
	- Google
	- Netflix
	- Facebook
	- Twitter
	- Android

-------------------------------------------------
-> # git vs GitHub
Git is an *offline* tool for version control.
^

* GitHub is an *online* service for hosting and managing *git* repositories.
^
	- You can set up your own [git server](https://git-scm.com/book/en/v2/Git-on-the-Server-Setting-Up-the-Server)

-------------------------------------------------
-> # Initializing your repository

Create a directory where you will store your project.
^

`$ mkdir Git_Tutorial`
`$ cd Git_Tutorial`
^

Initialize git for your directory.

^
`$ git init`
^

Creates a *hidden* folder `.git` where all content and history of your repository is stored.

^
All `git` commands follow the word `git`

-------------------------------------------------
-> # Track some files

Create some files to track
^

`$ echo "condensed matter matters" > cmgs.txt`
`$ echo "not tracking" > hi.txt`
^

We have to tell git which files to track.
^

`$ git add cmgs.txt`
^

Now git is tracking changes to `cmgs.txt`

-------------------------------------------------
-> # Check the status of your repo

`$ git status`
^

Prints information on the repo.
^
* Changes to tracked files
^
* New files added 
^
* Untracked files, etc.
^
Useful to run regularly.

-------------------------------------------------
-> # Writing to history

Adding a file is something we want to go down in history.
^

Writing the current state of the repo
is called *committing*
^

`$ git commit -m "first commit."`
^

Commits require a message describing the change.

-------------------------------------------------
-> # Make a change to track

Let's add a line to the end of our file.

`$ echo "actually no" >> cmgs.txt`
`$ git status`
^

We should see that git noticed a change.

-------------------------------------------------
-> # See the changes

`$ git diff`
^

Displays differences between last commit
and current state.


-------------------------------------------------
-> # Stage changes

If we like the changes we can tell git to track them.
^

`$ git add cmgs.txt`
^

Let's commit the new version to history.
^

`$ git commit -m "new line"`

-------------------------------------------------
-> # Viewing repo history

`$ git log`
^

Displays all the commits, who made them and when.

-------------------------------------------------
-> # We can go back in time

`$ git checkout [commit ID\] `
^

Brings the repo to the state at the given commit.
^

Once you're done looking around you can go back 
to the present.
^

`$ git checkout master`

-------------------------------------------------
-> # Branching

Let's say you want to test a different version
without affecting the rest of the repo.
^

You can create a new independent copy of the repo 
with the same history as the original.
^

`$ git branch test` 
^

Creates a new branch called `test`
^

You can checkout a branch.
^

`$ git checkout test`
^

You can commit changes to `test` and they will stay
in `test`.

`$ echo "hi from test" >> cmgs.txt"`
`$ git checkout master`

-------------------------------------------------
-> # Merging

If you liked how things worked in the test branch
you can merge them to the main, aka master branch.

`$ git merge test`

-------------------------------------------------
-> # Okay now some plumbing

You can get by quite nicely with these commands.

Git calls these the porcelain commands.

To really understand what's happening we have to
look at the ugly plumbing. 

-------------------------------------------------
-> # Git Objects

Git stores data in 3 major object types:
^

1. blob
^
2. tree
^
3. commit
^

All the commands we saw mainpulate there 3 object
types.

Most of the info I am presenting on git internals
is taken from the [Pro Git book](https://git-scm.com/book/en/v2/Git-Internals-Git-Objects).

-------------------------------------------------
-> # blobs

blobs are the way git stores *file contents*
^

Every version of a file is a different blob.
^

git is a _content addressable_ file-system.
^
	* Data in a repo is accessed based on its *content*.


-------------------------------------------------
-> # making a blob

Let's make a new repo to play around
with the plumbing.
^

```
$ cd ..
$ git init Plumbing
```

Git computes the [SHA1](https://en.wikipedia.org/wiki/SHA-1) hash
of the file's contents and an automatically generated header.

We can hash content from stdin:
^

```
$ echo "condensed matter matters" | git hash-object --stdin 
b1a1b80ca6f24ccdd220d8db24af08db4e096970
```

Or from a file:
^
```
$ echo "condensed matter matters" > cmgs.txt
$ git hash-object cmgs.txt
b1a1b80ca6f24ccdd220d8db24af08db4e096970
```
^

-------------------------------------------------

-> # Storing objects

If we want git to store the result use `-w`

```
$ git hash-object -w cmgs.txt
```

This creates a compressed file in `.git/objects`

```
$ find .git/objects -type f
.git/objects/b1/a1b80ca6f24ccdd220d8db24af08db4e096970
```

-------------------------------------------------
-> # Low level version control

Let's make a new version of the file.
^

```
$ echo "condensed matter doesn't matter" > cmgs.txt
$ git hash-object -w cmgs.txt
```

Now we have two objects stores
^

```
$ find .git/objects -type f
.git/objects/3a/918db0eb98806e55545a8457d5fa3675f5270c
.git/objects/b1/a1b80ca6f24ccdd220d8db24af08db4e096970
```

-------------------------------------------------
-> # Reading blobs

Since the hash depends on the content, we have 
a content-addressable filesystem.
^

First version
^
```
$ git cat-file -p b1a1b80ca6f24ccdd220d8db24af08db4e096970
Condensed matter matters
```
^
Second version
^
```
$ git cat-file -p 3a918db0eb98806e55545a8457d5fa3675f5270c
Condensed matter doesn't matter
```
^
We can revert back to the original version.
```
$ git cat-file -p b1a1b80ca6f24ccdd220d8db24af08db4e096970 > cmgs.txt
```
^

So now we pretty much have a version control system!
^

However, not very user-friendly.

-------------------------------------------------

-> # Suspend your presentation for hands-on examples <-

Use *Ctrl + z* to suspend the presentation.

Use *fg* to resume it.

