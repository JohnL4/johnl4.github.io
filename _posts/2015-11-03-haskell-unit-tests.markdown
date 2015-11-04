---
excerpt: Splitting your code out into a module and unit-testing it
---
Haskell Unit-Testing
=====================

So, I got this working today.  Allows me to make changes to code and re-run unit tests, secure in the knowledge that
I haven't broken anything.

You need to do two things (assuming you started developing w/out an eye toward unit testing).

- Split your functions out into another module
- Write some unit tests

Splitting your code out into another module
-------------------------------------------

Easy enough.  Create a new Haskell file (I think the convention is that your filename matches your module name,
including case) that looks like this:

~~~
module ModuleName where

...all your function defintions go here
~~~

Then, in your old code, comment out (or delete) those function definitions, and import your new module name:

~~~
import ModuleName
~~~

You may notice that your code stops compiling until you compile your new module.

Unit Tests
-----------

Now that you've broken your functions out into a separate module, you can write unit tests against them.
They'll look something like
[the unit tests I wrote for my program](https://github.com/JohnL4/PassphraseGenerator/blob/70e50f57db55c928c7afaa4126e029a946b30d33/spec.hs).

`import Test.Hspec`

import whatever other modules you need.

`import ModuleName`, your new module containing your old functions.

Define whatever global data you need (if any).

Define your unit tests in the form of text descriptions and "should be" assertions.

Then, at the command prompt: `runghc yourUnitTestFilename.hs`

Hopefully, you'll see a bunch of stuff pass (or expected failures, if you're using TDD).

See [http://hspec.github.io/](http://hspec.github.io/) for more info.
