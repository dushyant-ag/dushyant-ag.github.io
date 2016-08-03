---
layout: post
title:  "Ruby Length Size Count Dilemma"
date:   2016-07-14 10:18:00
comments: true
desc: "When to use ruby Length Size Count and how it varies in active record"
keywords: ruby, length, size, count, rails, active record
categories: ruby active-record
---

There has been many times when we have multiple options to achieve something. One of them is using ruby's length, count and size. Which one to use when ? 

In Ruby, arrays and hashes, `size` is an alias for `length`. They can be called as synonyms and do exactly the same thing. Whereas `count` is also same if no element is there, but if it is there, then it returns the number of items it matches.

Ex: 

```ruby
> [1,2,3].count{|z| z < 2 }
=> 1
```
So basically all are same in terms of result, but they differ in performance. 
`size` and `length` as I have mentioned are exactly same (i.e. same performance). However `count` without element takes more time to execute than length. 

Above was all about Ruby, but it has all together  different when it comes to active record. Lets dive right into it:

TLDR: Use `size`.

`length`: It will force load all the data and then perform length operation. 

```ruby
>> user.tasks.length
  Task Load (0.720687)   SELECT * FROM tasks WHERE (tasks.user_id = 2343) 
=> 216
```
This is bad. We do not want to load all data into memory to get the no. of items.

---

`count`: It will query the database with count.

```ruby
>> user.tasks.count
  SQL (0.070607)   SELECT count(*) FROM tasks WHERE (tasks.user_id = 2343) 
=> 216
```
Nice. We get what we want, without loading all data.

---

`size`: This is will give the no. of tasks without a query if the tasks are already loaded, or else perform the count database query.

```ruby
>> user.tasks.size
  SQL (0.070607)   SELECT count(*) FROM tasks WHERE (tasks.user_id = 2343) 
=> 216

>> tasks = user.tasks
>> tasks.size
=> 216
```
Awesome. It is smart. It detects when to do what. Use `size`.

