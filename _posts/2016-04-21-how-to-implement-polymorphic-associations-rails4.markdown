---
layout: post
title:  "Polymorphic Associations Rails4"
date:   2016-04-21 10:18:00
comments: true
desc: "How to implement polymorphic associations in rails 4."
keywords: polymorphic, rails, rails4, associations
categories: rails
---

**Polymorphism:** As per [Wiki][poly-wiki], it is the provision of a single interface to entities of different types.

**Polymorphic Associations (in Rails' terms):** With polymorphic associations, a model can belong to more than one other model, on a single association.

For example (**in this blog**), we will have a `Comment` model that belongs to either a `Post` model or a `Forum` model. 

First, we generate our Comment model. Below command will generate model, migration and test.

```ruby
rails g model Comment commentable_type:string commentable_id:integer user_id:integer body:text
```

then `rake db:migrate`

Now we will define our models as shown below:

```ruby
class Comment < ActiveRecord::Base
  belongs_to :commentable, polymorphic: true
end
 
class Post < ActiveRecord::Base
  has_many :comments, as: :commentable
end
 
class Forum < ActiveRecord::Base
  has_many :comments, as: :commentable
end
```

Alright, that would be all for modeling. Lets go to Controllers:

We create `comments_controller.rb` for all models we want to use this polymorphic association. So for our example, we create 

`controllers > posts > comments_controller.rb
controllers > forums > comments_controller.rb`

Sample code for posts > comments_controller.rb

```ruby
class Posts::CommentsController < ApplicationController
  before_action :authenticate_user!
  before_action :set_post

  # Create comment for post
  def create
    @comment = @post.comments.new(comment_params)
    @comment.user = current_user
    @comment.save
    redirect_to @post, notice: "Comment added successfully"
  end

  private
  
  def set_post
    @post = Post.find(params[:post_id])
  end

  def comment_params
    params.require(:comment).permit(:body)
  end
end
```

Similarly you can add for all the models using this polymorphic association. (You may create one comments_controller and put all common code in there).

Lets add routes for the comments at `config/routes.rb`

```ruby
resources :posts do
  resources :comments, module: :posts
end
resources :forums do
  resource :comments, module: :forums
end
```

Okay, most of our setup is ready. Lets add code to view all comments and form to add one.

```ruby
<h3>Comments</h3>
<% @post.comments.each do |comment| %>
  <div class="well right">
    <%= comment.body %>
  </div>
<% end %>
<%= form_for [@post, Comment.new] do |f| %>
  <div class="form-group">
    <%= f.text_area :body, class: "form-control" %>
  </div>
  <%= f.submit class: "btn btn-primary" %>
<% end %>
```

Alright, thats it. We have setup our polymorphic association. 

[poly-wiki]: https://en.wikipedia.org/wiki/Polymorphism_(computer_science)