---
linkTitle: "14.4.2 Concurrency Primitives in Clojure"
title: "Concurrency Primitives in Clojure: Atoms and Software Transactional Memory"
description: "Explore Clojure's concurrency primitives, focusing on atoms and software transactional memory (STM) with refs, to manage state in concurrent applications."
categories:
- Clojure Programming
- Concurrency
- Functional Programming
tags:
- Clojure
- Concurrency
- Atoms
- Software Transactional Memory
- Refs
date: 2024-10-25
type: docs
nav_weight: 1442000
canonical: "https://clojureforjava.com/1/14/4/2"
license: "© 2024 Tokenizer Inc. CC BY-NC-SA 4.0"
---

## 14.4.2 Concurrency Primitives in Clojure

Concurrency is a critical aspect of modern programming, especially in an era where multi-core processors are ubiquitous. Clojure, with its strong emphasis on functional programming, offers unique concurrency primitives that simplify the management of state in concurrent applications. This section delves into two of Clojure's primary concurrency primitives: **atoms** and **software transactional memory (STM)** using **refs**. These tools provide powerful mechanisms for managing shared state without the pitfalls commonly associated with traditional concurrency models.

### Understanding Concurrency in Clojure

Before diving into specific primitives, it's essential to understand Clojure's approach to concurrency. Unlike traditional languages that rely heavily on locks and mutable state, Clojure embraces immutability and functional programming principles. This paradigm shift allows developers to write concurrent programs that are easier to reason about and less prone to errors such as race conditions and deadlocks.

Clojure's concurrency model is built around the idea of managing state changes in a controlled and predictable manner. The language provides several constructs to handle state, each suited for different concurrency scenarios:

- **Atoms**: For managing synchronous, independent state changes.
- **Refs**: For coordinated, synchronous state changes using software transactional memory (STM).
- **Agents**: For asynchronous state changes.
- **Vars**: For thread-local state.

In this section, we will focus on atoms and refs, exploring how they enable safe and efficient state management in concurrent applications.

### Atoms: Managing Synchronous State

Atoms are one of the simplest concurrency primitives in Clojure, designed for managing shared, synchronous state. They provide a way to hold a mutable reference to an immutable value, ensuring that state changes are atomic and consistent.

#### Key Characteristics of Atoms

- **Atomicity**: State changes in atoms are atomic, meaning they are completed in a single, indivisible operation. This ensures that no other thread can see an intermediate state.
- **Consistency**: Atoms guarantee that state changes are consistent, adhering to the rules defined by the update function.
- **Isolation**: Each state change is isolated from others, preventing interference between concurrent updates.

#### Creating and Using Atoms

To create an atom, you use the `atom` function, passing the initial value as an argument:

```clojure
(def my-atom (atom 0))
```

The `my-atom` variable now holds an atom with an initial value of `0`. You can read the current value of an atom using the `deref` function or the `@` reader macro:

```clojure
(println @my-atom) ; Output: 0
```

#### Updating Atoms

To update the value of an atom, you use the `swap!` function, which takes an atom and a function that describes how to update the current value:

```clojure
(swap! my-atom inc)
(println @my-atom) ; Output: 1
```

The `swap!` function ensures that the update is atomic. If multiple threads attempt to update the atom simultaneously, `swap!` will retry the operation until it succeeds.

#### Practical Example: A Simple Counter

Let's consider a simple example of using an atom to implement a thread-safe counter:

```clojure
(def counter (atom 0))

(defn increment-counter []
  (swap! counter inc))

(defn decrement-counter []
  (swap! counter dec))

; Simulate concurrent updates
(doseq [_ (range 1000)]
  (future (increment-counter))
  (future (decrement-counter)))

(Thread/sleep 1000) ; Wait for all futures to complete

(println "Final counter value:" @counter) ; Output: 0
```

In this example, we create a counter initialized to `0` and define two functions, `increment-counter` and `decrement-counter`, to update the counter atomically. We then simulate concurrent updates using `future`, which runs each update in a separate thread. Despite the concurrent updates, the final counter value remains consistent due to the atomic nature of atoms.

#### Best Practices with Atoms

- **Use Atoms for Independent State**: Atoms are ideal for managing state that does not require coordination with other state changes. If your application involves multiple interdependent state changes, consider using refs and STM.
- **Avoid Long-Running Operations**: The update function passed to `swap!` should be short and efficient. Long-running operations can lead to contention and retries, reducing performance.
- **Leverage Immutability**: Remember that atoms hold immutable values. Each update returns a new immutable value, ensuring that previous states remain unchanged and accessible if needed.

### Software Transactional Memory (STM) with Refs

While atoms are suitable for independent state changes, refs and software transactional memory (STM) are designed for coordinated, synchronous state changes. STM allows you to group multiple state changes into a single atomic transaction, ensuring consistency across all changes.

#### Key Characteristics of STM and Refs

- **Atomic Transactions**: STM allows you to perform multiple state changes as a single atomic transaction. If any part of the transaction fails, the entire transaction is retried.
- **Consistency**: STM ensures that all state changes within a transaction are consistent, adhering to the rules defined by the transaction body.
- **Isolation**: Transactions are isolated from each other, preventing interference between concurrent transactions.

#### Creating and Using Refs

To create a ref, you use the `ref` function, passing the initial value as an argument:

```clojure
(def my-ref (ref 0))
```

The `my-ref` variable now holds a ref with an initial value of `0`. You can read the current value of a ref using the `deref` function or the `@` reader macro:

```clojure
(println @my-ref) ; Output: 0
```

#### Updating Refs with Transactions

