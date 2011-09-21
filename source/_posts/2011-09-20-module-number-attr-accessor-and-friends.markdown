---
layout: post
title: "Module#attr_accessor &amp; friends"
date: 2011-09-20 23:55
comments: true
categories:
- ruby
- tips
- beginner
---

Have u ever find urself writing simple reader & writer like this:

{% codeblock lang:ruby %}
class Thing
  def size=(size)
    @size = size
  end
  def size
    @size
  end
end
{% endcodeblock %}

You should probably be using `Module#attr_accessor`:

{% codeblock lang:ruby %}
class Thing
  attr_accessor :size
end

t = Thing.new
t.size = :xl
puts t.size # >> xl
{% endcodeblock %}

If u want to keep the writer private, while still having the reader as public,
you can do the following:

{% codeblock lang:ruby %}
class Thing
  attr_accessor :size
  private :size=

  def cheat(size)
    self.size = size
  end
end

t = Thing.new
#puts t.size = :xl # >> NoMethodError
t.cheat(:xl)
puts t.size        # >> xl
{% endcodeblock %}

Besides improving the readability of ur code, `Module#attr_accessor` is also
more performant than ur handcrafted accessors, here's a quick benchmark:

{% codeblock lang:ruby %}
class AA
  attr_accessor :size
end

class BB
  def size        ; @size        ; end
  def size=(size) ; @size = size ; end
end

require 'benchmark'
Benchmark.bm do |x|
  [AA, BB].each do |klass|
    x.report do
      1000000.times do
        aa = klass.new
        aa.size = 2
        aa.size
      end
    end
  end
end

#>> user     system      total        real
#>> 0.410000   0.000000   0.410000 (  0.412785)
#>> 0.450000   0.000000   0.450000 (  0.456264)
{% endcodeblock %}

The difference is there, but isn't too much. But as the number of
accessors involved increases, the difference becomes greater.

Besides `Module#attr_accessor`, `Module` also has `#attr_reader` &
`#attr_writer` as well, to generate only the reader/writer that u need.

