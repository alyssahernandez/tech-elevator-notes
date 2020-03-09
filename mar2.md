# Database & Java

## Key Terms

The following clients dictate how these other things can interact with the database.

*ODBC:* open database connection. you can connect java, sql, etc.

*JDBC:* java database connectivity. API that allows java, specifically, to connect to your resources.

*DBVisualizer:* give you a connection to your database and allow you to send sql scripts to it.

*your own code:* has rules for how people can interact with the data

*DAO:* we instantiate objects for every row. we define a container for our stuff and read the data from the database to create instances of these rows as a class.

*CRUD:* create, read, update, delete. in order to do this, we need an interface.

With our previous Java files, once we closed the application, our user data would be lost. Databases allow you to keep that data permanent in a persistent, automatic manner. If you want to write an application that has any meaningful permanence around it, you need to use a database. A text file can store data, but it has no rules about data types and it's not secure at all; you can't enforce your contracts.

