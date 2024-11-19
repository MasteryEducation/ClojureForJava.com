---
linkTitle: "8.3.2 Creating Custom Interceptors"
title: "Creating Custom Interceptors in Pedestal: A Comprehensive Guide"
description: "Explore the intricacies of creating custom interceptors in Pedestal, focusing on their structure, state management, and practical applications in enterprise integration."
categories:
- Clojure
- Web Development
- Enterprise Integration
tags:
- Clojure
- Pedestal
- Interceptors
- Middleware
- Web Services
date: 2024-10-25
type: docs
nav_weight: 832000
canonical: "https://clojureforjava.com/4/8/3/2"
license: "© 2024 Tokenizer Inc. CC BY-NC-SA 4.0"
---

## 8.3.2 Creating Custom Interceptors

In the world of web development with Clojure, Pedestal stands out for its powerful and flexible architecture, largely due to its use of interceptors. Interceptors are the backbone of Pedestal's request processing pipeline, allowing developers to implement cross-cutting concerns such as logging, authentication, and data transformation in a modular and reusable way. This section delves into the creation of custom interceptors, exploring their structure, state management, and the impact of their ordering on application behavior.

### Understanding the Interceptor Structure

An interceptor in Pedestal is a map that can contain up to three keys: `:enter`, `:leave`, and `:error`. Each of these keys corresponds to a function that takes a context map as an argument and returns a modified context map. Let's break down each component:

- **`:enter`**: This function is invoked when a request enters the interceptor. It is typically used for initial processing, such as extracting data from the request or performing authentication checks.

- **`:leave`**: This function is called when the request is leaving the interceptor, usually after the main processing logic has been executed. It is often used for tasks like response modification or logging.

- **`:error`**: This function is triggered if an error occurs during the processing of the request. It allows for custom error handling and recovery strategies.

Here's a basic template for a custom interceptor:

```clojure
(def my-interceptor
  {:enter (fn [context]
            ;; Enter logic here
            context)
   :leave (fn [context]
            ;; Leave logic here
            context)
   :error (fn [context exception]
            ;; Error handling logic here
            context)})
```

### State Management with the Context Map

The context map is a central concept in Pedestal's interceptor model. It serves as a shared state that can be passed between interceptors, allowing them to communicate and share data. The context map typically contains:

- **`:request`**: The original HTTP request map.
- **`:response`**: The HTTP response map, which can be modified by interceptors.
- **`:path-params`**: Parameters extracted from the request path.
- **`:query-params`**: Parameters extracted from the query string.
- **`:form-params`**: Parameters extracted from the form data.

To pass data between interceptors, you can add custom keys to the context map. Here's an example of how to add and retrieve data:

```clojure
(def add-user-id-interceptor
  {:enter (fn [context]
            (assoc context :user-id (get-in context [:request :headers "user-id"])))
   :leave (fn [context]
            (let [user-id (:user-id context)]
              (println "User ID:" user-id)
              context))})
```

In this example, the `:enter` function extracts a user ID from the request headers and adds it to the context map. The `:leave` function then retrieves and logs this user ID.

### Practical Examples of Custom Interceptors

#### Logging Interceptor

A logging interceptor is a common requirement in web applications, providing insights into request and response data. Here's a simple logging interceptor:

```clojure
(def logging-interceptor
  {:enter (fn [context]
            (println "Request:" (:request context))
            context)
   :leave (fn [context]
            (println "Response:" (:response context))
            context)})
```

This interceptor logs the request when it enters and the response when it leaves.

#### Authentication Interceptor

Authentication is a critical aspect of web applications. An authentication interceptor can check for valid credentials and halt the request processing if authentication fails:

```clojure
(defn authenticate [context]
  (let [auth-header (get-in context [:request :headers "authorization"])]
    (if (valid-auth? auth-header)
      context
      (assoc context :response {:status 401 :body "Unauthorized"}))))

(def auth-interceptor
  {:enter authenticate})
```

In this example, the `authenticate` function checks the `Authorization` header and either allows the request to proceed or returns a 401 Unauthorized response.

#### Data Transformation Interceptor

Sometimes, you need to transform request or response data. Here's an interceptor that transforms JSON request bodies into Clojure maps:

```clojure
(def json-body-interceptor
  {:enter (fn [context]
            (let [body (slurp (get-in context [:request :body]))]
              (assoc-in context [:request :json-body] (json/parse-string body true))))
   :leave (fn [context]
            (let [response-body (get-in context [:response :body])]
              (assoc-in context [:response :body] (json/generate-string response-body))))})
```

This interceptor reads the request body, parses it as JSON, and adds it to the context map. It also serializes the response body back to JSON.

### Interceptor Ordering and Its Impact

The order in which interceptors are executed can significantly affect application behavior. Interceptors are executed in the order they appear in the interceptor chain, with `:enter` functions being called first, followed by the main processing logic, and then `:leave` functions in reverse order.

Consider the following interceptor chain:

```clojure
(def service-interceptors
  [logging-interceptor
   auth-interceptor
   json-body-interceptor])
```

In this chain, the logging interceptor will log the request first, followed by the authentication check. If authentication fails, the request processing will halt, and the JSON body interceptor will not be executed. If authentication succeeds, the JSON body interceptor will parse the request body.

