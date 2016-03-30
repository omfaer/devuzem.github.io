---
layout: post
title:  "Rails ActiveSupport::Concern Kullanımı"
excerpt: ""
author: ecmelkytz
date:   2016-03-24
categories: articles
comments: true
share: true
---

Rails 4 ile gelen ActiveSupport'un concern modülü  [DRY][DRY]  ilkesine aykırı durumları idare etmemizi sağlar.

##### Model'de concern kullanımına bir örnek:

Aşağıdaki gibi `Post` ve `Comment` modellerimizin olduğunu ve like/dislike gibi oylama yapabilmemiz için `Vote` modelini kullandığımızı düşünelim.

{% highlight ruby %}
# models/post.rb
class Post < ActiveRecord::Base
  # Validations
  validates :title, :content, presence: :true
  # Relations
  has_many :votes
  has_many :comments

  def upvote_count
    votes.where(vtype: Vote.vtypes[:upvote]).count
  end

  def downvote_count
    votes.where(vtype: Vote.vtypes[:downvote]).count
  end
end
{% endhighlight %}

{% highlight ruby %}
# models/comment.rb
class Comment < ActiveRecord::Base
  # Validations
  validates :content, presence: :true
  # Relations
  has_many   :votes
  belongs_to :post

  def upvote_count
    votes.where(vtype: Vote.vtypes[:upvote]).count
  end

  def downvote_count
    votes.where(vtype: Vote.vtypes[:downvote]).count
  end
end
{% endhighlight %}

{% highlight ruby %}
# models/vote.rb
class Vote < ActiveRecord::Base
  enum vtype: { downvote: 0, upvote: 1 }
end

{% endhighlight %}

Görüldüğü gibi `downvote_count` ve `upvote_count` fonksiyonları hem `Post` hem de `Comment` modelinde tekrarlanıyor. Bu durumdan kurtulmak için concern'i devreye sokalım:

{% highlight ruby %}
# models/concern/votable.rb
module Votable
  extend ActiveSupport::Concern

  included do
    has_many :votes
  end

  def upvote_count
    votes.where(vtype: Vote.vtypes[:upvote]).count
  end

  def downvote_count
    votes.where(vtype: Vote.vtypes[:downvote]).count
  end
end
{% endhighlight %}


Bu fonksiyonları kullanabilmemiz için yapmamız gereken tek şey oluşturduğumuz module'ı kullanacağımız model içinde *include* etmektir.

{% highlight ruby %}
# models/post.rb
class Post < ActiveRecord::Base
  include Votable
  # Validations
  validates :title, :content, presence: true
  # Relations
  has_many :comments
end

# models/comment.rb
class Comment < ActiveRecord::Base
  include Votable
  # Validations
  validates :content, presence: :true
  # Relations
  belongs_to :post
end
{% endhighlight %}

Kullanım:

{% highlight ruby %}
pry(main)> post = Post.create(title:"Baslik", content:"Icerik")
# => <Post id: 1, title: "Baslik", content: "Icerik" >
pry(main)> Vote.create(vtype: 0, post_id: 1)
# => <Vote id: 1, vtype: 0, post_id: 1,  comment_id: nil >
pry(main)> post.downvote_count
# => 1
{% endhighlight %}

{% highlight ruby %}
pry(main)> comment = Comment.create(content:"Comment content", post_id:1)
# => <Comment id: 1, content: "Comment content", post_id: 1>
pry(main)> Vote.create(vtype: 1, comment_id: 1)
# => <Vote id: 2, vtype: 1, post_id: nil, comment_id: 1 >
pry(main)> comment.upvote_count
# => 1
{% endhighlight %}

Bunun gibi DRY ilkesine aykırı durumlardan kurtulmak için concern'i controller'larda da kullanabiliriz.

### Kaynaklar

[Rails ActiveSupport::Concern](http://api.rubyonrails.org/classes/ActiveSupport/Concern.html)

[Put chubby models on a diet with concerns](https://signalvnoise.com/posts/3372-put-chubby-models-on-a-diet-with-concerns)


[DRY]: https://en.wikipedia.org/wiki/Don%27t_repeat_yourself
