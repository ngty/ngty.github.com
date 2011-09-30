---
layout: post
title: "Yet Another Way to Access Vim Buffers"
date: 2011-09-23 12:55
comments: true
categories: 
- vim
- tips
---

How do you quickly access a particular buffer (amongst a long list of
buffers) in vim? For ages, i've been using `:ls`, followed by `:b<id>`,
where `<id>` is the id of a particular buffer.

Recently, i've discovered yet another way to acheive it using
[`BufExplorer`](http://www.vim.org/scripts/script.php?script_id=42),
to install it, download the
[latest version](http://www.vim.org/scripts/script.php?script_id=42)
& save it to `~/.vim/bundle`, then:

```
$ cd ~/.vim/bundle
$ unzip bufexplorer.zip
```

Restart your vim, open several files, & try `\be` (backslash + b + e),
you are then presented with `BufExplorer`, & within it, u can goto a
specific buffer with:

* search with `/`, followed by `enter`, or
* goto that line with `:<lineno>`, followed by `enter`, or
* simply `:b<id>`

If you want to be able to goto `BufExplorer` by doing `CTRL-b`, just add
the following line to ur `~/.vimrc`:

```
nnoremap <C-B> :BufExplorer<cr>
```

If you prefer loading `BufExplorer` in horizontal or vertical split, you
may wanna try:

* `\bs` (backslash + b + s) for horizontal split
* `\bv` (backslash + b + s) for vertical split

Pick the one u like & have fun !!
