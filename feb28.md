# Data Definition Language & Data Control Language

## Key Terms
- *DCL:* data control language. this is where we control access to the data. which users can access the data? can an individual user read, update or delete the data?
- *DDL:* data definition language. you're defining the tables/types of data.
- *DML:* data manipulation language. you're deleting, updating, changing, etc the table.
- *DQL:*

Tables are entities. Rows can be thought of as unique instances of an entity. 

## Three Steps to Designing/Planning a Database
1) Conceptual model: taking your data and forming the concept of what design would work. maybe your data source is an excel spreadsheet, maybe a physical media or maybe an interview.
2) Logical model: use you can use a design software, such as Visio from Microsoft. most of the time you'll start with a sketch. i'll have a column for this, and maybe i need this information. maybe the purchase history for transactions is actually related to two things. you're drawing the designing and figuring out the layout.
3) Physical model: use DDL (data definition language) to specifically create those objects/entities on your database server. the database becomes real, and you can now start adding data to it using *DML* (data manipulation language).

*Normalization:* structuring a relational database in accordance with a series of so-called normal forms in order to reduce data redundancy and improve data integrity. you're avoiding `A = B, B = C`. somewhere something is replicated. instead, with normalization, you would say `A = B` and that's it. you're minimizing redundancy.

*Denormalization:* no separation of data; you're replicating it in a single row. it's redundant, kind of like `A = B, B = C`.:

`customer_id, customer_first_name_, customer_last_name,`
`phone_number, phone_number2, phone_type, phone_type2`

## Setting Rules for the Tables

```SQL
BEGIN TRANSACTION;

CREATE TABLE art (
    artCodeId serial,
    title varchar(64) not null,
    artistId int not null,

    constraint pk_art primary key (artCodeId),
    constraint fk_art_artists foreign key (artistId) references artists (artistID)
);

CREATE TABLE customer_purchases (
    customerId int not null,
    artCodeId int not null,
    purchaseDate timestamp not null,
    price money not null,

    constraint pk_customer_purchases primary key (customerId, artCodeId, purchaseDate),
    constraint fk_customer_purchases_customer foreign key (customerId) references customers (customerI),odei
    constraint fk_customer_purchases_art foreign key (artCodeId) references art(artCodeId)
);

COMMIT TRANSACTION;
```