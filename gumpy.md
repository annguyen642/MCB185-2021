GUMPy
=====

Author: Ian Korf

## Introduction ##

GUMPy is a quick introduction to the tools of the trade for the emerging
bioinformatics programmer: GitHub, Unix, Markdown, and Python. Most of this
document is about Unix.

## Unix vs. Linux ##

Most people about to embark on an adventure in bioinformatics programming will
be using some flavor of Linux (e.g. Debian, Fedora, Mint, Ubuntu, etc.) and not
actually Unix. Is there a difference between Linux and Unix? Practically, no,
but philisophically, yes. Linux was designed to behave just like Unix, so they
are supposed to be very similar. However, Unix has its roots as a commercial
product and Linux has its roots in open source free software. In this document,
the terms _Linux_ and _Unix_ are used somewhat interchangeably.

## Where do I get Linux? ##

Before we begin, you need a command line Linux environment on your computer. Why
a CLI (command line interface) rather than a GUI (graphical user interface)?
When it comes to automating tasks, it's easier to automate text commands than
mouse clicks. Also, most computer clusters run Linux because it's free and
robust. For these reasons, most professional bioinformatics is done with a Linux
CLI. If you have any aspirations of becoming a bioinformatics programmer, you
need to become comfortable with the Linux CLI. But before we get to that, you
need Linux.

## Unix on Mac ##

If your computer is a Mac, you already have Unix installed, and your specific
flavor of Unix is called Darwin. You can get to the CLI with the _Terminal_
application. You may also find it useful to install Linux virtual machines on
your Mac. See below for more information.

## Linux on PC ##

If your computer is a PC currently running Windows, you will have to install
Linux _somehow_ and you have several choices. Each of these has advantages and
disadvantages, which are described in more detail below.

+ Virtual machine - recommended
+ Install Linux on PC - if you have a spare PC
+ Windows Subsystem for Linux - official Microsoft solution
+ Cygwin - may be useful for advanced users
+ Git bash - may be useful for advanced users

### Virtual Machine on Windows ###

This is the current recommendation for Linux on a Windows computer.

A virtual machine (VM) is a fictional computer running inside your normal
Windows operating system. The virtualization _host_ software (e.g. VirtualBox)
running on Windows tricks the new _guest_ operating system (Linux) into thinking
it is attached to its own motherboard, CPU, keyboard, mouse, monitor, etc.

The upside of virtualization is that it's safe and inexpensive. It's hard to
destroy data on your computer and you don't have to buy any new hardware.
VirtualBox is free software that works very well. Other popular virtualization
products include VMware and Parallels. If you want commercial support, you may
like those.

The downside of a VM is that your virtual machines will take up some RAM, CPU,
and storage. RAM is the most critical resource because it isn't easily shared.
If you have 8 GB RAM, you could set up your VM with half. But that means both
your real and virtual machines are running on 4 GB each. Computers run more
efficiently with more RAM, especially if you're the type of person to have 20
browser tabs open. Adding more RAM to your computer will improve your VM
experience. You can also run a VM with less RAM if you use a lightweight Linux
distribution.

On the CPU side, your programs running in a VM will run slower than they could.
The difference is pretty negligible though. We're talking 1-10% slower. You will
also have to dedicate about 5-10 GB of hard disk space. Even with the
downsides, VMs are a great way to run Linux on your PC.

There are many distributions of Linux. The most obvious differences among them
is the desktop Graphical User Interface (GUI). Some look like old-school Windows
while others look like Mac OS, and still others offer their own unique look and
feel. As bioinformatics programmers, we're more interested in the CLI than the
GUI, so I don't concern myself too much with what the desktop. My personal
favorite distributions are Debian, Mint, and Ubuntu.

Make sure you read the installation directions fully. There are some
post-install customizations you might need to do. On VirtualBox these include:

+ Install the Guest Additions "CD"
+ Switch the virtual video card if you can't resize the screen
+ Set up a shared folder if you want Linux and Windows to share files

### Install Linux on PC ###

This is the best way to run Linux, but it may change your PC permanently.

There are a variety of ways you can install Linux on a hard disk. This could be
an external hard disk you plug in when you want to run Linux (e.g. a flash
drive), or you can split your current hard disk into multiple partitions, or you
can wipe Windows and install Linux instead. All of these methods will give you
Linux with all of the RAM and CPU. Each one is slightly destructive, however,
and you may accidentally wipe your Windows partition even if you didn't intend
to. For these reasons, if you only have 1 computer, I don't recommend installing
Linux directly. Use VirtualBox, WSL, or Cygwin instead. However if you do have a
spare computer, installing Linux will give you that fully immersive experience
that helps you learn Linux faster.

If you want a really cheap Linux computer, you may like a Raspberry Pi. These
are single board computers using cell phone chips. They are about the size of a
deck of cards and cost about $50. You can also pick up used computers for next
to nothing at secondhand stores or from private sales on Craigslist and the
like.

### Windows Subsystem for Linux ###

The official Microsoft solution for running Linux is called the Windows
Subsystem for Linux (WSL). There are two types of WSL, Type 1 and Type 2. Type 1
is older. It is also compatible with virtual machines like VirtualBox. If you
want to run both WSL and VBox on the same machine, you should use WSL Type 1.

If you want to be more up-to-date, then use WSL Type 2. Unfortunately,
installing WSL2 will stop VirtualBox from running. You can have WSL2 and VBox on
the same computer, but not running at the same time; you will have to edit some
settings and restart to switch between the two.

