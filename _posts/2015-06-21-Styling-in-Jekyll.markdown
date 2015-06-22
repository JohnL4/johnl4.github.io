---
excerpt: How to get Jekyll to honor the included stylesheets
---

Styling in Jekyll
=================

So, I finally am on the road to getting this figured out.

You have to modify your `_config.yml` file to include something like the following:

~~~
defaults:
  -
    scope:
      path: ""
      type: "posts"
    values:
      layout: "post"
~~~

Note that you _do not_ need trailing whitespace on lines ending with "-" or ":".

Make sure `defaults` is _plural_ (which caused me some trouble at first).  The specified layout (`post`, in this case)
will correspond to a file named `post.html` in the `_layouts` directory.


