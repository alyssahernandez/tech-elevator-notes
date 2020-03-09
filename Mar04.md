# Data Security, Hashing & Encryption

## More Review

*JdbcTemplate:* is what actually interacts with the datasource.

## SQL Injection

*SQL Injection:* In Java, when you take user input and insert it into your SQL String statement, such as this:

```java
"SELECT to, from, message FROM messages " + 
"WHERE (to='" + username + "' OR from='" + username + "') 
AND message LIKE '%" + search + "%'";
```

You are directly inserting whatever the user input into your statement. That leaves your system very vulnerable to attacks if the user is familiar with SQL statements. In their input, they could type something such as `joe` for their username inputs, :

```java
"SELECT to, from, message FROM messages " +
WHERE (to='joe' OR from='joe') AND " +
"message LIKE '%%' OR 1=1 --%';
```

## Hashing

Remember in Java, values in the *heap* in a `HashMap` have an address that points to something in the stack. The address of the address are hashed. Similarly, it's best to store a user's password as a hash code. When it's saved for the first time, it's stored as a hash, which is then saved in the table. Every time the user inputs their password, it is generated as the same hash code. However, it cannot be reversed; it's a one-way street. Once you generate a hash code from something, you can never convert it back to the original value.

## Encryption

Encryption is similar to hashing--you store values as a random hash code--but it's different because, unlike hashing, you can decrypt/reverse it.

Encryption relies on keys; you want to be able to use the key to retrieve the value. There are such things called Digital Certificates, which contain both a public key and a private key. The public key is what allows you to send your data to a another server and encrypt it before it arrives. Your private key is what allows you to decrypt it when it's on its way back to you.

Note: There are people who can do a digital certificate attack.

There are two formatting options for encryption: AES256 and AES-NI. AES256 is more widely used.

Encrypting is bi-directional. We can take a big ugly blob of text and get our original text value back.

## Models (Representations of Tables in Java)

Models should only have default constructors. The whole point of the DAO//JDBC framework is to manipulate it in regards to the database, so adding parameters to the constructor would instantiate it in an incompatible way.

