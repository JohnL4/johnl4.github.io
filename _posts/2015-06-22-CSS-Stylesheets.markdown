---
excerpt: The existing CSS stylesheets and my new one (maybe)
tags: CSS
---

The existing CSS stylesheets and my new one (maybe)
===================================================

So, there's an existing stylesheet that came from somewhere magical (Jekyll install??).  It's got a bunch of
sophistication in it and the net result is not what I like, so I'm gonna hammer it.

Before I do though, I'll investigate what all this junk is.

First off, it's this:

~~~
Slate Theme for GitHub Pages
by Jason Costello, @jsncostello
~~~

So, there's this "meyerweb reset" that makes everything horrible:

~~~
  margin: 0;
  padding: 0;
  border: 0;
  font: inherit;
  vertical-align: baseline;
~~~

Thanks, whoever.  I'll be dumping that, in favor of the client defaults, which I will assume are _reasonable_.

Then, there's stuff like this:

~~~
  transition: color 0.5s ease;
  transition: text-shadow 0.5s ease;
  -webkit-transition: color 0.5s ease;
  -webkit-transition: text-shadow 0.5s ease;
  -moz-transition: color 0.5s ease;
  -moz-transition: text-shadow 0.5s ease;
  -o-transition: color 0.5s ease;
  -o-transition: text-shadow 0.5s ease;
  -ms-transition: color 0.5s ease;
  -ms-transition: text-shadow 0.5s ease;
~~~

and

~~~
  box-shadow: 0 0 5px #ebebeb;
  -webkit-box-shadow: 0 0 5px #ebebeb;
  -moz-box-shadow: 0 0 5px #ebebeb;
  -o-box-shadow: 0 0 5px #ebebeb;
  -ms-box-shadow: 0 0 5px #ebebeb;
~~~

and

~~~
  border-radius: 2px;
  -moz-border-radius: 2px;
  -webkit-border-radius: 2px;
~~~

and

~~~
#header_wrap {
  background: #212121;
  background: -moz-linear-gradient(top, #373737, #212121);
  background: -webkit-linear-gradient(top, #373737, #212121);
  background: -ms-linear-gradient(top, #373737, #212121);
  background: -o-linear-gradient(top, #373737, #212121);
  background: linear-gradient(top, #373737, #212121);
}
~~~

What _is_ all this webkit stuff?

`-webkit-border-radius`

These things are called "vender prefixes" and they're supposed to be temporary features.  I see all of the above have
CSS standard definitions, so why are we bothering w/the vendor prefixes?

Also, they're basically non-essential.  Rounded corners, animations and gradients?  Yes, lovely, but non-essential.
Gone.

I think I'll substitute my org-mode/wiki CSS, which is substantially simpler.

Yes, this is much better.  I guess that's enough for today.

Header 2
---------

text

### Header 3

text

#### Header 4

text

##### Header 5

text

###### Header 6

text

####### Header 7

text

######## Header 8

text
