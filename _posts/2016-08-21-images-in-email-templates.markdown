---
layout: post
title:  "Include images in email template rails"
date:   2016-08-21 10:18:00
comments: true
desc: "How to include images in email templates including devise in rails"
keywords: rails, emails, assets, devise
category: rails
---

In this blog we will see how to include images in our email templates in rails application. There would be two parts to this:

- General email templates 
- Devise email templates

**Lets see how to tackle them:**

There are lot of ways in which we can include the images in the email template. One of them is giving the static url. However what if you don't have static url, what if you have the required image in your assets folder. No problem, I have got an amazing solution, which just works perfect!

We will include them as an attachment and then use in our email template. 
**Lets see how:**

For general email templates (ideally located at `views/user_mailer/` and model at `mailers/user_mailer.rb`), include attachment for all the methods where you want to include as follows:


`attachments.inline['logo.png'] = File.read("#{Rails.root}/app/assets/images/logo.png")`

This is for general (self defined) email templates, what about devise ? Not to worry, its little bit tricky, but can be done easily. Here is how:

- Create new class called `devise_custom_mailer.rb` (or choose any name you like) at `app/mailers/`

- Add following content

```ruby
class DeviseCustomMailer < Devise::Mailer   
  helper :application # gives access to all helpers defined within `application_helper`.
  include Devise::Controllers::UrlHelpers # Optional. eg. `confirmation_url`
  default template_path: 'devise/mailer' # to make sure that your mailer uses the devise views

  before_filter :add_inline_attachment!

  def add_inline_attachment!
    attachments.inline['logo.png'] = File.read("#{Rails.root}/app/assets/images/logo.png")
  end
end
```

- Now add following line in `devise.rb`

`config.mailer = 'DeviseCustomMailer'`

Alright, we got the attachment ready. Now we need to use them in our templates. 

- In templates, whereever you want to use this logo, add the following:

`<%= image_tag attachments['logo.png'].url, width:"190", height:"155" %>`

You can give the attributes like width, height etc and can give styling too if you like. That's it folks!