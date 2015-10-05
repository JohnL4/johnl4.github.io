---
excerpt: Polymer Starter Kit and how to set values on documented properties
tags: Polymer
---

Polymer Starter Kit and how to set values on documented properties
==================================================================

Ok, so, I've been playing around w/the PSK, as it's called.  Getting started is
actually pretty straightforward.

- If you download the "light" zip file (which I did since I didn't want to be overwhelmed with stuff right away), you
  need to make sure you have Python, because that's how you serve it up (I'm running Python 2.7 in Cygwin). 
- Download the PSK.
- Unzip it somewhere and rename the unzipped folder to whatever you want (e.g., "HelloLite" or something).  That'll be
  your project directory.
- As the instructions in the PSK say, cd into the `app` folder and fire up the Python web server (also per the
  instructions).
- Point your browser at the appropriate address (probably something like `http://localhost:4040`, assuming you
  specified 4040 as your port number).

Setting Properties
------------------

So, what you came here for.

The starter app brings up a skeletal sort of contact-management system (or whatever it is), with a drawer-panel on the
left side that holds the menu.  I thought WAY too much horizontal space was devoted to that panel, and I wanted to
narrow it, preferably in ems, so if font sizes changed, the panel would, too.

If you read the docs on the Polymer `paper-drawer-panel`
([https://elements.polymer-project.org/elements/paper-drawer-panel](https://elements.polymer-project.org/elements/paper-drawer-panel)),
under "Properties", you see `drawerWidth`.

The way to set it is to transform the name `drawerWidth` to `drawer-width` (case is important) in accordance with the
transformation rules documented in the "Declared Properties" "Property name to attribute name mapping" section of the
Developor's Guide
([https://www.polymer-project.org/1.0/docs/devguide/properties.html#property-name-mapping](https://www.polymer-project.org/1.0/docs/devguide/properties.html#property-name-mapping)).

So, we can modify the `index.html` file in the PSK `app` directory as follows:

    <paper-drawer-panel id="paperDrawerPanel" drawer-width="10em">

(Search for `paper-drawer-panel`.)

