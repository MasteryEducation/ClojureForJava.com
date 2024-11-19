---
linkTitle: "8.1.2 When to Use Pedestal"
title: "Pedestal for High-Performance Web Services: When to Use It"
description: "Explore the scenarios where Pedestal excels, focusing on high-throughput applications and microservices architectures."
categories:
- Clojure
- Web Development
- Enterprise Integration
tags:
- Pedestal
- High-Performance
- Microservices
- Clojure
- Web Services
date: 2024-10-25
type: docs
nav_weight: 812000
canonical: "https://clojureforjava.com/4/8/1/2"
license: "© 2024 Tokenizer Inc. CC BY-NC-SA 4.0"
---

## 8.1.2 When to Use Pedestal

Pedestal is a powerful framework designed to build robust, high-performance web services in Clojure. It stands out for its unique architecture and capabilities, making it an excellent choice for specific use cases within enterprise environments. In this section, we will explore the scenarios where Pedestal shines, focusing on its suitability for high-throughput applications and its alignment with microservices architectures.

### Understanding Pedestal's Unique Features

Before delving into specific use cases, it's essential to understand what makes Pedestal unique:

- **Interceptor Architecture:** Pedestal uses an interceptor-based architecture that provides a flexible and composable way to handle HTTP requests and responses. This design allows developers to define reusable components that can be applied across different parts of an application.
  
- **Asynchronous Capabilities:** Pedestal is built with asynchronous processing in mind, making it well-suited for handling concurrent requests efficiently. This is crucial for applications that need to scale and maintain high performance under load.

- **Extensibility:** Pedestal's architecture is highly extensible, allowing developers to customize and extend the framework to meet specific application needs.

- **Focus on Simplicity and Clarity:** Despite its power, Pedestal maintains a focus on simplicity and clarity, making it accessible to developers who are familiar with Clojure.

### Use Cases for Pedestal

#### 1. High-Throughput Applications

One of the primary reasons to choose Pedestal is its ability to handle high-throughput applications. These are applications that need to process a large number of requests per second without compromising on performance or reliability.

**Key Features for High-Throughput:**

- **Non-blocking I/O:** Pedestal leverages non-blocking I/O operations, which allow it to handle multiple requests concurrently without waiting for each one to complete before starting the next. This is achieved through the use of asynchronous processing and event-driven architecture.

- **Efficient Resource Utilization:** By using asynchronous processing, Pedestal can make better use of system resources, reducing the overhead associated with managing multiple threads and processes.

- **Scalability:** Pedestal's architecture supports horizontal scaling, allowing applications to distribute load across multiple instances and servers. This makes it easier to scale applications to meet growing demand.

**Example Scenario:**

Consider an online streaming service that needs to serve thousands of concurrent users with minimal latency. Pedestal's non-blocking I/O and efficient resource management make it an ideal choice for building the backend services that handle user requests, stream data, and manage user sessions.

```clojure
(ns streaming-service.core
  (:require [io.pedestal.http :as http]
            [io.pedestal.http.route :as route]
            [clojure.core.async :as async]))

(defn stream-handler
  [request]
  (async/go
    (let [user-id (get-in request [:params :user-id])
          stream-data (fetch-stream-data user-id)]
      {:status 200
       :body stream-data})))

(def routes
  (route/expand-routes
   #{["/stream/:user-id" :get stream-handler]}))

(def service
  {:env :prod
   ::http/routes routes
   ::http/type :jetty
   ::http/port 8080})

(defn start []
  (http/start service))
```

In this example, the `stream-handler` function uses Clojure's `core.async` to fetch stream data asynchronously, allowing the server to handle other requests while waiting for the data to be retrieved.

#### 2. Microservices Architecture

Pedestal is also an excellent choice for building microservices, thanks to its modular design and support for asynchronous communication. Microservices architectures involve breaking down applications into smaller, independent services that communicate over a network. This approach offers several benefits, including improved scalability, flexibility, and ease of maintenance.

**Key Features for Microservices:**

- **Modularity:** Pedestal's interceptor architecture allows developers to create modular components that can be reused across different services. This promotes code reuse and consistency across the microservices ecosystem.

- **Asynchronous Communication:** Pedestal's support for asynchronous processing makes it well-suited for building services that need to communicate with each other over a network. This is particularly important in microservices architectures, where services often need to make remote calls to other services.

- **Service Discovery and Registration:** While Pedestal itself does not provide built-in service discovery and registration, it can be easily integrated with tools like Consul or Eureka to manage service instances and routing.

**Example Scenario:**

Imagine a retail platform that consists of multiple microservices, such as inventory management, order processing, and user authentication. Each service can be developed and deployed independently, allowing teams to work on different parts of the application without affecting others.

```clojure
(ns order-service.core
  (:require [io.pedestal.http :as http]
            [io.pedestal.http.route :as route]
            [clojure.core.async :as async]))

(defn process-order
  [request]
  (async/go
    (let [order-details (get-in request [:json-params :order])
          result (submit-order order-details)]
      {:status 200
       :body result})))

(def routes
  (route/expand-routes
   #{["/orders" :post process-order]}))

(def service
  {:env :prod
   ::http/routes routes
   ::http/type :jetty
   ::http/port 8081})

(defn start []
  (http/start service))
```

