---
canonical: "https://clojureforjava.com/1/3/3/3"
title: "Clojure Maps: Key-Value Pairs, Access, and Manipulation"
description: "Explore Clojure maps as key-value pairs, including creation, access, and manipulation techniques for Java developers transitioning to Clojure."
linkTitle: "3.3.3 Maps"
tags:
- "Clojure"
- "Functional Programming"
- "Maps"
- "Key-Value Pairs"
- "Data Structures"
- "Java Interoperability"
- "Immutability"
- "Collections"
date: 2024-11-25
type: docs
nav_weight: 33300
license: "© 2024 Tokenizer Inc. CC BY-NC-SA 4.0"
---

## 3.3.3 Maps

Maps in Clojure are a fundamental data structure that represent collections of key-value pairs. They are similar to Java's `HashMap` but come with the added benefits of immutability and functional programming paradigms. In this section, we will explore how to create, access, and manipulate maps in Clojure, drawing parallels to Java where applicable.

### Understanding Maps in Clojure

Maps in Clojure are immutable collections that store associations between keys and values. They are often used to represent structured data and are a core component of Clojure's data manipulation capabilities. Unlike Java's mutable `HashMap`, Clojure maps are immutable, meaning that any operation that modifies a map returns a new map with the modification applied, leaving the original map unchanged.

#### Creating Maps

In Clojure, maps are created using curly braces `{}`. Keys and values are specified in pairs, separated by spaces. Here's a simple example:

```clojure
(def person {:name "Alice" :age 30 :city "New York"})
```

In this example, `:name`, `:age`, and `:city` are keys, and `"Alice"`, `30`, and `"New York"` are their corresponding values. Notice the use of keywords (e.g., `:name`) as keys, which is a common practice in Clojure due to their efficiency and readability.

**Java Equivalent:**

In Java, you might use a `HashMap` to achieve similar functionality:

```java
import java.util.HashMap;
import java.util.Map;

Map<String, Object> person = new HashMap<>();
person.put("name", "Alice");
person.put("age", 30);
person.put("city", "New York");
```

**Key Differences:**

- **Immutability**: Clojure maps are immutable, whereas Java's `HashMap` is mutable.
- **Syntax**: Clojure uses a concise syntax with curly braces and keywords, while Java requires explicit method calls to manipulate the map.

### Accessing Values

Accessing values in a Clojure map can be done using the `get` function or by invoking the map with the key directly. Here's how you can access values:

```clojure
;; Using get
(get person :name) ;=> "Alice"

;; Direct key invocation
(person :age) ;=> 30
```

Both methods are idiomatic in Clojure, but direct key invocation is often preferred for its brevity.

**Java Equivalent:**

In Java, accessing a value from a `HashMap` involves using the `get` method:

```java
String name = (String) person.get("name"); // "Alice"
int age = (Integer) person.get("age"); // 30
```

**Key Differences:**

- **Type Safety**: Java requires explicit casting when retrieving values, whereas Clojure's dynamic typing handles this automatically.
- **Syntax**: Clojure's syntax is more concise and expressive.

### Associating and Dissociating Entries

Clojure provides functions to add or remove entries from a map, returning a new map with the changes applied.

#### Associating Entries

To add or update an entry in a map, use the `assoc` function:

```clojure
(def updated-person (assoc person :email "alice@example.com"))
```

This creates a new map `updated-person` with an additional `:email` entry.

**Java Equivalent:**

In Java, you would use the `put` method to add or update entries:

```java
person.put("email", "alice@example.com");
```

**Key Differences:**

- **Immutability**: `assoc` returns a new map, while `put` modifies the existing map.
- **Functional Approach**: Clojure's approach encourages a functional style by avoiding side effects.

#### Dissociating Entries

To remove an entry from a map, use the `dissoc` function:

```clojure
(def reduced-person (dissoc person :city))
```

This returns a new map without the `:city` entry.

**Java Equivalent:**

In Java, you would use the `remove` method:

```java
person.remove("city");
```

**Key Differences:**

- **Immutability**: `dissoc` returns a new map, while `remove` modifies the existing map.
- **Functional Approach**: Clojure's approach aligns with functional programming principles.

### Advanced Map Operations

Clojure maps offer a variety of advanced operations that enhance their utility and flexibility.

#### Merging Maps

You can merge multiple maps using the `merge` function:

```clojure
(def additional-info {:phone "123-456-7890" :city "Los Angeles"})
(def merged-person (merge person additional-info))
```

This combines `person` and `additional-info`, with values from `additional-info` taking precedence in case of key conflicts.

**Java Equivalent:**

In Java, merging maps requires iterating over entries and adding them manually:

```java
Map<String, Object> additionalInfo = new HashMap<>();
additionalInfo.put("phone", "123-456-7890");
additionalInfo.put("city", "Los Angeles");

person.putAll(additionalInfo);
```

**Key Differences:**

- **Conciseness**: Clojure's `merge` is more concise and expressive.
- **Immutability**: `merge` returns a new map, while `putAll` modifies the existing map.

#### Filtering Maps

Clojure allows you to filter maps using the `filter` function combined with a predicate:

