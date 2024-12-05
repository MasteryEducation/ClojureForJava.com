---
linkTitle: "2.1.1 The Gang of Four (GoF) Patterns"
title: "Gang of Four Design Patterns: Creational, Structural, and Behavioral"
description: "Explore the foundational Gang of Four design patterns, categorized into Creational, Structural, and Behavioral patterns, and their relevance in modern software design."
categories:
- Software Design
- Design Patterns
- Object-Oriented Programming
tags:
- Gang of Four
- Design Patterns
- OOP
- Software Architecture
- Creational Patterns
date: 2024-10-25
type: docs
nav_weight: 121100
canonical: "https://clojureforjava.com/10/1/2/1/1"
license: "© 2024 Tokenizer Inc. CC BY-NC-SA 4.0"
---

## 2.1.1 The Gang of Four (GoF) Patterns

In the realm of software engineering, design patterns serve as time-tested solutions to common design problems. The seminal work by Erich Gamma, Richard Helm, Ralph Johnson, and John Vlissides, collectively known as the Gang of Four (GoF), laid the foundation for understanding and applying these patterns in object-oriented programming (OOP). Their book, "Design Patterns: Elements of Reusable Object-Oriented Software," published in 1994, categorized 23 design patterns into three main types: Creational, Structural, and Behavioral. This section delves into these patterns, their historical context, and their application in addressing software design challenges.

### Historical Context and Significance

The GoF patterns emerged during a time when object-oriented programming was gaining prominence as a paradigm for software development. Prior to this, procedural programming dominated, but as software systems grew in complexity, the need for more modular and maintainable code became apparent. The GoF patterns provided a vocabulary for discussing solutions to common design problems, promoting best practices and encouraging code reuse.

The patterns are not prescriptive algorithms but rather templates that can be adapted to specific problems. They encapsulate best practices and principles such as encapsulation, abstraction, and polymorphism, which are central to OOP. By understanding and applying these patterns, developers can create software that is more flexible, scalable, and easier to maintain.

### Categorization of GoF Patterns

The 23 GoF patterns are divided into three categories based on their purpose:

1. **Creational Patterns**: These patterns deal with object creation mechanisms, trying to create objects in a manner suitable to the situation. The basic form of object creation could result in design problems or added complexity to the design. Creational design patterns solve this problem by controlling this object creation.

2. **Structural Patterns**: These patterns deal with object composition or the structure of classes. They help ensure that if one part of a system changes, the entire system doesn’t need to change along with it.

3. **Behavioral Patterns**: These patterns are concerned with algorithms and the assignment of responsibilities between objects. They help in defining how objects interact in a system and how responsibilities are distributed among them.

### Creational Patterns

Creational patterns abstract the instantiation process, making it more adaptable and flexible. They help in decoupling the client code from the objects it needs to instantiate. Here are the five creational patterns identified by the GoF:

1. **Singleton Pattern**: Ensures a class has only one instance and provides a global point of access to it. This pattern is useful when exactly one object is needed to coordinate actions across the system. However, it can lead to issues with global state and testing.

2. **Factory Method Pattern**: Defines an interface for creating an object, but lets subclasses alter the type of objects that will be created. It promotes loose coupling by eliminating the need to bind application-specific classes into the code.

3. **Abstract Factory Pattern**: Provides an interface for creating families of related or dependent objects without specifying their concrete classes. This pattern is particularly useful when the system needs to be independent of how its objects are created.

4. **Builder Pattern**: Separates the construction of a complex object from its representation, allowing the same construction process to create different representations. It is useful when an object needs to be created with many optional parts or configurations.

5. **Prototype Pattern**: Specifies the kinds of objects to create using a prototypical instance, and creates new objects by copying this prototype. This pattern is useful when the cost of creating a new instance of a class is more expensive than copying an existing instance.

#### Practical Example: Singleton Pattern in Java

In Java, a typical implementation of the Singleton pattern might look like this:

```java
public class Singleton {
    private static Singleton instance;

    private Singleton() {
        // private constructor to prevent instantiation
    }

    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
```

This implementation is straightforward but has potential issues with thread safety. To address this, the `getInstance` method can be synchronized, or a more sophisticated approach like the Bill Pugh Singleton Design can be used.

### Structural Patterns

Structural patterns focus on the composition of classes or objects. They use inheritance to compose interfaces and define ways to compose objects to obtain new functionality. Here are the seven structural patterns identified by the GoF:

1. **Adapter Pattern**: Allows the interface of an existing class to be used as another interface. It is often used to make existing classes work with others without modifying their source code.

