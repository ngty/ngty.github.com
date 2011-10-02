---
layout: post
title: "The Motion That You Must Know"
date: 2011-10-02 23:52
comments: true
categories: 
- vim
- tips
---

Let me tell you, `i` ("inside") is the motion that you MUST know.

Given `"this is awesome"`, anywhere from the starting `"` to
the ending one, just do a `ci"`, you can replace anything within
the quotes. This works for backtick & single-quote char as well,
but not for other delimiters like `"/"`, `"|"`, `"\"`, ..., etc.

Given `%(this is awesome)`, doing `ci(` or `ci)` works as
well. In fact, this works equally well for `ci<`, `ci>`, `ci[`,
`ci]`, `ci{` & `ci}`.

If you have installed the `vim-textobj-user` &
`vim-textobj-rubyblock` plugins:

```
$ cd ~/.vim/bundle
$ git clone https://github.com/kana/vim-textobj-user.git
$ git clone https://github.com/nelstrom/vim-textobj-rubyblock.git
```

You can do `cir` anywhere from start of a `class ... end`,
`module ... end`, `def ... end`, `do ... end`, `if ... end`, ...
to replace the contents within.

Last but not least, you may wish to know the `a` (stands for "around")
motion as well. Try out `ca"`, `ca(`, `car` & friends.

Have fun !!

