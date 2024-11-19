---
linkTitle: "3.2.2 Route Parameters and Query Strings"
title: "Clojure Route Parameters and Query Strings: Mastering Path and Query Parameters in Compojure"
description: "Learn how to effectively handle route parameters and query strings in Clojure using the Compojure library. This comprehensive guide covers path parameters, query parameters, route constraints, and provides practical examples for enterprise integration."
categories:
- Clojure
- Web Development
- Enterprise Integration
tags:
- Clojure
- Compojure
- Web Development
- Route Parameters
- Query Strings
date: 2024-10-25
type: docs
nav_weight: 322000
canonical: "https://clojureforjava.com/4/3/2/2"
license: "© 2024 Tokenizer Inc. CC BY-NC-SA 4.0"
---

## 3.2.2 Route Parameters and Query Strings

In the realm of web development, handling route parameters and query strings is a fundamental aspect of building dynamic and responsive web applications. In Clojure, the Compojure library provides a powerful and flexible way to define routes and manage parameters. This section delves into the intricacies of route parameters and query strings, offering a comprehensive guide for experienced Java developers transitioning to Clojure.

### Path Parameters

Path parameters are integral to defining dynamic routes in web applications. They allow you to capture values from the URL path and use them within your request handlers. In Compojure, path parameters are specified using a colon (`:`) followed by the parameter name in the route definition.

#### Extracting Path Parameters

To extract path parameters in Compojure, you define them directly in the route pattern. Here's an example of how to capture a user ID from the URL:

```clojure
(ns myapp.routes
  (:require [compojure.core :refer :all]
            [ring.util.response :refer :all]))

(defroutes app-routes
  (GET "/user/:id" [id]
    (response (str "User ID: " id))))
```

In this example, the route `/user/:id` captures the `id` parameter from the URL path. The `[id]` vector in the handler function automatically binds the captured value to the `id` variable, which can then be used within the handler.

#### Using Path Parameters in Handlers

Once extracted, path parameters can be used to perform various operations, such as database queries or business logic. Consider the following example where the captured `id` is used to fetch user details from a database:

```clojure
(defn get-user [id]
  ;; Simulate a database call
  {:id id :name "John Doe" :email "john.doe@example.com"})

(defroutes app-routes
  (GET "/user/:id" [id]
    (let [user (get-user id)]
      (response (str "User Details: " user)))))
```

In this scenario, the `get-user` function simulates a database call to retrieve user information based on the `id` path parameter.

### Query Parameters

Query parameters are key-value pairs appended to the URL, typically used to filter or modify the response. In Compojure, query parameters are accessed using destructuring within the handler function.

#### Parsing Query String Parameters

To parse query parameters, you can destructure the `request` map in the handler function. Here's an example of how to access query parameters:

```clojure
(defroutes app-routes
  (GET "/search" [q]
    (response (str "Search query: " q))))
```

In this example, the `q` parameter is extracted from the query string of the URL `/search?q=clojure`. The handler function then uses this parameter to perform the desired operation.

#### Validating Query Parameters

Validation of query parameters is crucial to ensure that your application behaves correctly and securely. You can implement validation logic within the handler function or use middleware for more complex validation scenarios.

```clojure
(defn validate-query [q]
  (if (and q (not (empty? q)))
    true
    false))

(defroutes app-routes
  (GET "/search" [q]
    (if (validate-query q)
      (response (str "Search query: " q))
      (response "Invalid query" 400))))
```

In this example, the `validate-query` function checks if the query parameter `q` is present and not empty. If the validation fails, a `400 Bad Request` response is returned.

### Route Constraints

Route constraints allow you to enforce specific rules on route parameters, ensuring that they meet certain criteria before the handler is executed. Compojure supports route constraints through regular expressions and custom validation functions.

#### Implementing Route Constraints

You can define route constraints directly in the route pattern using regular expressions. Here's an example of how to enforce a numeric constraint on a path parameter:

```clojure
(defroutes app-routes
  (GET ["/user/:id" :id #"\d+"] [id]
    (response (str "User ID: " id))))
```

In this example, the route `/user/:id` includes a constraint that ensures the `id` parameter is a sequence of digits (`\d+`). If the constraint is not met, the route will not match, and a `404 Not Found` response will be returned.

#### Custom Route Constraints

For more complex validation scenarios, you can implement custom route constraints using functions. Here's an example of a custom constraint that checks if a user ID is within a specific range:

```clojure
(defn valid-user-id? [id]
  (let [id-num (Integer/parseInt id)]
    (and (>= id-num 1000) (<= id-num 9999))))

(defroutes app-routes
  (GET ["/user/:id" :id valid-user-id?] [id]
    (response (str "User ID: " id))))
```

In this example, the `valid-user-id?` function checks if the `id` parameter is a number between 1000 and 9999. If the constraint is not satisfied, the route will not match.

### Practical Examples

To solidify your understanding of route parameters and query strings in Compojure, let's explore a practical example that combines both concepts.

#### Example: Building a Product Search API

