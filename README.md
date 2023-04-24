# Spring data JPA
Persist database. like MYSQL that is free, scalable and popular.

### Spring data JPA is the JPA based version of data repository access of the spring data family. 

## What is JPA?
* **Spring data** has many implementations for varios data storing:
    * MongoDB, Redis, Cassandra, GemFile, CouchBase, Neo4J
* **Sping data JPA** - is an abstraction layer built on top of JPA.
* **JPA** - Java Persistent API.
* JPA is a common API for working with relational databases.
* **Hibernate** is an impl of JPA (JPA= is an *interface*, and not impl)
* Other impls are TopLink, Apache OpenJPA, EclipseLink.

## What is Hibernate?
Hiberante is a **Object Relational Mapping (ORM)** Tool which is also implements the JPA API.

**Java** => Object Oriented Programming Language.

**SQL** => Persist data using relational data model.

## What is SQL?
* __Hibernate__ performs db operations using SQL.
* __SQL__ - Structured Query Language.

## What is JDBC?
* **JDBC** - Java DB Connectivity.
* JDBC is the Java API (interface) for connecting to db.
* JDBC implementaion is known as _JDBC Driver_.
* Each DB will have it's own JDBC Driver implementations.
* JDBC Driver handles the low level communications with db.

![Putting it all together](/assets/JPA.png)