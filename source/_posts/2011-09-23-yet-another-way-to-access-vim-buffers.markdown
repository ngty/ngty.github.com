---
layout: post
title: "Yet Another Way to Access Vim Buffers"
date: 2011-09-23 12:55
comments: true
categories: 
- vim
- tips
---

How do you quickly access a particular buffer (amongst
a long list of buffers) in vim? For ages, i've been
using `:ls`, followed by `:b<id>`, where `<id>` is
the id of a particular buffer.

Recently, a coworker showed me how to use `CTRL-b` to
achieve it. With it, you are presented with vim's
`BufExplorer`, & within it, u can goto a specific
buffer with:

* search with `/`, followed by `enter`, or
* goto that line with `:<lineno>`, followed by `enter`, or
* simply `:b<id>`

I'm sure there are more ways than the above-mentioned ...
have fun !!
