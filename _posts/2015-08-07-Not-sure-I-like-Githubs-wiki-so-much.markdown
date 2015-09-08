---
excerpt: So, I'm not so sure I like GitHub's wiki so much, after all (BUT WAIT! THERE'S A SOLUTION!)
---

So, I'm not so sure I like GitHub's wiki so much, after all
=============================================================

Looks like there's no way to execute a search, so you're reduced to stumbling around from linked page to linked page, trying to find what you're interested in.

:(

So, what to do?  I could keep on building [org-mode](orgmode.org) files, and that
might actually be the best bet.

Or I could find a way to make a zillion little Jekyll files here in another folder,
and figure out how to refer to them.

If I take the latter approach, is searchability any better? Apparently so.  Check this out:
[https://www.google.com/webhp?sourceid=chrome-instant&ion=1&espv=2&es_th=1&ie=UTF-8#q=stylesheet%20site%3Ajohnl4.github.io&es_th=1](https://www.google.com/webhp?sourceid=chrome-instant&ion=1&espv=2&es_th=1&ie=UTF-8#q=stylesheet%20site%3Ajohnl4.github.io&es_th=1)

Or maybe I should just continue to use Evernote, but better.

The Solution
-------------

* Make wikis editable only by collaborators:

    ![Making GitHub wikis editable only by collaborators](/images/github-wiki-not-public-edit.png)

  (After you click on the settings "gear" for your wiki.)

* Use Google's `site:` operator:

        site:github.com/NRules/NRules/wiki assembly

  Note that, for some reason, this search works, but the following one doesn't:

        site:github.com/JohnL4/johnl4.github.io/wiki markup
