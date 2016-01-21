---
layout: post
title:  "Yazım Kılavuzu"
excerpt: ""
author: emre_demir
date:   2016-01-21
categories: articles
tags: [kılavuz]
comments: true
share: true
---

### Link

{% highlight text %}
[Lorem ipsum](http://blog.uzem.omu.edu.tr/articles/yazim-kilavuzu/)
{% endhighlight %}

[Lorem ipsum](http://blog.uzem.omu.edu.tr/articles/yazim-kilavuzu/)

### İtalik

{% highlight text %}
_Lorem_ ipsum
{% endhighlight %}

_Lorem_ ipsum

### Bold

{% highlight text %}
__Lorem__ ipsum
{% endhighlight %}

__Lorem__ ipsum

### Geçersiz Yazı / Orta Çizgi

{% highlight text %}
<del>Lorem ipsum</del>
{% endhighlight %}

<del>Lorem ipsum</del>

### Alt Çizgi

{% highlight text %}
<ins>Lorem ipsum</ins>
{% endhighlight %}

<ins>Lorem ipsum</ins>

# Kod renklendirme

Kod türüne göre tip belirlenir. 'lineanchors' opsiyonel.

![desk](https://i.imgur.com/psIRbST.png)

Satır sabitleyici ile örnek bir `ruby` kodu. highlight tipi: ruby

{% highlight ruby lineanchors %}
# The most awesome of classes
class Awesome < ActiveRecord::Base
  include EvenMoreAwesome

  validates_presence_of :something
  validates :email, email_format: true

  def initialize(email, name = nil)
    self.email = email
    self.name = name
    self.favorite_number = 12
    puts 'created awesomeness'
  end

  def email_format
    email =~ /\S+@\S+\.\S+/
  end
end
{% endhighlight %}

Örnek bir `CSS` kodu. highlight tipi: css

{% highlight css %}
.foobar {
  /* Named colors rule */
  color: tomato;
}
{% endhighlight %}

Örnek bir `JavaScript` kodu. highlight tipi: js

{% highlight js %}
var isPresent = require('is-present')

module.exports = function doStuff(things) {
  if (isPresent(things)) {
    doOtherStuff(things)
  }
}
{% endhighlight %}

Örnek bir `HTML` kodu. highlight tipi: html

{% highlight html %}
<div class="m0 p0 bg-blue white">
  <h3 class="h1">Hello, world!</h3>
</div>
{% endhighlight %}

# Başlıklar

{% highlight text %}

# H1
## H2
### H3
#### H4
##### H5
###### H6

{% endhighlight %}

# H1

## H2

### H3

#### H4

##### H5

###### H6


### Listeler

{% highlight text %}

  * Apples
  * Oranges
  * Potatoes
  * Milk

  1. Mow the lawn
  2. Feed the dog
  3. Dance

{% endhighlight %}

  * Apples
  * Oranges
  * Potatoes
  * Milk

  1. Mow the lawn
  2. Feed the dog
  3. Dance

### Resim

![desk](https://cloud.githubusercontent.com/assets/1424573/3378137/abac6d7c-fbe6-11e3-8e09-55745b6a8176.png)

### Dipnot / Kaynak

Kaynak eklemek için istediğin yere `[^1]` yazman yeterli.

{% highlight text %}

En sona ilgili bağlantıları ekle[^1].

{% endhighlight %}

En sona ilgili bağlantıları ekle[^1].

### Alıntı

Alıntı yapmak için `>` karakterini kullan.

{% highlight text %}

> Lorem ipsum dolor sit amet, consectetur adipiscing elit. Suspendisse quis porta mauris.

{% endhighlight %}

> Lorem ipsum dolor sit amet, consectetur adipiscing elit. Suspendisse quis porta mauris.

Html ile yapmak istiyorsan:

{% highlight text %}

<blockquote>
  <p>
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Suspendisse quis porta mauris.
  </p>
  <footer><cite title="Söz Sahibi">Söz Sahibi</cite></footer>
</blockquote>

{% endhighlight %}

<blockquote>
  <p>
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Suspendisse quis porta mauris.
  </p>
  <footer><cite title="Söz Sahibi">Söz Sahibi</cite></footer>
</blockquote>


---

[^1]: http://blog.uzem.omu.edu.tr/articles/yazim-kilavuzu/.
