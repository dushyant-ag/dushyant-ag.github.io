---
layout: post
title:  "Query to get recent rows in each group in relational database"
date:   2016-07-26 10:18:00
comments: true
desc: "Query to get recent rows in each group in relational database like mysql, postgres etc."
keywords: ruby, rails, mysql, postgres, groupby, query
category: database
---

There has been many times, when we want to show the latest rows from table group by different user or by company etc. 

For ex: We have `comments` table as follows:

 id   | user_id   | comment 
 --- | --- | ---
1 | 2 | This is test comment  
2 | 2 | This is test comment  
3 | 2 | This is test comment  
4 | 3 | This is test comment  
5 | 3 | This is test comment  
6 | 4 | This is test comment  
7 | 5 | This is test comment  
8 | 5 | This is test comment  
9 | 5 | This is test comment  

Now how would you articulate your query if you want to have result as shown below: 

 id   | user_id   | comment 
 --- | --- | ---
3 | 2 | This is test comment  
5 | 3 | This is test comment  
6 | 4 | This is test comment  
9 | 5 | This is test comment  

Wondering ?? 

Well, if you do something like 

```ruby
SELECT * FROM comments GROUP BY user_id
```

then, it will get the first record, not the last one. 

Here is the query, which will get the desired results: 

```ruby
SELECT c1.*
FROM comments c1 LEFT JOIN comments c2
 ON (c1.user_id = c2.user_id AND c1.id < c2.id)
WHERE c2.id IS NULL;
```

Voila!
