---
canonical: "https://clojureforjava.com/9/22/4"
title: "Database Interaction with Clojure: `clojure.java.jdbc` and `next.jdbc`"
description: "Explore database connectivity in Clojure using `clojure.java.jdbc` and `next.jdbc`. Learn about connection management, data querying, and best practices for efficient database operations."
linkTitle: "22.4 Database Interaction with `clojure.java.jdbc` and `next.jdbc`"
tags:
- "Clojure"
- "Database"
- "Functional Programming"
- "clojure.java.jdbc"
- "next.jdbc"
- "HikariCP"
- "SQL"
- "Data Management"
date: 2024-11-25
type: docs
nav_weight: 224000
license: "© 2024 Tokenizer Inc. CC BY-NC-SA 4.0"
---

## 22.4 Database Interaction with `clojure.java.jdbc` and `next.jdbc`

In this section, we delve into the intricacies of database interaction within the Clojure ecosystem, focusing on two prominent libraries: `clojure.java.jdbc` and `next.jdbc`. These libraries offer robust solutions for interfacing with relational databases, enabling developers to perform efficient data operations using Clojure's functional paradigm.

### Database Connectivity in Clojure

Clojure's approach to database connectivity emphasizes simplicity and immutability, aligning with its functional programming principles. By leveraging libraries like `clojure.java.jdbc` and `next.jdbc`, developers can seamlessly integrate SQL databases into their applications, harnessing the power of Clojure's immutable data structures and expressive syntax.

### `clojure.java.jdbc`

`clojure.java.jdbc` is a well-established library that provides a comprehensive API for interacting with SQL databases. It offers a flexible approach to executing SQL statements, handling transactions, and mapping query results to Clojure data structures.

#### Overview of `clojure.java.jdbc`

Originally part of the Clojure Contrib project, `clojure.java.jdbc` has evolved into a standalone library that simplifies database operations. It abstracts the complexities of JDBC, allowing developers to focus on writing concise and expressive Clojure code.

```clojure
(require '[clojure.java.jdbc :as jdbc])

(def db-spec
  {:dbtype "h2" :dbname "test"})

;; Example: Inserting a record
(jdbc/insert! db-spec :users {:name "Alice" :age 30})

;; Example: Querying records
(jdbc/query db-spec ["SELECT * FROM users WHERE age > ?" 25])
```

In the example above, we define a database specification using a map, which is then used to perform insert and query operations. The `insert!` function adds a new record to the `users` table, while the `query` function retrieves records based on the specified criteria.

#### Key Features of `clojure.java.jdbc`

- **Simplicity**: The library provides a straightforward API for executing SQL statements and managing transactions.
- **Flexibility**: Developers can use raw SQL queries or leverage Clojure's data structures to build dynamic queries.
- **Compatibility**: Supports various SQL databases, including PostgreSQL, MySQL, and SQLite.

#### Limitations of `clojure.java.jdbc`

While `clojure.java.jdbc` is a powerful tool, it has some limitations that have led to the development of `next.jdbc`. These include performance bottlenecks and a somewhat verbose API for complex operations.

### Introducing `next.jdbc`

`next.jdbc` is a modern, high-performance library designed to address the limitations of `clojure.java.jdbc`. It offers a more streamlined API and improved performance, making it an ideal choice for modern Clojure applications.

#### Overview of `next.jdbc`

Developed by Sean Corfield, `next.jdbc` focuses on simplicity and speed. It leverages Java's `java.sql` package directly, providing a thin layer of abstraction that minimizes overhead.

```clojure
(require '[next.jdbc :as jdbc])

(def db-spec
  {:dbtype "h2" :dbname "test"})

;; Example: Inserting a record
(jdbc/execute! db-spec ["INSERT INTO users (name, age) VALUES (?, ?)" "Alice" 30])

;; Example: Querying records
(jdbc/execute! db-spec ["SELECT * FROM users WHERE age > ?" 25])
```