Consider a scenario where you need to build a product search API that supports filtering by category and sorting by price. The API should handle both path and query parameters.

```clojure
(defn get-products [category sort]
  ;; Simulate a product database query
  [{:id 1 :name "Laptop" :category "electronics" :price 999.99}
   {:id 2 :name "Smartphone" :category "electronics" :price 499.99}
   {:id 3 :name "Coffee Maker" :category "appliances" :price 79.99}])

(defroutes app-routes
  (GET "/products/:category" [category sort]
    (let [products (get-products category sort)
          filtered-products (filter #(= (:category %) category) products)
          sorted-products (if (= sort "price")
                            (sort-by :price filtered-products)
                            filtered-products)]
      (response (str "Products: " sorted-products)))))
```

In this example, the `/products/:category` route captures the `category` path parameter, while the `sort` query parameter is used to determine the sorting order. The `get-products` function simulates a database query, and the results are filtered and sorted based on the parameters.

### Best Practices and Common Pitfalls

When working with route parameters and query strings in Compojure, consider the following best practices and common pitfalls:

- **Validation:** Always validate path and query parameters to prevent invalid data from causing errors or security vulnerabilities.
- **Constraints:** Use route constraints to enforce parameter rules and reduce the need for additional validation logic in handlers.
- **Destructuring:** Leverage Clojure's destructuring capabilities to simplify parameter extraction and improve code readability.
- **Error Handling:** Implement robust error handling to gracefully manage invalid or missing parameters.
- **Security:** Be cautious of injection attacks and sanitize input data to protect your application.

### Conclusion

Mastering route parameters and query strings in Compojure is essential for building dynamic and responsive web applications in Clojure. By understanding how to extract, validate, and constrain parameters, you can create robust and secure APIs that meet the demands of enterprise integration.

## Quiz Time!

{{< quizdown >}}

### What is the purpose of path parameters in Compojure?

- [x] To capture values from the URL path and use them within handlers
- [ ] To define static routes that do not change
- [ ] To manage query string parameters
- [ ] To handle HTTP headers

> **Explanation:** Path parameters are used to capture dynamic values from the URL path, allowing handlers to use these values for processing requests.

### How are path parameters specified in Compojure route definitions?

- [x] Using a colon (:) followed by the parameter name
- [ ] Using a question mark (?) followed by the parameter name
- [ ] Using curly braces {} around the parameter name
- [ ] Using square brackets [] around the parameter name

> **Explanation:** In Compojure, path parameters are specified using a colon (:) followed by the parameter name in the route pattern.

### How can you access query parameters in a Compojure handler?

- [x] By destructuring the request map in the handler function
- [ ] By using a global variable
- [ ] By modifying the URL path
- [ ] By accessing the HTTP headers

> **Explanation:** Query parameters can be accessed by destructuring the request map in the handler function, allowing you to extract and use them easily.

### What is the purpose of route constraints in Compojure?

- [x] To enforce specific rules on route parameters
- [ ] To define the HTTP method for a route
- [ ] To manage session data
- [ ] To handle file uploads

> **Explanation:** Route constraints are used to enforce specific rules on route parameters, ensuring they meet certain criteria before the handler is executed.

### How can you implement a numeric constraint on a path parameter in Compojure?

- [x] By using a regular expression in the route pattern
- [ ] By using a query parameter
- [ ] By modifying the HTTP headers
- [ ] By using a global variable

> **Explanation:** Numeric constraints on path parameters can be implemented using regular expressions in the route pattern, ensuring the parameter matches the specified pattern.

### What is a common pitfall when handling query parameters?

- [x] Failing to validate query parameters
- [ ] Using too many query parameters
- [ ] Not using enough query parameters
- [ ] Ignoring path parameters

> **Explanation:** A common pitfall is failing to validate query parameters, which can lead to errors or security vulnerabilities if invalid data is processed.

### How can you implement custom route constraints in Compojure?

- [x] By using custom validation functions
- [ ] By modifying the URL path
- [ ] By using global variables
- [ ] By accessing the HTTP headers

> **Explanation:** Custom route constraints can be implemented using custom validation functions, allowing you to define complex validation logic for route parameters.

### What is the benefit of using destructuring for parameter extraction?

- [x] It simplifies parameter extraction and improves code readability
- [ ] It increases the complexity of the code
- [ ] It requires more lines of code
- [ ] It makes the code harder to maintain

> **Explanation:** Destructuring simplifies parameter extraction and improves code readability by allowing you to directly access parameters in a concise manner.

### Why is it important to sanitize input data in web applications?

- [x] To protect the application from injection attacks
- [ ] To increase the complexity of the code
- [ ] To make the application slower
- [ ] To reduce the number of parameters

> **Explanation:** Sanitizing input data is important to protect the application from injection attacks, ensuring that malicious input does not compromise the application's security.

### True or False: Route constraints can only be implemented using regular expressions.

- [ ] True
- [x] False

> **Explanation:** Route constraints can be implemented using both regular expressions and custom validation functions, providing flexibility in defining parameter validation rules.

{{< /quizdown >}}
