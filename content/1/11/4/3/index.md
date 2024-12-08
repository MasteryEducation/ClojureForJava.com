---
canonical: "https://clojureforjava.com/1/11/4/3"
title: "Replacing Inheritance with Composition in Clojure"
description: "Explore how to achieve code reuse and polymorphism in Clojure using composition and higher-order functions, replacing traditional inheritance hierarchies."
linkTitle: "11.4.3 Replacing Inheritance with Composition"
tags:
- "Clojure"
- "Functional Programming"
- "Composition"
- "Polymorphism"
- "Protocols"
- "Multimethods"
- "Java Interoperability"
- "Code Reuse"
date: 2024-11-25
type: docs
nav_weight: 114300
license: "© 2024 Tokenizer Inc. CC BY-NC-SA 4.0"
---

## 11.4.3 Replacing Inheritance with Composition

As experienced Java developers, we are accustomed to using inheritance as a primary mechanism for code reuse and polymorphism. However, in Clojure, a functional programming language, we can achieve these goals more effectively through composition and higher-order functions. This section will guide you through the transition from inheritance-based designs to composition-centric approaches in Clojure, leveraging its unique features such as protocols and multimethods.

### Understanding the Limitations of Inheritance

Inheritance is a powerful tool in object-oriented programming (OOP) but comes with its own set of limitations:

- **Tight Coupling**: Inheritance creates a strong relationship between parent and child classes, making changes in the parent class potentially disruptive to child classes.
- **Fragile Base Class Problem**: Modifications to a base class can inadvertently affect all derived classes, leading to unexpected behaviors.
- **Limited Flexibility**: Inheritance hierarchies can become rigid, making it difficult to adapt to new requirements without significant refactoring.

In contrast, composition offers a more flexible and modular approach to building systems.

### Embracing Composition in Clojure

Composition in Clojure involves building complex functionality by combining simpler, reusable components. This approach aligns well with Clojure's functional programming paradigm, where functions are first-class citizens.

#### Higher-Order Functions

Higher-order functions are functions that take other functions as arguments or return them as results. They are a cornerstone of functional programming and enable powerful composition patterns.

```clojure
(defn apply-discount [discount-fn price]
  (discount-fn price))

(defn percentage-discount [percent]
  (fn [price]
    (* price (- 1 (/ percent 100)))))

;; Usage
(def ten-percent-off (percentage-discount 10))
(apply-discount ten-percent-off 100) ; => 90
```

In this example, `apply-discount` is a higher-order function that applies a discount function to a price. The `percentage-discount` function returns a new function that calculates the discounted price, demonstrating how functions can be composed to achieve desired behaviors.

#### Protocols and Polymorphism

Clojure's protocols provide a way to define a set of functions that can be implemented by different data types, offering polymorphic behavior without inheritance.

```clojure
(defprotocol Discountable
  (apply-discount [this price]))

(defrecord PercentageDiscount [percent]
  Discountable
  (apply-discount [this price]
    (* price (- 1 (/ percent 100)))))

(defrecord FixedDiscount [amount]
  Discountable
  (apply-discount [this price]
    (- price amount)))

;; Usage
(def ten-percent (->PercentageDiscount 10))
(def five-dollars (->FixedDiscount 5))

(apply-discount ten-percent 100) ; => 90
(apply-discount five-dollars 100) ; => 95
```

Here, the `Discountable` protocol defines a polymorphic `apply-discount` function. Different discount strategies are implemented using records, each providing its own implementation of the protocol.

#### Multimethods for Flexible Dispatch

Multimethods in Clojure allow for flexible method dispatch based on arbitrary criteria, not just the type of a single argument.

```clojure
(defmulti discount-type (fn [discount price] (:type discount)))

(defmethod discount-type :percentage [discount price]
  (* price (- 1 (/ (:percent discount) 100))))

(defmethod discount-type :fixed [discount price]
  (- price (:amount discount)))

;; Usage
(def percentage-discount {:type :percentage :percent 10})
(def fixed-discount {:type :fixed :amount 5})

(discount-type percentage-discount 100) ; => 90
(discount-type fixed-discount 100) ; => 95
```

Multimethods provide a powerful mechanism for achieving polymorphic behavior based on multiple criteria, offering greater flexibility than traditional inheritance.

### Comparing Composition and Inheritance

To better understand the transition from inheritance to composition, let's compare the two approaches using a simple example: a system for calculating discounts.

#### Java Inheritance Example

```java
abstract class Discount {
    abstract double apply(double price);
}

class PercentageDiscount extends Discount {
    private final double percent;

    public PercentageDiscount(double percent) {
        this.percent = percent;
    }

    @Override
    double apply(double price) {
        return price * (1 - percent / 100);
    }
}

class FixedDiscount extends Discount {
    private final double amount;

    public FixedDiscount(double amount) {
        this.amount = amount;
    }

    @Override
    double apply(double price) {
        return price - amount;
    }
}
```

In Java, we define an abstract `Discount` class and extend it to create specific discount types. This approach uses inheritance to achieve polymorphism.

#### Clojure Composition Example

```clojure
(defprotocol Discount
  (apply-discount [this price]))

(defrecord PercentageDiscount [percent]
  Discount
  (apply-discount [this price]
    (* price (- 1 (/ percent 100)))))

(defrecord FixedDiscount [amount]
  Discount
  (apply-discount [this price]
    (- price amount)))
```

In Clojure, we use protocols and records to achieve the same polymorphic behavior. This approach is more flexible and decoupled, allowing for easier modifications and extensions.

### Advantages of Composition Over Inheritance

