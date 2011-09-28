---
layout: post
title: "Flexible Method Arguments With the Splat Operator"
date: 2011-09-29 00:16
comments: true
categories: 
- ruby
- tips
---

The splat operator allows a method to accepts 0 ~ ruby's max number
(hm, i don't know what number is that) of arguments, this makes
it super flexible, & here are some ways to take advantage of that:

## 1) Probably simple flat list

``` ruby
def mm(*args)
  args.each_with_index {|arg, i| puts "A[#{i}]: #{arg}" }
end

mm
# >> (blank)

mm(1)
# >> A[0]: 1

mm(1, 2)
# >> A[0]: 1
# >> A[1]: 2
```

## 2) May have array & must be flattened

``` ruby
def mm(*args)
  [args].flatten.each_with_index {|arg, i| puts "A[#{i}]: #{arg}" }
end

mm
# >> (blank)

mm(1) # same as mm([1])
# >> A[0]: 1

mm([1, 2]) # same as mm([1], [2]), mm(1, [2]) & mm([1], 2)
# >> A[0]: 1
# >> A[1]: 2

mm(1, [2, 3]) # same as mm([1, 2, 3]), mm([1], [2, 3]), etc
# >> A[0]: 1
# >> A[1]: 2
# >> A[2]: 3
```

## 3) May want to support options-like usage

``` ruby
def mm(*args)
  opts = args.last.is_a?(Hash) ? args.pop : {}
  args.each_with_index {|arg, i| puts "A[#{i}]: #{arg}" }
  opts.each {|key, val| puts "O[#{key}]: #{val}" }
end

mm
# >> (blank)

mm(x:1)
# >> O[x]: 1

mm(1)
# >> A[0]: 1

mm(1, x:2)
# >> A[0]: 1
# >> O[x]: 2

mm(1, 2, x:3, y:4)
# >> A[0]: 1
# >> A[1]: 2
# >> O[x]: 3
# >> O[y]: 4
```

## 4) May want to passing in a code-block

``` ruby
def mm(*args, &block)
  args.each_with_index {|arg, i| puts "A[#{i}]: #{arg}" }
  puts block.call if block_given?
end

mm
# >> (blank)

mm { "B[*]: rocks" }
# >> B[*]: rocks

mm(1) { "B[*]: rocks" }
# >> A[0]: 1
# >> B[*]: rocks

mm(1, 2) { "B[*]: rocks" }
# >> A[0]: 1
# >> A[1]: 2
# >> B[*]: rocks
```

## 5) All in one

``` ruby
def mm(*args, &block)
  opts = args.last.is_a?(Hash) ? args.pop : {}
  [args].flatten.each_with_index {|arg, i| puts "A[#{i}]: #{arg}" }
  opts.each {|key, val| puts "O[#{key}]: #{val}" }
  puts block.call if block_given?
end

mm(1, [2, 3], x:4, y:5) { "B[*]: rocks" }
# >> O[x]: 4
# >> O[y]: 5
# >> A[0]: 1
# >> A[1]: 2
# >> A[2]: 3
# >> O[x]: 4
# >> O[y]: 5
# >> B[*]: rocks
```

## Extra Reading

To advance ur ruby kungfu, you probably want some extra reading from the
[free chapter abt designing beautiful apis](http://github.com/sandal/rbp-book/raw/gh-pages/pdfs/ch02.pdf),
from [Ruby Best Practices](http://rubybestpractices.com/).
