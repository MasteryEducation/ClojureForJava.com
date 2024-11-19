---

linkTitle: "5.5 Writing Your First Clojure Programs"
title: "Writing Your First Clojure Programs: A Guide for Java Developers"
description: "Learn how to write your first Clojure programs with practical examples and detailed explanations, tailored for Java developers transitioning to Clojure."
categories:
- Programming
- Clojure
- Java
tags:
- Clojure Programming
- Functional Programming
- Java Developers
- REPL
- Clojure Syntax
date: 2024-10-25
type: docs
nav_weight: 550000
canonical: "https://clojureforjava.com/1/5/5"
license: "© 2024 Tokenizer Inc. CC BY-NC-SA 4.0"
---

## 5.5 Writing Your First Clojure Programs

Embarking on the journey of writing your first Clojure programs is an exciting step for any Java developer. This section will guide you through the process of creating simple Clojure programs, running them in the REPL, and executing them as standalone scripts. By the end of this section, you'll have a solid foundation to tackle more complex problems using Clojure's unique syntax and functional programming paradigms.

### Understanding the Basics of Clojure Programming

Before diving into writing code, it's essential to understand the basic structure and syntax of Clojure programs. Clojure is a Lisp dialect, which means it uses a lot of parentheses and relies on a prefix notation for function calls. This might seem unusual at first, especially if you're coming from a Java background, but it's a powerful and expressive way to write code.

#### The Structure of a Clojure Program

A typical Clojure program consists of expressions, which are evaluated to produce values. Unlike Java, where you have statements and expressions, in Clojure, everything is an expression. This means every piece of code returns a value, which can be used in further computations.

Here's a simple example of a Clojure expression:

```clojure
(+ 1 2 3)
```

This expression adds the numbers 1, 2, and 3, returning the result 6. Notice the use of prefix notation, where the operator `+` comes before the operands.

#### Defining Variables and Functions

In Clojure, you define variables using the `def` keyword. However, unlike Java, variables in Clojure are immutable by default, meaning once you assign a value, it cannot be changed.

```clojure
(def x 10)
```

To define functions, you use the `defn` keyword:

```clojure
(defn add [a b]
  (+ a b))
```

This defines a function `add` that takes two parameters `a` and `b` and returns their sum.

### Writing Your First Clojure Program in the REPL

The REPL (Read-Eval-Print Loop) is an interactive environment that allows you to write and test Clojure code quickly. It's an invaluable tool for learning and experimenting with Clojure.

#### Starting the REPL

To start the REPL, open your terminal and type:

```bash
clj
```

This command will launch the Clojure REPL. You should see a prompt where you can start typing Clojure expressions.

#### Writing and Evaluating Expressions

Let's write a simple program that calculates the area of a circle given its radius. You can type the following code directly into the REPL:

```clojure
(defn circle-area [radius]
  (* Math/PI (* radius radius)))

(circle-area 5)
```

This program defines a function `circle-area` that calculates the area using the formula πr². When you call `(circle-area 5)`, it returns the area of a circle with radius 5.

#### Experimenting with the REPL

One of the best ways to learn Clojure is by experimenting in the REPL. Try modifying the `circle-area` function to calculate the circumference of a circle:

```clojure
(defn circle-circumference [radius]
  (* 2 Math/PI radius))

(circle-circumference 5)
```

### Writing Standalone Clojure Scripts

While the REPL is great for experimentation, you'll eventually want to write standalone scripts that can be executed outside of the REPL.

#### Creating a Clojure Script

Create a new file called `hello.clj` and open it in your favorite text editor. Add the following code:

```clojure
(ns hello-world.core)

(defn -main []
  (println "Hello, Clojure World!"))

(-main)
```

This script defines a namespace `hello-world.core` and a `-main` function that prints a greeting to the console.

#### Running the Script

To run the script, use the following command in your terminal:

```bash
clj hello.clj
```

You should see the output:

```
Hello, Clojure World!
```

### Solving Basic Problems with Clojure

To reinforce your learning, let's solve a few basic problems using Clojure.

#### Problem 1: FizzBuzz

The FizzBuzz problem is a classic programming challenge. Write a program that prints the numbers from 1 to 100. For multiples of three, print "Fizz" instead of the number, and for multiples of five, print "Buzz". For numbers that are multiples of both three and five, print "FizzBuzz".

```clojure
(defn fizzbuzz [n]
  (cond
    (zero? (mod n 15)) "FizzBuzz"
    (zero? (mod n 3)) "Fizz"
    (zero? (mod n 5)) "Buzz"
    :else n))

(doseq [i (range 1 101)]
  (println (fizzbuzz i)))
```

#### Problem 2: Fibonacci Sequence

Write a function that returns the first `n` numbers of the Fibonacci sequence.

```clojure
(defn fibonacci [n]
  (loop [a 0 b 1 i 0 result []]
    (if (< i n)
      (recur b (+ a b) (inc i) (conj result a))
      result)))

(fibonacci 10)
```

