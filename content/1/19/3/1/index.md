---
canonical: "https://clojureforjava.com/1/19/3/1"
title: "Setting Up the Web Server with Clojure: A Guide for Java Developers"
description: "Learn how to set up a web server in Clojure using frameworks like Ring and Pedestal. This guide covers defining the application's entry point, configuring the server, and implementing middleware for logging, session management, and security."
linkTitle: "19.3.1 Setting Up the Web Server"
tags:
- "Clojure"
- "Web Development"
- "Ring"
- "Pedestal"
- "Middleware"
- "Java Interoperability"
- "Functional Programming"
- "Server Configuration"
date: 2024-11-25
type: docs
nav_weight: 193100
license: "© 2024 Tokenizer Inc. CC BY-NC-SA 4.0"
---

## 19.3.1 Setting Up the Web Server

In this section, we'll explore how to set up a web server in Clojure, focusing on frameworks like **Ring** and **Pedestal**. As experienced Java developers, you'll find parallels between Java's servlet-based web applications and Clojure's functional approach to handling HTTP requests. We'll guide you through defining the application's entry point, configuring the server, and implementing middleware for tasks such as logging, session management, and security.

### Introduction to Clojure Web Servers

Clojure's web development ecosystem is built on the foundation of functional programming principles, offering a unique approach compared to traditional Java web servers. **Ring** is a popular library that provides a simple and composable way to handle HTTP requests and responses. **Pedestal** builds on Ring, offering additional features for building robust web applications.

#### Why Use Clojure for Web Servers?

- **Immutability**: Clojure's immutable data structures simplify concurrent request handling.
- **Simplicity**: The functional approach reduces boilerplate code, making applications easier to maintain.
- **Interoperability**: Seamless integration with Java libraries allows leveraging existing Java code.

### Setting Up a Basic Web Server with Ring

**Ring** is a Clojure library that abstracts the HTTP protocol, allowing developers to focus on application logic. It uses a simple handler function to process requests and generate responses.

#### Step 1: Define the Application's Entry Point

First, let's create a basic Ring handler. A handler is a function that takes a request map and returns a response map.

```clojure
(ns my-app.core
  (:require [ring.adapter.jetty :refer [run-jetty]]))

(defn handler [request]
  {:status 200
   :headers {"Content-Type" "text/plain"}
   :body "Hello, World!"})

(defn -main []
  (run-jetty handler {:port 3000}))
```

**Explanation**:
- **`handler`**: A simple function that returns a response with a status code, headers, and body.
- **`run-jetty`**: A function from Ring's Jetty adapter to start the server.
- **`-main`**: The entry point of the application, starting the server on port 3000.

#### Step 2: Configure the Server

To configure the server, we use the `run-jetty` function, which accepts a handler and an options map. Here, we specify the port number.

```clojure
(run-jetty handler {:port 3000 :join? false})
```

**Note**: The `:join? false` option allows the server to run in a non-blocking manner, useful for REPL-driven development.

#### Step 3: Verify the Server is Running

Start the server by running the `-main` function. Open a web browser and navigate to `http://localhost:3000`. You should see "Hello, World!" displayed.

### Middleware Configuration

Middleware in Ring is a higher-order function that wraps a handler to add additional functionality, such as logging, session management, or security headers.

#### Adding Logging Middleware

Let's add logging to our server to track incoming requests.

```clojure
(ns my-app.middleware
  (:require [ring.middleware.logger :refer [wrap-with-logger]]))

(defn wrap-logging [handler]
  (wrap-with-logger handler))
```

**Explanation**:
- **`wrap-with-logger`**: A middleware function that logs each request.

To use this middleware, wrap the handler in the `-main` function.

```clojure
(defn -main []
  (run-jetty (wrap-logging handler) {:port 3000}))
```

#### Session Management

Ring provides session management middleware to handle user sessions.

```clojure
(ns my-app.middleware
  (:require [ring.middleware.session :refer [wrap-session]]))

(defn wrap-session-management [handler]
  (wrap-session handler))
```

**Explanation**:
- **`wrap-session`**: Adds session management to the handler.

Integrate session management by wrapping the handler.

```clojure
(defn -main []
  (run-jetty (wrap-session-management (wrap-logging handler)) {:port 3000}))
```

#### Security Headers

To enhance security, we can add middleware to set security-related HTTP headers.

```clojure
(ns my-app.middleware
  (:require [ring.middleware.defaults :refer [wrap-defaults site-defaults]]))

(defn wrap-security [handler]
  (wrap-defaults handler site-defaults))
```

**Explanation**:
- **`wrap-defaults`**: Applies a set of default middleware, including security headers.

Update the `-main` function to include security middleware.

```clojure
(defn -main []
  (run-jetty (wrap-security (wrap-session-management (wrap-logging handler))) {:port 3000}))
```

### Setting Up a Web Server with Pedestal

**Pedestal** is a more comprehensive framework that builds on Ring, providing additional features for building complex web applications.

#### Step 1: Define the Service

Pedestal uses a service map to define routes, interceptors, and other configurations.

```clojure
(ns my-app.service
  (:require [io.pedestal.http :as http]))

(def service
  {:env :prod
   ::http/routes #{["/" :get (fn [request] {:status 200 :body "Hello, Pedestal!"})]}
   ::http/type :jetty
   ::http/port 3000})
```

**Explanation**:
- **`::http/routes`**: Defines the routes and handlers.
- **`::http/type`**: Specifies the server type (Jetty in this case).
- **`::http/port`**: Sets the port number.

#### Step 2: Start the Server

Use the `http/create-server` and `http/start` functions to start the Pedestal server.