```clojure
(def adults (filter (fn [[k v]] (and (= k :age) (>= v 18))) person))
```

This filters the map to include only entries where the age is 18 or older.

**Java Equivalent:**

In Java, filtering requires iterating over entries and conditionally adding them to a new map:

```java
Map<String, Object> adults = person.entrySet().stream()
    .filter(entry -> entry.getKey().equals("age") && (Integer) entry.getValue() >= 18)
    .collect(Collectors.toMap(Map.Entry::getKey, Map.Entry::getValue));
```

**Key Differences:**

- **Functional Style**: Clojure's approach is more aligned with functional programming.
- **Conciseness**: Clojure's syntax is more concise and expressive.

### Visualizing Map Operations

To better understand map operations, let's visualize the process of associating and dissociating entries in a map:

```mermaid
graph TD;
    A[Original Map] -->|assoc :email "alice@example.com"| B[Updated Map];
    B -->|dissoc :city| C[Reduced Map];
```

**Diagram Explanation:**

- **Original Map**: The starting point with initial key-value pairs.
- **Updated Map**: Result of adding or updating an entry using `assoc`.
- **Reduced Map**: Result of removing an entry using `dissoc`.

### Try It Yourself

To solidify your understanding, try modifying the following Clojure code:

1. Create a map representing a book with keys `:title`, `:author`, and `:year`.
2. Add a new key `:genre` using `assoc`.
3. Remove the `:year` key using `dissoc`.
4. Merge the book map with another map containing additional details.

### Exercises

1. **Exercise 1**: Create a map representing a car with keys `:make`, `:model`, and `:year`. Add a new key `:color` and remove the `:year` key.
2. **Exercise 2**: Merge two maps representing different sets of contact information. Ensure that the second map's values take precedence in case of key conflicts.
3. **Exercise 3**: Filter a map to include only entries where the value is a string.

### Key Takeaways

- **Immutability**: Clojure maps are immutable, promoting a functional programming style.
- **Conciseness**: Clojure's syntax for map operations is concise and expressive.
- **Functional Approach**: Clojure encourages a functional approach to data manipulation, avoiding side effects.

By understanding and utilizing Clojure maps, you can effectively manage key-value data in a functional programming paradigm. Now that we've explored maps in Clojure, let's apply these concepts to build more complex data structures and applications.

### Further Reading

- [Official Clojure Documentation on Maps](https://clojure.org/reference/data_structures#Maps)
- [ClojureDocs: Map Functions](https://clojuredocs.org/quickref#Maps)

## Quiz: Mastering Clojure Maps

{{< quizdown >}}

### What is the primary characteristic of Clojure maps compared to Java's HashMap?

- [x] Immutability
- [ ] Mutability
- [ ] Type Safety
- [ ] Performance

> **Explanation:** Clojure maps are immutable, meaning any modification results in a new map, unlike Java's mutable HashMap.

### How do you create a map in Clojure?

- [x] Using curly braces `{}` with key-value pairs
- [ ] Using square brackets `[]` with key-value pairs
- [ ] Using parentheses `()` with key-value pairs
- [ ] Using angle brackets `<>` with key-value pairs

> **Explanation:** Clojure maps are created using curly braces `{}` with key-value pairs.

### Which function is used to add or update an entry in a Clojure map?

- [x] assoc
- [ ] dissoc
- [ ] merge
- [ ] get

> **Explanation:** The `assoc` function is used to add or update an entry in a Clojure map.

### How do you access a value in a Clojure map using a key?

- [x] By invoking the map with the key directly
- [ ] By using the `put` method
- [ ] By using the `remove` method
- [ ] By using the `add` method

> **Explanation:** You can access a value in a Clojure map by invoking the map with the key directly.

### What does the `dissoc` function do in Clojure?

- [x] Removes an entry from a map
- [ ] Adds an entry to a map
- [ ] Merges two maps
- [ ] Retrieves a value from a map

> **Explanation:** The `dissoc` function removes an entry from a map.

### How do you merge two maps in Clojure?

- [x] Using the `merge` function
- [ ] Using the `assoc` function
- [ ] Using the `dissoc` function
- [ ] Using the `get` function

> **Explanation:** The `merge` function is used to combine two maps in Clojure.

### What is a common practice for keys in Clojure maps?

- [x] Using keywords
- [ ] Using strings
- [ ] Using integers
- [ ] Using floats

> **Explanation:** Using keywords as keys is a common practice in Clojure maps due to their efficiency and readability.

### Which of the following is NOT a characteristic of Clojure maps?

- [x] Mutability
- [ ] Immutability
- [ ] Key-value pairs
- [ ] Functional approach

> **Explanation:** Clojure maps are immutable, not mutable.

### What is the result of using the `assoc` function on a Clojure map?

- [x] A new map with the added or updated entry
- [ ] The original map is modified
- [ ] An error is thrown
- [ ] The map is cleared

> **Explanation:** The `assoc` function returns a new map with the added or updated entry.

### Clojure maps are created using parentheses `()`.

- [ ] True
- [x] False

> **Explanation:** Clojure maps are created using curly braces `{}`, not parentheses `()`.

{{< /quizdown >}}
