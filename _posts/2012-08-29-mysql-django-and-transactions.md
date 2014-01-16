---
layout: post
title: MySql, Django and Transactions
description: Learning about Mysql's quirks the hard way
tags: [mysql, continuous integration, django, python, database]
---
{% include JB/setup %}
This week in my day job I've been working with Django, and our database interactions reached a certain level of complexity.
I'll explain the situation I found myself in, how I got there (ie why it was necessary), and what I had to learn to get out of it.
None of this information was in one single place on the internet, so bringing it all together, and adding in my personal experience to flavour it seems like a worthwhile thing to do.

# Too Long/Didn't read version
## For those pressed for time

* Complicated concurrent database usage may require transactions to ensure consistency
* The default storage engine for mysql- MyISAM does not support trnasactions - fast and light, not feature full
* The storage engine can be switched on a table basis to InnoDB - but all tables involved in an operation must do so for Django to use transactions
* Switching the table engine will dump all the data out tables and reload them - beware - there is a moment when no data is in the table, and this will change the insertion order if that was important.
* When you switch to InnoDB, the query retrieval system has a couple of modes - the default is one that means the first query results retrieved in a session without a transaction committed will always be returned - and polling will never get data changes.
* To ensure you get the data you want out, you need the READ COMMITTED transaction isolation level - set this globally
* You'll need existing client sessions to be kicked out and start again for these changes to take effect properly.

# Why Django and transactions?

My situation is that I am on a team running a busy installation of servers using a combination of bash and python scripts to manage large amounts of build, testing and integration tasks.

We have a collection of odd embedded hardware, that needs tests run on it with different software, and different combinations of other stuff, and this eventually led to needing a method of knowing which hardware was already in use, what the state of the hardware is, what it supported, if it was broken and other state information about it.