The upside of WSL is that it is the official Microsoft product. Most of the time
it works great. It uses less resources than a VM, so your actual and virtual
computers will be faster with WSL. The downside of WSL is the Windows and Linux
filesystems do not play well together. When Windows programs save files in the
Linux filesystem, some permissions may get reset. It can be annoying. As WSL
matures, it may become the best way to run Linux on Windows.

From WSL, your Windows C drive is conveniently mounted at `/mnt/c`. Finding your
Linux filesystem root from Windows is not so easy.

### Cygwin on Windows ###

Cygwin is a terminal with Unix commands. In use, it feels similar to WSL.

Cygwin is not an entire operating system but rather a terminal with POSIX
commands (POSIX is a standard for portable Unix). It does not come pre-installed
with Python, so you will have to run the Cygwin `Setup.exe` to install it and
possibly other programming tools. For basic Python programming, I've found
Cygwin to work great. However, when I tried to do a `pip3 install numpy` it did
not work out of the box. If you have a lot of previous Unix experience and don't
mind troubleshooting software installs, Cygwin can be great. If you're more of a
novice, use something else.

Your Windows C drive is mounted at `/cygdrive/c`. Your Cygwin root depends on
where you chose to install it (probably `C:\cygdrive`).

### Git Bash on Windows ###

Git Bash is another terminal with Unix commands.

Git Bash is software intended for running git commands on Windows PCs using a
command line interface. It can be used for more tasks, such as Python
programming. Some programming languages are built-in (e.g. Perl) but Python is
not by default. Git Bash feels very similar to Cygwin but software installation
is slightly more complex. Like Cygwin, experts may like Git Bash, but it's not
for novices.

## Terminal, Command Line, and Shell ##

To interact with Linux at the CLI you use a _terminal_ application. There are
many flavors of terminals, each with its own name. Most of them have the word
'term' in them somewhere. For example, `xterm`, `qterm`, or just `Terminal`.

Once you launch a terminal application, you are presented with a command prompt
where you type _stuff_. This environment is actually called a _shell_. There are
several flavors of shell, each one generally has 'sh' in the name. Examples
include `sh`, `bash`, `csh`, `ksh`, `tcsh`, and `zsh`.

Are you confused by terminals and shells? That would be normal. Let's have an
analogy to clear this up.

A _terminal_ is like a _word processor_. The default applications on Mac and
Windows are Pages and Word. But just because those are the defaults, doesn't
mean you can't install Open Office.

The terminal gives you access to the _shell_. Here is another place you have a
choice. Whatever form of Unix you're using will have a default shell. That may
be `bash` or `zsh` but you can switch from one to another easily. This is sort
of like changing the language preferences in your word processor from US English
to UK English. Some of the spellings and punctuation change, but there are more
similarities than differences.

### Terminal Basics ###

Launch the terminal application (the name of this will differ from one operating
system to another and even within a particular OS you will have several
options). Run the `date` command by typing in the terminal and ending with the
_return_ key.

	date

Congratulations, you just made your first Unix statement. You type words on the
command line (in this case just one) and then hit return to execute the command.
`date` is but one of many Unix commands you have at your fingertips (literally).
Like most Unix commands, `date` does more than simply output the current date in
the format you just witnessed. You can choose any number of formats and even set
the internal clock to a specific time. Let's explore this a tiny bit. Commands
can take _arguments_. Let's tell the `date` program that we want the date to
be formatted as year-month-day and with hours-minutes-seconds also. The syntax
below will seem arcane, but the various abbreviations should be make sense. Type
the command below and observe the output.

	date "+%Y-%m-%d %H:%M:%S"

### Manual Pages ###

If you want to learn more information about what `date` can do, you can either
look online or use the Unix built-in manual pages. For a quick refresher on a
command, the manual pages are often easiest. But if you have no idea what the
command does, than you might want to look for assistance online where you might
find questions, answers, and examples. To read the manual pages for `date` you
use the `man` command.

	man date

You can page through this with the space bar and exit with `q`. In the above
statement, `man` was the command and `date` was the argument. The program that
let you page through the documentation was another Unix command that you didn't
intentionally invoke, it just happens automatically when you execute the `man`
command.

### Injury Prevention ###

