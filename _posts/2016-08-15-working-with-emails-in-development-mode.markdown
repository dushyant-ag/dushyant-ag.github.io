---
layout: post
title:  "Working with emails in development mode"
date:   2016-08-15 10:18:00
comments: true
desc: "How to work with emails in development mode in rails"
keywords: rails, emails, development, mailcatcher
category: rails
---

In this blog we will see how to work with emails in development mode!

Its always been a pain to test the emails in development mode. When you have to check the formatting or the correctness etc, you need to send that email and verify which is a cumbersome and time taking process. 

One may argue that the correctness can be checked from development log, but with that we do not know if it is rendering correctly. 

Further what if you want to check whether the email is deliverying or not to the right person, to verfiy that you need to send to real email, which is not a good idea in development mode.

What's the solution, then ?? 

[MailCatcher][gem_link] - It runs a super simple SMTP server which catches any message sent to it to display in a web interface available at `http://localhost:1080`. 
You can also view both the HTML and plain text versions of emails. You can also view/download attachements associated with particular email, which is an icing on the cake. 

Alright, what are we waiting for, lets dive right into it!

- Install the mailcatcher gem

`gem install mailcatcher`

- Now you want to setup the ActionMailer settings in your `config/environments/development.rb` file as follows:

```ruby
config.action_mailer.delivery_method = :smtp
config.action_mailer.smtp_settings = { :address => "localhost", :port => 1025 }
```

- Finally start the mailcatcher 

`mailcatcher`

That's it. Now you can go to `http://127.0.0.1:1080` and check all the emails. Cheers!

[gem_link]: https://mailcatcher.me/