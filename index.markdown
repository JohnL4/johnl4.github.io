---

---
Hi, there
=========

This is my github web site.  Yay.

How-Tos
-------

- [Jekyll org-mode notes, Journey of a Noob](jekyll.html)

Ma Blog
-------

Here.  Knock yourself out:

{% for post in site.posts %}
   - {{ post.date }} - [{{ post.title }}]({{ post.url }}) ({{ post.tags }})
{% endfor %}

(Note: can't do something like `\{\{ post.date.strftime( "%Y-%m-%d (%a)") \}\}` here.  Comes out blank.)