- **Flexibility**: Composition allows for more flexible designs, as components can be easily swapped or combined.
- **Reusability**: Functions and protocols can be reused across different contexts without the constraints of an inheritance hierarchy.
- **Decoupling**: Systems built with composition are less tightly coupled, making them easier to maintain and extend.

### Practical Exercise: Refactor an Inheritance-Based Design

Let's refactor a simple Java inheritance-based design into a Clojure composition-based design. Consider a system with different types of notifications: email and SMS.

#### Java Inheritance Example

```java
abstract class Notification {
    abstract void send(String message);
}

class EmailNotification extends Notification {
    @Override
    void send(String message) {
        System.out.println("Sending email: " + message);
    }
}

class SMSNotification extends Notification {
    @Override
    void send(String message) {
        System.out.println("Sending SMS: " + message);
    }
}
```

#### Clojure Composition Example

```clojure
(defprotocol Notification
  (send-notification [this message]))

(defrecord EmailNotification []
  Notification
  (send-notification [this message]
    (println "Sending email:" message)))

(defrecord SMSNotification []
  Notification
  (send-notification [this message]
    (println "Sending SMS:" message)))

;; Usage
(def email (->EmailNotification))
(def sms (->SMSNotification))

(send-notification email "Hello via Email!")
(send-notification sms "Hello via SMS!")
```

### Try It Yourself

Experiment with the Clojure code by adding a new type of notification, such as a push notification. Implement it using the `Notification` protocol and test it with different messages.

### Summary and Key Takeaways

- **Composition over Inheritance**: Clojure encourages composition over inheritance, promoting flexibility and modularity.
- **Protocols and Multimethods**: Use protocols for polymorphism and multimethods for flexible dispatch based on multiple criteria.
- **Higher-Order Functions**: Leverage higher-order functions for powerful composition patterns.

By embracing these concepts, you can build more robust and adaptable systems in Clojure, moving beyond the limitations of traditional inheritance.

### Further Reading

- [Clojure Protocols and Records](https://clojure.org/reference/protocols)
- [Clojure Multimethods](https://clojure.org/reference/multimethods)
- [Functional Programming in Clojure](https://clojure.org/about/rationale)

### Exercises

1. Refactor a Java class hierarchy into a Clojure composition-based design.
2. Implement a new feature using protocols and multimethods.
3. Explore the use of higher-order functions to simplify complex logic.

Now that we've explored how to replace inheritance with composition in Clojure, let's apply these concepts to refactor and enhance your existing Java applications.

## Quiz: Mastering Composition in Clojure

{{< quizdown >}}

### What is a key advantage of using composition over inheritance in Clojure?

- [x] Flexibility and modularity
- [ ] Strong coupling between components
- [ ] Easier to implement inheritance hierarchies
- [ ] Requires less code

> **Explanation:** Composition offers flexibility and modularity, allowing components to be easily combined and reused without the constraints of inheritance hierarchies.

### How do protocols in Clojure help achieve polymorphism?

- [x] By defining a set of functions that can be implemented by different data types
- [ ] By creating inheritance hierarchies
- [ ] By using classes and interfaces
- [ ] By enforcing strict type checking

> **Explanation:** Protocols define a set of functions that can be implemented by different data types, providing a way to achieve polymorphism without inheritance.

### What is a higher-order function in Clojure?

- [x] A function that takes other functions as arguments or returns them as results
- [ ] A function that is defined at a higher level of abstraction
- [ ] A function that operates on higher-level data structures
- [ ] A function that is more complex than others

> **Explanation:** Higher-order functions take other functions as arguments or return them as results, enabling powerful composition patterns.

### Which Clojure feature allows for flexible method dispatch based on arbitrary criteria?

- [x] Multimethods
- [ ] Protocols
- [ ] Records
- [ ] Atoms

> **Explanation:** Multimethods allow for flexible method dispatch based on arbitrary criteria, not just the type of a single argument.

### In the provided Clojure example, what does the `apply-discount` function do?

- [x] Applies a discount function to a price
- [ ] Calculates the total price
- [ ] Creates a new discount function
- [ ] Returns the original price

> **Explanation:** The `apply-discount` function applies a discount function to a price, demonstrating the use of higher-order functions.

### What is the purpose of the `defrecord` construct in Clojure?

- [x] To define a new data type with specific fields and protocol implementations
- [ ] To create a new namespace
- [ ] To define a global variable
- [ ] To declare a function

> **Explanation:** `defrecord` is used to define a new data type with specific fields and protocol implementations, allowing for structured data and polymorphic behavior.

### How can you achieve polymorphic behavior in Clojure without using inheritance?

- [x] By using protocols and multimethods
- [ ] By creating abstract classes
- [ ] By using interfaces
- [ ] By defining static methods

> **Explanation:** Protocols and multimethods provide polymorphic behavior without the need for inheritance, offering more flexibility and decoupling.

### What is the main benefit of using higher-order functions in Clojure?

- [x] They enable powerful composition patterns
- [ ] They simplify syntax
- [ ] They enforce strict type checking
- [ ] They reduce the need for variables

> **Explanation:** Higher-order functions enable powerful composition patterns, allowing for more flexible and reusable code.

### Which of the following is NOT a benefit of using composition over inheritance?

- [ ] Flexibility
- [ ] Reusability
- [ ] Decoupling
- [x] Strong coupling

> **Explanation:** Composition promotes flexibility, reusability, and decoupling, whereas inheritance often leads to strong coupling.

### True or False: In Clojure, inheritance is the primary mechanism for achieving code reuse and polymorphism.

- [ ] True
- [x] False

> **Explanation:** False. In Clojure, composition, protocols, and multimethods are preferred over inheritance for achieving code reuse and polymorphism.

{{< /quizdown >}}
