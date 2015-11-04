---
layout: homepage
title: John's Blog And Stuff
---

John's Blog And Stuff
=====================

Hi, there.
----------

This is my github web site.  Yay.  You probably want the blog (below).

How-Tos
-------

- [Jekyll org-mode notes, Journey of a Noob](jekyll.html) -- So far, this is my monster blob o'
  notes with various TODOs and whatnot. *I haven't updated it in a while.* (How do I show date of last modification
      here?)

Ma Wiki
-------

[https://github.com/JohnL4/johnl4.github.io/wiki](https://github.com/JohnL4/johnl4.github.io/wiki). Knock yourself out,
but I don't update it very much.  I'm kinda looking for a better wiki solution.

Ma Blog
-------

This is what I mostly update these days.

{% for post in site.posts %}
   - {{ post.date | date_to_string }} - [{{ post.title }}]({{ post.url }}) ({{ post.tags }})

     {{ post.excerpt }}
{% endfor %}
