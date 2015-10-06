---
excerpt: Been playing around with Bootstrap. Meh.
tags: Bootstrap, Polymer, Angular, CSS
---
Bootstrap
=========

So, I've been playing around with Bootstrap, and I have this to say: meh.  It's on ok framework that doesn't try to do
too much.  It's really just a bunch of CSS and some javascript.  I don't (yet) know how I'd integrate it with something
else like Polymer or Angular, but that's always a possibility.

See [https://github.com/JohnL4/Bootstrap](https://github.com/JohnL4/Bootstrap). (`navbar` is the last one I worked on,
as of this writing.)

The big win, really, is its unambitious goals and that whole mobile adaptive UI thing.  Table columns get turned into
rows when the UI gets narrow enough, so you get stuff like:

~~~

         +---------------+----------------+
         |               |                |
         |               |                |
         |   Area 1      |    Area 2      |
         |               |                |
         |               |                |
         |               |                |
         |               |                |
         +---------------+----------------+
         |               |
         |               |
         |   Area 3      |
         |               |
         |               |
         |               |
         |               |
         +---------------+
~~~

becoming:

~~~

         +---------------+
         |               |
         |               |
         |   Area 1      |
         |               |
         |               |
         |               |
         |               |
         +---------------+
         |               |
         |               |
         |    Area 2     |
         |               |
         |               |
         |               |
         |               |
         +---------------+
         |               |
         |               |
         |   Area 3      |
         |               |
         |               |
         |               |
         |               |
         +---------------+
~~~

when the viewport gets narrow enough.

On Sidebars
-----------

So, based on a quick search, there are lots of sidebars available for Bootstrap, but they don't have
animation.  At this point, I have to ask myself: why not just use Polymer?  Bootstrap is great for
simple stuff, but I think I'd rather use Polymer for something more "real".
