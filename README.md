# Spring data JPA
Persist database. like MYSQL that is free, scalable and popular.

### Spring data JPA is the JPA based version of data repository access of the spring data family. 

## 1. What is JPA?
* **Spring data** has many implementations for varios data storing:
    * MongoDB, Redis, Cassandra, GemFile, CouchBase, Neo4J
* **Sping data JPA** - is an abstraction layer built on top of JPA.
* **JPA** - Java Persistent API.
* JPA is a common API for working with relational databases.
* **Hibernate** is an impl of JPA (JPA= is an *interface*, and not impl)
* Other impls are TopLink, Apache OpenJPA, EclipseLink.

## 2. What is Hibernate?
Hiberante is a **Object Relational Mapping (ORM)** Tool which is also implements the JPA API.

**Java** => Object Oriented Programming Language.

**SQL** => Persist data using relational data model.

## 3.What is SQL?
* __Hibernate__ performs db operations using SQL.
* __SQL__ - Structured Query Language.

## 4. What is JDBC?
* **JDBC** - Java DB Connectivity.
* JDBC is the Java API (interface) for connecting to db.
* JDBC implementaion is known as _JDBC Driver_.
* Each DB will have it's own JDBC Driver implementations.
* JDBC Driver handles the low level communications with db.

![Putting it all together](/assets/JPA.PNG)

## 5. Initialize a project
* Add these dependencies: spring web, spring data JPA, h2 db.

### Domain
* Create new package named "domain".
* In domain you have entity files. 
* Entity files start with **@Entity** annotaion.
* Entity class also has id variable, that has **@Id** annotation.
* Id variable can have **@GeneratedValue(strategy = GenerationType.AUTO)** that describe how to generate id value. 
    * AUTO => Db handle value generation.
    * TABLE
    * SEQUENCE
    * IDENTITY,
    * UUID
```
@Entity
public class Book {
    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    private Long id;
    private String title;
    private String isbn;
    private String publisher;
    .... // setter and getter and constructors
}
```
* We can Override hashCode and equal methods to customize equalization conditions, and hashcode.
```
@Override
public boolean equals(Object o) {
    if (this == o) return true;
    if (o == null || getClass() != o.getClass()) return false;

    Book book = (Book) o;

    return Objects.equals(id, book.id);
}

@Override
public int hashCode() {
    return id != null ? id.hashCode() : 0;
}
```

### Repository
You should make repository interface that handles all database using queries. This class should extend from JpaRepo.
```
public interface BookRepositories extends JpaRepository<Book, Long> {
    
}
```

### BootStrap
> If you want to run method exactly after runing application, put that method in class with annotaion of **@Component** and this class should implements **CommandLineRunner**. Write that method on *run* method.

```
@Component
public class DomainInitializer implements CommandLineRunner {
    private final BookRepositories bookRepositories;

    public DomainInitializer(BookRepositories bookRepositories) {
        this.bookRepositories = bookRepositories;
    }

    @Override
    public void run(String... args) throws Exception {
        Book bookDDD = new Book("domain driven design", "123", "RandomHouse");
        System.out.println("Id: "+ bookDDD.getId());
        Book savedDDD = bookRepositories.save(bookDDD);
        System.out.println("Id: "+ savedDDD.getId());

        Book bookSIA = new Book("Spring in action", "12332", "Oriely");
        Book savedSIA = bookRepositories.save(bookSIA);

        bookRepositories.findAll().forEach(book -> {
            System.out.println("book id: "+ book.getId());
            System.out.println("book title: "+ book.getTitle());
        });

    }
}
```
> As you've seen we didn't do any setup for database and sql and hibernate. Spring data JPA do all those things for us.


