---
canonical: "https://clojureforjava.com/1/13/2/2"
title: "Routing with Compojure: A Comprehensive Guide for Java Developers"
description: "Explore Compojure, a routing library for Clojure, and learn how to define routes, handlers, and build RESTful endpoints with concise syntax."
linkTitle: "13.2.2 Routing with Compojure"
tags:
- "Clojure"
- "Compojure"
- "Routing"
- "Web Development"
- "Functional Programming"
- "RESTful APIs"
- "Java Interoperability"
- "Middleware"
date: 2024-11-25
type: docs
nav_weight: 132200
license: "© 2024 Tokenizer Inc. CC BY-NC-SA 4.0"
---

## 13.2.2 Routing with Compojure

In this section, we delve into **Compojure**, a powerful routing library for Clojure, built on top of the Ring library. Compojure provides a concise and expressive syntax for defining routes and building RESTful endpoints, making it an excellent choice for web development in Clojure. As experienced Java developers, you'll find Compojure's approach to routing both familiar and refreshingly different from Java's traditional servlet-based frameworks.

### Introduction to Compojure

Compojure is a routing library that simplifies the process of defining routes and handling HTTP requests in Clojure web applications. It is built on top of Ring, a Clojure web application library that provides a simple and flexible way to handle HTTP requests and responses.

#### Why Use Compojure?

- **Concise Syntax**: Compojure's syntax is minimalistic and expressive, allowing you to define routes with ease.
- **Integration with Ring**: Compojure seamlessly integrates with Ring, enabling you to leverage Ring's middleware and request handling capabilities.
- **RESTful Endpoints**: Compojure makes it straightforward to build RESTful APIs, a common requirement in modern web applications.

### Setting Up Compojure

Before we dive into routing with Compojure, let's set up a basic Clojure web application with Compojure and Ring.

1. **Create a New Clojure Project**: Use Leiningen to create a new Clojure project.

   ```bash
   lein new compojure-example
   ```

2. **Add Dependencies**: Update your `project.clj` file to include Compojure and Ring.

   ```clojure
   (defproject compojure-example "0.1.0-SNAPSHOT"
     :dependencies [[org.clojure/clojure "1.10.3"]
                    [compojure "1.6.2"]
                    [ring/ring-defaults "0.3.2"]])
   ```

3. **Create a Basic Server**: Set up a basic Ring server in `src/compojure_example/core.clj`.

   ```clojure
   (ns compojure-example.core
     (:require [compojure.core :refer :all]
               [compojure.route :as route]
               [ring.adapter.jetty :refer [run-jetty]]
               [ring.middleware.defaults :refer [wrap-defaults site-defaults]]))

   (defroutes app-routes
     (GET "/" [] "Hello, World!")
     (route/not-found "Not Found"))

   (def app
     (wrap-defaults app-routes site-defaults))

   (defn -main []
     (run-jetty app {:port 3000 :join? false}))
   ```

4. **Run the Server**: Start your server using Leiningen.

   ```bash
   lein run
   ```

Visit `http://localhost:3000` in your browser, and you should see "Hello, World!" displayed.

### Defining Routes with Compojure

Compojure allows you to define routes using a DSL (Domain-Specific Language) that is both powerful and easy to read. Let's explore how to define routes and handle parameters.

#### Basic Route Definitions

Routes in Compojure are defined using the `GET`, `POST`, `PUT`, `DELETE`, and other HTTP method macros. Here's a simple example:

```clojure
(defroutes app-routes
  (GET "/" [] "Welcome to Compojure!")
  (GET "/hello/:name" [name] (str "Hello, " name "!"))
  (POST "/submit" {params :params} (str "Submitted: " params)))
```

- **GET "/"**: A simple route that returns a welcome message.
- **GET "/hello/:name"**: A route with a path parameter `:name`. The parameter is extracted and used in the response.
- **POST "/submit"**: A route that handles POST requests and accesses form parameters.

#### Handling Parameters

Compojure makes it easy to handle both path and query parameters. Let's look at an example:

```clojure
(GET "/search" [query] (str "Searching for: " query))
```

