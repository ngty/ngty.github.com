---
layout: post
title: "What you should know abt ActiveRecord's callbacks"
date: 2011-09-22 23:04
comments: true
categories: 
- rails
- ruby
- tips
---

I'm a fan of ActiveRecord's callbacks, as i see it a clean way to
get things done in the life-cycle of a model instance. Yet, today
a couple of us just tripped over the following:

{% codeblock lang:ruby %}
class Thing < ActiveRecord::Base
  before_create :reset_pretty_flag

private

  def reset_pretty_flag
    # Let's KISS for now, even though the logic is flawed :P
    self.pretty = name.downcase.include?('pretty')
  end
end
{% endcodeblock %}

The problem with `Thing#reset_pretty_flag` is that in the unfortunate
case that thing isn't pretty, its creation fails. Why ?? Cos when thing
isn't pretty, a false is returned, & this halts the create executation
chain. The workaround is therefore to return a true always:

{% codeblock lang:ruby %}
def reset_pretty_flag
  self.pretty = name.downcase.include?('pretty')
  true # any other non nil/false value will work as well
end
{% endcodeblock %}

To learn more, i strongly encourage a good read on [ActiveRecord's callbacks
](http://guides.rubyonrails.org/active_record_validations_callbacks.html#callbacks-overview)
