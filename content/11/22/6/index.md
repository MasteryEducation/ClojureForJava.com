---
canonical: "https://clojureforjava.com/11/22/6"
title: "ClojureScript Frontend Development with Reagent and Re-frame"
description: "Explore how to build Single-Page Applications (SPAs) using Reagent and Re-frame in ClojureScript, leveraging functional programming principles for efficient and scalable frontend development."
linkTitle: "22.6 Frontend Development with Reagent and Re-frame"
tags:
- "Clojure"
- "ClojureScript"
- "Reagent"
- "Re-frame"
- "Frontend Development"
- "Single-Page Applications"
- "Functional Programming"
- "State Management"
date: 2024-11-25
type: docs
nav_weight: 226000
license: "© 2024 Tokenizer Inc. CC BY-NC-SA 4.0"
---

## 22.6 Frontend Development with `Reagent` and `Re-frame`

In the world of web development, Single-Page Applications (SPAs) have become increasingly popular due to their ability to provide a seamless user experience. As experienced Java developers, you may be familiar with frameworks like Angular, React, or Vue.js for building SPAs. However, ClojureScript offers a unique approach to frontend development through its functional programming paradigm. In this section, we will explore how to build SPAs using `Reagent` and `Re-frame`, two powerful libraries in the ClojureScript ecosystem.

### Single-Page Applications (SPAs)

SPAs are web applications that load a single HTML page and dynamically update the content as the user interacts with the app. This approach provides a more fluid user experience compared to traditional multi-page applications, where each interaction requires a full page reload.

**ClojureScript and SPAs**: ClojureScript is a variant of Clojure that compiles to JavaScript, allowing you to leverage the power of functional programming on the frontend. By using immutable data structures and pure functions, ClojureScript enables you to build robust and maintainable SPAs.

### `Reagent` Basics

`Reagent` is a minimalistic interface to React, designed to take advantage of ClojureScript's functional programming features. It allows you to create React components using ClojureScript's syntax and data structures.

#### Key Concepts of `Reagent`

- **Components**: In `Reagent`, components are functions that return hiccup-style data structures representing HTML. This is similar to React components in JavaScript, but with the added benefit of ClojureScript's immutability and expressiveness.

- **Reactive Atoms**: `Reagent` uses reactive atoms to manage state. Atoms are mutable references that hold a value and notify components when the value changes, triggering a re-render.

- **Hiccup Syntax**: `Reagent` uses hiccup syntax to define HTML. This syntax is concise and leverages Clojure's data structures, making it easy to compose and manipulate UI elements.

#### Creating a Simple `Reagent` Component

Let's start by creating a simple `Reagent` component that displays a greeting message.

```clojure
(ns my-app.core
  (:require [reagent.core :as r]))

(defn greeting []
  [:div
   [:h1 "Hello, ClojureScript!"]])

(defn mount-root []
  (r/render [greeting]
            (.getElementById js/document "app")))

(defn init []
  (mount-root))
```

In this example, we define a `greeting` component using a function that returns a hiccup-style vector. The `mount-root` function renders the component into the DOM.

#### Try It Yourself

Experiment with modifying the `greeting` component to display a personalized message. Try adding an input field and a button to update the message dynamically.

### State Management with `Re-frame`

As your application grows in complexity, managing state becomes crucial. `Re-frame` is a framework built on top of `Reagent` that provides a structured approach to state management using unidirectional data flow.

#### Key Concepts of `Re-frame`

- **Events**: In `Re-frame`, events are used to describe user interactions or other changes in the application. Events are dispatched to trigger state updates.

- **Subscriptions**: Subscriptions allow components to access the application state. They define how components derive data from the global state.

- **Effects and Coeffects**: Effects are actions that modify the state or interact with the outside world. Coeffects represent the context in which an event handler operates.

- **Unidirectional Data Flow**: `Re-frame` enforces a unidirectional data flow, where data flows in a single direction: from events to state updates to UI rendering.

#### Setting Up a `Re-frame` Application

To demonstrate `Re-frame`, let's build a simple counter application.

