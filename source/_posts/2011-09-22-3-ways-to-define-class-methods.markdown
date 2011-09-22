---
layout: post
title: "3 Ways to Define Class Methods"
date: 2011-09-22 23:47
comments: true
categories: 
- tips
- ruby
---

There are 3 ways to create class methods in ruby:

``` ruby Probably when you just need one
class Thing
  def self.all
    :everything
  end
end

Thing.all # >> :everything
```

``` ruby Probably when you need several
class Thing
  class << self

    def self.all
      :everything
    end

    def self.some
      :something
    end

  end
end

Thing.all  # >> :everything
Thing.some # >> :something
```

``` ruby Probably when you are going bananas
class Thing
  def Thing.all
    :everything
  end
end

Thing.all # >> :everything
```

If you work with me & u use the last one, i'll hunt u down &
haunt you :P