#### Best Practices for Interceptor Ordering

- **Place authentication and authorization interceptors early** in the chain to prevent unauthorized access to resources.
- **Logging interceptors can be placed at the beginning and end** of the chain to capture both request and response data.
- **Data transformation interceptors should be placed after authentication** to ensure that only authenticated requests are processed.

### Advanced Interceptor Techniques

#### Conditional Interceptors

Sometimes, you may want to execute an interceptor conditionally based on certain criteria. You can achieve this by wrapping the interceptor logic in a conditional statement:

```clojure
(defn conditional-interceptor [condition-fn interceptor]
  {:enter (fn [context]
            (if (condition-fn context)
              ((:enter interceptor) context)
              context))
   :leave (fn [context]
            (if (condition-fn context)
              ((:leave interceptor) context)
              context))
   :error (fn [context exception]
            (if (condition-fn context)
              ((:error interceptor) context exception)
              context))})
```

This function takes a condition function and an interceptor, executing the interceptor only if the condition is met.

#### Composing Interceptors

For complex applications, you might want to compose multiple interceptors into a single unit. This can be done by creating a composite interceptor that combines the logic of several interceptors:

```clojure
(def composite-interceptor
  {:enter (fn [context]
            (-> context
                (first-interceptor :enter)
                (second-interceptor :enter)))
   :leave (fn [context]
            (-> context
                (second-interceptor :leave)
                (first-interceptor :leave)))
   :error (fn [context exception]
            (-> context
                (first-interceptor :error exception)
                (second-interceptor :error exception)))})
```

This composite interceptor applies the `:enter`, `:leave`, and `:error` functions of two interceptors in sequence.

### Conclusion

Creating custom interceptors in Pedestal is a powerful way to manage cross-cutting concerns in your web applications. By understanding the interceptor structure, effectively managing state with the context map, and carefully considering interceptor ordering, you can build robust and maintainable applications. Whether you're implementing logging, authentication, or data transformation, interceptors provide the flexibility and modularity needed for enterprise integration.

## Quiz Time!

{{< quizdown >}}

### What are the three main components of a Pedestal interceptor?

- [x] `:enter`, `:leave`, `:error`
- [ ] `:start`, `:process`, `:finish`
- [ ] `:init`, `:execute`, `:finalize`
- [ ] `:begin`, `:middle`, `:end`

> **Explanation:** A Pedestal interceptor consists of `:enter`, `:leave`, and `:error` functions, which handle the request as it enters, leaves, or encounters an error.

### How can data be passed between interceptors in Pedestal?

- [x] Using the context map
- [ ] Using global variables
- [ ] Using session storage
- [ ] Using environment variables

> **Explanation:** The context map is used to pass data between interceptors, allowing them to share and modify state.

### Which interceptor function is used for initial processing of a request?

- [x] `:enter`
- [ ] `:leave`
- [ ] `:error`
- [ ] `:init`

> **Explanation:** The `:enter` function is used for initial processing when a request enters the interceptor.

### What is a common use case for the `:leave` function in an interceptor?

- [x] Modifying the response
- [ ] Authenticating the user
- [ ] Parsing the request body
- [ ] Handling errors

> **Explanation:** The `:leave` function is often used to modify the response before it is sent back to the client.

### In what order are interceptors executed in Pedestal?

- [x] `:enter` functions in order, then `:leave` functions in reverse order
- [ ] `:leave` functions in order, then `:enter` functions in reverse order
- [ ] `:enter` and `:leave` functions in parallel
- [ ] `:error` functions first, then `:enter` and `:leave`

> **Explanation:** Interceptors execute `:enter` functions in the order they appear, followed by `:leave` functions in reverse order.

### What happens if an interceptor's `:enter` function returns a response map directly?

- [x] The interceptor chain is halted, and the response is returned immediately
- [ ] The response is ignored, and processing continues
- [ ] An error is thrown
- [ ] The response is logged but not returned

> **Explanation:** If an `:enter` function returns a response map, it halts the interceptor chain, and the response is sent immediately.

### How can you execute an interceptor conditionally?

- [x] By wrapping the interceptor logic in a conditional statement
- [ ] By using a special `:conditional` key in the interceptor
- [ ] By setting a global flag
- [ ] By modifying the context map directly

> **Explanation:** You can execute an interceptor conditionally by wrapping its logic in a conditional statement that checks a specific condition.

### What is a composite interceptor?

- [x] An interceptor that combines the logic of multiple interceptors
- [ ] An interceptor that handles both requests and responses
- [ ] An interceptor that can be reused across different applications
- [ ] An interceptor that logs all requests

> **Explanation:** A composite interceptor combines the logic of multiple interceptors into a single unit, allowing for more complex processing.

### Which of the following is a best practice for interceptor ordering?

- [x] Place authentication interceptors early in the chain
- [ ] Place logging interceptors at the end of the chain
- [ ] Place data transformation interceptors before authentication
- [ ] Place error handling interceptors first

> **Explanation:** Authentication interceptors should be placed early to prevent unauthorized access to resources.

### True or False: The context map is immutable and cannot be modified by interceptors.

- [ ] True
- [x] False

> **Explanation:** False. The context map is mutable and can be modified by interceptors to pass data and state.

{{< /quizdown >}}