```clojure
(ns my-app.core
  (:require [re-frame.core :as rf]
            [reagent.core :as r]))

;; Define the initial state
(def default-db
  {:counter 0})

;; Define an event to increment the counter
(rf/reg-event-db
 :increment-counter
 (fn [db _]
   (update db :counter inc)))

;; Define a subscription to access the counter value
(rf/reg-sub
 :counter
 (fn [db _]
   (:counter db)))

;; Define the main component
(defn counter []
  (let [counter (rf/subscribe [:counter])]
    (fn []
      [:div
       [:h1 "Counter: " @counter]
       [:button {:on-click #(rf/dispatch [:increment-counter])}
        "Increment"]])))

(defn mount-root []
  (r/render [counter]
            (.getElementById js/document "app")))

(defn init []
  (rf/dispatch-sync [:initialize-db])
  (mount-root))
```

In this example, we define an event `:increment-counter` to update the counter value and a subscription `:counter` to access the counter value in the component. The `counter` component subscribes to the counter value and dispatches the `:increment-counter` event when the button is clicked.

#### Try It Yourself

Modify the counter application to include a decrement button. Add a reset button to set the counter back to zero.

### Side Effects Handling

Managing side effects is a critical aspect of building SPAs. `Re-frame` provides a robust mechanism for handling side effects through events and effects handlers.

#### Handling Side Effects with `Re-frame`

- **Effects Handlers**: Effects handlers are responsible for executing side effects, such as making HTTP requests or updating the local storage.

- **Event Handlers**: Event handlers define how events are processed and how they affect the application state.

#### Example: Fetching Data from an API

Let's extend our counter application to fetch data from an API and update the counter.

```clojure
(ns my-app.core
  (:require [re-frame.core :as rf]
            [reagent.core :as r]
            [ajax.core :refer [GET]]))

;; Define an event to fetch data from an API
(rf/reg-event-fx
 :fetch-counter
 (fn [_ _]
   {:http-xhrio {:method          :get
                 :uri             "https://api.example.com/counter"
                 :response-format (ajax/json-response-format {:keywords? true})
                 :on-success      [:fetch-counter-success]
                 :on-failure      [:fetch-counter-failure]}}))

;; Define an event to handle successful API response
(rf/reg-event-db
 :fetch-counter-success
 (fn [db [_ response]]
   (assoc db :counter (:counter response))))

;; Define an event to handle API failure
(rf/reg-event-db
 :fetch-counter-failure
 (fn [db _]
   (assoc db :error "Failed to fetch counter")))

;; Define the main component
(defn counter []
  (let [counter (rf/subscribe [:counter])]
    (fn []
      [:div
       [:h1 "Counter: " @counter]
       [:button {:on-click #(rf/dispatch [:fetch-counter])}
        "Fetch Counter"]])))

(defn mount-root []
  (r/render [counter]
            (.getElementById js/document "app")))

(defn init []
  (rf/dispatch-sync [:initialize-db])
  (mount-root))
```

In this example, we define an event `:fetch-counter` to fetch data from an API. The `:fetch-counter-success` and `:fetch-counter-failure` events handle the API response and update the state accordingly.

#### Try It Yourself

Experiment with different APIs and modify the application to display additional data, such as a list of items or user profiles.

### Developing a SPA

Now that we have explored the basics of `Reagent` and `Re-frame`, let's build a more comprehensive SPA. We will create a task manager application that allows users to add, edit, and delete tasks.

#### Application Structure

Our task manager application will consist of the following components:

- **Task List**: Displays a list of tasks.
- **Task Form**: Allows users to add or edit tasks.
- **Task Item**: Represents a single task with options to edit or delete.

#### Implementing the Task Manager

```clojure
(ns my-app.core
  (:require [re-frame.core :as rf]
            [reagent.core :as r]))

;; Define the initial state
(def default-db
  {:tasks []})

;; Define an event to add a task
(rf/reg-event-db
 :add-task
 (fn [db [_ task]]
   (update db :tasks conj task)))

;; Define an event to remove a task
(rf/reg-event-db
 :remove-task
 (fn [db [_ task-id]]
   (update db :tasks #(remove (fn [task] (= (:id task) task-id)) %))))

;; Define a subscription to access the tasks
(rf/reg-sub
 :tasks
 (fn [db _]
   (:tasks db)))

;; Define the task item component
(defn task-item [task]
  [:li
   [:span (:name task)]
   [:button {:on-click #(rf/dispatch [:remove-task (:id task)])} "Delete"]])

;; Define the task list component
(defn task-list []
  (let [tasks (rf/subscribe [:tasks])]
    (fn []
      [:ul
       (for [task @tasks]
         ^{:key (:id task)} [task-item task])])))

;; Define the task form component
(defn task-form []
  (let [task-name (r/atom "")]
    (fn []
      [:div
       [:input {:type "text"
                :value @task-name
                :on-change #(reset! task-name (-> % .-target .-value))}]
       [:button {:on-click #(do
                              (rf/dispatch [:add-task {:id (random-uuid) :name @task-name}])
                              (reset! task-name ""))}
        "Add Task"]])))

;; Define the main component
(defn task-manager []
  [:div
   [task-form]
   [task-list]])

(defn mount-root []
  (r/render [task-manager]
            (.getElementById js/document "app")))

(defn init []
  (rf/dispatch-sync [:initialize-db])
  (mount-root))
```

