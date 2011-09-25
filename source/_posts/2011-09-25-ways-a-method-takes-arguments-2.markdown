---
layout: post
title: "Ways a Method Takes Arguments (2)"
date: 2011-09-25 23:57
comments: true
categories: 
- ruby
- tips
---

### 6. Required hash argument

``` ruby
class HTML
  def self.div(attrs)
    attrs = attrs.map{|k,v| "#{k}='#{v}'" }.join(' ')
    "<div #{attrs}></div>"
  end
end

HTML.div                                   # ArgumentError
HTML.div({:id => 'body'})                  # >> "<div id="body"></div>"
HTML.div({:class => 'red', :id => 'body'}) # >> "<div class="red" id="body"></div>"
```

Well, the `{...}` isn't necessary when dealing with hash argument as
the only or last argument, thus the above can be rewritten as:

``` ruby
HTML.div(:id => 'body')                  # >> "<div id="body"></div>"
HTML.div(:class => 'red', :id => 'body') # >> "<div class="red" id="body"></div>"
```

And using the newer (1.9) json-like hash, we can again rewrite the above as:

``` ruby
HTML.div(id: 'body')               # >> "<div id="body"></div>"
HTML.div(class: 'red', id: 'body') # >> "<div class="red" id="body"></div>"
```

### 7. Optional hash argument

``` ruby
class HTML
  def self.div(attrs = {})
    attrs = attrs.map{|k,v| "#{k}='#{v}'" }.join(' ')
    "<div #{attrs}></div>"
  end
end

HTML.div                           # >> "<div ></div>"
HTML.div(id: 'body')               # >> "<div id="body"></div>"
HTML.div(class: 'red', id: 'body') # >> "<div class="red" id="body"></div>"
```

Let's say we want `id` attribute to be always present, & when unspecified,
we auto-generate one:

``` ruby
class HTML
  class << self
    def div(attrs = {})
      attrs[:id] ||= "div-#{count}"

      attrs = attrs.map{|k,v| "#{k}='#{v}'" }.join(' ')
      "<div #{attrs}></div>"
    end

    def count
      @count ||= 0
      @count += 1
    end
  end
end

HTML.div(id: 'body')   # >> "<div id="body"></div>"
HTML.div(class: 'red') # >> "<div class="red" id="div-1"></div>"
```

### 8. Mixed arguments with last as optional hash

``` ruby
class HTML
  class << self
    def element(tag, attrs = {})
      attrs[:id] ||= "#{tag}-#{count}"

      attrs = attrs.map{|k,v| "#{k}='#{v}'" }.join(' ')
      "<#{tag} #{attrs}></#{tag}>"
    end

    def count
      @count ||= 0
      @count += 1
    end
  end
end

HTML.element                        # >> ArgumentError
HTML.element('div')                 # >> "<div id="div-1"></div>"
HTML.element('div', {id: 'body'})   # >> "<div id="body"></div>"
HTML.element('div', {class: 'red'}) # >> "<div class="red" id="div-2"></div>"
```

Again, the `{...}` isn't necessary when dealing with hash argument as
the only or last argument, thus the above can be rewritten as:

``` ruby
HTML.element('div', id: 'body')   # >> "<div id="body"></div>"
HTML.element('div', class: 'red') # >> "<div class="red" id="div-3"></div>"
```
