---
layout: post
title:  "Download and Setup Heroku Database Backup"
date:   2016-08-03 10:18:00
comments: true
desc: "How to download and setup heroku database backup locally"
keywords: heroku, backup, postgres
categories: heroku backups
---

Here are the steps to download and setup the database locally:

- Make sure you are in project directory `path/to/project `
- Get the latest database backup url from heroku using below command:
`heroku pg:backups public-url`
- Copy the url and paste it into the browser and hit Enter. This will download the file (which
is encrypted).
- Rename the downloaded file to something more appropriate (Ex: latest.dump). Note the
extension being “.dump”.
- Create a new postgres database (Ex: latest_database) sorry for the weird name, I just
couldn't think of anything better. LOL
- Run this command to restore

```ruby
pg_restore --verbose --clean --no-acl --no-owner -h localhost -U your_username -d your_database_name path/to/latest.dump
```

P.S. You can check the status of backups at any point of time by running this command: `heroku pg:backups`