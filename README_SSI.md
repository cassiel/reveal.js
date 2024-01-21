`-*- word-wrap: t; -*-`

# Server Side Includes

The file `index-ssi.shtml` is a copy of `index.html` with the actual slide content, and some header content, removed; instead it contains a couple of server side include statements. (It therefore needs to be rendered through a server which supports SSI, such as Apache.)

In the `<head>` section there's this:

    <!--#include file="_included/head.html" -->

and in the body there's this:

    <!--#include file="_included/content.html" -->

The `_included` subdirectory isn't checked into this repo, and is something you're presumably going to create and populate yourself. (I'm generating slides from Clojure via Hiccup, and have a few Clojure source files, one for each presentation, each of which builds its own `head.html` and `content.html` for me.)

`head.html` should provide the `<title>` and (if required) `<meta ...>` elements. It must also contain a `<link ...>` for the main theme (since it seems reasonable that different presentations might use different styles).

`content.html` contains the actual slides, wrapped in the `<div class="reveal">` element.

## Slides in Clojure

See the [companion project](https://github.com/cassiel/reveal-js-demo-slides) for an example slide deck and instructions for generating a presentation as a sub-module of this project.

## Setup

We need a web server configured to allow SSI. In [reveal-js-demo-slides](https://github.com/cassiel/reveal-js-demo-slides) look at `server.sh`: it uses Docker to start up a web server. Run that in the top-level directory of our `reveal.js`. Then hit up `http://localhost:5050` for the reveal.js demo, or `http://localhost:5050/index-ssi.html` for the SSI page with (hopefully) generated content.

## Update

It seems we got fed up with relying on SSI, so more recent versions of the Clojure renderer just process `index-ssi.html` as a template and insert the content directly, copying over static dependencies.

## Author

[Nick Rothwell](https://cassiel.com).
