---
layout: post
title:  "Implement Markdown with Rails4 app"
date:   2016-04-04 10:18:00
categories: rails4 markdown coderay
---

Markdown is popular tool to convert text to HTML. 
In this blog we will learn how to integrate Markdown in our rails 4 app using `redcarpet` and `coderay` gems. 

Little bit about the two gems: 

**RedCarpet-** Redcarpet is a Ruby library for Markdown processing. The core of the Redcarpet library is the Redcarpet::Markdown class. Each instance of the class is attached to a Renderer object; the Markdown class performs parsing of a document and uses the attached renderer to generate output.

**CodeRay-** CodeRay is a Ruby library for syntax highlighting.You put your code in, and you get it back colored; Keywords, strings, floats, comments - all in different colors. And with line numbers.

Let's dive straight to the implementation:

Add following gems to your gemfile:

{% highlight ruby %}
gem 'redcarpet'
gem 'coderay'
{% endhighlight %}

then, `bundle install`

Now in your `application_helper.rb`, lets define a helper method to covert text to HTML and simultaneously have syntax highlighting integrated.

{% highlight ruby %}
class CodeRayify < Redcarpet::Render::HTML
  def block_code(code, language)
    CodeRay.scan(code, language).div
  end
end

def markdown(text)
  coderayified = CodeRayify.new(filter_html: true,  hard_wrap: true)
  options = {
    :fenced_code_blocks => true,
    :no_intra_emphasis => true,
    :autolink => true,
    :strikethrough => true,
    :lax_html_blocks => true,
    :superscript => true
  }
  markdown_to_html = Redcarpet::Markdown.new(coderayified, options)
  markdown_to_html.render(text).html_safe
end
{% endhighlight %}

Now wherever you need to convert text to HTML, you can simply pass that text into a method named 'markdown' as show below

{% highlight ruby %}
markdown(@post.body)
{% endhighlight %}

ALright! That's it! We are done implementing markdown format for our rails app. The blog post is classic example of redcarpet + coderay.

Few tips/tricks: 

If you want to have line numbers with your code blocks. 
use `CodeRay.scan(code, language).div(line_numbers: :inline)` OR `CodeRay.scan(code, language).div(line_numbers: :table)`

If you don't want CodeRay to autodetect code, then, remove `filter_html: true` from CodeRayify object. So it becomes, `CodeRayify.new(hard_wrap: true)`

Possible use of this is when you want to use write direct html in your content, as sometimes it might be required. 

This blog post is highly inspired by this [post][blog-link] and most of the code is re-written.

[blog-link]: http://allfuzzy.tumblr.com/post/27314404412/markdown-and-code-syntax-highlighting-in-ruby-on