Typing is bad for your health. Seriously, if you type all day, you will end up
with a repetitive stress injury. Don't type for hours at a time. Make sure you
schedule breaks. Unix has several ways to save your fingers. Let's go back and
run the `date` program again. Instead of typing it in, use the _up arrow_ on
your keyboard to go backwards through your command history. If you scroll back
too far, you can use the _down arrow_ to move forward through your history
(but not into the future, Unix isn't that smart).

	date "+%Y-%m-%d %H:%M:%S"

You can use the _left arrow_ and _right arrow_ to position the cursor so you can
edit the text on the command line.

To see your entire history of commands in this session, use the `history`
command.

	history

Probably the most important finger saver in Unix is **tab completion**. When you
hit the tab key, the shell completes the rest of the word for you if it can
guess what you want next. For example, instead of typing out `history` you can
instead type `his` followed by the tab key, the rest of the word will be
completed. If you use something less specific, you can hit the tab key a second
time and Unix will show you the various legal words. Try typing `h` and then the
tab key twice. Those are all the commands that begin with the letter h. You
should use tab completion constantly. Not only does it save you key presses and
time, it also ensures that your spelling is correct. Try misspelling the
`history` command to observe the error it reports.

	historie

### Variables ###

The shell defines various variables which are called _shell variables_ or
_environment variables_. For example, the `USER` variable contains your user
name. You can examine the contents of a variable with the `printenv` command.

	printenv USER

Another way to print the contents of an environment variable is to use the
`echo` command to dereference the `$USER` variable.

	echo Hello $USER, your shell is $SHELL

We won't use variables much, but it's important to know they exist because some
programs use them for configuration. If you want to see all your environment
variables, you can use the `printenv` command without any arguments.

	printenv

Don't worry if you find the topic of environment variables to be a little
confusing at this time. We will revisit the topic a little later when it matters
more.

### Setting Up Your Workspace ###

Depending on the specific flavor of your operating system, you may have various
folders in your home directory. For example, Mac, Windows, and Linux generally
have _Desktop_, _Documents_,  and _Downloads_ folders. These are default
locations for your point-n-click files. Let's set up a folder to do our
programming and bioinformatics work. Open a terminal and type the following
command.

	cd

The `cd` command is used to "change directory". If you don't give it any
specific place to go, it will take you to your home directory. There are two
other ways to get to your home directory: _tilde_ and `$HOME`. Both of these
commands do the same thing.

	cd ~
	cd $HOME

To examine the exact path to your home directory, use the `pwd` command, which
stands for "print working directory".

	pwd

To see the other files in your home directory, type the `ls` command.

	ls

You should see your Documents, Downloads, and other folders created by default
by the operating system. Now it's time to create a new working directory for all
of your bioinformatics programming stuff. Let's call it _Work_.

	mkdir Work

Note that all of the directories given to you by default were a single word
starting with a capital letter (e.g. Downloads). We followed this convention
when we chose _Work_. However, the typical Unix world is all lowercase. So once
we enter the Work directory, we'll follow Unix standards and go all lowercase.
Let's make another directory inside the _Work_ directory called _bin_. Then `cd`
to _Work_ and have a look around with the `ls` command.

	mkdir Work/bin
	cd Work
	ls

You should see _bin_ and nothing else. Let's create another directory in here
called _lib_.

	mkdir lib
	ls

Now you should see two things, _bin_ and _lib_. We won't be using these
directories right away, but we will be using them soon.

### Creating and Viewing Files ###

(For the this exercise and others that follow, it may be useful to have your
graphical desktop displaying the contents of your Work directory. That way you
can see that typing and clicking are related. You won't actually be using the
mouse though.)

There are a number of ways to create a file. The `touch` command will create a
file or change its modification time (Unix records when the last time a file was
edited) if it already exists. Let's first make sure we are in our Work
directory. Here you can see why we use the tilde to represent our home
directory: it saves typing.

	cd ~/Work
	touch foo

The file `foo` doesn't contain anything at all. It is completely empty. If your
graphical file browser was open to your Work directory, when you typed you would
have seen the file magically appear in the file browser. Now lets create a file
with some content in it.

	ls /bin > bar

This command listed the `/bin` directory and **redirected** the output to a file
named `bar`. The greater-than sign allows you to send a stream of characters to
a file. Those characters can be streamed from the `ls` command as was done here,
or you could type them at the keyboard. Let's try putting some content into
`foo` with the keyboard.

	cat > foo

After you type the line above, the shell appears to hang. It's waiting for you
to start typing. Go ahead and write a few lines of poetry. To close the stream
of data and save the file, type ^D. What the heck is ^D? In Unix parlance, that
means hit the _control_ key followed by the _d_ key. This is sometimes written
as control-D. Note that even though ^D and control-D have a capital D in them,
you don't actually use the shift key. So go ahead and type ^D.

The most useful ways to view a file are with `head`, `tail`, `more`, and `less`.
`head` shows you the first 10 lines of a file, while `tail` shows you the last
10. Of course there are command line options to change the number of lines.
Let's try them out.

	head foo
	tail foo
	head -5 bar
	tail -5 bar

If you want to view a whole file you can do that with `cat` or `less`. We just
saw how `cat` could be used to create a file, but it can also be used to view
them.

	cat bar

This isn't very useful for viewing large files unless you're a speed reader. A
more useful way to look at files is with a _pager_. The `more` and `less`
commands let you see a file one terminal page at a time. This is what you used
before when viewing the manual page for the `date` command. Use the spacebar to
advance by one page, the _b_ key to go backwards by one page, and when you're
done, hit _q_ to quit. `more` and `less` do more or less the same thing, but
oddly enough `less` does more than `more`. There are a lot of silly jokes in
Unix culture.

	less bar

### Editing Files ###

Let's try editing a file with `nano`, which is a terminal-based editor.

	nano foo

This changes the entire look of your terminal. No longer are you typing commands
at a prompt. Now you're editing a file and can change the random text you just
wrote. Use the arrow keys to move the cursor around. Add some text by typing.
Remove some text with the delete key. At the bottom, you can see a menu that
uses control keys. To save the file you hit the ^O key (control and then the
letter o). You will then be prompted for the file name, at which point you can
overwrite the current file (bar) or make a new file with a different name. To
exit nano, hit ^X. Note, you don't need to give nano a file name when you start
it up.

Unix file names often have the following properties:

* all lowercase letters
* no spaces in the name (use underscores or dashes instead)
* an extension such as .txt

### Navigating Directories ###

Whenever you are using a terminal, the shell's command line is focused on a
particular directory. The files you just created above were in a specific
directory (~/Work). To determine what directory you are currently in, use the
`pwd` command (print working directory). Let's make sure you're in your home
directory and examine its path.

	cd
	pwd

Your home directory should be listed below based on your operating
system.

* MacOS -  `/Users/your_name`
* Ubuntu - `/home/your_name`
* Lubuntu - `/home/your_name`
* WSL - `/home/your_name`

A path that begins with a `/` is called an _absolute path_. Your location also
has a _relative path_, which is simply the dot `.` character. Your full name is
like an absolute path while pronouns are like a relative path. So "Ian Frederick
Korf" describes the author absolutely, while "me" describes me more relatively.
If I want to reference other people, I can use an absolute or relative path.
"Mario Takechi Korf" describes my brother in absolute terms while "twin brother"
describes him in relative terms.

If you want to know what files are in your home directory, you can do that with
an absolute path regardless of where your shell is currently focused. You can
type out the path you found above, or you can dereference the `HOME` environment
variable.

	echo $HOME
	ls $HOME

You can also list your home directory using a relative path. Read the dot as
"here" so the following command is "list here".

	ls .

`ls` will list your current directory if you don't give it an argument, so an
equivalent statement is simply:

	ls

Notice that `ls` reports both the files and directories in your current
directory. Without icons it's a little difficult to figure out which names
correspond to file and which to directories. So let's add a command line option
to the `ls` command that will decorate directories with a special character.

	ls -F

This command adds a character to the end of the file names to indicate what kind
of files they are. A forward slash character indicates that the file is a
directory. These directories inside your working directory are called
_sub-directories_. They are **below** your current location. There are also
directories **above** your current focus. There is at most one directory
immediately above you. We call this the **parent** directory, which in Unix is
called `..` (that wasn't a typo, it's two dots). You can list your parent
directory as follows:

	ls ..

The `ls` command has a lot of options. Try reading the `man` pages and trying
some of them out. Now is a good time to experiment with a few command line
options. Note that you can specify them in any order and collapse them if they
don't take arguments (some options have arguments).

	man ls
	ls -a
	ls -l
	ls -l -a
	ls -a -l
	ls -la
	ls -al

There are two ways to specify a directory: _relative_ path and _absolute_ path.
The command `ls ..` listed the directory above the current directory. The
command `nano bar` edited the file `bar` in the current directory. You could
also have written `nano ./bar`. What if you want to list some directory
somewhere else or edit a file somewhere else? We actually did that before with
`ls /bin > foo`. To specify the absolute path, you precede the path with a
forward slash. For example, to list the absolute root of the Unix file system,
you would type the following:

	ls /

To list the contents of /usr/bin you would do the following:

	ls /usr/bin

This works exactly the same from whatever your current working directory is
because `/usr/bin` is an absolute path. However, if you do `ls bin` it only
works if you happen to have a directory or file called `bin` in your current
focus.

---

To change your working directory, use the `cd` command. Try changing to the root
directory

	cd /
	pwd
	ls

Now return to your home directory by executing `cd` without any arguments.

	cd
	pwd
	ls
	
Now go back to the root directory and create a file in your Work directory. That
is, your shell will have its focus on the root directory, but the files you
create will be in your Work directory. Open your GUI file browser to your Work
directory before you begin these commands.

	cd /
	touch $HOME/Work/file1
	touch ~/Work/file2
	ls ~/Work

### Moving and Renaming Files ###

Your home directory is starting to fill up with a bunch of crap. Let's organize
that stuff. First off, let's create a new directory for `stuff` using the
`mkdir` command.

	cd ~/Work
	mkdir stuff

Let's move some files into that new directory with the `mv` (move) command.

	mv foo stuff

The file `foo` is now inside the directory `stuff`. You can observe this by
listing the current directory, which no longer contains `foo`, and `stuff`,
where it now resides.

	ls .
	ls stuff

The weird thing about the `mv` command is that it not only moves files into
directories, it can also rename them. Let's try renaming `bar` to `bark`.

	mv bar bark

The difference between `mv foo stuff` and `mv bar bark` is that in the former
case there was a directory called `stuff` and in the latter there wasn't. This
is the key to `mv` command. If the last argument exists, it tries moving the
first argument (the file) into the last argument (the directory). What if you
try moving a file onto an already existing file? Let's do that with the
previously created `file` and `file2`.

	mv file1 file2
	ls .

Whoops. `file1` just got renamed to `file2`. In other words, the contents of
`file2` just got permanently deleted. For this reason, sometimes people use the
`-i` flag to turn on interactive mode. Let's recreate the previous files and try
this again.

	touch file1 file2
	ls
	mv -i file1 file2

Now you get a warning before doing any destructive activities!

`mv` can move and rename a file at the same time. Let's put `bark` into the
`stuff` directory and change its name back to `bar`.

	mv bark stuff/bar
	ls stuff

`mv` can move multiple things at the same time. Let's move both `file1` and
`file2` into the `stuff` directory.

	mv file1 file2 stuff
	ls stuff

### Wildcards ###

One of the most useful time-saving tricks in the shell is the use of the `*`
character as a wildcard. The `*` character matches missing characters if it can.
If we want to list the files in `stuff` that start with the letter _f_ we do the
following:

	ls stuff/f*

A very common use of the wildcard is to match all files with a specific file
extension. Let's try that.

	touch a.txt b.txt
	ls *.txt
	mv *.txt stuff

### Copying and Aliasing ###

The `cp` command copies files. Let's say you wanted to make a copy of `bar`
which is currently in your Work directory. You have to tell `cp` where you want
that copy to exist. It can't exist in the exact same location. You'll either
have to give it a different location or change its name. Let's first try giving
it a new location.

	cp stuff/bar .

The previous command reads as "copy the bar file from the stuff directory to my
current location". We could also copy the file without changing its location,
but we have to give it a new name.

	cp stuff/bar stuff/bark
	ls stuff
	
### Deleting Files ###

You delete files with the `rm` command. Be careful, because once gone, files are
gone forever. If you want a safer, interactive version of `rm` use it with the
`-i` flag (we saw this earlier with `mv`).

	ls stuff
	rm stuff/file1
	ls stuff
	rm -i bar

As a reminder, you didn't type those file names completely, right? You used tab
completion, right?

You can delete multiple files at once too and even whole directories. Watch out
though, that can get dangerous. If you want to completely remove everything in
the `stuff` directory, you _could_ do the following (but please don't):

	rm stuff/*

That will still leave the `stuff` directory intact, but without any files. If
you want to remove the directory, you use the `rmdir` command. You can try this,
but it won't work because the directory isn't empty. `rmdir` only removes empty
directories.

	rmdir stuff

If you want to remove a directory and everything it contains, you can use the
`-r` flag to recursively delete everything inside and the `-f` flag to force
delete of protected files. This is highly, highly destructive, so maybe don't do
it.

	rm -rf stuff

The worst possible thing you could do is unintentionally use the wildcard `*`
with the `rm` command with slightly incorrect syntax. Here, let me show you how
to destroy everything.

	rm -rf stuff *

You may have wanted to do `rm -rf stuff/*` but the space between `stuff` and `*`
means that `*` matches **EVERYTHING**. So that's how you delete everything in
your current directory. If you happen to be in your home directory, you just
deleted everything you own. Ask me how I know.

Since `mv`, `cp`, and `rm` can be so dangerous, many people create aliases that
force each command to be interactive. We'll see how to do this a little farther
below when we get to the more advanced Unix section.

## Markdown ##

Most of the files we work with in Linux are plain text files. Many things change
in this world, but not the format of text files. Got some old poetry you wrote
in WriteNow? Well, that software doesn't exist anymore, so good luck viewing it.
However, any text file since the dawn of Unix still works just fine.

### Text vs Binary ###

There are two main types of files you will encounter: text and binary. You can
view text files with `less` and edit them with `nano`, for example. All of the
programs we will write will be text files. You can also view and edit binary
files but they look like gobledygook, not English. If you want to see what a
binary file looks like, try the following.

	less /bin/ls

You're looking at the machine code for the `ls` program. It's not meant to be
human-readable. These are machine-specific instructions designed for machines,
not humans. So what makes a file text or binary? To answer that, we need to
delve into the world of bits and bytes.

### Bits, Bytes, and ASCII ###

A _bit_ is a single binary digit representing a 0 or 1. The number "1" is just 1
as we know it. The number "10" is 2 in decimal notation. There is a "1" in the
2s place and a 0 in the "1s" place, so 2 + 0 = 2. Similarly, the number "11" in
binary is 3 in decimal and the number "101" in binary is "5" in decimal (1 four,
zero 2, 1 one).

A byte is 8 bits. Computers usually deal in bytes. So we don't normally talk
about a number like "101" to represent 5 but rather the 8-digit version of that
"00000101". So what number is "10000000"? Well that depends if you're working in
base 2, decimal, or something else entirely. In order to clarify these things,
people often put two characters at the front to signify the base when it's not
base-10. Prepending the numerals with "0b" tells people "I'm using binary". So
"0b10000000" means 128 and not ten million.

We actually use the "byte" more frequently than you might guess. However, when
we do so, it's usually in _hexidecimal_ notation. In base 2, there are 2
symbols: 0 and 1. In base 10 (ordinary decimal) there are 10 symbols: 0, 1, 2,
3, 4, 5, 6, 7, 8 , and 9. In base 16 (hexidecimal), there are 16 symbols: 0, 1,
2, 3, 4, 5, 6, 7, 8, 9, A, B, C, D, E, and F. So the symbol "B" in hexidecimal
means "11" in decimal.

Have you ever seen internet addresses of the form 192.168.1.1? Ever wondered
what those 4 numbers are? Each one is a byte. So each one can have a value from
"0b00000000" to "0b11111111". In other words, each value can be from "0x00" to
"0xFF". Or more familiarly, from 0 to 255. These same byte notations are used
all over the place in computers. You might have seen colors such as "FF0000" or
"FF00FF" (those are red and magenta respectively). Or you may have had to use
the MAC address of your network adapater, which may have looked like
"f0:18:98:e9:f2:be" (upper and lowercase don't matter in hexidecimal).

So now it's time to understand the difference between text an binary. A text
file typically uses only the 7 bits defined by ASCII (American Standard Code for
Information Interchange). That is, each byte is confined to the range from 0 to
127. In binary that's "0b00000000" to "0b01111111". In hex, that's "0x00" to
"0x7F". All of the numbers equal to or greater than than "0b10000000" or "0x80"
or 128 are outside the ACSII space.

In a plain text file, every symbol (e.g letter or punctuation) has a
corresponding value in the range of 0-127. For example, captial "A" is
"0b01000001" or "0x41" or 65 (decimal). Similarly, capital "B" is "0b01000010"
or "0x42" or 66. The numbers from 0-9 are in ASCII slots 48-57, the capital
letters are 65-90, the lowercase letters are 97-122, and other symbols are in
various places (32-47, 58-64, 91-96, 123-127). Everything below 32 is invisible.

At this point you may be wondering about other alphabets and how they get
encoded in a computer. Surely you can't fit all of the symbols in human language
into the range of 0-127. You can't. There are 2-byte encodings that offer many
more symbols. But for now, we are only considering ASCII.

### Formatting Plain Text ###

Text files are incredibly simple. There are no choices of ruler settings, font
family, font style, lists, or tables you expect to find in a word processing
document. However, sometimes you want part of a text file to look like a
heading, or boldface, or a list. There are lots of ways you can imagine doing
that from the use of capital letters to punctuation. Markdown is a Internet
standard for writing text files. If you follow the standard, you can turn your
plain text documents into beautifully formatted HTML or PDF that has actual
headings, hyperlinks, font styles, lists, etc.

To find out how to write Markdown, check out the website linked below. This is
the official home of vanilla Markdown. There are a few customizations of
Markdown that add a few more things like tables.

[https://daringfireball.net/projects/markdown](Markdown)

Another way to learn Markdown is to compare an HTML or PDF file to its original
Markdown plain text source document.

Let's create our first Markdown document in `nano`.

	nano plans.md

Now let's enter some content.

	To Do List
	==========
	
	Here are some of the things I'm working on this week.
	
	+ Learn some Unix commands
	+ Learn how to write in Markdown **now**
	+ Learn how to program in Python
	+ Get my code into GitHub like all _professional_ developers

As you can see, even without the use of headings, font sizes, type faces,
rulers, etc. we are able to communicate document structure and emphasis. "To Do
List" is clearly the title. The plus signs are clearly a bulleted list. The use
of asterixes and underscores clearly show emphasis. Follow a few simple Markdown
rules and you'll end up with beautiful documents that are easy to write and a
pleasure to read as text, HTML, PDF, etc.

## GitHub Repository ##

If you want people to believe you're a programmer, you have to act like one.
That starts with you having a GitHub account. Your repositories and activity are
part of your CV. If you don't have a GitHub account, it's time to point your web
browser to go to [https://github.com](GitHub) and create your account.

Choose a username that isn't stupid. Remember, this will be part of your CV. I
use my full name. After setting your email and password, choose the free plan
and then answer a few questions about your interests to create your account.

Now check your email to verify your email address. It's time to create your
first repository! Name this `learning_python`. Select the radio button to make
this Public, and also check the box to initialize with a README. Lastly, you
should add a license in the dropdown menu to get in the habit of doing all
programming things properly. I generally use the MIT License.

The next step is to add your repository to the Work directory you just created.
Click on the green **Clone or download** button and copy the URL there. It
should look something like "https://github.com/USERNAME/learning_python.git",
where USERNAME is whatever you chose as your GitHub name.

	cd ~/Work
	git clone https://github.com/USERNAME/learning_python.git

This will create a new directory called `learning_python` in your `Work`
directory. If you look inside, you will see that it contains two files:
`LICENSE` and `README.md`. The LICENSE basically says that other people can use
your code but that they have to acknowledge that you wrote it and if anything
bad happens, it wasn't your fault.

## Git Commands ##

Enter your repository and check its status.

	cd learning_python
	git status

You will see that git reports that your repository is up to date. Let's modify a
file and see what happens. Edit the `README.md` file so that it has a little
more information. For example, you might add your name and someting about your
learning goals.

	nano README.md

After saving your changes, check your repository status again.

	git status

This shows that `README.md` has been changed. In order to put those changes back
into GitHub, you'll need to `add`, `commit`, and `push`.

	git add README.md
	git commit -m "update"
	git push

The `add` argument tells `git` we want to start tracking changes to this file.
The `commit` tells `git` we are done with edits, and the `-m` provides a short
message about what work was done. The `push` tells git to upload it back to
GitHub.

The general workflow with `git` is the following.

1. Create a file
2. `git add`
3. `git commit`
4. `git push`
5. Time passes...
6. `git pull`
7. Edit files
8. Go back to step 2

## Hello World ##

It's time to write your first Python program. We're going to do this with
`nano`. Start `nano` by typing the command name followed by the file you want to
create.

	cd ~/Work
	nano hello_world.py

Now type the following line:
	
	print('hello world')

Hit ^O (that's the command key plus the o key) to save the file and the ^W to
exit nano. Now let's try running the command from the shell.

	python3 hello_world.py

If everything worked okay, you should have seen 'hello world' in your terminal.
If not, don't go on. Ask for help fixing your computing environment.

---

Now it's time to add your new file to your repository. First let's check the
status of your repo.

	git status

This shows that `hello_world.py` is not currently being tracked. So let's add,
commit, and push it.

	git add hello_world.py
	git commit -m "initial commit"
	git push

Check the GitHub website. You'll see that your changes to `README.md` are there
as well as the new file `hello_world.py`.

It might seem like git is a lot of effor just to upload your code to a website.
If that's all git did, it would be too much effort, but git allows you to do a
lot more. Git tracks every change you make to a file, allowing you to rewind it
to any point in time. Git allows you to make a _branch_ of related work and then
later merge it back in with the main trunk if desired. More importantly, git
allows multiple developers to work simultaneously on the same project without
destroying each others work. We aren't using those advanced features yet. Right
now, our focus is on backing up our code and logging our programming activity to
the GitHub website.

---

Previously, when we wanted to run the program `hello_world.py` we had to proceed
that with the command `python3`. Most of the programs you've seen so far, like
`date` or `ls` did not require anything other than the name of the program. We
can change `hello_world.py` to work in the same manner. While this isn't really
necessary, it's very important to understand how programs work, so we're going
to modify `hello_world.py` to be just like `ls`.

Use nano top edit the file.

	nano hello_world.py

Now modify it so that it looks like the following:

	#!/usr/bin/env python3
	print('hello world')

The file should have _exactly_ 2 lines. Line 1 has the "hash bang" _interpreter
directive_. The first line of a text file tells Unix which language to use. Make
sure the first character of the file is `#` and that there are no additional
leading spaces. Line 2 is what you had before. Save this file and then push the
changes back to your repo. We're not done yet. This is just the first step.

## More Linux ##

In order for a text file to function as a program it needs 3 things.

1. An interpreter directive on the first line (we just did this)
2. Permission to be executed
3. Placed in the executable path

### File Permissions ###

A file can have 3 kinds of permissions: read, write, and execute. These are
abbreviated as `rwx`. If a file has read permissions, you can view it. If it has
write permissions, you can edit it, which includes deleting it. If it has
execute permissions, you can run it as a program.

Directories are special kinds of files that also have the same permissions.
Here, read means you can view the files in the directory. Write means you can
add or delete files in the directory. Execute means you can enter the directory.

Generally, you would like to be able to read, write, and execute the directories
you own. But this isn't always true of files. You may have downloaded some
important data and want to make sure you can't modify or delete it. Permissions
allow you to modify what actions can be take by whom.

In addition to having 3 types of permissions (read, write, execute), every file
also has 3 types of people that can access it: the owner (you), the group you
belong to (e.g. a laboratory), or the public (everyone else who has access to
the computer).

Let's examine the file permissions on the directories and files you
currently have.

	cd ~/Work
	ls -lF

You should see something like the following:

	drwxr-xr-x  2 ian ian 4096 Feb 7 10:01 bin/
	drwxr-xr-x  2 ian ian 4096 Feb 7 10:01 lib/
	drwxr-xr-x  2 ian ian 4096 Feb 7 10:11 learning_python/

Let's break down what's happening with the first arcane set of symbols. The
first letter is `d` which indicates that the file is a directory. We can also
see this because of the trailing slash from the `ls -F`. The next 9 characters
are 3 triplets.

+ rwx the first triplet are your permissions
+ r-x the second triplet are group permissions
+ r-x the third triplet are public permissions

You may read, write, and execute the directory. That is, you have permission to
`ls` the directory, `rm` files in the directory, and `cd` into the directory.
Users who belong to your group can also read and enter your directories, but
they can't modify their contents.

Let's take a look at the permissions of `hello_world.py`.

	cd learning_python
	ls -l hello_world.py

On Ubuntu, this is what I found, however the default permissions for your Linux
distribution may be different.

	-rw-r--r-- 1 ian ian 44 Feb 7 11:00 hello_world.py

After the leading dash, there are 3 triplets of symbols. The first triplet shows
user permissions `rw-`. I have read and write permission but not execute. The
next triplets are for group and public. Both have read permission, but not write
or execute. Let's first turn on all permissions for everyone using the `chmod`
command and then list again.

	chmod 777 hello_world.py
	ls -l hello_world.py

Notice that you can now see `rwx` for owner, group, and public.

	insert whatever

Does it make sense for _everyone_ to be able to edit your files? Probably not.
It also doesn't make sense for plain text files with your shopping list to have
executable permissions. So turning everything on isn't a good idea.

The `chmod` command has two different syntaxes. The more human readable one
looks like this.

	chmod u-x hello_world.py
	ls -l hello_world.py

This command says: "change the user (u) to remove (-) the execute (x) permission
from file hello_world.py". You add permissions with +.

	chmod u+x hello_world.py
	ls -l hello_world.py

The less readable `chmod` format assigns all parameters in octal format. 4 is
the read permission. 2 is the write permission. 1 is the execute permission.
Each rwx corresponds to one octal number from 0 to 7. So `chmod 777` turns on
all permissions for all types of people and `chmod 000` turns them all off.

| Read | Write | Exec | Sum | Meaning
|:----:|:-----:|:----:|:---:|:--------
|   4  |   0   |   0  |  4  | only reading allowed
|   4  |   2   |   0  |  6  | reading and writing allowed
|   4  |   2   |   1  |  7  | reading, writing, and executing allowed
|   4  |   0   |   1  |  1  | reading and executing allowed
 

### Making hello_world.py Executable ##

Now that your hello_world.py program has execute permissions, you can use it
like a Unix program. That is, you don't have to type `python3` before the
program name.

	./hello_world.py

But what's with the `./` before the program name. You don't have to type that
when you run the `ls` command or the `chmod` command, for example. That's
because those programs are in your **executable path** and `hello_world.py` is
not. We'll fix that in a bit.

### Files on Flash Drives ###

Most flash drives are formatted to be compatible with Windows machines. Each
operating system has a different idea about how to store filesystem metadata
such as permissions. Because of this, most files on flash drives end up with all
permission set. In octal, that would be 777 (read, write, execute) for owner,
group, and public. This is the most permissive setting and can be a little
dangerous. After copying files from a flash drive to your Unix machine, it's
probably a good idea to change the permissions to something more sensible.

### Customizing Your Shell ###

In order to simplify a few things, we need to customize your shell. First, we
have to figure out which shell you're running. Your shell is in your SHELL
environment variable. Here are two ways of seeing that.

	printenv SHELL
	echo $SHELL

If your shell is `/bin/bash` then check if you have a file called `.profile` or
`.bash_profile` or `.bashrc` in your home directory. If you already have one of
those files, edit it with nano. If not, create a `.profile` with nano.

If your shell is `/bin/zsh` then check if you have a file called `.zshrc`. If it
exists, edit it with nano. If not, create it with nano.

Now enter the following 2 lines into the file you're editing.

	alias ls="ls -F"
	export PATH=$PATH:$HOME/Work/bin

The first line makes it so that whenever you use the `ls` command, you're
actually invoking `ls -F` which displays the file type by appending a `*` to
executable files and a `/` to directories.

The second line adds your `Work/bin` directory to the executable path. Now, any
script you put into `Work/bin` can be run like any other program. Note that this
is optional. Also, instead of moving programs into `Work/bin` you could make
aliases there that connect to the original location of the scripts.

To protect yourself from accidentally overwriting or removing files, you might
want to add interactive mode for a few commands.

	alias rm="rm -i"
	alias mv="mv -i"
	alias cp="cp -i"

### PYTHONPATH ###

Just like your shell needs to know where your programs live, Python needs to
know where your libraries live. It's going to be a while before we are writing
our own libraries, but we should set things up for that later. It looks very
similar to the PATH setup you just did.

	export PYTHONPATH=$PYTHONPATH:$HOME/Work/lib
	
## Editors and IDEs ##

It's time to stop using `nano`. While it is useful for very small tasks, it's
not a great programming editor. Most of us are more efficient navigating
documents with a mouse than a keyboard. All of the files you have been editing
with `nano` could have been edited with Atom, BBEdit, Gedit, Notepad++, etc.

Some people prefer programming in an Integrated Development Environment (IDE).
Popular IDEs for Python include IDLE, PyCharm, Spyder and Eclipse. IDEs can make
debugging easier as they automatically place your cursor and lines with bugs and
let you manually inspect variable contents. While IDEs may make your Python
programming more efficient, they separate you from Unix. Since one of the
reasons you are taking this course is to learn some Unix, I don't recommend
using an IDE at this time.

So which programming/text editor should you use? Whatever is installed by
default in your Linux distribution should be fine.

## Useful Unix Commands ##

The `wc` program counts the characters, words, and lines in text files. You
could counts the words in this document, for example.

	wc gumpy.md

One of the most useful programs is `grep`. This prints out lines that match
specific strings or patterns. For example, if you wanted to print out all the
lines with the word Unix you would do the following:

	grep Unix gumpy.md

To count how many lines that was, you could either use the `-c` flag to `grep`
or **pipe** the output to `wc`.

	grep -c Unix gumpy.md
	grep Unix gumpy.md | wc

When working with tabular data, you will find that `sort` is very useful, as it
let's you sort the lines on different columns.

When monitoring the progress of programs that take a long time to run, you will
find `time` useful for timing how long a program runs and `top` for monitoring
how much RAM or other resources a program is taking.

To see how much free space you have on your file system, use the `df` (disk
free) command with the `-h` option to make it more human-readable (try it both
ways).

	df
	df -h

Another useful command is `du` (disk usage) which shows how much space each of
your files and directories uses.

	du
	du -h

## Unix Quick Reference ##

| Token   | Function
|:--------|:-------------------------------------|
| .       | your current directory (see pwd)
| ..      | your parent directory
| ~       | your home directory (also $HOME)
| ^C      | send interrupt signal
| ^D      | send end-of-file character
| tab     | tab-complete names
| *       | wildcard - matches everything
| \|      | pipe output from one command to another
| >       | redirect output to file

| Command   | Example       | Intent                        |
|:----------|:--------------|:------------------------------|
| `cat`     | `cat > f`     | create file f and wait for keyboard (see ^D)
|           | `cat f`       | stream contents of file f to STDOUT
|           | `cat a b > c` | concatenate files a and b into c
| `cd`      | `cd d`        | change to relative directory d
|           | `cd ..`       | go up one directory
|           | `cd /d`       | change to absolute directory d
| `chmod`   | `chmod 644 f` | change permissions for file f in octal format
|           | `chmod u+x f` | change permissions for f the hard way
| `cp`      | `cp f1 f2`    | make a copy of file f1 called f2
| `date`    | `date`        | print the current date
| `df`      | `df -h .`     | display free space on file system
| `du`      | `du -h ~`     | display the sizes of your files
| `git`     | `git add f`   | start tracking file f
|           | `git commit -m "message"` | finished edits, ready to upload
|           | `git push`    | put changes into repository
|           | `git pull`    | retrieve latest documents from repository
|           | `git status`  | check on status of repository
| `grep`    | `grep p f`    | print lines with the letter p in file f
| `gzip`    | `gzip f`      | compress file f
| `gunzip`  | `gunzip f.gz` | uncompress file f.gz
| `head`    | `head f`      | display the first 10 lines of file f
|           | `head -2 f`   | display the first 2 lines of file f
| `history` | `history`     | display the recent commands you typed
| `kill`    | `kill 1023`   | kill process with id 1023
| `less`    | `less f`      | page through a file
| `ln`      | `ln -s f1 f2` | make f2 an alias of f1
| `ls`      | `ls`          | list current directory
|           | `ls -l`       | list with file details
|           | `ls -la`      | also show invisible files
|           | `ls -lta`     | sort by time instead of name
|           | `ls -ltaF`    | also show file type symbols
| `man`     | `man ls`      | read the manual page on ls command
| `mkdir`   | `mkdir d`     | make a directory named d
| `more`    | `more f`      | page through file f (see less)
| `mv`      | `mv foo bar`  | rename file foo as bar
|           | `mv foo ..`   | move file foo to parent directory
| `nano`    | `nano`        | use the nano text file editor
| `pwd`     | `pwd`         | print working directory
| `rm`      | `rm f1 f2`    | remove files f1 and f2
|           | `rm -r d`     | remove directory d and all files beneath
|           | `rm -rf /`    | destroy your computer
| `rmdir`   | `rmdir d`     | remove directory d
| `sort`    | `sort f`      | sort file f alphabetically by first column
|           | `sort -n f`   | sort file f numerically by first column
|           | `sort -k 2 f` | sort file f alphabetically by column 2
| `tail`    | `tail f`      | display the last 10 lines of file f
|           | `tail -f f`   | as above and keep displaying if file is open
| `tar`     | `tar -cf ...` | create a compressed tar-ball (-z to compress)
|           | `tar -xf ...` | decompress a tar-ball (-z if compressed)
| `time`    | `time ...`    | determine how much time a process takes
| `top`     | `top`         | display processes running on your system
| `touch`   | `touch f`     | update file f modification time (create if needed)
| `wc`      | `wc f`        | count the lines, words, and characters in file f
