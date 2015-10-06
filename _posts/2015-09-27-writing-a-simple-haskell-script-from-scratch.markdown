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

Pattern-matching and guards
---------------------------

First off, here's the [entire script](/haskell/filterCommonSuffixes.html). (Generated with the following command:)

~~~
hscolour -css filterCommonSuffixes.hs >| filterCommonSuffixes.html
~~~

This is one way we introduce conditionals into our program.

The function `filterSuffixes` has both pattern-matching and guards.

### Pattern-matching

That's the stuff that looks like:

~~~
filterSuffixes [] = []
filterSuffixes [lastword] = [lastword]
filterSuffixes (prefix : [lastword])
filterSuffixes (prefix : nextword : restwords)
~~~

The idea is that we match the actual arguments against various patterns.  The patterns chosen should cover all the
possible cases, and we do, in this case.

The first pattern is the case of an empty list.

The second pattern is the case of a list containing exactly one word.

The third, a list containing exactly two words.

> Note that `[]` denotes a *sequence* (list) in Haskell, and `:` is the "cons" operator.  In the expression `x : xs`,
  `x` is a single element, and `xs` is a *list* of elements (you can think of `x` being pluralized), so the result is a
  new list with `x` being the first element and all the elements of `xs` being the 2nd and following elements.

The fourth pattern is the case of three or more words.

### Guards

Once you're inside a function, you can also be conditional in terms of the function definition (or, as another way to
think of it, you can be conditional in terms of what you return).

That looks like this:

~~~
filterSuffixes (prefix : nextword : restwords)
  | (hasSuffix prefix nextword)  = filterSuffixes (prefix : restwords)
  | otherwise                    = prefix : (filterSuffixes (nextword : restwords))
~~~

The condition is the part between the `|` and the `=`.  `otherwise`, obviously, is your catch-all "else" clause.

### Simple, unconditional function definition

If you don't want any conditionals, your function definition is pretty straightforward:

~~~
-- | Doubles x.
f x = 2 * x
~~~

Various tricks and idioms
-------------------------

### Printing lists joined with delimiters

`concat (intersperse delimiter list)`:

~~~
putStr ("Suffixes are:\n\t" ++ (concat (intersperse "\n\t" suffixes)))
~~~