2. **Bridge Pattern**: Decouples an abstraction from its implementation so that the two can vary independently. This pattern is useful when both the abstractions and their implementations should be extensible by subclassing.

3. **Composite Pattern**: Composes objects into tree structures to represent part-whole hierarchies. It lets clients treat individual objects and compositions of objects uniformly.

4. **Decorator Pattern**: Adds additional responsibilities to an object dynamically. Decorators provide a flexible alternative to subclassing for extending functionality.

5. **Facade Pattern**: Provides a unified interface to a set of interfaces in a subsystem. It defines a higher-level interface that makes the subsystem easier to use.

6. **Flyweight Pattern**: Uses sharing to support large numbers of fine-grained objects efficiently. It is particularly useful when many objects must be created that share a common state.

7. **Proxy Pattern**: Provides a surrogate or placeholder for another object to control access to it. This pattern is useful for implementing lazy initialization, access control, logging, etc.

#### Practical Example: Adapter Pattern in Java

Consider a scenario where you have a `MediaPlayer` interface that your application uses, but you need to integrate a third-party library that uses a `AdvancedMediaPlayer` interface. The Adapter pattern can bridge this gap:

```java
public interface MediaPlayer {
    void play(String audioType, String fileName);
}

public class AudioPlayer implements MediaPlayer {
    MediaAdapter mediaAdapter;

    @Override
    public void play(String audioType, String fileName) {
        if(audioType.equalsIgnoreCase("mp3")) {
            System.out.println("Playing mp3 file. Name: " + fileName);
        } else if(audioType.equalsIgnoreCase("vlc") || audioType.equalsIgnoreCase("mp4")) {
            mediaAdapter = new MediaAdapter(audioType);
            mediaAdapter.play(audioType, fileName);
        } else {
            System.out.println("Invalid media. " + audioType + " format not supported");
        }
    }
}

public class MediaAdapter implements MediaPlayer {
    AdvancedMediaPlayer advancedMusicPlayer;

    public MediaAdapter(String audioType){
        if(audioType.equalsIgnoreCase("vlc") ){
            advancedMusicPlayer = new VlcPlayer();
        } else if (audioType.equalsIgnoreCase("mp4")){
            advancedMusicPlayer = new Mp4Player();
        }
    }

    @Override
    public void play(String audioType, String fileName) {
        if(audioType.equalsIgnoreCase("vlc")){
            advancedMusicPlayer.playVlc(fileName);
        } else if(audioType.equalsIgnoreCase("mp4")){
            advancedMusicPlayer.playMp4(fileName);
        }
    }
}
```

### Behavioral Patterns

Behavioral patterns are concerned with algorithms and the assignment of responsibilities between objects. They help in defining how objects interact in a system and how responsibilities are distributed among them. Here are the eleven behavioral patterns identified by the GoF:

1. **Chain of Responsibility Pattern**: Avoids coupling the sender of a request to its receiver by giving more than one object a chance to handle the request. It chains the receiving objects and passes the request along the chain until an object handles it.

2. **Command Pattern**: Encapsulates a request as an object, thereby allowing for parameterization of clients with queues, requests, and operations. It also provides support for undoable operations.

3. **Interpreter Pattern**: Provides a way to evaluate language grammar or expression. It is useful for designing a language interpreter or a compiler.

4. **Iterator Pattern**: Provides a way to access the elements of an aggregate object sequentially without exposing its underlying representation.

5. **Mediator Pattern**: Defines an object that encapsulates how a set of objects interact. It promotes loose coupling by keeping objects from referring to each other explicitly.

6. **Memento Pattern**: Captures and externalizes an object's internal state so that it can be restored later, without violating encapsulation.

7. **Observer Pattern**: Defines a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically.

8. **State Pattern**: Allows an object to alter its behavior when its internal state changes. The object will appear to change its class.

9. **Strategy Pattern**: Defines a family of algorithms, encapsulates each one, and makes them interchangeable. It lets the algorithm vary independently from clients that use it.

10. **Template Method Pattern**: Defines the skeleton of an algorithm in an operation, deferring some steps to subclasses. It lets subclasses redefine certain steps of an algorithm without changing the algorithm's structure.

11. **Visitor Pattern**: Represents an operation to be performed on the elements of an object structure. It lets you define a new operation without changing the classes of the elements on which it operates.

#### Practical Example: Observer Pattern in Java

The Observer pattern is commonly used in event-driven systems. Here's a simple implementation in Java:

