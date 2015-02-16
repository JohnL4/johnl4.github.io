---

---
Hi, there
=========

This is my github web site.  Yay.

How-Tos
-------

- [Jekyll](jekyll-howto.html)
- [Jekyll org-mode notes](jekyll.html)

Ma Blog
-------

Here.  Knock yourself out:

{% for post in site.posts %}
   - [{{ post.title }}]({{ post.url }})
{% endfor %}
