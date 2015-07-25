---
---


Hi, there
=========

This is my github web site.  Yay.

How-Tos
-------

- [Jekyll org-mode notes, Journey of a Noob](jekyll.html) -- So far, this is my monster blob o'
  notes with various TODOs and whatnot.

Ma Blog
-------

Here.  Knock yourself out.  Not much to it, so far:

{% for post in site.posts %}
   - {{ post.date | date_to_string }} - [{{ post.title }}]({{ post.url }}) ({{ post.tags }})

     {{ post.excerpt }}
{% endfor %}