```java
import java.util.ArrayList;
import java.util.List;

interface Observer {
    void update(String message);
}

class Subject {
    private List<Observer> observers = new ArrayList<>();

    public void addObserver(Observer observer) {
        observers.add(observer);
    }

    public void removeObserver(Observer observer) {
        observers.remove(observer);
    }

    public void notifyObservers(String message) {
        for (Observer observer : observers) {
            observer.update(message);
        }
    }
}

class ConcreteObserver implements Observer {
    private String name;

    public ConcreteObserver(String name) {
        this.name = name;
    }

    @Override
    public void update(String message) {
        System.out.println(name + " received message: " + message);
    }
}
```

### Applying GoF Patterns in Modern Software Development

While the GoF patterns were originally conceived for OOP, their principles can be adapted to other paradigms, including functional programming. In functional languages like Clojure, some patterns may be unnecessary or take a different form due to the language's inherent features, such as first-class functions and immutable data structures.

#### Adapting Patterns to Functional Programming

In Clojure, the need for certain patterns like Singleton or Factory diminishes because functions and closures can naturally encapsulate behavior and state. However, understanding these patterns is still valuable, as they provide insights into solving design problems and can guide the development of idiomatic functional solutions.

For example, the Strategy pattern can be implemented using higher-order functions in Clojure, where different strategies are simply passed as functions. Similarly, the Observer pattern can be reimagined using functional reactive programming (FRP) concepts, leveraging libraries like `core.async` for event handling.

### Conclusion

The Gang of Four design patterns have stood the test of time, providing a foundational framework for software design. They offer a common language for developers to communicate and solve complex design problems. While the patterns may evolve as programming paradigms shift, their core principles remain relevant, guiding developers in creating robust, maintainable, and scalable software systems.

By understanding these patterns and their applications, Java professionals transitioning to Clojure can leverage their existing knowledge while embracing the functional paradigm's unique strengths. This synthesis of OOP and functional programming concepts can lead to innovative solutions and a deeper appreciation of software design's art and science.

## Quiz Time!

{{< quizdown >}}

### Which of the following is a Creational pattern?

- [x] Singleton
- [ ] Adapter
- [ ] Observer
- [ ] Strategy

> **Explanation:** The Singleton pattern is a Creational pattern, focusing on object creation mechanisms.

### What is the primary purpose of Structural patterns?

- [ ] To manage object creation
- [x] To define object composition
- [ ] To encapsulate algorithms
- [ ] To handle object state

> **Explanation:** Structural patterns focus on the composition of classes or objects, defining how they are composed to form larger structures.

### Which pattern provides a way to access elements of an aggregate object sequentially?

- [ ] Command
- [ ] Mediator
- [x] Iterator
- [ ] Visitor

> **Explanation:** The Iterator pattern provides a way to access elements of an aggregate object sequentially without exposing its underlying representation.

### In which pattern does an object alter its behavior when its internal state changes?

- [ ] Observer
- [ ] Template Method
- [x] State
- [ ] Chain of Responsibility

> **Explanation:** The State pattern allows an object to alter its behavior when its internal state changes.

### Which pattern is used to define a family of algorithms and make them interchangeable?

- [ ] Singleton
- [ ] Decorator
- [x] Strategy
- [ ] Proxy

> **Explanation:** The Strategy pattern defines a family of algorithms, encapsulates each one, and makes them interchangeable.

### Which pattern provides a unified interface to a set of interfaces in a subsystem?

- [ ] Flyweight
- [ ] Composite
- [x] Facade
- [ ] Bridge

> **Explanation:** The Facade pattern provides a unified interface to a set of interfaces in a subsystem, simplifying its use.

### What is the main advantage of the Command pattern?

- [ ] It provides a way to access elements sequentially.
- [x] It encapsulates a request as an object.
- [ ] It defines a one-to-many dependency.
- [ ] It separates construction from representation.

> **Explanation:** The Command pattern encapsulates a request as an object, allowing for parameterization and queuing of requests.

### Which pattern uses sharing to support large numbers of fine-grained objects efficiently?

- [x] Flyweight
- [ ] Proxy
- [ ] Decorator
- [ ] Adapter

> **Explanation:** The Flyweight pattern uses sharing to support large numbers of fine-grained objects efficiently.

### Which pattern defines an object that encapsulates how a set of objects interact?

- [ ] Memento
- [x] Mediator
- [ ] Visitor
- [ ] Interpreter

> **Explanation:** The Mediator pattern defines an object that encapsulates how a set of objects interact, promoting loose coupling.

### True or False: The GoF patterns are only applicable to object-oriented programming.

- [ ] True
- [x] False

> **Explanation:** While the GoF patterns were originally conceived for OOP, their principles can be adapted to other paradigms, including functional programming.

{{< /quizdown >}}
