---
canonical: "https://clojureforjava.com/1/19/4/6"
title: "ClojureScript Routing and Navigation: Implementing Client-Side Routing in SPAs"
description: "Learn how to implement client-side routing in ClojureScript using libraries like Secretary and Bidi. Manage navigation within single-page applications, handle browser history, and support deep linking."
linkTitle: "19.4.6 Routing and Navigation"
tags:
- "Clojure"
- "ClojureScript"
- "Single-Page Applications"
- "Routing"
- "Navigation"
- "Secretary"
- "Bidi"
- "Frontend Development"
date: 2024-11-25
type: docs
nav_weight: 194600
license: "© 2024 Tokenizer Inc. CC BY-NC-SA 4.0"
---

## 19.4.6 Routing and Navigation

In the world of web development, single-page applications (SPAs) have become increasingly popular due to their ability to provide a seamless user experience. SPAs load a single HTML page and dynamically update the content as the user interacts with the application. This approach requires a robust client-side routing mechanism to manage navigation and maintain the application's state. In this section, we'll explore how to implement client-side routing in ClojureScript using libraries like Secretary and Bidi. We'll also discuss how to handle browser history and support deep linking.

### Understanding Client-Side Routing

Client-side routing is the process of managing the navigation within a web application without reloading the entire page. This is crucial for SPAs, where the goal is to provide a fluid user experience by updating only the necessary parts of the page. In traditional multi-page applications, navigation is handled by the server, which serves different HTML pages for each route. In contrast, SPAs use JavaScript to manage routes and update the view accordingly.

#### Key Concepts of Client-Side Routing

- **Routes**: Define the different paths or URLs that the application can navigate to.
- **Router**: A mechanism that listens for changes in the URL and updates the view based on the current route.
- **History Management**: The ability to navigate back and forth between routes using the browser's back and forward buttons.
- **Deep Linking**: The ability to link directly to a specific view or state within the application.

### Implementing Routing with Secretary

Secretary is a popular routing library for ClojureScript that provides a simple and declarative way to define routes. It integrates well with Reagent, a ClojureScript interface to React, making it a great choice for building SPAs.

#### Setting Up Secretary

To get started with Secretary, you'll need to add it to your project dependencies. Here's how you can do that in your `project.clj` file:

```clojure
(defproject my-app "0.1.0-SNAPSHOT"
  :dependencies [[org.clojure/clojure "1.10.3"]
                 [org.clojure/clojurescript "1.10.844"]
                 [reagent "1.1.0"]
                 [secretary "1.2.3"]])
```

#### Defining Routes with Secretary

Secretary allows you to define routes using the `defroute` macro. Each route is associated with a handler function that is called when the route is activated. Here's an example of how to define some basic routes:

```clojure
(ns my-app.core
  (:require [reagent.core :as reagent]
            [secretary.core :as secretary :refer-macros [defroute]]))

(defn home-page []
  [:div "Welcome to the Home Page!"])

(defn about-page []
  [:div "Learn more About Us."])

(defn contact-page []
  [:div "Contact Us here."])

(defroute "/" []
  (reagent/render [home-page] (.getElementById js/document "app")))

(defroute "/about" []
  (reagent/render [about-page] (.getElementById js/document "app")))

(defroute "/contact" []
  (reagent/render [contact-page] (.getElementById js/document "app")))
```

In this example, we define three routes: the home page, about page, and contact page. Each route is associated with a Reagent component that renders the corresponding view.

#### Handling Navigation

To handle navigation, you'll need to set up a listener for changes in the URL. Secretary provides a `dispatch!` function that you can call whenever the URL changes. Here's how you can set it up:

```clojure
(defn hook-browser-navigation! []
  (doto (.-history js/window)
    (.addEventListener "popstate" #(secretary/dispatch! (.-pathname js/location)))))

(defn init []
  (hook-browser-navigation!)
  (secretary/dispatch! (.-pathname js/location)))
```

The `hook-browser-navigation!` function sets up an event listener for the `popstate` event, which is triggered when the user navigates using the browser's back and forward buttons. The `init` function initializes the application by dispatching the current URL.

### Managing Browser History

