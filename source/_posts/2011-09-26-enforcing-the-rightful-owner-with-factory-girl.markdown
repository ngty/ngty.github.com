---
layout: post
title: "Enforcing the Rightful Owner With Factory Girl"
date: 2011-09-26 00:10
comments: true
categories: 
- ruby
- tips
- factories
- spec
---

We use thoughtbot's FactoryGirl extensively in our daily spec (& feature)
writing. One recent problem we encounter is the failure to correctly set the
associations between the following 2 example models.

``` ruby
class Blog < ActiveRecord::Base
  has_many :comments
end

class Comment < ActiveRecord::Base
  belongs_to :blog
end
```

The factory definitions are as follow:

``` ruby
FactoryGirl.define do
  factory :comment do
    # (blah blah)
    blog
  end
end

FactoryGirl.define do
  factory :blog do
    # (blah blah)

    factory :commented_blog do
      comments { [association(:comment)] }
    end
  end
end
```

The problem with the above definitions is that calling
`Factory(:commented_blog)` creates `2 blogs & 1 comment` instead of the
expected `1 blog & 1 comment`, and the comment isn't owned by the
intended blog.

Fixing this problem turns up to be pretty simple, all we need to do
is when creating a comment, we enforces the desired ownership:

``` ruby
FactoryGirl.define do
  factory :blog do
    # (blah blah)

    factory :commented_blog do
      # Explicte declaring the rightful owner of the comment
      after_create {|blog| Factory(:comment, blog: blog) }
    end
  end
end
```

If you have some time to spare, u really should take a good read of [this doc
](https://github.com/thoughtbot/factory_girl/blob/master/GETTING_STARTED.md)
