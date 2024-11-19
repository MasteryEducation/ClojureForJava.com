---
linkTitle: "10.4.1 Designing Endpoints with Pedestal"
title: "Designing RESTful Endpoints with Pedestal in Clojure"
description: "Explore how to design RESTful endpoints using Pedestal, a powerful framework for building web services in Clojure. Learn about interceptors, service maps, and handling JSON payloads."
categories:
- Clojure
- Web Development
- RESTful Services
tags:
- Pedestal
- Clojure
- REST
- Web Services
- JSON
date: 2024-10-25
type: docs
nav_weight: 1041000
canonical: "https://clojureforjava.com/2/10/4/1"
license: "© 2024 Tokenizer Inc. CC BY-NC-SA 4.0"
---

## 10.4.1 Designing RESTful Endpoints with Pedestal in Clojure

In the realm of web development, designing robust and scalable web services is a crucial skill. For Clojure developers, Pedestal offers a powerful framework that simplifies the process of building web applications and services. In this section, we'll delve into the core concepts of Pedestal, including interceptors and service maps, and guide you through setting up a new project to create RESTful endpoints. We'll also discuss the significance of HTTP methods, status codes, and resource-oriented design, along with handling JSON payloads and content negotiation.

### Introduction to Pedestal

Pedestal is a set of libraries designed to help developers build web applications and services in Clojure. It emphasizes simplicity, composability, and performance, making it an excellent choice for creating RESTful services. Pedestal's architecture is based on the concept of interceptors, which allow you to define reusable components that can be composed to handle HTTP requests and responses.

#### Core Concepts of Pedestal

Before we dive into building endpoints, let's explore some of the core concepts that make Pedestal a powerful tool for web development:

- **Interceptors**: At the heart of Pedestal is the interceptor pattern. Interceptors are functions that can be composed to form a pipeline, which processes HTTP requests and responses. They allow you to separate concerns such as authentication, logging, and error handling, making your code more modular and maintainable.

- **Service Maps**: A service map is a data structure that defines the configuration of your Pedestal service. It includes information about routes, interceptors, and other settings required to run your service. The service map is the blueprint for your application, dictating how requests are handled and responses are generated.

- **Routes**: Routes in Pedestal define the mapping between URL paths and the handlers that process them. They are specified in the service map and can include path parameters, query parameters, and constraints.

### Setting Up a New Pedestal Project

To get started with Pedestal, you'll need to set up a new project. We'll walk through the steps to create a basic Pedestal service that can handle RESTful endpoints.

#### Prerequisites

Before you begin, ensure that you have the following installed on your system:

- [Clojure](https://clojure.org/guides/getting_started)
- [Leiningen](https://leiningen.org/), a build automation tool for Clojure

#### Creating a New Project

1. **Generate a New Pedestal Project**: Use Leiningen to create a new Pedestal project. Open your terminal and run the following command:

   ```bash
   lein new pedestal-service my-pedestal-service
   ```

   This command generates a new project with a basic Pedestal service structure.

2. **Navigate to the Project Directory**: Change into the newly created project directory:

   ```bash
   cd my-pedestal-service
   ```

3. **Explore the Project Structure**: The generated project includes several directories and files. Key components include:

   - `src`: Contains the source code for your service.
   - `resources`: Holds static resources such as HTML, CSS, and JavaScript files.
   - `project.clj`: The project configuration file, where dependencies and build settings are defined.

#### Configuring the Service Map

The service map is the core configuration for your Pedestal service. Open the `src/my_pedestal_service/service.clj` file and examine the default service map. It typically includes the following sections:

- **Routes**: Define the URL paths and their corresponding handlers.
- **Interceptors**: Specify the interceptors to be applied to requests and responses.
- **Server Options**: Configure server settings such as port and host.

Here's an example of a simple service map:

```clojure
(def service
  {:env :prod
   ::http/routes #{["/hello" :get (conj interceptors `hello-handler)]}
   ::http/type :jetty
   ::http/port 8080})
```

### Creating RESTful Endpoints

With the project set up, let's create RESTful endpoints. REST (Representational State Transfer) is an architectural style that uses HTTP methods to interact with resources. In Pedestal, you define endpoints using routes and handlers.

#### Defining Routes

Routes in Pedestal are defined in the service map. Each route consists of a path, an HTTP method, and a handler function. Here's an example of defining a route for a `GET` request:

```clojure
(def routes
  #{["/api/users" :get (conj interceptors `list-users-handler)]
    ["/api/users/:id" :get (conj interceptors `get-user-handler)]
    ["/api/users" :post (conj interceptors `create-user-handler)]
    ["/api/users/:id" :put (conj interceptors `update-user-handler)]
    ["/api/users/:id" :delete (conj interceptors `delete-user-handler)]})
```

In this example, we've defined routes for common CRUD (Create, Read, Update, Delete) operations on a `users` resource.

#### Implementing Handlers

Handlers are functions that process requests and generate responses. They receive a context map containing the request data and return a modified context map with the response. Here's an example of a simple handler function:

```clojure
(defn list-users-handler
  [context]
  (let [users (get-all-users)]
    (assoc context :response {:status 200 :body users})))