In this example, the `process-order` function handles incoming order requests asynchronously, allowing the service to process multiple orders concurrently.

### Performance Needs and Optimization

When building high-performance applications with Pedestal, it's important to consider various optimization strategies to ensure that your application can handle the expected load. Here are some best practices:

- **Optimize Interceptor Chains:** Carefully design your interceptor chains to minimize unnecessary processing. Remove any redundant or unused interceptors to reduce overhead.

- **Use Caching Wisely:** Implement caching strategies to reduce the load on your backend services. This can include caching responses for frequently requested data or using in-memory caches to store temporary data.

- **Monitor and Profile Performance:** Use monitoring tools to track the performance of your application in real-time. Profiling can help identify bottlenecks and areas for improvement.

- **Leverage Horizontal Scaling:** Deploy your application across multiple instances to distribute the load and improve resilience. Use load balancers to manage traffic and ensure even distribution.

### Integration with Existing Systems

Pedestal's flexibility and extensibility make it a great choice for integrating with existing systems. Whether you're building new services or modernizing legacy applications, Pedestal can be adapted to fit your needs.

**Integration Strategies:**

- **Interfacing with Databases:** Use Pedestal's extensible architecture to integrate with various databases, such as SQL, NoSQL, or in-memory data stores. Libraries like HugSQL or Yesql can be used to manage database interactions.

- **Connecting to Messaging Systems:** Pedestal can be integrated with messaging systems like Kafka or RabbitMQ to enable asynchronous communication between services. This is particularly useful in event-driven architectures.

- **Interoperability with Java:** Leverage Clojure's interoperability with Java to integrate Pedestal with existing Java libraries and frameworks. This allows you to reuse existing code and infrastructure.

### Conclusion

Pedestal is a powerful framework that excels in building high-performance web services and microservices architectures. Its unique features, such as the interceptor architecture and support for asynchronous processing, make it an ideal choice for applications that require high throughput and scalability. By understanding when to use Pedestal and how to optimize its performance, you can build robust, efficient, and maintainable applications that meet the demands of modern enterprise environments.

## Quiz Time!

{{< quizdown >}}

### What is one of the primary architectural features of Pedestal that makes it unique?

- [x] Interceptor Architecture
- [ ] Monolithic Design
- [ ] Synchronous Processing
- [ ] Built-in ORM

> **Explanation:** Pedestal's interceptor architecture provides a flexible and composable way to handle HTTP requests and responses, making it unique.

### Why is Pedestal well-suited for high-throughput applications?

- [x] Non-blocking I/O
- [ ] Built-in Database Support
- [ ] Monolithic Design
- [ ] Synchronous Processing

> **Explanation:** Pedestal uses non-blocking I/O operations, allowing it to handle multiple requests concurrently, which is ideal for high-throughput applications.

### How does Pedestal support microservices architectures?

- [x] Modularity and Asynchronous Communication
- [ ] Built-in Service Discovery
- [ ] Monolithic Design
- [ ] Synchronous Processing

> **Explanation:** Pedestal's modularity and support for asynchronous communication make it well-suited for microservices architectures.

### What is a common strategy for optimizing Pedestal applications?

- [x] Optimize Interceptor Chains
- [ ] Use Monolithic Architecture
- [ ] Avoid Caching
- [ ] Use Synchronous Processing

> **Explanation:** Optimizing interceptor chains by removing unnecessary processing is a common strategy for improving Pedestal application performance.

### Which of the following is NOT a feature of Pedestal?

- [ ] Interceptor Architecture
- [ ] Asynchronous Capabilities
- [x] Built-in ORM
- [ ] Extensibility

> **Explanation:** Pedestal does not include a built-in ORM; it focuses on web service architecture and extensibility.

### How can Pedestal be integrated with existing systems?

- [x] Interfacing with Databases and Messaging Systems
- [ ] Only through Java Interoperability
- [ ] By Rewriting Existing Systems
- [ ] Using Built-in ORM

> **Explanation:** Pedestal can be integrated with existing systems through interfacing with databases, messaging systems, and leveraging Java interoperability.

### What is a benefit of using Pedestal's asynchronous capabilities?

- [x] Efficient Resource Utilization
- [ ] Increased Latency
- [ ] Simplified Synchronous Code
- [ ] Reduced Scalability

> **Explanation:** Pedestal's asynchronous capabilities allow for efficient resource utilization, enabling better handling of concurrent requests.

### Which tool can be used with Pedestal for service discovery?

- [x] Consul
- [ ] Built-in Service Discovery
- [ ] Monolithic Registry
- [ ] Synchronous Directory

> **Explanation:** While Pedestal does not provide built-in service discovery, it can be integrated with tools like Consul for this purpose.

### What is a key consideration when building high-performance applications with Pedestal?

- [x] Monitoring and Profiling Performance
- [ ] Avoiding Caching
- [ ] Using Monolithic Design
- [ ] Limiting Scalability

> **Explanation:** Monitoring and profiling performance is crucial for identifying bottlenecks and optimizing high-performance applications built with Pedestal.

### True or False: Pedestal is only suitable for small-scale applications.

- [ ] True
- [x] False

> **Explanation:** False. Pedestal is suitable for both small-scale and large-scale applications, particularly those requiring high throughput and scalability.

{{< /quizdown >}}
