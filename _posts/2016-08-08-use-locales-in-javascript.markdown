---
layout: post
title:  "Use Rails Locales in Javascript"
date:   2016-08-08 10:18:00
comments: true
desc: "How to use rails locales in javascript"
keywords: rails, locales, javascript
categories: rails javascipt
---

In this blog, I will explain how to use locales (like en.yml or nl.yml etc) in your javascript code. We will be using this awesome gem called [i18n-js][gem_link]

Below are the step you can follow to use locales in your javascript code:

- Add `i18n-js` to your gemfile.

`gem "i18n-js"`

- Add available locales to your `application.rb`

`I18n.available_locales = [:nl, :en] // or any other you have.`

- Add middleware to your `application.rb`

`config.middleware.use SimplesIdeias::I18n::Middleware`

- In your `application.html.erb`

```ruby
<%= javascript_include_tag "i18n" %>
  <%= javascript_include_tag "translations" %>
  <%= javascript_tag do %>
    I18n.defaultLocale = "<%= I18n.default_locale %>";
    I18n.locale = "<%= I18n.locale %>";
<% end %>
```
or if you are using `application.js`, then

`//= require i18n/translations`

- In your `assets.rb`

`Rails.application.config.assets.precompile += %w( i18n.js )`

That's it. Now you an restart your server and it will create `translations.js` file at `/public/javascript` folder.

Now you can use internationalization in your javascript codes as follows:

```ruby
var text = I18n.t('string.anything_you_defined');
```

**Some tips and techniques:**

- When you update your locales, then you need to run following commands in order to make translations work in js.

```ruby
rake i18n:js:setup
rake i18n:js:export
```

[gem_link]: https://github.com/fnando/i18n-js
