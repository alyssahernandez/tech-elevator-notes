# Keys, Joins & Unions

## Keys

*Keys:* unique identifiers for each row. There are two kinds:
- Naturally occuring: such as a SSN
  - has meaning to that row
  - means something in the real world
- Surrogate keys: which is something we create
  - also called an identity column
  - typically an integer
  - doesn't appear in the real world

*Primary key (PK):* provides a unique identifier for every row in the table. It makes them unique and identifiable. Other keys may be shared, such as gender or user ID.

*Foreign key (FK):* This is a key that links to a primary key in another table.

You may be wondering how, if in a table, there are two columns that seem to contain primary keys, first, see what the table is actually for. If it's for purchases, the PK is probably the purchase order, even if it contains a seemingly unique column of credit card numbers, it's possible for two users to use the same card. Order numbers cannot be duplicates.

*****Referential integrity*****

## Relationships Between Tables

Let's say, in another table, we have purchases. Every purchase is unique. Maybe it has a specific timestamp or the type of payment method. But it also has a user attached to it. Maybe purchase 5 of the day belongs to Jane Doe. Jane Doe is linked to a user in the user table.

*Crowfoot notation:* shows that individual X can relate to many Ys.

*Cardinality:* the maximum number of times a unique row is related to another entity.

*Ordinality:* the minimum number of times a unique row is related to another entity.
- it's possible for this to be zero, meaning that they share nothing in common.

*Many to many:* multiple users can have the same address, and multiple addresses may belong to the same user.

## Joins

The `FROM` is defining the relationship; the tables we're pulling. The `JOIN` is defining the overlap. The `SELECT` is selecting which attributes we're interested in.

If we had to find a way to combine users with shipping addresses, we would need to look at the intersection between them (think of venn diagrams). We need to show where those two identities are related to each other. We have a venn diagram 

*Left join:* for every object on the left, we're looking for objects on the right to relate for it.
- another type of left join: select A where B is null

Let's say we only want users in PA who do not have a shipping address. A (users) is not null, but B is null for those users.

*Right joins:* for every object on the right, we're looking for objects on the left that relate to it.
- another type of right join: select B where A is null

Let's say we have a list of addresses and we want a list of all shipping addresses that are not related to any users. That would be where A is null and B has values.

What if instead of listing all users and their shipping addresses, we just wanted to list one particular user's shipping addresses? All we want to know is where the two tables *interjoin.*

*Interjoin:* I want the table/rows *only* where those two tables intersect. On a left join, I would see all users and their associated shipping addresses.

*Outerjoin:* A does not have any relations to B.

*Full outerjoin:* we want *everything.*

*Cross join:* joining two datasets that are not related at all, but we want to pull data from each of them; these are exceedingly rare.

### Venn Diagram; Users Left, Addresses Right

**INNER JOIN:** we're looking at the middle. the user table has user IDs, which are unique. the address table has a list of addresses, some of which have the same user ID listed because some users have multiple addresses. the common link between the two tables is the user ID.

Let's say we have Joe with two addresses and Patty with one:

```sql
SELECT
    u.user_id, ADD(a.address)
FROM 
    users AS u
    INNER JOIN address as a
        ON a.user_id = a.user_id
WHERE
    a.address IS NOT NULL
```

The above would return:
- 1 | 2
- 2 | 1

But what if there is user 3 and user 4 with no shipping addresses yet? An INNER JOIN will only return 2 rows, excluding the two users, because we're looking where there is an overlap. That is where a *lEFT* join comes in:

```sql
SELECT
    u.user_id, a.address
FROM
    users AS u
    LEFT JOIN address AS a
        ON a.user_id = u.user_id;
```

Here, we're pulling all of the users from the left side, meaning we're returning all of the them, regardless of whether they have an address or not. A LEFT JOIN would return five user rows, where user 1 has two because there are two addresses listed. User 4 and user 5 would have null values. You *could* specify IS NOT NULL, but then it's just behaving like an INNER JOIN.

Let's say you want to *only* want to grab the users with *no* addresses. That's also a LEFT JOIN. You would do:

```sql
SELECT
    u.user_id
FROM
    users AS u
    LEFT JOIN address AS a
        ON a.user_id = u.user_id
WHERE
    a.address IS NULL;
```

The above would only return user 3 and 4 because they have null addresses.

UNIONS return the results of two separate select statements.

***Cardinality vs ordinality on hw #15?***