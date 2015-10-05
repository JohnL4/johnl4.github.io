---
excerpt: Quickly getting up to speed with Haskell on your Linux machine
tags: Haskell
---
Quickly getting up to speed with Haskell on your Linux machine
==============================================================

So, I got Haskell working on my work laptop (Windows 7) and then tried to compile the code on my Linux machine.

Hand in face.

So, here's how to straighten out *that* mess.

Haskell itself
--------------

First off, my machine had two version of Haskell, both out of date.

It's a Linux Mint Qiana (17?) machine, based on Ubuntu 14.04 LTS (codename "trusty", I think).

I had Haskell 7.8 in /usr/local, and Haskell 7.6 in /usr/bin.  Current version, as of this writing, is 7.10.2a.

Using Synaptic to manage packages, I installed "haskell platform", but no joy. It certainly didn't change anything, and
it's possible that it just installed 7.6 on top of itself.

So, in Synaptic, I had to select all things Haskell (actually, I just selected my installed ghc, and things went ok
after that) and uninstalled.

Then, I went to the Haskell page (http://haskell.org) and selected **generic** Linux machine (not Mint, since that seems
to only get an outdated package).  It downloaded a monster compressed tarball for 7.10.2a.  Right beside
`~/Downloads/haskell-platform-2014.2.0.0-unknown-linux-x86_64.tar.gz`, which must be how I got 7.8 on my system.

After the download finished, I unzipped/untarred it into /tmp/Haskell and ran the install script. No Synaptic/apt-get
nonsense.

The result was this:

~~~
Phobos$ ls -l /usr/local/bin/ghc
lrwxrwxrwx 1 root root 44 Sep 26 15:59 /usr/local/bin/ghc -> /usr/local/haskell/ghc-7.10.2-x86_64/bin/ghc

Phobos$ ls -l /usr/local/haskell/
total 8
drwxr-xr-x 7 3300 3300 4096 Aug  1 14:11 ghc-7.10.2-x86_64
drwxr-xr-x 7 john john 4096 Jul 31  2014 ghc-7.8.3-x86_64
~~~

Extra non-standard packages
---------------------------

My script that I developed on my work laptop used some non-standard libraries ("packages"), so I had to go get them.

Naturally, I couldn't remember what I had used (I have a memory like a steel collander), so I got compile errors on
various `import` statements.

So, using [Hoogle](https://www.haskell.org/hoogle/), I typed in the names of the packages I wanted (`System.IO.Strict`
and `Text.Regex.TDFA`), and found out they were in packages `strict` and `regex-tdfa`.

(There were actually two strict i/o packages I had to decide between, `strict` and `strict-io`. `strict-io` seemed to
be available only for NixOS (whatever that is), so I picked the one that was available for more platforms, including
Debian.)

`cabal install <packageName>` does the trick there.

And then I was done!
