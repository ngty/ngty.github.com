---
layout: post
title: "A Little Bit of Sed Kungfu"
date: 2011-10-06 23:02
comments: true
categories: 
- tips
- shell
- sed
---

Just picked up a little bit of [sed](http://www.gnu.org/s/sed/)
kungfu today while pairing with
[jeff](https://plus.google.com/116177061453197380672/posts).

## In-place editing with "-i"

If you want to do in-place editing of a file, you can pass the
`-i` option to sed. Let's say we have the following file:

```
sed is cool
```

With:

```
$ sed -i /path/to/file -e 's/cool/awesome/'
```

We get:

```
sed is awesome
```

So how do i acheive this previously ?? This is embarrassing, it
used to be like this:

```
$ cat /path/to/file | sed 's/cool/awesome' > /path/to/file.new
$ mv /path/to/file.new /path/to/file
```

## Replacing only lines matching pattern

Let's say you have the following file:

```
Vim is really cool,
& sed is cool as well.
```
We want to replace only the line with the occurrence of "sed". We
can acheive it using the script command
`/<pattern>/s/<original-text>/<replacement-text>`, just like this:

```
sed -e '/sed/s/cool/awesome/' /path/to/file
```

This is what we get in stdout:

```
Vim is really cool,
& sed is awesome as well.
```

Happy Sed-ing :)
