# Databases

Databases are all about storing information. 

We are all familiar with storing information in files. We write papers in word processing systems, take notes, keep todo lists, keep track of our finances, write stories or compose gaming adventures in a variety of different file types. If you are particularly organized, you may even use an elaborate hierarchy of directories and subdirectories to store your files, allowing easier retrieval later. 

Now, imagine that your information is more structured than, say, a term paper or the prose of a gaming adventure. For example, imagine keeping track of a book, video game or film collection. For each one that you collect, you wish to track the relevant information, such as the following for tracking a film collection:

* Title
* Director
* Production Company
* Year of release
* Genre
* Format (VHS, DVD, Blu-Ray)
* Run Time
* Star Actors
* Composer
* Rating (1-5)
* Review

You could use a simple text file for this, or maybe even an Excel document to make use of the tabular structure. 

Now, let's assume that you become very passionate about this project and begin keeping track of directors, actors, composers and their information. You would keep track of name, birthdate, death date, awards and a short bio. You could keep each one in additional files, or if you were using Excel, in different worksheets/tabs. 

Then you begin tracking genres, including descriptions, notable examples, years of popularity or origin. This would require additional files or worksheets. 

Now, any time you add a new film to your collection, you can add your entries in the relevant files. You definitely need a new entry in the films file, and if it's by a director you aren't tracking yet, you'll need to add that. Same with actors, composer or if it's from a new genre. 

This process wouldn't be impossible, but it would eventually get tiresome, especially if you are a prolific collector. It also gets easier to make mistakes. For example, you might forget to enter a new composer, or you accidentally duplicate an actor. The more you add, the easier these kinds of mistakes are to make. 

Several things could make this project much more complex:

* You decided to keep track of every film you see, and not just the ones you collect (significantly more data)
* Your friends also want to keep track too, so you can all compare notes and make suggestions (distinguishing different people, their reviews and collections)
* You all decide that you would like to publish your reviews online (must be the data source for a web app)
* You would like to invite anyone to sign up and share their reviews and collections too (tracking users, accounts, passwords and profiles)
* You would like to keep track of statistics, and ask more complex questions from the data source, such as "What are the top-5 horror movies made before 1950 among all users?"

Obviously, doing this with simple text files or even an Excel document would not be feasible. You need a more sophisticated way to store all of this information, and the answer is, of course, a __database__. 

The definition of databases from Wikipedia is:

> A database is an organized collection of data, generally stored and accessed electronically from a computer system.

In other words, a database is a collection of data stored and structured in different database tables. Databases provide the following benefits over using individual files:

* Reduces the chance of duplication of information
* Prevents entering erroneous types of information
* Allows the creation of relationships between tables
* Uses more sophisticated data storage algorithms allowing better performance
* Much easier to share information between many users
* Easier to ask complex questions (or queries) or compile statistics
* Can server as a data store for easier to use "front-end" applications

A complete database management system is referred to as a Database Management System, or __DBMS__. A DBMS consists of the underlying data storage system, a language used for managing the databases and their content, user interfaces for managing the database system, and programming APIs that allow applications to connect to and use the database. 

The primary roles of the DBMS software are:

* Defining database schemas (the structure of the data)
* Inserting, updating and deleting data
* Retrieving data through simple or complex queries
* Administrative tasks such as user management, network connection parameters, performance tuning, backup and restore

### Types of Databases

Databases can be useful on a wide range of devices, ranging from small microcontrollers and embedded devices, to office desktop applications, larger servers and mainframes, all the way up to supercomputers. 

As such, there is a variety in types of databases and their implementations. 

#### Files vs Servers

Smaller databases such as those used on embedded or mobile devices, or even home and office desktops, may be best implemented as single-file databases. They are typically lightweight, require less system resources and store their data all in a single file. This file may be shared with others, stored on SD cards, copied like any other file or even attached to emails. 

