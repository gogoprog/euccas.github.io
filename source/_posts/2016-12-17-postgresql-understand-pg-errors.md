---
layout: post
title: "PostgreSQL: Understand PG Errors"
date: 2016-12-17 09:06:21 -0800
comments: true
categories: Database PostgreSQL Ruby
---

When using Ruby Gem ```pg``` and establish database connections to a PostgreSQL database, you'll see PG errors when the database connection becomes problematic. In my experience, two typical PG errors are ```PG::AdminShutdown``` and ```PG::UnableToSend```.

# Error PG::AdminShutdown

The error message contains the following information:

<code>
FATAL:  terminating connection due to administrator command (PG::AdminShutdown) server closed the connection unexpectedly
      This probably means the server terminated abnormally
      before or while processing the request.
</code>

<!--more--> 

The PG::AdminShutdown error could be caused by database server receiving SIGTERM/SIGINT/SIGQUIT or kill command on the connection process. Each system signal shut down server processes in different manners, see the [pgadmin document](https://www.pgadmin.org/docs/1.4/pg/postmaster-shutdown.html) to know the details.

When you hit the PG::AdminShutdown error, you'll like to check if the database server gets restarted and if the server resumes to the normal state.
 
# Error PG::UnabletoSend

The error message looks like:

<code>
server closed the connection unexpectedly (PG::UnableToSend)
This probably means the server terminated abnormally before or while processing the request.
</code>

The PG::UnabletoSend error usually means a connection timeout or network issue. It could be a temporary issue though. You can check if the other connections to the database server work well or not.
