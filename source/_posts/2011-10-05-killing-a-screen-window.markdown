---
layout: post
title: "Killing a Screen Window"
date: 2011-10-05 23:42
comments: true
categories: 
- screen
- tips
---

I use [screen](http://www.gnu.org/software/screen/) everyday, yet i
must admit i've always been only scratching its surface. Today,
coworker [+kelvin](https://plus.google.com/105093850720627751966/posts)
showed me how to kill a screen window with `CTRL-a + k`.

How did i do it in the past ?? Err, this is embarrassing, i usually
either just type `exit` in the window.

Finally, let's say if u start with windows 1$, 2$, 3$ & 4$. When u
kill 3$, 4$ still retains its "4". To fix this issue, you can
`CTRL-a :number 3` to reset "4" to "3".

PS: a personal todo is to dig into `man screen` .. or bug someone to
do the digging & teach me :)
