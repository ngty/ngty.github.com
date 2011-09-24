---
layout: post
title: "Ways a Method Takes Arguments (1)"
date: 2011-09-24 22:27
comments: true
categories: 
- ruby
- tips
---

### 1. Argument is required

``` ruby
class Writer
  def self.type(w)
    "#{w}"
  end
end

Writer.type      # >> ArgumentError
Writer.type("1") # >> "1"
```

### 2. Argument is optional

``` ruby
class Writer
  def self.type(w = nil)
    "#{w}"
  end
end

Writer.type      # >> ""
Writer.type("1") # >> "1"
```

### 3. One argument is required while the other optional

``` ruby
class Writer
  def self.type(w1, w2 = nil)
    "#{w1}#{w2}"
  end
end

Writer.type           # >> ArgumentError
Writer.type("1")      # >> "1"
Writer.type("1", "2") # >> "12"
```

### 4. Any number of arguments is ok

``` ruby
class Writer
  def self.type(*w)
    "#{w * ''}"
  end
end

Writer.type                # >> ""
Writer.type("1")           # >> "1"
Writer.type("1", "2", "3") # >> "123"
```

### 5. One argument is required while the rest are optional & can be any number

``` ruby
class Writer
  def self.type(w1, *w)
    "w1#{w * ''}"
  end
end

Writer.type                # >> ArgumentError
Writer.type("1")           # >> "1"
Writer.type("1", "2", "3") # >> "123"
```

