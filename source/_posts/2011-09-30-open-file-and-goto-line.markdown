---
layout: post
title: "Open File &amp; Goto Line"
date: 2011-09-30 12:37
comments: true
categories: 
- vim
- tips
---

I only get to know this recently, you can open a file & goto
a specific line in vim with:

```
$ vim /path/to/file +100
```

The above opens `/path/to/file` & sets u on `line 100`. When
are already in vim, you can acheive it with:

```
:e /path/to/another/file +99
```

But this won't work for buffer though, meaning NONE of the
following will work :(

```
:b /path/to/another/file +99
:b<id> +99
:b# +99
```

