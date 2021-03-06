# PostgreSQL Workshop

This workshop is designed to build your confidence in querying data using SQL. We will work through some examples as a group before you tackle the challenges in pairs.

## Set up

We will be working with the dataset in the `data.sql` file. This file contains a set of SQL commands that will create a set of tables and fill them with data. We will connect to the PostgreSQL server running locally on our individual computers and tell it to run the file.

Make sure that you have correctly installed PostgreSQL according to [these instructions](https://github.com/dwyl/learn-postgresql). Check that you can connect to your locally-running database by running `psql` from the command line.

If you run into problems, on a Mac using Postgres.app check that you can see a little elephant in the menu bar. On Ubuntu, run `sudo service postgresql restart` and try to connect again.

## Loading the file

Please download the file and navigate in the Terminal to its location.

Now run the command `psql --file=data.sql` in a new Terminal window/tab.

If it doesn't work try `psql -f data.sql`. If it still doesn't work then holler.

This will connect to your PostgreSQL server and run all of the SQL in `data.sql`, setting up our database for us.

## psql

We mentioned above that PostgreSQL using a server-client model. Currently we're running both on the same machine but if we wanted to we could have the server running on a different computer and connect to it via the client. We will cover this soon.

Now that we're set up, we can connect to our newly-created database by running `psql` (if it gives an 'access denied' error, try `psql -U [your-user-name]`).

Slightly confusingly, `psql` has its own set of commands that are entirely different from SQL. You can identify them because they start with a backwards slash (\) and **don't** end in a semicolon.

Once you are in `psql` try some of the following commands:

`\d` - list all tables (know as 'relations' in psql)

`\d [table name]` - give information on a given table

`\l` - list all databases

## Syntax hints

Before we jump into the challenges, here are a few syntax points to be aware of:

Don't forget to use semicolons at the end of SQL commands. If you hit enter and you just get empty lines this is probably what you're missing.

In PostgreSQL words in double quotes mean identifiers like the names of tables and columns. Single quotes are used for values. If you do something like:

`SELECT * FROM authors WHERE first_name = "Sharon"`

You'll get an error because PostgreSQL thinks "Sharon" is the name of a column. Use single quotes so that PostgreSQL knows it's a value. You can optionally put double quotes around `authors` and `first_name`, but single quotes won't work (because they are the names of identifiers within our database).

Note that a single equals is used for equality testing, not assignment.

SQL keywords like `SELECT`, `WHERE` etc can be in upper or lower case. The convention is upper case to distinguish them from identifiers and values but PostgreSQL will understand either way.

SQL is pretty flexible with whitespace so you can spread your statements out on to as many lines as you want. Keeping things aligned can help make big statements easier to read. Just remember to end with a semicolon!

## Schema diagrams

Here are the schema diagrams to help:

### Authors
Column | Type | Modifiers
--- | --- | ---
id | integer | not null default
first_name | character varying(100) | not null
surname | character varying(100) | not null
location | character varying(100) |

### Books

Column | Type | Modifiers
--- | --- | ---
id | integer | not null default
name | character varying(100) | not null
release_date | date | not null
publisher_id | integer | foreign key (publishers.id)

### Publishers

Column | Type | Modifiers
--- | --- | ---
id | integer | not null default
name | character varying(100) | not null

### Book Authors

Column | Type | Modifiers
--- | --- | ---
book_id | integer | foreign key (books.id)
author_id | integer | foreign key (authors.id)


## The challenges

We will work through a couple of challenges as a group before you split into pairs and work through the others. Once everyone's done the introductory ones we will do a couple of harder ones together before working in pairs again.

Please don't feel that you have to get through all of them or be able to answer them all right away! The idea is to introduce you to the kind of queries we do regularly with SQL.

### Introductory

These challenges cover the basics of SQL: selects, joins and conditions.

* Find the first name and surname of every author.

* Sort everyone by surname and find the first three.

* Find everyone who is not in Nazareth.

* Find everyone who has a location specified.

* Find everyone with 'Wistle' in their surname (bonus points for case insensitivity).

* Find the name of the publisher who released 'Python Made Easy'.

* Find all the books published by 'No Starch Press'.

* Show a list of every book and their authors (one row per author).

* Find all the languages that Ted Burns authored.

### Intermediate

These slightly trickier challenges will require you to use [aggregate functions](https://www.tutorialspoint.com/PostgreSQLql/PostgreSQLql_useful_functions.htm) and/or [subqueries](http://www.PostgreSQLqltutorial.com/PostgreSQLql-subquery/)

* Find everyone who wrote at least three books.

* Order the publishers by the number of books they have published.

* Find all books released after 1st Jan 1996, ordered by the number of people who wrote them.

* What's the highest number of authors per book? The lowest?

### Hard

Doing these is not required! Only look at these if you have time at the end.

* What's the average number of authors per book?

* Show every author who has only written for one publisher.

* Which location has the higher figure for books per author?

* Let's say you are the first developer at a new start up called 'Amazonia'. Your boss asks you to modify the database so that customers can add books to their shopping carts. What tables and associations would you need?