In this route, `query` is a query parameter that can be accessed directly in the route handler.

#### Using Route Destructuring

Compojure supports destructuring, allowing you to extract parameters from the request map. Here's an example:

```clojure
(POST "/login" {params :params} 
  (let [{:keys [username password]} params]
    (if (and (= username "admin") (= password "secret"))
      "Login successful!"
      "Invalid credentials.")))
```

In this example, we destructure the `params` map to extract `username` and `password`.

### Integrating with Ring Middleware

Middleware in Ring is a way to wrap handlers with additional functionality, such as logging, authentication, or session management. Compojure routes can be easily integrated with Ring middleware.

#### Applying Middleware

To apply middleware to your Compojure routes, use the `wrap-defaults` function from `ring.middleware.defaults`. Here's how you can add session and security middleware:

```clojure
(def app
  (-> app-routes
      (wrap-defaults site-defaults)))
```

The `site-defaults` middleware includes common middleware for web applications, such as session handling and security headers.

#### Custom Middleware

You can also create custom middleware to add specific functionality to your application. Here's an example of a simple logging middleware:

```clojure
(defn wrap-logging [handler]
  (fn [request]
    (println "Request received:" request)
    (handler request)))

(def app
  (-> app-routes
      (wrap-logging)
      (wrap-defaults site-defaults)))
```

### Building RESTful Endpoints

Compojure is well-suited for building RESTful APIs. Let's create a simple API for managing a list of items.

#### Defining RESTful Routes

Here's an example of a basic RESTful API with Compojure:

```clojure
(def items (atom []))

(defroutes api-routes
  (GET "/items" [] @items)
  (POST "/items" {params :params}
    (let [item (get params "item")]
      (swap! items conj item)
      (str "Added item: " item)))
  (DELETE "/items/:id" [id]
    (let [id (Integer. id)]
      (swap! items #(vec (remove #(= id (first %)) %)))
      (str "Deleted item with id: " id))))
```

- **GET "/items"**: Returns the list of items.
- **POST "/items"**: Adds a new item to the list.
- **DELETE "/items/:id"**: Deletes an item by its ID.

#### Handling JSON Data

In modern web applications, JSON is a common data format for APIs. Let's modify our API to handle JSON data using the `ring-json` middleware.

1. **Add the Dependency**: Update your `project.clj` to include `ring-json`.

   ```clojure
   [ring/ring-json "0.5.0"]
   ```

2. **Apply JSON Middleware**: Use `wrap-json-body` and `wrap-json-response` to handle JSON requests and responses.

   ```clojure
   (ns compojure-example.core
     (:require [compojure.core :refer :all]
               [compojure.route :as route]
               [ring.adapter.jetty :refer [run-jetty]]
               [ring.middleware.defaults :refer [wrap-defaults site-defaults]]
               [ring.middleware.json :refer [wrap-json-body wrap-json-response]]))

   (def app
     (-> app-routes
         (wrap-json-body)
         (wrap-json-response)
         (wrap-defaults site-defaults)))
   ```

3. **Update the API**: Modify the API to work with JSON data.

   ```clojure
   (POST "/items" {body :body}
     (let [item (:item body)]
       (swap! items conj item)
       {:status 201 :body {:message "Item added" :item item}}))
   ```

### Comparing Compojure with Java Servlets

For Java developers, the transition to Compojure from traditional servlet-based frameworks can be enlightening. Let's compare a simple route in Compojure with a Java servlet.

#### Compojure Example

```clojure
(GET "/hello/:name" [name] (str "Hello, " name "!"))
```

#### Java Servlet Example

```java
@WebServlet("/hello/*")
public class HelloServlet extends HttpServlet {
    protected void doGet(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        String name = request.getPathInfo().substring(1);
        response.getWriter().write("Hello, " + name + "!");
    }
}
```

**Comparison**:
- **Conciseness**: Compojure's syntax is more concise and expressive.
- **Parameter Handling**: Compojure automatically extracts path parameters, whereas Java servlets require manual extraction.
- **Functional Approach**: Compojure embraces a functional programming style, making it easier to reason about and test.

