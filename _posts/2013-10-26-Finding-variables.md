---
layout: post
title:  "Finding variables across a project"
date:   2013-10-26 16:34:13
categories: emacs
---

Quite often, I want to find a variable across the whole project I'm working on. I have progressed
through a few different methods of doing so. When I was new to emacs and ran it in a terminal, I
would flick to another tab in my terminal and just run `grep`.

Then I learnt about `grep -n`, which also displays the line
numbers. I could then flick back to my emacs session and `M-g M-g` to go to that line. This is a bit
of a pain, as I had to keep switching between tabs to find the next search result.

This year, I started using emacs in its gui, as I was mostly working locally, rather than on remote
machines. Now I had to switch between emacs and my terminal, which was getting annoying. I
discovered the wonders of `M-x eshell` - a terminal inside emacs! Using grep from eshell opens a new
buffer with the grep results. From this buffer, you can use `n` and `p` to move between search
results, which automatically displays the relevant section in a different buffer.

Then this week I came across `M-x occur` (shortcut: `M-s o`). This searches the current buffer for a regexp and displays
the results in a new buffer. You can search across multiple buffers with `M-x multi-occur`, however
you have to specify each buffer manually. A better command is `M-x
multi-occur-in-matching-buffers`, which searches buffers that match a regexp.

So here is how I've started searching for variables across projects:

1. First, I open all the project files (`C-x C-f *.[fF]90`, for example)
2. Run `M-x multi-occur-in-matching-buffers` with the first argument as an elisp regexp
   (e.g. `.*\.[fF]90`)
3. Switch to the `*Occur*` buffer and run `M-x next-error-follow-minor-mode` (this can actually be
   toggled with `C-c C-f`, same as in `compilation-mode`)
4. Use `C-n` and `C-p` to move between search results, displaying the result in a different window
