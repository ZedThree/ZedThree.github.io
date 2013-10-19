---
layout: post
title:  "Building a blog"
date:   2013-10-19 22:01:06
categories: jekyll
---

I have made various short-lived websites over the years, using sundry template sites - geocities and
their ilk. This one was built using a bunch of free tools and templates too, but it's the only one
where I have actually laid down money for a domain name. In getting this one off the ground, I have
learnt how little I actually knew about hosting a site.  Fusionplasma.co.uk is hosted on
[GitHub Pages](http://pages.github.com/), the domain name came from
[Vidahost](https://www.vidahost.com/), and the backend is done in [Jekyll](http://jekyllrb.com/)
(which in turn is written in Ruby).

Messing about with projects on GitHub, I discovered that projects can have their own website, hosted
on GitHub, very simply. In fact, users can have their own pages too. I had been thinking for some
time about having some little space on the web to put little snippets of code, and so on. At the
same time, I had also been thinking about getting a slightly more professional personal email
address. This seemed like the perfect spur to action, so I started a new project on GitHub with the
name "ZedThree.GitHub.io" (ZedThree being my GitHub username). A project named like this becomes
your user page, accessible from http://ZedThree.github.io

The next step was to get my own domain name. As all variations on my name were already taken, I
decided to go with something related to my job - a researcher in fusion. There are two steps to
actually using this domain name as the url for the GitHub user-page. This first is to put the domain
name into a file named CNAME in the repo. This tells GitHub to serve your pages from that domain,
instead of username.github.io. Next, you need to point your domain name to GitHub's servers. This
is done using a nameserver. Nameservers translate the natural-language domain name into a numeric IP
address. Your registrar might provide a nameserver; if not, there are free ones available.

Well, it took me a while to actually finish writing this post. I guess I've not got into the habit yet.
