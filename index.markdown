---
layout: post
title: John's Blog And Stuff
---


John's Blog And Stuff
=====================

Hi, there.
----------

This is my github web site.  Yay.

How-Tos
-------

- [Jekyll org-mode notes, Journey of a Noob](jekyll.html) -- So far, this is my monster blob o'
  notes with various TODOs and whatnot.

Ma Wiki
-------

[https://github.com/JohnL4/johnl4.github.io/wiki](https://github.com/JohnL4/johnl4.github.io/wiki). Knock yourself out.

Ma Blog
-------

Here.  Not much to it, so far, but oh well:

{% for post in site.posts %}
   - {{ post.date | date_to_string }} - [{{ post.title }}]({{ post.url }}) ({{ post.tags }})

     {{ post.excerpt }}
{% endfor %}
