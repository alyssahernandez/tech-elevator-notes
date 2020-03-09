# Integration Testing

## Key DAO and JDCBC Concepts

*DAO:* data access object; allows

*Connection pool:* used to reduce the overhead of creating new database connections by keeping references to several open database connections and sharing them.

*Spring JDBC:* a framework that sits on top of the JDBC, which talks to the JDBC drivers, which then talks to the databases.

*JDBC template Class:* this is the thing were you would use `execute` or `update`. It's a Class that executes to SQL.

***A lot of what jr developers will be doing anyway will be just mimicking what other developers do at the company until you get it... Look at the Oracle definitions, hover over the terms in Eclipse, etc.***

## How JUnit Testing Works with SQL

It works very similar to regular JUnit tests. We update a value and retrieve it; and then call it using SELECT to make sure it returns the correct value.

## Advantages vs Disadvantages of Different Database Hosts

### Remotely Hosted Database

#### Advantages

- You can work anywhere; easy access.
- It already exists.
- Production-like environment. Three tiers in the corporate world, one of which is dev (developing copy); subject to the most change. The downside to this is that you might be working with stale data. However, it's still *live* and *real* data.

#### Disadvantages

- The data itself can be unreliable because so many other devs are probably working on it. What you're testing may not always be what you want.
- No test isolation. With our ACID tests in SQL, I(isolation) is extremely important. When we're running our tests on the remote database, maybe someone else is running tests too. Obviously, that can cause a problem.

### Locally Hosted Database (this is what we do!)

#### Advantages

- Isolation; you won't be interrupted by other people and you're in complete control of it.
- Reliable; you know exactly what's in there.

#### Disadvantages

- Security concerns. If you lose your laptop somewhere, there's a huge risk of someone accessing the data.
- Because it's local, you need a SQL server on your machine which can take up a lot of resources.
- You have to have all of the administrative tools involved.

### Embedded/In-Memory Database

#### Advantages

- Fast/lightweight; an example might be txt files on our machines.
- *Very reliable.* It's part of our program package. We don't have to worry about DB connections or servers or anything like that.
- Consistent because the test set is part of the program package, so everyone has access to the types of tests you run.

#### Disadvantages

- Not necessarily comprehensive; you could be missing some info because you designed it all yourself.
- No RDBMS support/features. No server protection, rollbacks, etc because you're technically not using a server.

## Testing the Code

***MAKE SURE YOU TURN AUTO-COMMIT OFF!!!!!!!!!!!!!!!***

*DAO:* a data access object; it's typically a single thing. This is what we use to access our databases.

*DAL:* data access layer. This controls *how* we interact with the database. This contains all of the DAOs.

1) DAL
   1) SELECT: insert dummy data before you test. If you know your selection returns something, insert the data and compare it to what you expect. It's easier to write tests than having to continuously check DBVis.
   2) INSERT: test by searching for/SELECTing the known data you're inserting.
   3) UPDATE: pre-SELECT, UPDATE, test post-SELECT. You can instantiate an object from the `City Class` for example by calling a method. Then you can call another method to return the values and compare them to the `Expected Result` values.  
   4) DELETE: check for the number of rows pre-delete and then check again to make sure it's 0 post-delete. The problem with this is that you're only checking the rows you're trying to delete, so you could accidentally delete *all* of the rows and not know it. Make sure you're checking the *total* number of rows!

## Setting Up Testing File

```java
public Class {
    private static final String TEST_COUNTRY = 'XYZ';

    private static SingleConnectionDataSource dataSource;
    private JDCBCityDAO dao;

    @BeforeClass // ensures that this is run no matter what
    // runs automatically
    public static void setupDataSource() {
        dataSource = new SingleConnectionDataSource() {
        dataSource.setURL("jdb:postgresql://localhost:5432/world");
        dataSource.setUsername("postgres");
        dataSource.setPassword("postgres1");
        dataSource.setAutoCommit(false);
        }
    }

    @AfterClass
    public static void closeDataSource() throws SQLException {
        dataSource.destory();
    }
}
```

There's more to it than that ^.

***PRACTICE JAVA DATE FUNCTIONS IN JavaDateExample.java FILE!!!***