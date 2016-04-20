---
layout: post
title:  "Adding meta tags in Rails 4 app for each post in Views"
date:   2016-03-06 10:18:00
comments: true
desc: "How to add meta-content into rails 4 app, which will render meta content with respect to each blog post. "
keywords: meta-tags, rails4, seo
categories: rails4 meta-tags
---

In this blog post, we will learn how to add meta-content into our rails 4 app, which will render meta content with respect to each blog post. 

We are going to use a fantastic gem called [meta-tags by Dmytro Shteflyuk][gem-link], which not only made it fairly easy to implement but also gives us all the flexibility to customize according to our needs (but that would be out of scope of this post).

Now let’s dive right into the implementation. 

I am assuming you already have your rails app running. Let’s add the meta-tags gem to your Gemfile. Then `bundle install`.

Create a migration file to add meta fields for your model (in this case I am using my Post model).

{% highlight ruby %}
rails g migration AddMetaFieldsToPosts
{% endhighlight %}

You may want to add 'title', if you would like to have different title in your meta data or if you have not already defined 'title' in Posts table. You may find complete list of attributes here, feel free to add more/less fields as per your needs.

{% highlight ruby %}
def change
   add_column :posts, :meta_description, :string
   add_column :posts, :keywords, :text
   add_column :posts, :canonical, :string
   add_column :posts, :author, :string
   add_column :posts, :publisher, :string
end
{% endhighlight %}

You can find descriptions for all above added fields in the [Gem's documentation][doc-link] or by doing a quick Google search. Be sure to add all the newly added fields in strong parameters (Rails 4 :-))

{% highlight ruby %}
params.require(:post).permit(:title, :description, :body, :user_id, :status, :minutes_to_read, :tag_list, :meta_description, :keywords,:canonical, :author, :publisher)
{% endhighlight %}

Add the new added fields to the Post's form and... Voila! We are done with setting up our Add/Edit/Update. Now comes the main part, showing meta information for each post in views. 

For that to happen, let's first set all the meta tags using meta-tags' predefined method `set_meta_tags`, which would look something like this: 

{% highlight ruby %}
def show # assuming you have show.html.erb for rendering post
@post = Post.find(params[:id])
set_meta_tags(title: @post.title,
                     description: @post.meta_description,
                     keywords: @post.keywords,
                     canonical: @post.canonical,
                     author: @post.author,
                     publisher: @post.publisher)
end
{% endhighlight %}

Now we need to show these meta tags in the head section of our page. But the `<head>` section of our views renders in application.html.erb. Hmm? How are we going to get this to work? Not to worry ;-)

Go to your application.html.erb, and in the `<head>` section add

{% highlight ruby %}
<% if content_for?(:head) %>
    <%= yield(:head) %>
<% else %>
    <title>D Agarwal</title>
<% end %>
{% endhighlight %} 

In the else section, you may write all the default tags, you want to add to other pages. 

Now in Views for post , we write content for `<head>` as follows:

{% highlight ruby %}
<% content_for :head do %>
     <%= display_meta_tags %>
<% end %>
{% endhighlight %}

where `display_meta_tags` is meta-tags gem's method to display meta tags. 

Voila! We just implemented our blogging site with dynamic meta-tags loading. 

[gem-link]: https://github.com/kpumuk/meta-tags
[doc-link]: https://github.com/kpumuk/meta-tags