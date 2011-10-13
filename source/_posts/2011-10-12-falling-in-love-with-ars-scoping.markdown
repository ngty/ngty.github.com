---
layout: post
title: "Falling in Love With AR's Scoping"
date: 2011-10-12 15:10
comments: true
categories: 
- ruby
- rails
- activerecord
---

If you do activerecord, you should fall in love with scoping, as it
can really boast ur AR-fu.

Here's an example:

``` ruby
class Shirt
  belongs_to :owner, :polymorphic => true
end

class Cat
  has_many :shirts, :as => :owner
end

class Dog
  has_many :shirts, :as => :owner
end
```

Let's say i want to be able to retrieve doggie's red shirts:

``` ruby
class Dog
  # (blah blah)

  def red_shirts
    shirts.where(:color => 'red')
  end
end

doggie.shirts     # all shirts
doggie.red_shirts # all red shirts
```

Ok, what if we want to retrieve kitty's red shirts as well ?

``` ruby
class Cat
  # (blah blah)

  def red_shirts
    shirts.where(:color => 'red')
  end
end

kitty.shirts     # all shirts
kitty.red_shirts # all red shirts
```

Hmmm, duplication detected, but not so bad (yet) .. how abt i
want to retrieve all red shirts ? AR supports this via the
`scope` declarative:

``` ruby
class Shirt
  # (blah blah)

  scope :red, where(:color => 'red')

  # * A less DSL-ish approach is to declare a class method
  # def self.red
  #   where(:color => 'red')
  # end
end

Shirt.red # all red shirts
```

And you know what, with the new `Shirt.red`, i can throw away
`Cat#red_shirts` & `Dog#red_shirts`. If i ever want to fetch
the red shirts of doggie & kitty:

``` ruby
doggie.shirts     # all doggie's shirts
doggie.shirts.red # all doggie's red shirts

kitty.shirts      # all kitty's shirts
kitty.shirts.red  # all kitty's red shirts
```

And to make it even sweeter, i can do the following as well:

``` ruby
doggie.shirts.red.create(:size => :xl) # doggie gets a new red :xl shirt
kitty.shorts.red.create(:size => :xs)  # kitty gets a new red :xs shirt
```

Honestly, we should love AR's scoping rite ?!

If u have the time, take a look at the
[activerecord doc](http://api.rubyonrails.org/classes/ActiveRecord/NamedScope/ClassMethods.html).
