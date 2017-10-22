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
* Basic git demo
^
* From the bottom: piping
^
* Typical git commands: porcelain
^
* GitHub collaborations

-------------------------------------------------

-> # What is git? 

* git is a **local** version control system for tracking changes in files.
^
* Created by Linus Torvalds (inventor of Linux) in 2005
^
* Wanted something fast, free and *decentralized*
^
* git is *distributed*: everyone has a full *independent* history and copy of the files.

-------------------------------------------------

-> # Fun facts about git

* git is British slang for 'unpleasant person'
^
> "I'm an egotistical bastard, and I name all my projects after myself. First 'Linux', now 'git'." - Linus Torvalds
^
* git is now the most widely used VCS
	- Google
	- Netflix
	- Facebook
	- Twitter
	- Android

-------------------------------------------------
-> # git vs GitHub

-------------------------------------------------
-> # Initializing your repository

* Create a directory where you will store your project.
^

`mkdir Git_Tutorial`
`cd Git_Tutorial`
^

* Initialize git for your directory.
^

`git init`
^

* Creates a *hidden* folder `.git` where all content and history of your repository is stored.
^
* All `git` commands follow the word `git`

-------------------------------------------------
-> # Track some files

* Create some files to track
^

`echo "condensed matter matters" > cmgs.txt`
`echo "not tracking" > hi.txt`
^

* We have to tell git which files to track.
^

`git add cmgs.txt`
^

Now git is tracking changes to `cmgs.txt`

-------------------------------------------------
-> # Check the status of your repo

`git status`
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
-> # Make a change to track

Let's add a line to the end of our file.

`echo "actually no" >> cmgs.txt`
`git status`


-------------------------------------------------
-> # Supported markdown formatting <-

The input file is split into multiple slides by
horizontal rules (hr). A hr consisting of at
least 3 *\** or *-*. It can also contain spaces but
no other characters.

Each of these represents the start of a new slide.

\* \* \*
\---
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*
\- - -

-------------------------------------------------

-> # Supported markdown formatting <-

First-level headers can be prefixed by single *#*
or underlined by *===*.

\# first-level

becomes

# first-level

-------------------------------------------------

-> # Supported markdown formatting <-

Second-level headers can be prefixed by *##* or
underlined by *---*.

second-level
\------------

becomes

second-level
------------


-------------------------------------------------

-> # Supported markdown formatting's <-

Inline codes are surrounded with backticks.

C program starts with \`main()\`.

becomes

C program starts with `main()`.

-------------------------------------------------

-> # Supported markdown formatting <-

Code blocks are automatically detected by 4 spaces
at the beginning of a line.

Tabs are automatically expanded to 4 spaces while
parsing the input.

\    int main(int argc, char \*argv[]) {
\        printf("%s\\n", "Hello world!");
\    }

becomes

    int main(int argc, char *argv[]) {
        printf("%s\n", "Hello world!");
    }

-------------------------------------------------

-> # Supported markdown formatting <-

You can also use [pandoc](http://pandoc.org/demo/example9/pandocs-markdown.html)'s fenced code block
extension. Use at least three ~ chars to open and
at least as many or more ~ for closing.

\~~~ {.numberLines}
\int main(int argc, char \*argv[]) {
\    printf("%s\\n", "Hello world!");
\}
\~~~~~~~~~~~~~~~~~~

becomes

~~~ {.numberLines}
int main(int argc, char *argv[]) {
    printf("%s\n", "Hello world!");
}
~~~~~~~~~~~~~~~~~~

Pandoc attributes (like ".numberlines" etc.)
will be ignored

-------------------------------------------------

-> # Supported markdown formatting <-

You can also use [github](https://guides.github.com/features/mastering-markdown/#GitHub-flavored-markdown) flavored markdown's
code block. Use at least three backticks to open
and at least as many or more backticks for closing.

\```
\int main(int argc, char \*argv[]) {
\    printf("%s\\n", "Hello world!");
\}
\```

becomes

```
int main(int argc, char *argv[]) {
    printf("%s\n", "Hello world!");
}
```

Language hint will be ignored

-------------------------------------------------

-> # Supported markdown formatting <-

Quotes are auto-detected by preceding *>*.

Multiple *>* are interpreted as nested quotes.

\> quote
\>> nested quote 1
\> > nested quote 2

becomes

> quote
>> nested quote 1
> > nested quote 2

-------------------------------------------------

-> # Supported markdown formatting <-

Inline highlighting is supported as followed:

\- *\** colors text as red
\- *\_* underlines text

\_some\_ \*highlighted\* \_\*text\*\_

becomes

_some_ *highlighted* _*text*_

-------------------------------------------------

-> # Supported markdown formatting <-

Backslashes force special markdown characters
like *\**, *\_*, *#* and *>* to be printed as
normal characters.

\\\*special\\\*

becomes

\*special\*

-------------------------------------------------

-> # Supported markdown formatting <-

Leading *\** or *-* indicate lists.

list
\* major
\    - minor
\        - \*important\*
\          detail
\    - minor

becomes

list
* major
    - minor
        - *important*
          detail
    - minor

-------------------------------------------------

-> # Supported markdown formatting <-

A single *\<br\>* or *^* in a line indicates mdp
to stop the output on that position.

This can be used to show bullet points
line by line.

*\<br\>* is also not displayed in HTML converted
output.

Agenda
<br>
* major
<br>
    * minor
<br>
* major
  ^
    * minor
      ^
        * detail

-------------------------------------------------

-> # Supported markdown formatting <-

Leading *->* indicates centering.

\-> # test <-
\-> ## test <-
\-> test
\-> \_\*test\*\_ <-

becomes

-> # test <-
-> ## test <-
-> test
-> _*test*_ <-

-------------------------------------------------

-> # Supported markdown formatting <-

URL in pandoc style are supported:

\[Google](http://www.google.com/)

becomes

[Google](http://www.google.com/)

-------------------------------------------------

-> ## More information about markdown <-

can be found in the [markdown documentation](http://daringfireball.net/projects/markdown/).

-------------------------------------------------

-> # Support for UTF-8 special characters <-

Here are some examples.

ae = ä, oe = ö, ue = ü, ss = ß
upsilon = Ʊ, phi = ɸ

▛▀▀▀▀▀▀▀▀▀▜
▌rectangle▐
▙▄▄▄▄▄▄▄▄▄▟


-------------------------------------------------

-> # Suspend your presentation for hands-on examples <-

Use *Ctrl + z* to suspend the presentation.

Use *fg* to resume it.

-------------------------------------------------

-> # Convert your presentation to PDF <-

To publish your presentation later on, you may
want to convert it to PDF.

This can be achieved by two additional tools:

\- *markdown* to convert to HTML
\- *wkhtmltopdf* to convert from HTML to PDF

After installing them, you can simply type:

    $ markdown sample.md | wkhtmltopdf - sample.pdf

-------------------------------------------------

-> ## Last words <-

I hope you like *mdp*.

If you observe strange behavior, feel free to
open an issue on [GitHub](https://github.com/visit1985/mdp).