```

This handler retrieves a list of users and returns them in the response body with a `200 OK` status.

### Understanding HTTP Methods and Status Codes

When designing RESTful endpoints, it's essential to understand the role of HTTP methods and status codes:

- **HTTP Methods**: Common methods include `GET`, `POST`, `PUT`, `DELETE`, and `PATCH`. Each method has a specific purpose, such as retrieving data (`GET`), creating new resources (`POST`), or updating existing resources (`PUT`).

- **Status Codes**: HTTP status codes indicate the outcome of a request. For example, `200 OK` signifies a successful request, `201 Created` indicates a new resource was created, and `404 Not Found` means the requested resource was not found.

### Handling JSON Payloads and Content Negotiation

In modern web services, JSON is a popular format for data exchange. Pedestal provides tools for handling JSON payloads and content negotiation.

#### Parsing JSON Requests

To parse JSON requests, you'll need to add a JSON parsing library to your project. One popular choice is `cheshire`. Add it to your `project.clj` dependencies:

```clojure
(defproject my-pedestal-service "0.0.1-SNAPSHOT"
  :dependencies [[org.clojure/clojure "1.10.3"]
                 [io.pedestal/pedestal.service "0.5.8"]
                 [cheshire "5.10.0"]])
```

Then, use `cheshire` to parse JSON in your handlers:

```clojure
(require '[cheshire.core :as json])

(defn create-user-handler
  [context]
  (let [user-data (json/parse-string (slurp (:body context)) true)]
    (create-user user-data)
    (assoc context :response {:status 201 :body "User created"})))
```

#### Content Negotiation

Content negotiation allows your service to respond with different formats based on the `Accept` header in the request. Pedestal supports content negotiation through interceptors. Here's an example of setting up content negotiation:

```clojure
(defn negotiate-content
  [context]
  (let [accept (get-in context [:request :headers "accept"])]
    (cond
      (clojure.string/includes? accept "application/json")
      (assoc-in context [:response :headers "Content-Type"] "application/json")

      (clojure.string/includes? accept "text/html")
      (assoc-in context [:response :headers "Content-Type"] "text/html")

      :else
      (assoc-in context [:response :headers "Content-Type"] "application/json"))))
```

### Best Practices for Designing RESTful Endpoints

When designing RESTful endpoints with Pedestal, consider the following best practices:

- **Resource-Oriented Design**: Structure your endpoints around resources, using nouns for paths and HTTP methods to define actions.

- **Consistent Naming**: Use consistent naming conventions for your endpoints, such as plural nouns for collections (e.g., `/api/users`) and singular nouns for individual resources (e.g., `/api/users/:id`).

- **Error Handling**: Implement robust error handling to provide meaningful error messages and appropriate status codes.

- **Security**: Ensure your endpoints are secure by implementing authentication and authorization mechanisms.

- **Documentation**: Document your endpoints using tools like Swagger or OpenAPI to provide clear and comprehensive API documentation.

### Conclusion

Pedestal offers a powerful and flexible framework for building RESTful web services in Clojure. By understanding its core concepts, such as interceptors and service maps, and following best practices for endpoint design, you can create robust and scalable web services. With the ability to handle JSON payloads and perform content negotiation, Pedestal equips you with the tools needed to build modern web applications.

## Quiz Time!

{{< quizdown >}}

### What is the primary architectural pattern used in Pedestal?

- [x] Interceptor pattern
- [ ] Observer pattern
- [ ] Singleton pattern
- [ ] Factory pattern

> **Explanation:** Pedestal uses the interceptor pattern, which allows for modular and composable request and response processing.

### In Pedestal, what is a service map?

- [x] A data structure that defines the configuration of a Pedestal service
- [ ] A map of all available services in a Clojure application
- [ ] A list of all interceptors in a Pedestal application
- [ ] A configuration file for database connections

> **Explanation:** A service map in Pedestal defines the configuration of the service, including routes, interceptors, and server options.

### Which HTTP method is typically used to create a new resource in a RESTful service?

- [ ] GET
- [x] POST
- [ ] PUT
- [ ] DELETE

> **Explanation:** The POST method is used to create new resources in RESTful services.

### What library is commonly used in Clojure for parsing JSON?

- [ ] Ring
- [x] Cheshire
- [ ] Compojure
- [ ] Pedestal

> **Explanation:** Cheshire is a popular library in Clojure for parsing and generating JSON.

### What is the purpose of content negotiation in a web service?

- [x] To respond with different formats based on the request's Accept header
- [ ] To negotiate the server's response time
- [ ] To determine the client's IP address
- [ ] To handle authentication and authorization

> **Explanation:** Content negotiation allows a web service to respond with different formats (e.g., JSON, HTML) based on the Accept header in the request.

### Which of the following is NOT a common HTTP status code used in RESTful services?

- [ ] 200 OK
- [ ] 404 Not Found
- [ ] 500 Internal Server Error
- [x] 302 Temporary Redirect

> **Explanation:** While 302 is a valid HTTP status code, it is not commonly used in RESTful services compared to others like 200, 404, and 500.

### What is the purpose of interceptors in Pedestal?

- [x] To process HTTP requests and responses in a modular way
- [ ] To manage database connections
- [ ] To handle file uploads
- [ ] To generate HTML content

> **Explanation:** Interceptors in Pedestal are used to process HTTP requests and responses in a modular and composable manner.

### How can you specify a route in a Pedestal service map?

- [x] Using a vector with a path, method, and handler
- [ ] Using a map with keys for path, method, and handler
- [ ] Using a list with elements for path, method, and handler
- [ ] Using a string with the path, method, and handler concatenated

> **Explanation:** Routes in a Pedestal service map are specified using a vector that includes the path, HTTP method, and handler function.

### Which HTTP method is used to update an existing resource in a RESTful service?

- [ ] GET
- [ ] POST
- [x] PUT
- [ ] DELETE

> **Explanation:** The PUT method is used to update existing resources in RESTful services.

### True or False: Pedestal can only handle JSON payloads.

- [ ] True
- [x] False

> **Explanation:** Pedestal can handle various payload formats, including JSON, XML, and HTML, through content negotiation.

{{< /quizdown >}}