### Try It Yourself

Now that we've covered the basics of routing with Compojure, try modifying the code examples to deepen your understanding:

- **Add a PUT route**: Implement a route to update an existing item.
- **Enhance Error Handling**: Add error handling for invalid requests.
- **Integrate with a Database**: Replace the in-memory atom with a database-backed storage solution.

### Exercises

1. **Create a Simple Blog API**: Define routes for creating, reading, updating, and deleting blog posts.
2. **Implement Authentication**: Add middleware to handle user authentication and authorization.
3. **Build a JSON API**: Create a JSON-based API for managing a collection of books.

### Summary and Key Takeaways

- **Compojure** is a powerful routing library for Clojure, built on top of Ring.
- It provides a concise and expressive syntax for defining routes and building RESTful endpoints.
- Compojure integrates seamlessly with Ring middleware, allowing you to add functionality like logging, authentication, and JSON handling.
- Compared to Java servlets, Compojure offers a more concise and functional approach to web development.

By leveraging Compojure, you can build robust and maintainable web applications in Clojure. As you continue your journey, explore more advanced features and integrations to fully harness the power of Clojure for web development.

---

## Quiz: Mastering Routing with Compojure

{{< quizdown >}}

### What is Compojure primarily used for in Clojure web applications?

- [x] Routing
- [ ] Database management
- [ ] User authentication
- [ ] Logging

> **Explanation:** Compojure is primarily used for routing in Clojure web applications, providing a concise syntax for defining routes.

### Which library does Compojure build upon to handle HTTP requests and responses?

- [x] Ring
- [ ] Luminus
- [ ] Pedestal
- [ ] Reitit

> **Explanation:** Compojure is built on top of Ring, a Clojure library for handling HTTP requests and responses.

### How does Compojure handle path parameters in routes?

- [x] Automatically extracts them
- [ ] Requires manual extraction
- [ ] Uses annotations
- [ ] Through configuration files

> **Explanation:** Compojure automatically extracts path parameters, making it easy to access them in route handlers.

### What is the purpose of the `wrap-defaults` function in a Compojure application?

- [x] To apply common middleware
- [ ] To define routes
- [ ] To handle exceptions
- [ ] To manage database connections

> **Explanation:** The `wrap-defaults` function is used to apply common middleware, such as session handling and security headers, to a Compojure application.

### Which HTTP method macro is used in Compojure to define a route that handles POST requests?

- [ ] GET
- [x] POST
- [ ] PUT
- [ ] DELETE

> **Explanation:** The `POST` macro is used in Compojure to define routes that handle POST requests.

### What is a common data format for APIs that Compojure can handle with the help of middleware?

- [x] JSON
- [ ] XML
- [ ] CSV
- [ ] YAML

> **Explanation:** JSON is a common data format for APIs, and Compojure can handle it using middleware like `ring-json`.

### In Compojure, how can you apply custom middleware to a route?

- [x] By using the `->` threading macro
- [ ] By modifying the `project.clj` file
- [ ] By creating a new namespace
- [ ] By using annotations

> **Explanation:** Custom middleware can be applied to routes in Compojure using the `->` threading macro to wrap the routes with middleware functions.

### What is the primary advantage of using Compojure over Java servlets?

- [x] Conciseness and expressiveness
- [ ] Better performance
- [ ] More security features
- [ ] Easier database integration

> **Explanation:** Compojure offers a more concise and expressive syntax compared to Java servlets, making it easier to define routes and handle requests.

### Which middleware function is used to handle JSON requests and responses in Compojure?

- [x] wrap-json-body
- [ ] wrap-session
- [ ] wrap-params
- [ ] wrap-cookies

> **Explanation:** The `wrap-json-body` middleware function is used to handle JSON requests and responses in Compojure.

### True or False: Compojure requires manual extraction of query parameters in route handlers.

- [ ] True
- [x] False

> **Explanation:** False. Compojure allows direct access to query parameters in route handlers, eliminating the need for manual extraction.

{{< /quizdown >}}
