---
excerpt: Writing a simple Haskell script from scratch, given that I've forgotten almost everything over the last few weeks
---
Writing a simple Haskell script from scratch
============================================

(Given that I've forgotten almost everything over the last few weeks.  I'll probably remember pretty fast.)

First off, there's a nice-looking page on how to structure your new project:
[https://wiki.haskell.org/How_to_write_a_Haskell_program](https://wiki.haskell.org/How_to_write_a_Haskell_program)

`main`
------

First off, your program needs a `main`, like all programs.  The signature and dummy body is:

~~~
main :: IO()
main = do
  putStrLn suffixes
  putStrLn "Done."

suffixes = ["s","es","ed","ing","ly"] -- Just some stupid variable, but it shows you can define
                                      -- things after you refer to them. 
~~~

Compile with `ghc <progName.hs>`. Ghc will generate your executable.

`do`
----

That's your IO part.  You put separate IO statements on each line.

`<-`
----

Ok, time to figure out what this really does.  From _Real-World Haskell_: "Put simply, that binds the result from
executing an I/O action to a name."

Here's the whole program so far:

~~~
-- | Filter a word list, removing those words that are duplicates apart from common suffixes.  |
-- | Reads SORTED list on stdin, emits filtered list on stdout.
main :: IO()
main = do
  allInput <- getContents
  putStrLn ("Got " ++ (show (myLength (lines allInput))) ++ " lines")
  putStrLn (show suffixes)
  putStrLn ("suffixes is a list of length " ++ (show (myLength suffixes)))
  putStrLn "Done."

-- | The common suffixes we will be removing
suffixes :: [[Char]]
suffixes = ["s","es","ed","ing","ly"] 

myLength :: [a] -> Integer
myLength [] = 0
myLength (_:xs) = 1 + (myLength xs)
~~~

So, `<-` **"binds"** the result of `getContents` to `allInput`.  That doesn't mean it actually *evaluates*
`getContents`, it just binds it.

I really don't get it yet, but the i/o action is only _performed_ when the thing it's bound to (`allInput`) is
evaluated.  Note that, due to laziness, this evaulation doesn't actually happen until (really, probably) the following
`putStrLn` is called.  None of these functions need to be evaluated until the sequential `do` operator in `main` forces
them to be: all of `lines`, `myLength`, `show` and the `++` operators are probably lazy, not actually doing anything
until they absolutely have to.  Note that `lines` is a pure function (as is `myLength`).

I think of `<-` as "de-IO-ing" the i/o operation, meaning, we take that `IO` impurity off the operation, allowing its
results to be used in a pure function.

Check back with me later on the accuracy of that statement.

Various tricks and idioms
-------------------------

### Printing lists joined with delimiters

`concat (intersperse delimiter list)`:

~~~
putStr ("Suffixes are:\n\t" ++ (concat (intersperse "\n\t" suffixes)))
~~~