In this example, we define events to add and remove tasks, subscriptions to access the tasks, and components to display and manage tasks.

#### Try It Yourself

Enhance the task manager by adding features such as task editing, task completion status, and filtering tasks based on their status.

### Conclusion

In this section, we explored how to build SPAs using `Reagent` and `Re-frame` in ClojureScript. We learned about the basics of `Reagent`, state management with `Re-frame`, handling side effects, and developing a comprehensive SPA. By leveraging ClojureScript's functional programming paradigm, you can create efficient and scalable frontend applications.

### Knowledge Check

Now that we've covered the essentials of frontend development with `Reagent` and `Re-frame`, let's test your understanding with a quiz.

## Quiz: Mastering Frontend Development with Reagent and Re-frame

{{< quizdown >}}

### What is the primary advantage of using ClojureScript for frontend development?

- [x] Leveraging functional programming principles
- [ ] Simplifying HTML and CSS
- [ ] Reducing JavaScript code size
- [ ] Enhancing browser compatibility

> **Explanation:** ClojureScript allows developers to leverage functional programming principles, such as immutability and pure functions, for building robust and maintainable frontend applications.

### Which library provides a minimalistic interface to React in ClojureScript?

- [x] Reagent
- [ ] Re-frame
- [ ] Redux
- [ ] Angular

> **Explanation:** Reagent is a minimalistic interface to React, designed to take advantage of ClojureScript's functional programming features.

### In Re-frame, what is the purpose of subscriptions?

- [x] To access the application state
- [ ] To dispatch events
- [ ] To handle side effects
- [ ] To define components

> **Explanation:** Subscriptions in Re-frame allow components to access the application state and derive data from the global state.

### How does Re-frame handle side effects?

- [x] Through events and effects handlers
- [ ] By using promises
- [ ] By directly modifying the DOM
- [ ] Through synchronous functions

> **Explanation:** Re-frame handles side effects through events and effects handlers, which define how events are processed and how they affect the application state.

### What is the primary benefit of unidirectional data flow in Re-frame?

- [x] Simplified state management
- [ ] Faster rendering
- [ ] Reduced code complexity
- [ ] Enhanced styling capabilities

> **Explanation:** Unidirectional data flow simplifies state management by ensuring that data flows in a single direction, making it easier to track changes and debug the application.

### Which component in the task manager application is responsible for displaying a list of tasks?

- [x] task-list
- [ ] task-form
- [ ] task-item
- [ ] task-manager

> **Explanation:** The task-list component is responsible for displaying a list of tasks in the task manager application.

### How can you modify the counter application to include a decrement button?

- [x] By defining a new event to decrement the counter
- [ ] By modifying the existing increment event
- [ ] By changing the subscription logic
- [ ] By adding a new component

> **Explanation:** To include a decrement button, you need to define a new event that decrements the counter value and dispatch it when the button is clicked.

### What is the role of reactive atoms in Reagent?

- [x] To manage state and trigger re-renders
- [ ] To define components
- [ ] To handle side effects
- [ ] To perform asynchronous operations

> **Explanation:** Reactive atoms in Reagent are used to manage state and trigger re-renders when the state changes.

### Which syntax does Reagent use to define HTML?

- [x] Hiccup syntax
- [ ] JSX syntax
- [ ] XML syntax
- [ ] JSON syntax

> **Explanation:** Reagent uses hiccup syntax to define HTML, which is concise and leverages Clojure's data structures.

### True or False: Re-frame enforces a bidirectional data flow.

- [ ] True
- [x] False

> **Explanation:** False. Re-frame enforces a unidirectional data flow, where data flows in a single direction from events to state updates to UI rendering.

{{< /quizdown >}}

By mastering `Reagent` and `Re-frame`, you can harness the power of ClojureScript to build efficient and scalable SPAs. Keep experimenting with different features and libraries in the ClojureScript ecosystem to further enhance your frontend development skills.
