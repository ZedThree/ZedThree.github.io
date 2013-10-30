---
layout: post
title:  "Graphing Fortran Projects"
date: 2013-10-30 21:47:07
categories: Fortran,python
---

Currently, I am refactoring the code that I work on and I wanted to see how the different modules
depend on each other. Doxygen generates graphs of how individual functions and routines call each
other, which is pretty nifty, but it doesn't seem to do it for the modules. Looking into how doxygen
generates these graphs, I found out it uses the graphviz package, in particular `dot`.

Dot is a very simple language used to describe
graphs. [Wikipedia](http://en.wikipedia.org/wiki/DOT_%28graph_description_language%29) has some nice
examples.

I wrote a short python function to crudely extract the module dependencies from my code and put them
into a dot graph:

{% gist 7196938 %}

Writing the output of this function to a file and running `dot` on it produces lovely images like
this:

![messy graph]({{ site.baseurl }}/images/fenicia_test.svg)

...I'm not sure if my refactoring is making it better or worse.