#### Problem 3: Palindrome Checker

Write a function that checks if a given string is a palindrome.

```clojure
(defn palindrome? [s]
  (= (seq s) (reverse (seq s))))

(palindrome? "racecar")  ; true
(palindrome? "hello")    ; false
```

### Best Practices for Writing Clojure Programs

As you start writing more Clojure code, keep these best practices in mind:

- **Embrace Immutability:** Use immutable data structures to avoid side effects and make your code easier to reason about.
- **Leverage Higher-Order Functions:** Take advantage of Clojure's rich set of higher-order functions like `map`, `reduce`, and `filter` to write concise and expressive code.
- **Use Descriptive Names:** Choose meaningful names for your functions and variables to make your code self-documenting.
- **Write Small, Composable Functions:** Break down complex problems into smaller, reusable functions to improve code readability and maintainability.

### Common Pitfalls and Optimization Tips

- **Avoid Overusing `def`:** Use `let` for local bindings instead of `def` to prevent polluting the global namespace.
- **Optimize Recursion with `recur`:** Use the `recur` keyword for tail-recursive functions to avoid stack overflow errors.
- **Profile Your Code:** Use tools like [Criterium](https://github.com/hugoduncan/criterium) to benchmark and optimize your code for performance.

### Conclusion

Writing your first Clojure programs is a rewarding experience that opens the door to a new way of thinking about programming. By leveraging the power of the REPL, writing standalone scripts, and solving basic problems, you've taken the first steps toward mastering Clojure. As you continue your journey, remember to embrace the functional programming paradigms and explore the rich ecosystem of libraries and tools available in the Clojure community.

## Quiz Time!

{{< quizdown >}}

### What is the primary difference between statements in Java and expressions in Clojure?

- [x] In Clojure, everything is an expression that returns a value.
- [ ] In Java, everything is an expression that returns a value.
- [ ] Clojure uses statements, while Java uses expressions.
- [ ] There is no difference; both languages use statements and expressions interchangeably.

> **Explanation:** In Clojure, every piece of code is an expression that evaluates to a value, whereas Java distinguishes between statements and expressions.

### How do you define a variable in Clojure?

- [x] Using the `def` keyword.
- [ ] Using the `var` keyword.
- [ ] Using the `let` keyword.
- [ ] Using the `set` keyword.

> **Explanation:** In Clojure, variables are defined using the `def` keyword, which creates an immutable binding.

### What is the purpose of the `recur` keyword in Clojure?

- [x] To optimize recursion by enabling tail-call optimization.
- [ ] To declare a recursive function.
- [ ] To iterate over a collection.
- [ ] To define a new variable.

> **Explanation:** The `recur` keyword is used in Clojure to optimize recursive functions by allowing tail-call optimization, preventing stack overflow errors.

### Which of the following is a higher-order function in Clojure?

- [x] `map`
- [ ] `def`
- [ ] `println`
- [ ] `if`

> **Explanation:** `map` is a higher-order function in Clojure that takes a function and a collection as arguments, applying the function to each element of the collection.

### How do you start the Clojure REPL from the command line?

- [x] By typing `clj`.
- [ ] By typing `java`.
- [ ] By typing `repl`.
- [ ] By typing `start-clojure`.

> **Explanation:** You start the Clojure REPL by typing `clj` in the command line, which launches the interactive environment.

### What is the result of evaluating the expression `(+ 1 2 3)` in Clojure?

- [x] 6
- [ ] 123
- [ ] 5
- [ ] 7

> **Explanation:** The expression `(+ 1 2 3)` adds the numbers 1, 2, and 3, resulting in the value 6.

### Which function checks if a string is a palindrome in the provided example?

- [x] `palindrome?`
- [ ] `fibonacci`
- [ ] `circle-area`
- [ ] `fizzbuzz`

> **Explanation:** The function `palindrome?` is used to check if a given string is a palindrome by comparing it to its reverse.

### What does the `doseq` function do in Clojure?

- [x] Iterates over a collection, executing a body of code for each element.
- [ ] Filters elements of a collection.
- [ ] Maps a function over a collection.
- [ ] Reduces a collection to a single value.

> **Explanation:** `doseq` is used to iterate over a collection, executing a body of code for each element, similar to a `for` loop in other languages.

### What is the output of the following Clojure code: `(println "Hello, Clojure World!")`?

- [x] Hello, Clojure World!
- [ ] "Hello, Clojure World!"
- [ ] Hello, Clojure World
- [ ] "Hello, Clojure World"

> **Explanation:** The `println` function prints the string "Hello, Clojure World!" to the console, including the exclamation mark.

### True or False: In Clojure, variables defined with `def` are mutable.

- [ ] True
- [x] False

> **Explanation:** Variables defined with `def` in Clojure are immutable, meaning their values cannot be changed once assigned.

{{< /quizdown >}}
