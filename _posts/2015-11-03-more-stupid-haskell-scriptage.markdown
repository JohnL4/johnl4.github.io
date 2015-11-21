---
excerpt: Moar stupid Haskell script stuff, and an excursion into laziness, strictness and profiling
tags: Haskell
---
More simple Haskell script-programming tricks
==============================================

So, it's been a while since I posted, and I should catch up a bit.

I've been working on a script to scan the raw data files for Google NGrams and figure out what the most common words
are.  It took a while because I had a memory-consumption issue.  I won't call it a "leak", because it wasn't:
I wasn't unintentionally holding references to memory that filled up the RAM (and swap file), even though that's
exactly what happened.

> So, what the heck, John?  Here's what happened, and this is a common problem with Haskell programs, I think:
Because evaluation is lazy, the Haskell runtime builds up these huge lists (or trees) of function application. So,
when you make a recursive call, you might just get a huge string of recursive function applications (you won't if
it's a simple [tail-recursive](https://en.wikipedia.org/wiki/Tail_call) call). The reason it does this is because
it's lazy: why evaluate a function if you don't need to? Wait until you need it (usually when you output something).
So, you wind up with these huge stacks of function calls just waiting to be applied, and memory fills up. If the
program manages to actually reach the end of execution properly (and output its results), then this huge stack
of function calls is actually evaluated and all the memory is reclaimed, so it's not like leaks in imperative
languages, where you just sort of accidentally keep a reference to some piece of memory you no longer need.

So, what have I learned in the last few weeks?

For starters, here's the code: [mostFrequent.hs](https://github.com/JohnL4/PassphraseGenerator/blob/7996ce96f6bf0840a1ed30ca98efd92b84046e63/mostFrequent.hs).
Note that this isn't the _latest_ code, which might change after I post this blog entry. It's a particular version
so I can talk about particular pieces without it changing underneath me (even though I'll be the guy changing it.)

`splitOn` to split text into pieces
------------------------------------

A lot of scripting (at least, the stuff I write) is reading text, breaking it up into pieces and doing something
with the pieces.  The first thing I look for is a "split" operator.  In Haskell, that's
[splitOn](http://hackage.haskell.org/package/text-1.2.1.3/docs/Data-Text.html#v:splitOn).  You can see it used
around line 61 of the `mostFrequent.hs` script.

regular expressions
-------------------

See [this StackOverflow post](http://stackoverflow.com/a/32150031/370611).

Also, this looks like a good basic post on the topic:
[http://www.serpentine.com/blog/2007/02/27/a-haskell-regular-expression-tutorial/](http://www.serpentine.com/blog/2007/02/27/a-haskell-regular-expression-tutorial/)

In my dumb script, I used regular expressions in a boolean ("match?") to filter out Roman numerals, like this:

~~~
romanNumeral :: Regex
romanNumeral = makeRegexOpts defaultCompOpt{multiline=False} defaultExecOpt "^[ivxlc]+$"
-- ...
in if (year < aYear)
      || (ngramRole == "DET") -- Skip "determiners" (words like "a", "an", "the")
      || ((length ngram) < 3)  -- Two-letter words
      || (match romanNumeral ngram) -- Also need to eliminate Roman numerals: [ivxlc]+ (not using
                                    -- "m" because "mix" is a real word)
~~~

(Hopefully, there won't be a bunch of dates, like MCMLXXXIV.)

`!!` to select array elements
-----------------------------

`!!` is the array-indexing operator. `a!!0` is the zero-th element of the array `a`.

`if` conditional values
------------------------

So, I talked about pattern-matching and guards last time.  Another big conditional construct is `if`, which is
essentially the C ternary operator.

~~~
if (conditon) then (value1) else (value2)
~~~

You can see it used at line 66.

Excessive laziness
-------------------

The real problem with the script is solved by a single "!" character in a strategic location (line 60), and I don't understand
why it works or how much it costs.  I still need to figure that out.

The problem is the "leak" I mentioned at the beginning.  Without that "!" (the use of which is enabled by the pragma
in line 4), memory consumption of the program goes through the roof, and it runs out of space processing a 1.2-GB file.
The problem is the recursive call at line 68.  I'm not sure which of the arguments to `wordCounts` are unevaluated
in such a way as to cause the space consumption (it's _lists_ that occupy the space, by the way; can you see where
_lists_ are built up? I can't), but putting the "!" on the map argument to `wordCounts` causes that argument to be
evaluated strictly, collapsing those chains of unevaluated operators.

I need to figure out what the time cost of collapsing the map is, though.  I'm sure there's a more efficient way
to do it.

Although... when I profile, as follows:

~~~
ghc -prof -fprof-auto mostFrequent.hs
cat googlebooks-eng-us-all-1gram-20120701-a-filtered-100000 \
  | ./mostFrequent +RTS -pa -s >/dev/null
~~~

it looks like the program spends most of its time converting the "year" field to an integer in order to perform a comparison.  (I wonder if I could do a string comparison here, since all the years are exactly four digits.  Hmmm...)

What's truly interesting is the program spends a lot less time converting `matchCount` to an integer, even though
it occurs (is bound) at exactly the same place as `year` (lines 64 and 65).  This is the benefit of laziness: about
half the time, the year is < 1950 (the hardcoded cutoff in the program), so we really don't need to even bother
converting `matchCount` to an integer at all, and we don't!
