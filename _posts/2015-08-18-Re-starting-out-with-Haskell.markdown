---
excerpt: (Re-) Starting out with Haskell
---

(Re-) Starting out with Haskell
===============================

So, last night, I started reading where I left off w/Haskell many moons ago.  Or, I tried to.

This is my favorite Haskell book so far: [Learn You a Haskell for Great Good!](http://learnyouahaskell.com/) (You can
read it online.)

[Real-World Haskell](http://book.realworldhaskell.org/) is also pretty decent, but it's a bit more gritty and O'Reilly-y.

But there are some other good resources.

Here's a relatively reasonable intro, a short and fast tutorial for command-line-based Haskell scripts to replace
your shell scripts (shell scripting with Haskell: who knew?):
[https://wiki.haskell.org/Tutorials/Programming_Haskell](https://wiki.haskell.org/Tutorials/Programming_Haskell)

Stuff I need to learn from that tutorial:

* `>>=`
* `>>`
* `<-` -- Really, I kinda sorta have a handle on this one, but I need to know a little bit more.

And this:

~~~
flags =
       [Option ['b'] []       (NoArg Blanks)
            "Implies the -n option but doesn't count blank lines."
       ,Option ['e'] []       (NoArg Dollar)
            "Implies the -v option and also prints a dollar sign (`$') at the end of each line."
       ,Option ['n'] []       (NoArg Number)
            "Number the output lines, starting at 1."
       ,Option ['s'] []       (NoArg Squeeze)
            "Squeeze multiple adjacent empty lines, causing the output to be single spaced."
       ,Option ['t'] []       (NoArg Tabs)
            "Implies the -v option and also prints tab characters as `^I'."
       ,Option ['u'] []       (NoArg Unbuffered)
            "The output is guaranteed to be unbuffered (see setbuf(3))."
       ,Option ['v'] []       (NoArg Invisible)
            "Displays non-printing characters so they are visible."
       ,Option []    ["help"] (NoArg Help)
            "Print this help message"
       ]
~~~

More Tutorials
--------------

Here's a "meta-tutorial", really, a collection of tutorial references:
[https://wiki.haskell.org/Meta-tutorial](https://wiki.haskell.org/Meta-tutorial).

And, finally, from the above meta-tutorial, this, which is supposedly more condensed than Learn You a Haskell:
[http://www.seas.upenn.edu/~cis194/lectures.html](http://www.seas.upenn.edu/~cis194/lectures.html).

Editing, IDEs
-------------

Haskell doesn't really have slick IDEs, but you can probably get pretty close with your favorite editor.
Mine happens to be emacs [haskell-mode](https://github.com/haskell/haskell-mode).

GHCi
----

The interactive interpreter is going to be handy for debugging code, so here's the minimum you need to start running it:

* `:quit` to quit
* `:help` to get help
* `:load` to load a Haskell file.  Strictly speaking this isn't the minimum you need to know, but you'll start off
    with this command most of the time.

Primary References
------------------

...are here: [http://downloads.haskell.org/~ghc/7.8.3/docs/html/](http://downloads.haskell.org/~ghc/7.8.3/docs/html/).
(Every version has something, so you can be very specific as to which version's documentation you read.)

[Haskell Report](https://www.haskell.org/onlinereport/haskell2010/)

General Notes
-------------

### Directory Walking

~~~
import Control.Monad (forM)
import System.Directory (doesDirectoryExist, getDirectoryContents)
import System.FilePath ((</>))

getRecursiveContents :: FilePath -> IO [FilePath]

getRecursiveContents topdir = do
  names <- getDirectoryContents topdir
  let properNames = filter (`notElem` [".", ".."]) names
  paths <- forM properNames $ \name -> do
    let path = topdir </> name
    isDirectory <- doesDirectoryExist path
    if isDirectory
      then getRecursiveContents path
      else return [path]
  return (concat paths)
~~~

There's probably a better way to do this than a for-loop, but...

From _RWH_, chapter 8: "The unfamiliar forM function above acts a little like a “for” loop: it maps its second argument (an action) over its first (a list), and returns the list of results."

**</>**: An operator that joins two strings with a filepath separator.

### Sample Code

[https://github.com/JohnL4/HaskellXamlScan](https://github.com/JohnL4/HaskellXamlScan)
