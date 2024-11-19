---
linkTitle: "Appendix A: Clojure Cheat Sheet"
title: "Clojure Cheat Sheet: Essential Syntax and Functions for Java Developers"
description: "A comprehensive Clojure cheat sheet for Java developers, covering essential syntax, functions, and best practices for quick reference."
categories:
- Clojure
- Functional Programming
- Java Interoperability
tags:
- Clojure
- Java
- Functional Programming
- Syntax
- Cheat Sheet
date: 2024-10-25
type: docs
nav_weight: 1610000
canonical: "https://clojureforjava.com/1/16/1"
license: "© 2024 Tokenizer Inc. CC BY-NC-SA 4.0"
---

## Appendix A: Clojure Cheat Sheet

This Clojure cheat sheet is designed to serve as a quick reference guide for Java developers transitioning to Clojure. It covers essential syntax, functions, and best practices, providing a handy resource for developers to consult during their Clojure programming journey. Whether you're writing your first Clojure program or need a refresher on specific functions, this cheat sheet has you covered.

### Basic Syntax and Structure

#### S-Expressions

Clojure code is composed of S-expressions (symbolic expressions), which are lists enclosed in parentheses. These lists can represent function calls, data, or both.

```clojure
(+ 1 2 3) ; Adds numbers, resulting in 6
```

#### Comments

Comments in Clojure start with a semicolon (`;`). Everything after the semicolon on the same line is ignored by the compiler.

```clojure
; This is a single-line comment
```

#### Defining Variables

Use `def` to bind a value to a symbol, creating a global variable.

```clojure
(def pi 3.14159)
```

#### Functions

Functions are first-class citizens in Clojure. Define them using the `defn` macro.

```clojure
(defn add [a b]
  (+ a b))
```

### Data Structures

Clojure provides a rich set of immutable data structures.

#### Lists

Lists are ordered collections, typically used for code (S-expressions).

```clojure
'(1 2 3 4) ; A list of numbers
```

#### Vectors

Vectors are ordered collections, optimized for random access.

```clojure
[1 2 3 4] ; A vector of numbers
```

#### Maps

Maps are collections of key-value pairs.

```clojure
{:name "Alice" :age 30} ; A map with two key-value pairs
```

#### Sets

Sets are collections of unique values.

```clojure
#{1 2 3 4} ; A set of numbers
```

### Core Functions

#### Arithmetic

Clojure supports standard arithmetic operations.

```clojure
(+ 1 2) ; Addition
(- 5 3) ; Subtraction
(* 2 3) ; Multiplication
(/ 10 2) ; Division
```

#### Comparison

Comparison operators return boolean values.

```clojure
(= 1 1) ; Equality
(not= 1 2) ; Inequality
(< 1 2) ; Less than
(> 2 1) ; Greater than
(<= 1 2) ; Less than or equal to
(>= 2 1) ; Greater than or equal to
```

#### Logical Operators

Logical operators work with boolean values.

```clojure
(and true false) ; Logical AND
(or true false) ; Logical OR
(not true) ; Logical NOT
```

### Control Structures

#### Conditional Expressions

Clojure provides several ways to handle conditional logic.

```clojure
(if true "yes" "no") ; Basic if expression

(cond
  (< 1 2) "less"
  (> 1 2) "greater"
  :else "equal") ; Cond expression for multiple conditions
```

#### Looping

Clojure emphasizes recursion over traditional loops.

```clojure
(loop [i 0]
  (when (< i 10)
    (println i)
    (recur (inc i)))) ; Loop and recur for iteration
```

### Functions and Higher-Order Programming

#### Defining Functions

Functions are defined using `defn`.

```clojure
(defn greet [name]
  (str "Hello, " name))
```

#### Anonymous Functions

Anonymous functions are created using `fn` or the shorthand `#()`.

```clojure
(fn [x] (* x x)) ; Anonymous function
#(* % %) ; Shorthand for the same
```

#### Higher-Order Functions

Functions that take other functions as arguments or return them.

```clojure
(map inc [1 2 3]) ; Applies inc to each element
(filter even? [1 2 3 4]) ; Filters even numbers
(reduce + [1 2 3 4]) ; Sums the elements
```

### Immutability and Persistent Data Structures

Clojure's data structures are immutable, meaning they cannot be changed once created. Instead, operations on these structures return new versions with the desired changes.

#### Structural Sharing

Clojure uses structural sharing to efficiently manage memory when creating new versions of data structures.

```clojure
(def original [1 2 3])
(def modified (conj original 4)) ; Adds 4, creating a new vector
```

