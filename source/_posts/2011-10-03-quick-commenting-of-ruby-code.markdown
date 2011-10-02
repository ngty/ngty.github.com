---
layout: post
title: "Quick Commenting of Ruby Code"
date: 2011-10-03 00:36
comments: true
categories: 
- vim
- tips
---

What is the fastest way to comment a block of ruby code ?? Sorry,
i'm too fast, no time to wait, let's install the extra plugins
1st:

```
$ cd ~/.vim/bundle
$ git clone https://github.com/kana/vim-textobj-user.git
$ https://github.com/nelstrom/vim-textobj-rubyblock.git
$ https://github.com/tomtom/tcomment_vim.git
```

To comment an entire method, goto anywhere of that method,
`var` & `gc`.

To comment the inner content of a method, again anywhere of
that method, `vir` & `gc`.

Sorry, too fast & too sweet ?? See
[this vimcast](http://vimcasts.org/blog/2010/12/a-text-object-for-ruby-blocks)
to learn more abt `var` & `vir` :)