Managing browser history is crucial for SPAs to ensure that users can navigate back and forth between views. Secretary leverages the HTML5 History API to manage browser history. This API allows you to manipulate the browser's history stack without reloading the page.

#### Using the History API

The History API provides two main methods for managing history:

- `pushState`: Adds a new entry to the history stack.
- `replaceState`: Modifies the current entry in the history stack.

Secretary automatically uses `pushState` when navigating to a new route. If you need to modify the current route without adding a new entry, you can use `replaceState`.

### Supporting Deep Linking

Deep linking allows users to link directly to a specific view or state within the application. This is important for SPAs to ensure that users can bookmark and share URLs that point to specific content.

#### Implementing Deep Linking

Secretary supports deep linking out of the box. When a user navigates to a URL, Secretary will automatically dispatch the corresponding route and render the appropriate view. This ensures that the application is in the correct state when the page is loaded.

### Implementing Routing with Bidi

Bidi is another routing library for ClojureScript that provides a more data-driven approach to defining routes. It allows you to define routes as data structures, making it easy to manipulate and reason about them.

#### Setting Up Bidi

To use Bidi, you'll need to add it to your project dependencies:

```clojure
(defproject my-app "0.1.0-SNAPSHOT"
  :dependencies [[org.clojure/clojure "1.10.3"]
                 [org.clojure/clojurescript "1.10.844"]
                 [reagent "1.1.0"]
                 [bidi "2.1.6"]])
```

#### Defining Routes with Bidi

Bidi allows you to define routes as nested vectors, where each route is associated with a handler function. Here's an example of how to define routes with Bidi:

```clojure
(ns my-app.core
  (:require [reagent.core :as reagent]
            [bidi.bidi :as bidi]
            [bidi.ring :as ring]))

(def routes
  ["/" {"about" :about
        "contact" :contact
        "" :home}])

(defn home-page []
  [:div "Welcome to the Home Page!"])

(defn about-page []
  [:div "Learn more About Us."])

(defn contact-page []
  [:div "Contact Us here."])

(defn handler [route]
  (case route
    :home (reagent/render [home-page] (.getElementById js/document "app"))
    :about (reagent/render [about-page] (.getElementById js/document "app"))
    :contact (reagent/render [contact-page] (.getElementById js/document "app"))))

(defn init []
  (let [current-route (bidi/match-route routes (.-pathname js/location))]
    (handler (:handler current-route))))
```

In this example, we define routes as a nested vector, where each route is associated with a keyword. The `handler` function renders the appropriate view based on the current route.

#### Handling Navigation with Bidi

To handle navigation with Bidi, you'll need to set up a listener for changes in the URL and dispatch the corresponding route. Here's how you can do that:

```clojure
(defn hook-browser-navigation! []
  (doto (.-history js/window)
    (.addEventListener "popstate" #(let [current-route (bidi/match-route routes (.-pathname js/location))]
                                     (handler (:handler current-route))))))

(defn navigate! [path]
  (.pushState (.-history js/window) nil "" path)
  (let [current-route (bidi/match-route routes path)]
    (handler (:handler current-route))))

(defn init []
  (hook-browser-navigation!)
  (navigate! (.-pathname js/location)))
```

The `navigate!` function updates the URL and dispatches the corresponding route. The `hook-browser-navigation!` function sets up an event listener for the `popstate` event to handle browser navigation.

### Comparing Secretary and Bidi

Both Secretary and Bidi are powerful routing libraries for ClojureScript, but they have different approaches to defining routes. Secretary uses a more declarative approach with macros, while Bidi uses a data-driven approach with nested vectors. The choice between the two depends on your preference and the complexity of your routing needs.

#### Key Differences

- **Declarative vs. Data-Driven**: Secretary uses macros to define routes, while Bidi uses data structures.
- **Integration with Reagent**: Secretary integrates seamlessly with Reagent, making it a popular choice for Reagent-based applications.
- **Flexibility**: Bidi's data-driven approach provides more flexibility for complex routing scenarios.

### Best Practices for Routing and Navigation

When implementing routing and navigation in a ClojureScript application, consider the following best practices:

