---
title: better search for windows
date: 2021-01-20
tags: ["windows", "search", "Python", "SQL", "tinydb"]
---
The Windows 10 search is _slow_ and resource intensive.  So I decided to build a new one!  

The new search engine uses a flask-sqlite backend, using a jinja html front end.  

It first indexes both of the drives and parses their files into the databases in a custom format  

Then the front-end does a SQL query on the database to find the files. After that the custom jinja templates do a HTML "render" with the data from the query and send it to you!  

An interesting feature is the "open" function that executes a "start" command on the host machine, which then open the files.