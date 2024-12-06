---
canonical: "https://clojureforjava.com/3/3/1"
title: "Clojure Syntax: A Comprehensive Guide for Java Developers"
description: "Explore the fundamental syntax of Clojure and understand how it differs from Java. Learn to write basic expressions and functions in Clojure, leveraging your Java knowledge for a smooth transition."
linkTitle: "3.1 Introduction to Clojure Syntax"
tags:
- "Clojure"
- "Functional Programming"
- "Java Interoperability"
- "Syntax"
- "Expressions"
- "Functions"
- "Immutability"
- "Lisp"
date: 2024-11-25
type: docs
nav_weight: 31000
license: "© 2024 Tokenizer Inc. CC BY-NC-SA 4.0"
---

## 3.1 Introduction to Clojure Syntax

As experienced Java developers, you are already familiar with the intricacies of object-oriented programming and the syntax that comes with it. Transitioning to Clojure, a functional programming language, involves understanding a new syntax paradigm that emphasizes simplicity and expressiveness. In this section, we will explore the fundamental syntax of Clojure, drawing parallels to Java where applicable, and guide you through writing basic expressions and functions.

### Understanding the Syntax Differences Between Java and Clojure

Clojure is a dialect of Lisp, which means its syntax is quite different from Java's. While Java uses a C-style syntax with braces and semicolons, Clojure employs a prefix notation with parentheses. This might seem unusual at first, but it offers significant advantages in terms of code manipulation and macro capabilities.

#### Key Differences

1. **Parentheses and Prefix Notation**:
   - **Java**: Uses infix notation, where operators are placed between operands.
   - **Clojure**: Uses prefix notation, where the operator is placed before the operands.

   **Java Example**:
   ```java
   int sum = 1 + 2;
   ```

   **Clojure Example**:
   ```clojure
   (def sum (+ 1 2))
   ```

2. **Immutable Data Structures**:
   - **Java**: Mutable by default, requiring explicit handling for immutability.
   - **Clojure**: Immutable by default, promoting safer concurrent programming.

3. **Functions as First-Class Citizens**:
   - **Java**: Methods are tied to classes.
   - **Clojure**: Functions are independent and can be passed around as values.

4. **No Semicolons**:
   - **Java**: Statements end with semicolons.
   - **Clojure**: No semicolons are used; expressions are delimited by parentheses.

5. **Dynamic Typing**:
   - **Java**: Statically typed.
   - **Clojure**: Dynamically typed, with optional type hints for performance.

### Writing Basic Expressions and Functions

Let's delve into writing basic expressions and functions in Clojure, leveraging your Java knowledge to ease the transition.

#### Expressions

In Clojure, everything is an expression, and expressions are evaluated to produce a value. This is a fundamental concept that differs from Java, where statements do not always produce a value.

**Example: Arithmetic Expression**

```clojure
(+ 3 4 5) ; Adds 3, 4, and 5, resulting in 12
```

**Try It Yourself**: Modify the expression to subtract or multiply the numbers.

#### Defining Variables

Clojure uses `def` to bind a name to a value, similar to declaring a variable in Java.

**Java Example**:
```java
int number = 10;
```

**Clojure Example**:
```clojure
(def number 10)
```

**Note**: In Clojure, `def` creates a global binding. For local bindings, use `let`.

#### Functions

Functions are central to Clojure's syntax. They are defined using the `defn` keyword.

**Java Example**:
```java
public int add(int a, int b) {
    return a + b;
}
```

**Clojure Example**:
```clojure
(defn add [a b]
  (+ a b))
```

**Try It Yourself**: Create a function that multiplies two numbers.

#### Higher-Order Functions

Clojure, like other functional languages, supports higher-order functions—functions that take other functions as arguments or return them as results.

**Example: Using `map`**

```clojure
(map inc [1 2 3 4]) ; Increments each number in the list, resulting in (2 3 4 5)
```

**Try It Yourself**: Use `map` to square each number in a list.

### Visual Aids

To better understand Clojure's syntax, let's look at a diagram illustrating the flow of data through a higher-order function.

```mermaid
graph TD;
    A[Input List: [1, 2, 3, 4]] --> B[Function: inc]
    B --> C[Output List: [2, 3, 4, 5]]
```

**Diagram Description**: This flowchart shows how the `map` function applies the `inc` function to each element of the input list, producing an output list.

### References and Links

For further reading and deeper dives into Clojure syntax, consider these resources:

