---
layout: post
title: "Method aliasing"
date: 2011-09-22 22:26
comments: true
categories: 
- ruby
- tips
---

Method aliasing is what every budding rubyists should pick up.
This is done using `Module#alias_method`:

{% codeblock lang:ruby %}
class Thing
  def size; :xl; end
  alias_method :mass, :size
end

thing = Thing.new
thing.size # >> xl
thing.mass # >> xl
{% endcodeblock %}

To say that it is simple aliasing is abit deceiving. Under the hood,
ruby creates a copy of the original method `Thing#size`, thus, even
if you change the original method, the new method `Thing#mass` still
points to the same method. Here's an extension of the above example:

{% codeblock lang:ruby %}
class Thing
  # Redefining the original method
  def size; :xxl; end
end

thing = Thing.new
thing.size # >> xxl
thing.mass # >> xl
{% endcodeblock %}

It is important to note that the last technique isn't encouraged in
proper software engineering, yet it can really be useful when u need
a quick hack on somebody's code, just to patch & get things done.

If u have some time to spare, you should read more abt
[yehuda's case against rails' `alias_method_chain`
](http://yehudakatz.com/2009/03/06/alias_method_chain-in-models).
