---
canonical: "https://clojureforjava.com/1/19/4/3"
title: "Building User Interfaces with Reagent: A ClojureScript Guide"
description: "Learn how to build dynamic user interfaces using Reagent, a ClojureScript interface to React. Explore component creation, state management, and lifecycle events."
linkTitle: "19.4.3 Building the User Interface with Reagent"
tags:
- "Clojure"
- "ClojureScript"
- "Reagent"
- "React"
- "Frontend Development"
- "Functional Programming"
- "Web Development"
- "User Interface"
date: 2024-11-25
type: docs
nav_weight: 194300
license: "© 2024 Tokenizer Inc. CC BY-NC-SA 4.0"
---

## 19.4.3 Building the User Interface with Reagent

In this section, we will explore how to build a dynamic and responsive user interface using Reagent, a minimalistic ClojureScript interface to React. Reagent leverages the power of React while allowing developers to write components in ClojureScript using a syntax called hiccup. We'll cover creating components, managing state with Reagent atoms, and handling component lifecycle events. This guide is designed for experienced Java developers transitioning to Clojure, so we'll draw parallels between Java and Clojure concepts where appropriate.

### Introduction to Reagent

Reagent is a ClojureScript library that provides a simple and efficient way to build React components. It allows developers to write components using ClojureScript, offering a more concise and expressive syntax compared to JavaScript. Reagent's use of hiccup syntax makes it easy to define HTML-like structures directly in ClojureScript.

#### Why Use Reagent?

- **Simplicity**: Reagent's syntax is straightforward, making it easy to learn and use.
- **Performance**: Reagent leverages React's virtual DOM for efficient rendering.
- **Functional Programming**: Reagent encourages a functional approach to UI development, aligning with Clojure's philosophy.
- **Interoperability**: Reagent can interoperate with existing React components and libraries.

### Creating Components with Hiccup Syntax

In Reagent, components are defined using hiccup syntax, which is a Clojure data structure that represents HTML. This syntax allows you to write HTML-like code directly in ClojureScript.

#### Basic Component Example

Let's start by creating a simple Reagent component that displays a greeting message.

```clojure
(ns my-app.core
  (:require [reagent.core :as r]))

(defn greeting []
  [:div
   [:h1 "Hello, Clojure!"]])

(defn mount-root []
  (r/render [greeting]
            (.getElementById js/document "app")))

(defn init []
  (mount-root))
```

**Explanation:**

- **Namespace Declaration**: We declare a namespace `my-app.core` and require `reagent.core` as `r`.
- **Component Definition**: The `greeting` function returns a hiccup vector representing a `div` with an `h1` element.
- **Rendering**: The `mount-root` function renders the `greeting` component into the DOM element with the ID "app".
- **Initialization**: The `init` function is called to start the application.

#### Try It Yourself

Modify the `greeting` component to display a personalized message. Try adding more HTML elements, such as a paragraph or a list.

### Handling State with Reagent Atoms

State management is a crucial aspect of building interactive user interfaces. Reagent provides a simple way to manage state using atoms, which are mutable references to immutable values.

#### Stateful Component Example

Let's create a component that displays a counter and allows the user to increment it.

```clojure
(defn counter []
  (let [count (r/atom 0)]
    (fn []
      [:div
       [:p "Current count: " @count]
       [:button {:on-click #(swap! count inc)} "Increment"]])))

(defn mount-root []
  (r/render [counter]
            (.getElementById js/document "app")))
```

**Explanation:**

- **Atom Creation**: We create an atom `count` initialized to `0`.
- **Dereferencing**: We use `@count` to dereference the atom and get its current value.
- **State Update**: The `swap!` function is used to update the atom's value when the button is clicked.

#### Try It Yourself

Experiment with the counter component by adding a decrement button. Use the `reset!` function to add a button that resets the counter to zero.

### Managing Component Lifecycle Events

Reagent components can respond to lifecycle events, similar to React components. This allows you to perform actions at specific points in a component's lifecycle.

#### Lifecycle Example

Let's create a component that logs messages to the console when it mounts and unmounts.

```clojure
(defn lifecycle-demo []
  (r/create-class
   {:component-did-mount
    (fn [] (js/console.log "Component mounted"))

    :component-will-unmount
    (fn [] (js/console.log "Component will unmount"))

    :reagent-render
    (fn []
      [:div "Check the console for lifecycle messages"])}))

(defn mount-root []
  (r/render [lifecycle-demo]
            (.getElementById js/document "app")))
```

**Explanation:**

- **Lifecycle Methods**: We define `:component-did-mount` and `:component-will-unmount` to log messages when the component mounts and unmounts.
- **Reagent Render**: The `:reagent-render` function defines the component's UI.

#### Try It Yourself

Add more lifecycle methods, such as `:component-did-update`, to log messages when the component updates. Experiment with different lifecycle events to see how they work.

### Comparing Reagent with Java

In Java, building a user interface typically involves using libraries like JavaFX or Swing. These libraries require a more verbose syntax and imperative approach compared to Reagent's functional style.

#### JavaFX Example

Here's a simple JavaFX example that creates a window with a button:

```java
import javafx.application.Application;
import javafx.scene.Scene;
import javafx.scene.control.Button;
import javafx.scene.layout.StackPane;
import javafx.stage.Stage;

public class HelloWorld extends Application {
    @Override
    public void start(Stage primaryStage) {
        Button btn = new Button();
        btn.setText("Say 'Hello World'");
        btn.setOnAction(event -> System.out.println("Hello World"));

        StackPane root = new StackPane();
        root.getChildren().add(btn);

        Scene scene = new Scene(root, 300, 250);

        primaryStage.setTitle("Hello World!");
        primaryStage.setScene(scene);
        primaryStage.show();
    }

    public static void main(String[] args) {
        launch(args);
    }
}
```