### Namespaces and Code Organization

#### Creating Namespaces

Namespaces help organize code and manage dependencies.

```clojure
(ns my-app.core) ; Declare a namespace
```

#### Using Other Namespaces

Use `require` to include other namespaces.

```clojure
(require '[clojure.string :as str]) ; Alias clojure.string as str
```

### Java Interoperability

Clojure runs on the JVM and can seamlessly interact with Java code.

#### Calling Java Methods

Use the `.` operator to call Java methods.

```clojure
(.toUpperCase "hello") ; Calls Java String method
```

#### Creating Java Objects

Use `new` to create Java objects.

```clojure
(new java.util.Date) ; Creates a new Date object
```

### Best Practices

- **Embrace Immutability:** Favor immutable data structures to avoid side effects.
- **Leverage Higher-Order Functions:** Use functions like `map`, `reduce`, and `filter` for concise and expressive code.
- **Use Namespaces Wisely:** Organize code into namespaces for better modularity and maintainability.
- **Interoperate with Java:** Utilize Java libraries and frameworks when needed, but keep Clojure idioms in mind.

### Common Pitfalls

- **Misunderstanding Immutability:** Remember that operations on data structures return new versions, not modifications.
- **Overusing Anonymous Functions:** While convenient, excessive use can lead to less readable code.
- **Ignoring Lazy Evaluation:** Be mindful of lazy sequences and their potential impact on performance.

### Optimization Tips

- **Use Persistent Data Structures:** They provide efficient memory usage and performance.
- **Profile and Benchmark:** Use tools like `criterium` to measure performance and identify bottlenecks.
- **Avoid Premature Optimization:** Focus on writing clear and maintainable code first.

## Quiz Time!

{{< quizdown >}}

### What is the primary purpose of S-expressions in Clojure?

- [x] To represent code and data as lists
- [ ] To define variables
- [ ] To handle exceptions
- [ ] To create namespaces

> **Explanation:** S-expressions are used in Clojure to represent both code and data, typically as lists enclosed in parentheses.

### How do you define a global variable in Clojure?

- [x] Using `def`
- [ ] Using `let`
- [ ] Using `var`
- [ ] Using `set`

> **Explanation:** The `def` keyword is used to define a global variable in Clojure.

### Which of the following is an immutable data structure in Clojure?

- [x] Vector
- [ ] Array
- [ ] HashMap
- [ ] LinkedList

> **Explanation:** Vectors in Clojure are immutable, meaning they cannot be changed once created.

### What is the purpose of the `recur` keyword in Clojure?

- [x] To enable tail-recursive loops
- [ ] To define a new function
- [ ] To create a new namespace
- [ ] To handle exceptions

> **Explanation:** The `recur` keyword is used in Clojure to enable tail-recursive loops, allowing efficient recursion.

### How do you call a static Java method from Clojure?

- [x] Using the `.` operator
- [ ] Using `invoke`
- [ ] Using `call`
- [ ] Using `apply`

> **Explanation:** The `.` operator is used to call Java methods, including static methods, from Clojure.

### What is the result of `(filter even? [1 2 3 4])`?

- [x] (2 4)
- [ ] (1 3)
- [ ] (1 2 3 4)
- [ ] (4 2)

> **Explanation:** The `filter` function returns a sequence of elements that satisfy the predicate, in this case, even numbers.

### Which keyword is used to create an anonymous function in Clojure?

- [x] `fn`
- [ ] `defn`
- [ ] `lambda`
- [ ] `anon`

> **Explanation:** The `fn` keyword is used to create anonymous functions in Clojure.

### What does the `map` function do in Clojure?

- [x] Applies a function to each element of a collection
- [ ] Filters elements of a collection
- [ ] Reduces a collection to a single value
- [ ] Sorts a collection

> **Explanation:** The `map` function applies a given function to each element of a collection, returning a new sequence.

### How do you include another namespace in your Clojure code?

- [x] Using `require`
- [ ] Using `import`
- [ ] Using `include`
- [ ] Using `use`

> **Explanation:** The `require` function is used to include other namespaces in your Clojure code.

### Clojure's data structures are mutable. True or False?

- [ ] True
- [x] False

> **Explanation:** Clojure's data structures are immutable, meaning they cannot be changed once created.

{{< /quizdown >}}

This cheat sheet provides a comprehensive overview of Clojure's syntax and core functions, serving as a valuable resource for Java developers learning Clojure. By understanding these fundamental concepts, developers can effectively leverage Clojure's powerful features in their projects.