- **Keep Routes Simple**: Define routes that are easy to understand and maintain. Avoid overly complex route definitions.
- **Use Named Routes**: Use named routes to make it easier to refer to routes throughout your application.
- **Handle 404s Gracefully**: Provide a fallback route or component to handle unknown routes gracefully.
- **Test Your Routes**: Ensure that your routes work as expected by writing tests for your routing logic.

### Try It Yourself

Now that we've explored how to implement routing and navigation in ClojureScript, try modifying the code examples to add new routes or change the existing ones. Experiment with both Secretary and Bidi to see which approach works best for your application.

### Exercises

1. **Add a New Route**: Add a new route to the Secretary example for a "Services" page. Create a corresponding Reagent component to render the view.
2. **Implement Deep Linking**: Modify the Bidi example to support deep linking for a specific section within the "About" page.
3. **Handle 404s**: Implement a 404 page in both the Secretary and Bidi examples to handle unknown routes gracefully.

### Summary and Key Takeaways

In this section, we've explored how to implement client-side routing in ClojureScript using Secretary and Bidi. We've discussed how to manage navigation within SPAs, handle browser history, and support deep linking. By following the best practices outlined in this section, you can create a seamless and intuitive navigation experience for your users.

---

## Quiz: Mastering ClojureScript Routing and Navigation

{{< quizdown >}}

### What is the primary purpose of client-side routing in SPAs?

- [x] To manage navigation without reloading the entire page
- [ ] To handle server-side requests
- [ ] To improve server performance
- [ ] To manage database connections

> **Explanation:** Client-side routing allows SPAs to manage navigation and update views without reloading the entire page, providing a seamless user experience.

### Which library provides a declarative way to define routes in ClojureScript?

- [x] Secretary
- [ ] Bidi
- [ ] Reagent
- [ ] React

> **Explanation:** Secretary provides a declarative way to define routes using macros, making it easy to manage navigation in ClojureScript applications.

### How does Secretary handle browser history?

- [x] By using the HTML5 History API
- [ ] By storing history in local storage
- [ ] By using cookies
- [ ] By creating a custom history object

> **Explanation:** Secretary leverages the HTML5 History API to manage browser history, allowing users to navigate back and forth between views.

### What is deep linking in the context of SPAs?

- [x] Linking directly to a specific view or state within the application
- [ ] Linking to external websites
- [ ] Linking to the homepage
- [ ] Linking to a database entry

> **Explanation:** Deep linking allows users to link directly to a specific view or state within the application, ensuring that the application is in the correct state when the page is loaded.

### Which method is used to add a new entry to the browser's history stack?

- [x] pushState
- [ ] replaceState
- [ ] addState
- [ ] updateState

> **Explanation:** The `pushState` method is used to add a new entry to the browser's history stack, allowing for navigation without reloading the page.

### What is a key difference between Secretary and Bidi?

- [x] Secretary uses macros, while Bidi uses data structures
- [ ] Secretary is only for server-side routing
- [ ] Bidi is not compatible with Reagent
- [ ] Bidi does not support deep linking

> **Explanation:** Secretary uses macros to define routes, while Bidi uses a data-driven approach with nested vectors, providing different ways to manage routing.

### How can you handle unknown routes gracefully in a ClojureScript application?

- [x] By providing a fallback route or component
- [ ] By ignoring the route
- [ ] By redirecting to the homepage
- [ ] By logging an error

> **Explanation:** Providing a fallback route or component allows you to handle unknown routes gracefully, improving the user experience.

### What is the purpose of the `navigate!` function in the Bidi example?

- [x] To update the URL and dispatch the corresponding route
- [ ] To initialize the application
- [ ] To render the homepage
- [ ] To log navigation events

> **Explanation:** The `navigate!` function updates the URL and dispatches the corresponding route, ensuring that the correct view is rendered.

### Which of the following is a best practice for routing in ClojureScript?

- [x] Use named routes for easier reference
- [ ] Define routes in multiple files
- [ ] Avoid testing routes
- [ ] Use complex route definitions

> **Explanation:** Using named routes makes it easier to refer to routes throughout your application, improving maintainability.

### True or False: Bidi integrates seamlessly with Reagent.

- [x] True
- [ ] False

> **Explanation:** Bidi integrates well with Reagent, providing a flexible and data-driven approach to routing in ClojureScript applications.

{{< /quizdown >}}
