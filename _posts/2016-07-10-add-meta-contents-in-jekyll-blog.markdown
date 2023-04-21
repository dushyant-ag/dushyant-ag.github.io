---
layout: post
title:  "Add meta contents in Jekyll blog"
date:   2016-07-10 10:18:00
comments: true
desc: "Add SEO meta contents in Jekyll blog"
keywords: jekyll, meta-tags, seo
category: jekyll
---

In this blog post, we will learn how to add meta content into our Jekyll blog, which will render meta content with respect to each blog post. Awesome, insn't it! 

Well before we get started, lets first understand some basic concepts

* [SEO Optimization giude pdf](http://static.googleusercontent.com/media/www.google.com/en/us/webmasters/docs/search-engine-optimization-starter-guide.pdf)
* [Front Matter](https://jekyllrb.com/docs/frontmatter/)

Alright, now we have basic understanding, lets dive right into the implementation:

In this post, I will be using basic elements of meta contents i.e. `title` `description` and `keywords`. You can add more as you wish. (For ref: Here is a [guide](https://gist.github.com/kevinSuttle/1997924) to all meta tags available.)

For `<title>` we’ll get the value from a Front Matter variable if it is there or else we will use the default:

**Note:** I have changed `{ % % }` to `% %` and `{ { variable} }` to `{ variable }`. Otherwise it will render the respective values.

{% highlight ruby %}
<title>
% if page.title %
	{ page.title }
% else %
	Default Page Title
% endif %
</title>
{% endhighlight %}

Similarly, we can define for `<meta> description` and `<meta> keywords` as follows:

{% highlight ruby %}
% if page.desc %
	<meta name="description" content="{ page.desc }" />
% else %
	<meta name="description" content="I’m a Ruby on Rails developer with a passion for coding and ruby standards." />
% endif %

% if page.keywords %
	<meta name="keywords" content="{ page.keywords }" />
% else %
	<meta name="keywords" content="ruby, ruby on rails, git, vim, web design, development, jekyll, Dushyant Agarwal, dushyant" />
% endif %
{% endhighlight %}

So you are all set to have meta tags for your individual posts, all you need to do now is add these values in each of your post's `front matter` as shown below:

{% highlight ruby %}
---
layout: post
title:  "Add meta contents in Jekyll blog"
desc: "Add SEO meta contents in Jekyll blog"
keywords: jekyll, meta-tags, seo
---
{% endhighlight %}

Hope it helps! :)