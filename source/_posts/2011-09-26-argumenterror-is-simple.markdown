---
layout: post
title: "ArgumentError Is Simple"
date: 2011-09-26 23:10
comments: true
categories: 
- ruby
- tips
---

What do you get if u invoke a method with the wrong number of arguments ??
It throws in ur face `ArgumentError` ... it doesn't try to be polite, you
are at fault since you are the one that breaches the contract !!

``` ruby
def m0
  :ok
end

m0    # >> :ok
m0(1) # >> (...) wrong number of arguments (1 for 0) (ArgumentError)
```

It tells you that it is expecting `0 argument`, yet you have passed it
`1 argument`. Let's have another one:

``` ruby
def m2(x, y)
  :ok
end

m2       # >> (...) wrong number of arguments (0 for 2) (ArgumentError)
m2(1)    # >> (...) wrong number of arguments (1 for 2) (ArgumentError)
m2(1, 2) # >> :ok
```

Pretty readable rite ?