- [Official Clojure Documentation](https://clojure.org/reference/documentation)
- [ClojureDocs](https://clojuredocs.org/)
- [Relevant GitHub Repositories](https://github.com/clojure)

### Knowledge Check

Let's engage with some questions to reinforce your understanding of Clojure syntax:

1. What is the primary difference between Java's infix notation and Clojure's prefix notation?
2. How does Clojure handle immutability differently from Java?
3. Write a Clojure expression to calculate the product of 4, 5, and 6.
4. Define a Clojure function that subtracts two numbers.
5. Explain how higher-order functions work in Clojure.

### Exercises

1. **Exercise 1**: Write a Clojure function that calculates the factorial of a number.
2. **Exercise 2**: Use `reduce` to sum a list of numbers in Clojure.
3. **Exercise 3**: Create a Clojure function that filters even numbers from a list.

### Encouraging Tone

Now that we've explored the basics of Clojure syntax, you're well on your way to mastering this expressive language. Remember, the key to transitioning smoothly is practice and experimentation. Don't hesitate to modify the examples and try new things—it's the best way to learn!

### Summary

In this section, we've covered the fundamental syntax differences between Java and Clojure, explored how to write basic expressions and functions, and introduced higher-order functions. By understanding these core concepts, you're building a strong foundation for your journey into functional programming with Clojure.

## **Quiz: Are You Ready to Migrate from Java to Clojure?**

{{< quizdown >}}

### What is the primary difference between Java's infix notation and Clojure's prefix notation?

- [x] Infix notation places operators between operands, while prefix notation places operators before operands.
- [ ] Infix notation places operators before operands, while prefix notation places operators between operands.
- [ ] Infix notation is used for function calls, while prefix notation is used for arithmetic operations.
- [ ] Infix notation is unique to Clojure, while prefix notation is unique to Java.

> **Explanation:** Java uses infix notation where operators are placed between operands, whereas Clojure uses prefix notation where operators precede operands.

### How does Clojure handle immutability differently from Java?

- [x] Clojure is immutable by default, while Java requires explicit handling for immutability.
- [ ] Clojure uses mutable data structures by default, while Java is immutable by default.
- [ ] Clojure and Java both handle immutability in the same way.
- [ ] Clojure does not support immutability.

> **Explanation:** Clojure promotes immutability by default, which is a key feature for safe concurrent programming, unlike Java which requires explicit handling for immutability.

### Write a Clojure expression to calculate the product of 4, 5, and 6.

- [x] `(* 4 5 6)`
- [ ] `(4 * 5 * 6)`
- [ ] `(* 4) (* 5) (* 6)`
- [ ] `(multiply 4 5 6)`

> **Explanation:** In Clojure, the `*` operator is used in prefix notation to multiply numbers.

### Define a Clojure function that subtracts two numbers.

- [x] `(defn subtract [a b] (- a b))`
- [ ] `(defn subtract (a b) (a - b))`
- [ ] `(subtract a b) = a - b`
- [ ] `def subtract(a, b): return a - b`

> **Explanation:** The correct syntax for defining a function in Clojure uses `defn`, followed by the function name, parameters, and the body.

### Explain how higher-order functions work in Clojure.

- [x] They take other functions as arguments or return them as results.
- [ ] They are functions that only operate on numbers.
- [ ] They are functions that are defined at a higher level in the code.
- [ ] They are functions that cannot be passed as arguments.

> **Explanation:** Higher-order functions in Clojure can take other functions as arguments or return them as results, allowing for more flexible and reusable code.

### What is the purpose of the `def` keyword in Clojure?

- [x] To bind a name to a value globally.
- [ ] To define a local variable.
- [ ] To declare a class.
- [ ] To create a loop.

> **Explanation:** The `def` keyword in Clojure is used to create a global binding of a name to a value.

### How are functions defined in Clojure?

- [x] Using the `defn` keyword.
- [ ] Using the `function` keyword.
- [ ] Using the `def` keyword.
- [ ] Using the `fn` keyword.

> **Explanation:** Functions in Clojure are defined using the `defn` keyword, which stands for "define function."

### What is a key advantage of Clojure's prefix notation?

- [x] It allows for uniform syntax and easier manipulation of code.
- [ ] It is more readable than infix notation.
- [ ] It is unique to Clojure and not found in other languages.
- [ ] It requires fewer parentheses than infix notation.

> **Explanation:** Prefix notation provides a uniform syntax that is easier to manipulate, especially when using macros.

### What is the result of the expression `(+ 1 2 3)` in Clojure?

- [x] 6
- [ ] 5
- [ ] 3
- [ ] 1

> **Explanation:** The expression `(+ 1 2 3)` adds the numbers 1, 2, and 3, resulting in 6.

### True or False: In Clojure, semicolons are used to end expressions.

- [ ] True
- [x] False

> **Explanation:** Clojure does not use semicolons to end expressions; expressions are delimited by parentheses.

{{< /quizdown >}}
