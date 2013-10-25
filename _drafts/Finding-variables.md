---
layout: post
title:  "Finding variables across a project"
date:   2013-10-25 09:14:43

categories: emacs
---

Quite often, I want to find a variable across the whole project I'm working on. I have progressed
through a few different methods of doing so. When I was new to emacs, I would flick to another
terminal and just run grep:

{% highlight bash %}
$ grep foo *.f90
a.f90: integer :: foo
b.f90: foo = 4
{% endhighlight %}