**Comparison:**

- **Syntax**: Reagent's hiccup syntax is more concise and expressive than JavaFX's imperative style.
- **State Management**: Reagent uses atoms for state management, while JavaFX uses properties and listeners.
- **Lifecycle**: Reagent components have lifecycle methods similar to React, while JavaFX uses event handlers.

### Advanced Reagent Concepts

#### Component Composition

Reagent allows you to compose components by nesting them within each other. This promotes code reuse and modularity.

```clojure
(defn button [label on-click]
  [:button {:on-click on-click} label])

(defn app []
  [:div
   [button "Click me" #(js/alert "Button clicked!")]])
```

**Explanation:**

- **Reusable Components**: The `button` component is reusable and can be used with different labels and click handlers.
- **Composition**: The `app` component composes the `button` component within a `div`.

#### Conditional Rendering

You can conditionally render components based on state or props.

```clojure
(defn conditional-render [show?]
  (fn []
    [:div
     (when show?
       [:p "This text is conditionally rendered"])]))
```

**Explanation:**

- **Conditional Logic**: The `when` function is used to conditionally render a paragraph based on the `show?` argument.

### Exercises and Practice Problems

1. **Create a Todo List**: Build a simple todo list application using Reagent. Allow users to add, remove, and mark tasks as complete.
2. **Form Handling**: Create a form with input fields and a submit button. Use Reagent atoms to manage form state and display submitted data.
3. **Component Lifecycle**: Implement a component that fetches data from an API when it mounts and displays a loading spinner until the data is loaded.

### Key Takeaways

- **Reagent** provides a simple and efficient way to build React components using ClojureScript.
- **Hiccup Syntax** allows you to write HTML-like structures directly in ClojureScript.
- **State Management** is handled using Reagent atoms, providing a functional approach to managing state.
- **Lifecycle Methods** enable components to respond to lifecycle events, similar to React components.
- **Component Composition** promotes code reuse and modularity.

### Further Reading

- [Reagent Documentation](https://reagent-project.github.io/)
- [ClojureScript Documentation](https://clojurescript.org/)
- [React Documentation](https://reactjs.org/)

Now that we've explored how to build user interfaces with Reagent, let's apply these concepts to create dynamic and interactive web applications.

## Reagent and ClojureScript Quiz: Test Your Knowledge

{{< quizdown >}}

### What is Reagent in the context of ClojureScript?

- [x] A minimalistic ClojureScript interface to React
- [ ] A JavaScript library for building user interfaces
- [ ] A Clojure library for backend development
- [ ] A tool for managing Clojure dependencies

> **Explanation:** Reagent is a ClojureScript library that provides a simple interface to React, allowing developers to build user interfaces using ClojureScript.

### How does Reagent manage state in components?

- [x] Using atoms
- [ ] Using JavaScript objects
- [ ] Using global variables
- [ ] Using session storage

> **Explanation:** Reagent uses atoms to manage state in components, providing a functional approach to state management.

### What syntax does Reagent use to define components?

- [x] Hiccup syntax
- [ ] JSX syntax
- [ ] XML syntax
- [ ] JSON syntax

> **Explanation:** Reagent uses hiccup syntax, which is a Clojure data structure that represents HTML, to define components.

### Which function is used to render a Reagent component into the DOM?

- [x] `r/render`
- [ ] `r/mount`
- [ ] `r/display`
- [ ] `r/show`

> **Explanation:** The `r/render` function is used to render a Reagent component into the DOM.

### What is the purpose of lifecycle methods in Reagent components?

- [x] To perform actions at specific points in a component's lifecycle
- [ ] To define the initial state of a component
- [ ] To handle user interactions
- [ ] To manage component styles

> **Explanation:** Lifecycle methods in Reagent components allow developers to perform actions at specific points in a component's lifecycle, such as when it mounts or unmounts.

### How can you conditionally render components in Reagent?

- [x] Using the `when` function
- [ ] Using the `if` statement
- [ ] Using the `switch` statement
- [ ] Using the `case` statement

> **Explanation:** The `when` function is used in Reagent to conditionally render components based on state or props.

### What is the benefit of component composition in Reagent?

- [x] It promotes code reuse and modularity
- [ ] It simplifies state management
- [ ] It enhances performance
- [ ] It reduces the need for lifecycle methods

> **Explanation:** Component composition in Reagent promotes code reuse and modularity by allowing developers to nest components within each other.

### Which of the following is a common use case for Reagent?

- [x] Building dynamic user interfaces
- [ ] Managing server-side state
- [ ] Performing data analysis
- [ ] Compiling Clojure code

> **Explanation:** Reagent is commonly used for building dynamic user interfaces in web applications.

### How does Reagent compare to JavaFX in terms of syntax?

- [x] Reagent's syntax is more concise and expressive
- [ ] Reagent's syntax is more verbose
- [ ] Reagent's syntax is similar to JavaFX
- [ ] Reagent's syntax is identical to JavaFX

> **Explanation:** Reagent's syntax, using hiccup, is more concise and expressive compared to JavaFX's imperative style.

### True or False: Reagent can interoperate with existing React components and libraries.

- [x] True
- [ ] False

> **Explanation:** Reagent can interoperate with existing React components and libraries, allowing developers to leverage the React ecosystem.

{{< /quizdown >}}