This database grew with some design, and some organic growth as features were added. As the system became critical to some company operations, we needed more testing of our infrastructure and test libraries, and we started to need a management system. This is where django came in. It's admin was an easy way to start managing the database, with authentication and so on. We then started using it's ORM (Object Relational Model) to map the database into objects with a managed database connection, all over the project, outside of Django (possible, but has it's own implications - including for testing and so on).

This now meant that we had an admin interface, and many scripts/apps accessing the database at any given time. At that point we needed to put some kind of locking in for some of the data tables to ensure that the data wasn't getting into inconsistent states between the different processes. We aren't talking a few, but hundreds of them. There are hundreds of devices under test, and many post-test analysis systems running after those, long after the hardware has been given to something else.

Recently the game was upped. We started to need ways to queue our hardware requirements, the hardware requirements became more complex and combinatorial. We needed a way for a queue to run, to try and get all the hardware needed for a test, or wait until it could allowing other tests with simpler requirements to get in there. It needed to be sure that the request would be satisfiable in ideal conditions. It also needed to coexist with other systems, and needed to be absolutely sure the same hardware didn't go out to two different systems.

After looking at the system, and the way to get it to do this, a transaction system where requests are partially fulfilled until they can be completed, or rolled back until a later attempt was needed. Transactions turned out to be more interesting than I first thought.

# Adding transactions into the Django apps
## What looked like it may work

So my testing was a bit underpowered. The queue system had a service process, run as a Django manage command. The Unit testing of this tried different single requests. Those who know django will know that you can chose for unit tests to run on a fast in memory sqlite database. With no other processes involved, transactions wont mean anything (sqlite doesn't implement them as far as I know), and there is no possibility of data inconsistency.

I used a mock system to verify that the transaction calls were being made. This looked like it was working, and I unleashed it to replace the older system. As I did - chaos - half serviced requests were leaving hardware booked all over, I had to quickly turn it off, and figure out what went wrong.

At this point - I questioned if the django API worked the way I thought it did.

Django has in its DB package a transactions module. This has a couple of context handlers (I'll explain those below).
transaction.commit_manually - the code in here must manually commit or rollback any changes before the end of the handler, otherwise an exception will be thrown (regardless of database engine support)
transaction.commit_on_success - at the end of the code inside this context, the transaction will be commited, unless either an exception was thrown, or the transactions were rolled back explicitly. I used this method - it is the least hassle, and is perfect for my inner loop of grabbing hardware until it could no longer satisfy, or had fully satisfied the request.

There are probably other context methods, but I didn't investigate them.
I initially was returning from the context handler, with the explicit rollback, when a requirement couldn't be satisfied. This looked right, but the hardware bookings were going into the live database.

At this point, Django's manage.py shell command, a python interactive shell prooved yet again to be handy. I starting manually trying operations in there, using the context manager above. I had to prove to myself that during the transaction, the data was not yet in the database. And then I found that it was. Disaster - something was silently failing to do transactions. No exceptions, or errors to tell me it was wrong, but no transactions either.

# A mysql interlude
## I had to learn about mysql's table engines, and fast

At this point - I shut down my queue processor completely before it could do any more harm, and went to understanding (using that command line mentioned above) why it wouldn't behave the way it looked like it should. I wasn't able to find out which of django or mysql was silently not doing stuff, but django allows those transaction commands to run on sqlite, a db which definitely didn't do transactions, without errors in the test scenario - although they did nothing.

Why did they do nothing on mysql - I'd prove this. I started reading about table models - reading about mysql transactions, with an inkling about table engines at the back of my brain, I quickly came to the truth.

The default table engine in mysql is MyIsam - a quick, low storage table engine. It is suited to web apps - it has little or no relationship handling, full text search indexing table locking (no row locking) and *no transaction support*. The row locking would have been suitable for us somewhere, although the Django ORM only partially supports that (with the select_for_update query modifier).

On a tangential note this is also when I found that the default characterset and collation for mysql is latin1 Swedish too - because the mysql devs are Swedish.

So the setup was suited to a webapp, but our webapp was only the admin, the database was other used for plenty of concurrent processes and needed better integrity. Our DB wasn't doing any transactions because the table engine we had, a default which we'd not thought of until this point, didn't support them.

There are other table engines in MySQL. The important one for our task was InnoDB. The InnoDB storage engine supports row locking, proper relationships (foreign keys) and importantly *transactions*. It has a little more storage and IO overhead.


Seeing that this was the solution, I used phpmyadmin (awesome web tool for modifying/inspecting mysql databases) to switch tables in our db to InnoDB. Trying stuff in django led me to think that I probably needed all tables in a query to support transactions before Django would use them. So I switched many of the tables (incidentally switching their collation to utf8 general).

Disaster! This was a bit of a mistake - and should have been done on a test database, or during quiet hours. I said that this was a busy installation, and the database holds live bookings. Do not switch table engines on live databases! I did and...

Switching engines works by dumping out all the data in the table, truncating the table (dropping all its rows), and then loading it back in. This had a critical effect - a load of our tests dropped out the moment I did one of the tables, as they found the hardware they were checking against in the database (to make sure we didn't want it released immediately) no longer existed there. These tests were all rendered invalid. Ouch.

There was another side effect - the reloading of data meant that the insertion order was different. I'd not realised that some scripts in our system depended on insertion order (IMHO they should always order based on an index and never insertion order), and this caused their results to come out in an odd way.

The damage was done, and couldn't be undone. But I'd learned a fair bit at this point. The story doesn't end yet.

# Queries, but not as we know them
## The same stale data...

I verified at this point that transactions were taking place. Only something odd was happening - some queries were not updating based on updates elsewhere. I was able to verify in phpmyadmin that stuff was changing, but that some sessions were not getting fresh data. What was going on here?

First I looked to see if Django was doing some kind of odd caching- but why would it suddenly turn on with InnoDB?

Then I found out about something related to the table engines, and transactions - a transaction model/mode. To keep data integrity at different levels, there are a number of these modes, that can be set per session, or globally (unless overridden locally). The current mode was "REPEATABLE READ". This deadly setting meant that nothing that was polling data would work. What it means is that the data queried at the start of the session, will be the same data it gets, unless it issues a transaction and commits that. Most of the clients processes only read from the database (their output is generally Jenkins logs and artifacts). I was then able to see a whole bunch of processes were stuck - with bits they were polling (waiting for hardware to be unlocked) never changing for them because of this "REPEATABLE READ" setting.

I read about this, and it's alternatives [SET TRANSACTION Syntax](http://dev.mysql.com/doc/refman/5.0/en/set-transaction.html) and decided that we needed the READ COMMITTED setting, and globally. I modified the current global setting, and the server settings (in my.cnf) to ensure that this would be the case on subsequent restarts. Note that existing sessions are unaffected. Which meant I had to basically kill those things stuck in polling loops.

This got things flowing and unstuck - some stuff had waited 9 hours for its data to change - we spotted them throughout the day. At this point - I definitely had provably working transactions - which was my goal. I now turned my service back on.

# About the writer

I develop, maintaining and support infrastructure on a clients CI (continuous integration) system and continuous delivery system, designed to give the project it is used with the confidence to make changes and add features fearlessly.

I have two children - a girl and a boy, and we live in Richmond-upon-Thames, Uk. In my spare time I build stuff, grow stuff, read stuff and like to write about it. I like to philosophise, research and learn, and then go the next step and apply, do and build. I love reading How-to's and will experiment with things to see what else I can learn.
