---
layout: post
title: "Tripping Over Method &amp; Local Variable"
date: 2011-09-28 23:14
comments: true
categories: 
- ruby
- tips
---

As you know, ruby always tries hard to get out of the programmer's
way most of the time. One good example is when u invoke a method
that doesn't require any argument:

``` ruby
def mm
  :ok
end

mm   # >> :ok
mm() # >> :ok
```

Almost always, to invoke `mm`, `mm` is preferred over `mm()`, doing
it the `mm()` way is so un-rubyish. Yet this flexibility tripped us
over today, consider the following:

``` ruby
describe Thing do
  let(:alien) { Factory(:thing, name: 'alien') }
  let(:robot) { Factory(:thing, name: 'robot') }

  %w{alien robot}.each do |thing|
    context "as #{thing}" do
      let(:subject) { thing }
      let(:thing) { send(thing) }
      it { should be_macho }
    end
  end
end
```

When we ran the above spec, we get
`undefined method 'macho' for "alien":String (NoMethodError)` .. why ??

Here's our intended behaviour:

``` ruby
describe Thing do
  let(:alien) { Factory(:thing, name: 'alien') } # defines alien()
  let(:robot) { Factory(:thing, name: 'robot') } # defines robot()

  %w{alien robot}.each do |thing|  # set local var thing
    context "as #{thing}" do
      let(:subject) { thing }      # defines subject() to return thing()
      let(:thing) { send(thing) }  # defines thing() to return the evaluate alien() or robot()
      it { should be_macho }
    end
  end
end
```

This is what happened instead:

``` ruby
describe Thing do
  let(:alien) { Factory(:thing, name: 'alien') } # defines alien()
  let(:robot) { Factory(:thing, name: 'robot') } # defines robot()

  %w{alien robot}.each do |thing| # set local var thing
    context "as #{thing}" do
      let(:subject) { thing }     # ** defines subject() to return the local var thing
      let(:thing) { send(thing) } # ** defines thing() which never gets invoked
      it { should be_macho }
    end
  end
end
```

To fix the problem, we can either:

* avoid confusing names by renaming the local variable `thing` to
`_thing` & amend all its intended usage accordingly, OR

* be explicte when invoking method by rewriting
`let(:subject) { thing }` as `let(:subject) { thing() }`