In this example, we use `execute!` to perform both insert and query operations. The API is consistent and easy to use, with a focus on performance and simplicity.

#### Key Features of `next.jdbc`

- **Performance**: Optimized for speed, with minimal overhead compared to `clojure.java.jdbc`.
- **Simplicity**: A consistent API that reduces boilerplate code and enhances readability.
- **Flexibility**: Supports various SQL databases and integrates seamlessly with Clojure's data structures.

#### Transitioning from `clojure.java.jdbc` to `next.jdbc`

For developers familiar with `clojure.java.jdbc`, transitioning to `next.jdbc` is straightforward. The core concepts remain the same, with improvements in API design and performance.

### Connection Management

Efficient connection management is crucial for any database-driven application. Clojure provides several options for managing connections, including pooling libraries like HikariCP.

#### Best Practices for Connection Management

- **Pooling**: Use connection pooling to manage database connections efficiently. Libraries like HikariCP provide robust pooling solutions that enhance performance and reliability.
- **Resource Management**: Ensure that connections are properly closed after use to prevent resource leaks.
- **Configuration**: Optimize connection settings based on your application's requirements, such as connection timeout and pool size.

#### Using HikariCP with `next.jdbc`

HikariCP is a popular connection pooling library known for its high performance and low overhead. It integrates seamlessly with `next.jdbc`, providing an efficient solution for managing database connections.

```clojure
(require '[next.jdbc :as jdbc])
(require '[hikari-cp.core :as hikari])

(def db-spec
  (hikari/make-datasource
    {:jdbc-url "jdbc:h2:mem:test"
     :username "sa"
     :password ""}))

;; Example: Querying with connection pooling
(jdbc/execute! db-spec ["SELECT * FROM users"])
```

In this example, we use `hikari/make-datasource` to create a pooled data source, which is then used with `next.jdbc` for executing queries. This approach ensures efficient connection management and improved application performance.

### Working with Data

Clojure's functional paradigm shines when working with data. Both `clojure.java.jdbc` and `next.jdbc` provide powerful tools for querying data, handling transactions, and mapping results to Clojure data structures.

#### Querying Data

Querying data is a fundamental operation in any database-driven application. Both libraries offer flexible APIs for executing SQL queries and retrieving results.

```clojure
;; Example: Querying data with next.jdbc
(require '[next.jdbc.result-set :as rs])

(defn get-users [db-spec age]
  (jdbc/execute! db-spec
                 ["SELECT * FROM users WHERE age > ?" age]
                 {:builder-fn rs/as-unqualified-maps}))

(get-users db-spec 25)
```

In this example, we use `next.jdbc` to query users older than a specified age. The `:builder-fn` option allows us to customize the result set mapping, returning results as unqualified maps.

#### Handling Transactions

Transactions ensure data consistency and integrity. Both libraries provide mechanisms for managing transactions, allowing developers to group multiple operations into a single atomic unit.

```clojure
;; Example: Handling transactions with next.jdbc
(jdbc/with-transaction [tx db-spec]
  (jdbc/execute! tx ["INSERT INTO users (name, age) VALUES (?, ?)" "Bob" 28])
  (jdbc/execute! tx ["UPDATE users SET age = ? WHERE name = ?" 29 "Alice"]))
```

In this example, we use `with-transaction` to execute multiple operations within a single transaction. This ensures that all operations are committed atomically, maintaining data integrity.

#### Mapping Results to Clojure Data Structures

Clojure's immutable data structures provide a natural fit for representing database query results. Both `clojure.java.jdbc` and `next.jdbc` offer flexible options for mapping results to Clojure maps and vectors.

```clojure
;; Example: Mapping results with clojure.java.jdbc
(jdbc/query db-spec ["SELECT * FROM users"]
            {:row-fn #(select-keys % [:name :age])})
```

In this example, we use `clojure.java.jdbc` to query users and map the results to a vector of maps, selecting only the `name` and `age` fields.

### Conclusion