There are two approaches to using file based databases. The first is by using a companion interface that allows the creation of user forms, reports and otherwise gives all of the tools needed to use the database. The prime example of this type of database is Microsoft Access, and there are some notable historic examples such as dBase and FoxPro.

The second approach is developing a custom application that opens and works with the database file. This may be done with an Android or iOS app, a Python script, Java graphical interface, Windows app and numerous other means. The most popular example here is SQLite. 

Other examples include:

* UnQLite - a key/value pair database
* Realm - used on mobile devices
* RocksDB - high performance key/value storage, optimized for high speed flash storage

Database servers, on the other hand, run as background services/daemons that also provide network connections. In other words, the application that uses the database need not run on the same system as the database server. The application is configured as a client that will make a network connection to the database server. 

Database servers are used where higher performance and larger data storage is most important. Database servers are capable of handling many simultaneous connections and requests, and use sophisticated storage systems and algorithms that span multiple files, sometimes across many disks in a single storage array, such as RAID or ZFS.

Examples of database servers include:

* MySQL
* MariaDB
* PostGRES
* Microsoft SQL Server
* Oracle Database Server

For this book, we will focus on SQLite and MySQL/MariaDB, as they are both free, open source and industry standards. 

#### Relational (SQL) vs NoSQL

Another way of categorizing databases that is increasingly important is **relational** and **NoSQL** (non-relational). Twenty years or so ago this distinction may have been mostly academic, as the vast majority of databases were relational, but NoSQL has seen a rapid popularity increase. 

The term NoSQL stems from the fact that most relational databases use the SQL language (the primary subject of this book), while non-relational databases use other languages or means of interaction.

NoSQL databases have a wide variety of different data storage schemes, but usually focus on simplicity and speed. This makes them popular for big data systems, and large scale systems that must quickly propagate changes across many different servers.

There are many NoSQL database systems, but two popular implementations are MongoDB and Google's BigTable.

## Authentication and Permissions

Many RDBMS implementations, especially database servers, user authentication and apply strict permissions to database resources. The need for this should be obvious, as databases may contain confidential or crucial information that must not be accessed or modified by those without proper authorization. 

Database servers have accounts that serve as administrator roles, intended only for database server management, such as troubleshooting, creating and modifying other users, applying permissions, creating  or deleting databases, backups, replication, and performance tuning. The administrative account on MySQL/MariaDB is known as 'root'. This root account is not the same as the Unix/Linux root user account, as it is specific to the DBMS. In Microsoft SQL server this account is called 'sa' (server administrator). 

Normal user accounts are typically created for the purposes of building database schema, entering test data, building queries, and as authentication for the client applications that will connect to the database. For example, if you were to build the film database example from earlier, the web application would need to connect to this database. Somewhere in the web app code there will need to be a connection made with a valid username and password for the server. 



## Tables and columns

You've most likely worked with spreadsheet systems like Excel or Google Sheets. At a very basic level, database tables are quite similar to spreadsheets.

Each table has different **columns** which could contain different types of data. Each **row** represents and entry in the table. 

For example, if you have a todo list app, you would have a database, and in your database, you would have different tables storing different information like:

* Users - In the users table, you would have some data for your users like: `username`, `name`, and `active`, for example.
* Tasks - The tasks table would store all of the tasks that you are planning to do. The columns of the tasks table would be for example, `task_name`, `status`, `due_date` and `priority`.

The Users table may look like this:

```
+----+----------+---------------+--------+
| id | username | name          | active |
+----+----------+---------------+--------+
| 1  |    bobby | Bobby Iliev   |   true |
| 2  |    grisi | Greisi I.     |   true |
| 3  |  devdojo | Dev Dojo      |  false |
+----+----------+---------------+--------+
```

Rundown of the table structure:
* We have 4 columns: `id`, `username`, `name` and `active`.
* We also have 3 rows/entries/users.
* The `id` column is a unique identifier of each user and is auto-incremented.

In the next chapter, we will learn how to install MySQL and create our first database.