To update the value of a ref, you use the `dosync` macro, which defines a transactional context. Within this context, you can use the `ref-set` and `alter` functions to update refs:

```clojure
(dosync
  (ref-set my-ref 10))

(println @my-ref) ; Output: 10
```

The `ref-set` function sets the value of a ref directly, while the `alter` function applies a function to the current value:

```clojure
(dosync
  (alter my-ref inc))

(println @my-ref) ; Output: 11
```

#### Practical Example: A Bank Account System

Let's consider a practical example of using refs and STM to implement a simple bank account system with support for transfers between accounts:

```clojure
(def account-a (ref 100))
(def account-b (ref 200))

(defn transfer [from to amount]
  (dosync
    (alter from - amount)
    (alter to + amount)))

; Transfer 50 from account-a to account-b
(transfer account-a account-b 50)

(println "Account A balance:" @account-a) ; Output: 50
(println "Account B balance:" @account-b) ; Output: 250
```

In this example, we define two bank accounts, `account-a` and `account-b`, each represented by a ref. The `transfer` function performs a transaction that deducts the specified amount from the `from` account and adds it to the `to` account. The use of STM ensures that the transfer is atomic and consistent, even in the presence of concurrent transactions.

#### Best Practices with STM and Refs

- **Use Refs for Coordinated State**: Refs are ideal for managing state that requires coordination across multiple changes. If your application involves independent state changes, consider using atoms.
- **Keep Transactions Short**: Transactions should be short and efficient to minimize contention and retries. Long-running transactions can lead to performance bottlenecks.
- **Avoid Side Effects**: Transactions should be free of side effects, such as I/O operations, to ensure consistency and reliability.

### Comparing Atoms and Refs

While both atoms and refs provide mechanisms for managing state in concurrent applications, they are suited for different scenarios:

- **Atoms**: Use atoms for independent, synchronous state changes. They are simple and efficient, making them ideal for scenarios where state changes do not require coordination.
- **Refs**: Use refs and STM for coordinated, synchronous state changes. They provide a powerful mechanism for ensuring consistency across multiple state changes, making them suitable for complex applications with interdependent state.

### Conclusion

Clojure's concurrency primitives, particularly atoms and software transactional memory with refs, offer powerful tools for managing state in concurrent applications. By embracing immutability and functional programming principles, Clojure provides a concurrency model that is both robust and easy to reason about. Whether you're building a simple counter or a complex financial system, Clojure's concurrency primitives enable you to write safe and efficient concurrent programs.

For further exploration of Clojure's concurrency model, consider diving into agents for asynchronous state changes and vars for thread-local state. Additionally, explore the rich ecosystem of Clojure libraries and frameworks that build on these primitives to provide advanced concurrency solutions.

## Quiz Time!

{{< quizdown >}}

### What is the primary purpose of atoms in Clojure?

- [x] To manage shared, synchronous state
- [ ] To manage asynchronous state
- [ ] To handle thread-local state
- [ ] To manage distributed state

> **Explanation:** Atoms in Clojure are designed to manage shared, synchronous state, ensuring atomic and consistent updates.

### How do you create an atom in Clojure?

- [x] Using the `atom` function
- [ ] Using the `ref` function
- [ ] Using the `agent` function
- [ ] Using the `var` function

> **Explanation:** The `atom` function is used to create an atom in Clojure, initializing it with a given value.

### Which function is used to update the value of an atom?

- [x] `swap!`
- [ ] `alter`
- [ ] `ref-set`
- [ ] `send`

> **Explanation:** The `swap!` function is used to update the value of an atom atomically.

### What is the purpose of software transactional memory (STM) in Clojure?

- [x] To perform coordinated, synchronous state changes
- [ ] To perform asynchronous state changes
- [ ] To handle thread-local state
- [ ] To manage distributed state

> **Explanation:** STM in Clojure is used to perform coordinated, synchronous state changes, ensuring consistency across multiple refs.

### How do you create a ref in Clojure?

- [x] Using the `ref` function
- [ ] Using the `atom` function
- [ ] Using the `agent` function
- [ ] Using the `var` function

> **Explanation:** The `ref` function is used to create a ref in Clojure, initializing it with a given value.

### Which macro is used to define a transactional context in Clojure?

- [x] `dosync`
- [ ] `sync`
- [ ] `transaction`
- [ ] `atomic`

> **Explanation:** The `dosync` macro is used to define a transactional context in Clojure, allowing for coordinated state changes.

### What is the difference between `ref-set` and `alter` in Clojure?

- [x] `ref-set` sets the value directly, while `alter` applies a function
- [ ] `alter` sets the value directly, while `ref-set` applies a function
- [ ] Both set the value directly
- [ ] Both apply a function

> **Explanation:** `ref-set` sets the value of a ref directly, while `alter` applies a function to update the value.

### When should you use atoms over refs in Clojure?

- [x] When managing independent, synchronous state changes
- [ ] When managing coordinated, synchronous state changes
- [ ] When managing asynchronous state changes
- [ ] When managing distributed state

> **Explanation:** Atoms are ideal for managing independent, synchronous state changes, where coordination is not required.

### What should transactions in STM avoid?

- [x] Side effects, such as I/O operations
- [ ] Short and efficient operations
- [ ] Coordinated state changes
- [ ] Atomic updates

> **Explanation:** Transactions in STM should avoid side effects, such as I/O operations, to ensure consistency and reliability.

### True or False: Atoms in Clojure can be used for asynchronous state changes.

- [ ] True
- [x] False

> **Explanation:** Atoms in Clojure are used for synchronous state changes, not asynchronous ones.

{{< /quizdown >}}