Interfacing with relational databases in Clojure is both powerful and intuitive, thanks to libraries like `clojure.java.jdbc` and `next.jdbc`. By leveraging Clojure's functional paradigm, developers can build scalable and efficient applications that seamlessly integrate with SQL databases.

For further reading and resources, consider exploring the following links:

- [Clojure Official Documentation](https://clojure.org/reference)
- [clojure.java.jdbc GitHub Repository](https://github.com/clojure/java.jdbc)
- [next.jdbc GitHub Repository](https://github.com/seancorfield/next-jdbc)
- [HikariCP GitHub Repository](https://github.com/brettwooldridge/HikariCP)

## **Test Your Knowledge: Database Interaction with `clojure.java.jdbc` and `next.jdbc` Quiz**

{{< quizdown >}}

### What is the primary advantage of using `next.jdbc` over `clojure.java.jdbc`?

- [x] Improved performance and a simpler API
- [ ] Better support for NoSQL databases
- [ ] Enhanced security features
- [ ] Built-in data visualization tools

> **Explanation:** `next.jdbc` offers improved performance and a simpler API compared to `clojure.java.jdbc`, making it a preferred choice for modern applications.


### Which library is recommended for connection pooling in Clojure?

- [x] HikariCP
- [ ] Apache Commons DBCP
- [ ] C3P0
- [ ] BoneCP

> **Explanation:** HikariCP is a popular connection pooling library known for its high performance and low overhead, making it ideal for use with Clojure.


### How do you execute a SQL query using `next.jdbc`?

- [x] Using the `execute!` function
- [ ] Using the `run-query` function
- [ ] Using the `query-db` function
- [ ] Using the `fetch-results` function

> **Explanation:** The `execute!` function in `next.jdbc` is used to execute SQL queries and commands.


### What is the purpose of the `:builder-fn` option in `next.jdbc`?

- [x] To customize the result set mapping
- [ ] To specify the database connection timeout
- [ ] To enable connection pooling
- [ ] To define the transaction isolation level

> **Explanation:** The `:builder-fn` option in `next.jdbc` allows developers to customize how the result set is mapped to Clojure data structures.


### Which function is used to manage transactions in `next.jdbc`?

- [x] `with-transaction`
- [ ] `begin-transaction`
- [ ] `start-transaction`
- [ ] `transactional-execute`

> **Explanation:** The `with-transaction` function in `next.jdbc` is used to manage transactions, ensuring atomicity of multiple operations.


### What is a key feature of `clojure.java.jdbc`?

- [x] Flexibility in executing raw SQL queries
- [ ] Built-in support for JSON data types
- [ ] Automatic schema migration
- [ ] Native support for graph databases

> **Explanation:** `clojure.java.jdbc` is known for its flexibility in executing raw SQL queries, allowing developers to leverage SQL directly.


### How can you map query results to Clojure maps using `clojure.java.jdbc`?

- [x] Using the `:row-fn` option
- [ ] Using the `:map-fn` option
- [ ] Using the `:result-fn` option
- [ ] Using the `:data-fn` option

> **Explanation:** The `:row-fn` option in `clojure.java.jdbc` is used to map each row of the query result to a Clojure map.


### What is the main advantage of using connection pooling?

- [x] Improved performance and resource management
- [ ] Enhanced security features
- [ ] Simplified query syntax
- [ ] Built-in data analytics

> **Explanation:** Connection pooling improves performance and resource management by reusing database connections, reducing the overhead of opening and closing connections.


### Which of the following is NOT a feature of `next.jdbc`?

- [x] Built-in support for NoSQL databases
- [ ] High performance and low overhead
- [ ] Consistent API design
- [ ] Integration with Clojure data structures

> **Explanation:** `next.jdbc` is designed for SQL databases and does not provide built-in support for NoSQL databases.


### True or False: `next.jdbc` can be used with HikariCP for connection pooling.

- [x] True
- [ ] False

> **Explanation:** True. `next.jdbc` can be integrated with HikariCP for efficient connection pooling and management.

{{< /quizdown >}}
