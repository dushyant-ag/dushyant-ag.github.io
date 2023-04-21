---
layout: post
title:  "Optimize Views in Rails"
date:   2016-10-25 10:18:00
comments: true
desc: "How to optimize views in rails by removing multiple queries which creates N+1 query problem"
keywords: rails5, optimization, nplus1
category: rails
---

In this blog we will see how to optimize our rails views by removing multiple queries.

There are many times when we have to show associations in the view. **For ex:**

```ruby
class Customer
	has_many: appointments
end
class Appointment
	belongs_to: customer
end
```

Now in the index view of appointments, you want to show customer details (customer name atleast) too. What generally we do:

`@appointments = Appointment.all`

and then in view for each appointment, we get 

`appointment.customer.name`

Now with this, we do database query for each appointment, which seeds to N+1 query problem. 

**How to avoid that ?**

You can make use of `include` and reduce loading problem by great margin.

`Appointment.includes(:customer)`

Now you might be wondering, what if, you want to include nested associations. Well you can achieve that like this:

For all appointments with their respective customer, and customer with their respective address.

`Appointment.includes(customer: :address)`

or (for multiple nested associations)

`Appointment.includes(customer: [:goals, :tips])`

Further, you can find out all the N+1 queries in your project, with this amazing gem [Bullet][gem_link]

Further read: [apidock includes](http://apidock.com/rails/ActiveRecord/QueryMethods/includes)

[gem_link]: https://github.com/flyerhzm/bullet
