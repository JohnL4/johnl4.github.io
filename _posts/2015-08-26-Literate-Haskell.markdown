---
excerpt: Making Literate Haskell present nicely
---
Making Literate Haskell present nicely
======================================

So, you can write "text" (blog entries, plain text, LaTeX, whatever) that is both readable by humans *and* readable
by computers.  The same text.  This is done by inverting documentation (comments) and code: you don't use special marks
to indicate comments, but you *do* use special marks to indicate *code*.

Use something like the following to generate literate haskell from your ordinary Haskell:

~~~
../Literate/hs2lhs find-common-resources.hs >| find-common-resources.lhs
~~~

(Install hs2lhs from [https://github.com/jeffreyrosenbluth/Literate](https://github.com/jeffreyrosenbluth/Literate).)

See [this blog entry](http://passingcuriosity.com/2008/literate-haskell-with-markdown-syntax-hightlighting/) (or
whatever it is) on how.

The first problem with this is that everything just goes ripping straight down the left margin, and that, in my
opinion, really impacts readability in a bad way.  I'm a huge fan of the hanging indent and indented code, so I'll be
fixing up the CSS to provide that.