```clojure
(defn -main []
  (-> service
      http/create-server
      http/start))
```

#### Step 3: Verify the Server is Running

Run the `-main` function and visit `http://localhost:3000` to see "Hello, Pedestal!" displayed.

### Middleware in Pedestal

Pedestal uses interceptors, which are similar to middleware in Ring but offer more flexibility.

#### Adding Logging Interceptor

```clojure
(ns my-app.interceptors
  (:require [io.pedestal.interceptor :refer [interceptor]]))

(def log-interceptor
  (interceptor
    {:name ::log
     :enter (fn [context]
              (println "Request received:" (:request context))
              context)}))
```

**Explanation**:
- **`interceptor`**: Defines an interceptor with an `:enter` function to log requests.

Add the interceptor to the service map.

```clojure
(def service
  {:env :prod
   ::http/routes #{["/" :get (fn [request] {:status 200 :body "Hello, Pedestal!"})]}
   ::http/type :jetty
   ::http/port 3000
   ::http/interceptors [log-interceptor]})
```

### Comparing Ring and Pedestal

| Feature         | Ring                          | Pedestal                      |
|-----------------|-------------------------------|-------------------------------|
| Simplicity      | Simple and minimalistic       | More features, more complex   |
| Middleware      | Uses middleware functions     | Uses interceptors             |
| Flexibility     | Highly composable             | Comprehensive, more opinionated|
| Use Case        | Small to medium applications  | Large, complex applications   |

### Try It Yourself

Experiment with the following:

- Modify the Ring handler to return JSON instead of plain text.
- Add a new route in Pedestal that returns a different message.
- Implement custom middleware in Ring to track request processing time.

### Summary and Key Takeaways

- **Ring** provides a simple, functional approach to handling HTTP requests with middleware for extensibility.
- **Pedestal** builds on Ring, offering a more comprehensive framework with interceptors for complex applications.
- Both frameworks leverage Clojure's strengths, such as immutability and simplicity, to create robust web servers.
- Middleware and interceptors allow for modular and reusable code, enhancing maintainability.

### Further Reading

- [Ring Documentation](https://github.com/ring-clojure/ring)
- [Pedestal Documentation](https://github.com/pedestal/pedestal)
- [ClojureDocs](https://clojuredocs.org/)

### Exercises

1. Create a new Ring application with a custom middleware that adds a timestamp to each response.
2. Build a Pedestal service with multiple routes and interceptors for logging and authentication.
3. Compare the performance of a simple Ring server and a Pedestal server under load.

## SEO optimized quiz title

{{< quizdown >}}

### What is the primary function of a Ring handler in Clojure?

- [x] To process HTTP requests and generate responses
- [ ] To manage database connections
- [ ] To handle user authentication
- [ ] To serve static files

> **Explanation:** A Ring handler is a function that processes HTTP requests and generates responses, forming the core of a Ring-based web application.

### Which Clojure library provides a simple and composable way to handle HTTP requests?

- [x] Ring
- [ ] Pedestal
- [ ] Compojure
- [ ] Luminus

> **Explanation:** Ring is a Clojure library that provides a simple and composable way to handle HTTP requests and responses.

### What is the purpose of middleware in a Ring application?

- [x] To add additional functionality to handlers
- [ ] To compile Clojure code
- [ ] To manage database transactions
- [ ] To render HTML templates

> **Explanation:** Middleware in Ring is used to add additional functionality to handlers, such as logging, session management, and security.

### How do you start a Ring server using the Jetty adapter?

- [x] By using the `run-jetty` function
- [ ] By calling the `start-server` method
- [ ] By executing the `launch-jetty` command
- [ ] By invoking the `init-server` function

> **Explanation:** The `run-jetty` function from Ring's Jetty adapter is used to start a Ring server.

### What is an interceptor in Pedestal?

- [x] A component that processes requests and responses
- [ ] A type of database connection
- [ ] A method for rendering views
- [ ] A tool for compiling Clojure code

> **Explanation:** An interceptor in Pedestal is a component that processes requests and responses, similar to middleware in Ring.

### Which option allows a Ring server to run in a non-blocking manner?

- [x] `:join? false`
- [ ] `:async true`
- [ ] `:block false`
- [ ] `:non-blocking true`

> **Explanation:** The `:join? false` option allows a Ring server to run in a non-blocking manner, which is useful for REPL-driven development.

### What is the primary advantage of using Pedestal over Ring?

- [x] More features for building complex applications
- [ ] Simpler syntax for defining routes
- [ ] Better performance for small applications
- [ ] Easier integration with Java libraries

> **Explanation:** Pedestal offers more features for building complex applications compared to Ring, which is simpler and more minimalistic.

### How do you define routes in a Pedestal service map?

- [x] Using the `::http/routes` key
- [ ] By calling the `define-routes` function
- [ ] By setting the `:routes` option in `run-jetty`
- [ ] By using the `:path` key in the service map

> **Explanation:** Routes in a Pedestal service map are defined using the `::http/routes` key.

### What is the role of the `wrap-defaults` middleware in Ring?

- [x] To apply a set of default middleware, including security headers
- [ ] To manage database connections
- [ ] To compile Clojure code
- [ ] To render HTML templates

> **Explanation:** The `wrap-defaults` middleware in Ring applies a set of default middleware, including security headers, to enhance security.

### True or False: Pedestal uses middleware functions like Ring.

- [ ] True
- [x] False

> **Explanation:** False. Pedestal uses interceptors, which are similar to middleware but offer more flexibility and are a key part of Pedestal's architecture.

{{< /quizdown >}}
