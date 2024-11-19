---
linkTitle: "10.1.3 Serving Static Content and Templates"
title: "Serving Static Content and Templates in Clojure Web Applications"
description: "Learn how to serve static files and use templating libraries like Selmer and Hiccup to create dynamic HTML content in Clojure web applications."
categories:
- Clojure
- Web Development
- Functional Programming
tags:
- Clojure
- Web Development
- Templating
- Static Content
- Security
date: 2024-10-25
type: docs
nav_weight: 1013000
canonical: "https://clojureforjava.com/2/10/1/3"
license: "© 2024 Tokenizer Inc. CC BY-NC-SA 4.0"
---

## 10.1.3 Serving Static Content and Templates

In the realm of web development, serving static content and generating dynamic HTML pages are fundamental tasks. As a Java engineer venturing into Clojure, you'll find that Clojure offers elegant solutions for both. This section will guide you through serving static files using middleware and creating dynamic views with templating libraries such as Selmer and Hiccup. We'll also explore best practices for organizing templates and ensuring security against common web vulnerabilities like Cross-Site Scripting (XSS).

### Serving Static Files with Middleware

Static files such as CSS, JavaScript, and images are integral to web applications. In Clojure, serving these files efficiently can be achieved using middleware. Middleware acts as an intermediary layer that processes requests and responses, making it ideal for handling static content.

#### Using Ring Middleware for Static Content

Ring, a popular Clojure web application library, provides a straightforward way to serve static files. The `ring.middleware.resource` middleware is commonly used for this purpose. It allows you to specify a directory from which static files will be served.

Here's an example of how to set up a Ring application to serve static files:

```clojure
(ns myapp.core
  (:require [ring.adapter.jetty :refer [run-jetty]]
            [ring.middleware.resource :refer [wrap-resource]]
            [ring.middleware.defaults :refer [wrap-defaults site-defaults]]))

(defn app [request]
  {:status 200
   :headers {"Content-Type" "text/html"}
   :body "<h1>Welcome to My Clojure Web App</h1>"})

(defn -main []
  (run-jetty (wrap-defaults (wrap-resource app "public") site-defaults)
             {:port 3000}))
```

In this setup, the `wrap-resource` middleware is used to serve static files from the `public` directory. When a request is made for a static file, such as `/css/style.css`, the middleware will look for the file in the `public/css` directory and serve it if found.

#### Organizing Static Files

To keep your project organized, it's a good practice to structure your static files in a clear directory hierarchy. A common convention is to have a `public` directory at the root of your project, with subdirectories for different types of static content:

```
myapp/
├── src/
│   └── myapp/
│       └── core.clj
├── public/
│   ├── css/
│   │   └── style.css
│   ├── js/
│   │   └── app.js
│   └── images/
│       └── logo.png
└── resources/
```

### Templating with Selmer and Hiccup

Dynamic web pages require templating systems to generate HTML content. Clojure offers several templating libraries, with Selmer and Hiccup being among the most popular.

#### Selmer: A Django-Inspired Templating Engine

Selmer is a templating engine for Clojure inspired by Django's template language. It allows you to create templates with familiar syntax and supports features like variable interpolation and control structures.

##### Setting Up Selmer

To use Selmer, add it to your project dependencies:

```clojure
:dependencies [[selmer "1.12.40"]]
```

##### Creating a Selmer Template

Selmer templates are typically stored in the `resources/templates` directory. Here's an example of a simple Selmer template:

```html
<!-- resources/templates/welcome.html -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Welcome</title>
    <link rel="stylesheet" href="/css/style.css">
</head>
<body>
    <h1>Welcome, {{name}}!</h1>
    {% if logged_in %}
    <p>You are logged in as {{username}}.</p>
    {% else %}
    <p>Please log in to access more features.</p>
    {% endif %}
</body>
</html>
```

##### Rendering a Selmer Template

To render a Selmer template, use the `selmer.parser/render-file` function:

```clojure
(ns myapp.core
  (:require [selmer.parser :refer [render-file]]))

(defn render-welcome-page [name logged-in username]
  (render-file "templates/welcome.html"
               {:name name
                :logged_in logged-in
                :username username}))
```

This function takes the template file path and a map of variables to interpolate into the template. It returns the rendered HTML as a string.

#### Hiccup: Generating HTML with Clojure Data Structures

Hiccup is another popular templating library that allows you to generate HTML using Clojure data structures. It provides a more programmatic approach compared to Selmer's template files.

##### Creating HTML with Hiccup

With Hiccup, HTML elements are represented as Clojure vectors. Here's an example of generating a simple HTML page:

```clojure
(ns myapp.core
  (:require [hiccup.page :refer [html5 include-css]]))

(defn welcome-page [name logged-in username]
  (html5
    [:head
     [:title "Welcome"]
     (include-css "/css/style.css")]
    [:body
     [:h1 (str "Welcome, " name "!")]
     (if logged-in
       [:p (str "You are logged in as " username ".")]
       [:p "Please log in to access more features."])]))
```

In this example, `html5` is a helper function that generates the HTML5 doctype and basic structure. The `include-css` function is used to include a CSS file.

### Creating Dynamic Views with Templates

Dynamic views are essential for interactive web applications. Both Selmer and Hiccup support variable interpolation and control structures, allowing you to create rich, dynamic content.

#### Variable Interpolation

Variable interpolation is the process of inserting variable values into a template. In Selmer, this is done using the `{{variable}}` syntax, while in Hiccup, you can directly use Clojure expressions.

#### Control Structures

Control structures like conditionals and loops are crucial for dynamic content. Selmer supports these with `{% if %}`, `{% else %}`, and `{% for %}` tags. Hiccup, being a Clojure library, uses standard Clojure control structures like `if` and `for`.

Here's an example of using a loop in a Selmer template:

```html
<!-- resources/templates/items.html -->
<ul>
{% for item in items %}
    <li>{{item}}</li>
{% endfor %}
</ul>
```

And the equivalent in Hiccup:

```clojure
(defn items-list [items]
  [:ul
   (for [item items]
     [:li item])])
```

### Organizing Templates and Partials

As your application grows, organizing templates becomes crucial for maintainability. A common practice is to use partials—reusable template fragments that can be included in other templates.

#### Using Partials in Selmer

Selmer supports partials through the `{% include %}` tag. Here's how you might use a partial for a navigation bar:

```html
<!-- resources/templates/navbar.html -->
<nav>
    <ul>
        <li><a href="/">Home</a></li>
        <li><a href="/about">About</a></li>
        <li><a href="/contact">Contact</a></li>
    </ul>
</nav>
```

```html
<!-- resources/templates/base.html -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>{{title}}</title>
    <link rel="stylesheet" href="/css/style.css">
</head>
<body>
    {% include "navbar.html" %}
    <div class="content">
        {{content}}
    </div>
</body>
</html>
```

#### Using Partials in Hiccup

In Hiccup, you can create reusable functions for partials:

```clojure
(defn navbar []
  [:nav
   [:ul
    [:li [:a {:href "/"} "Home"]]
    [:li [:a {:href "/about"} "About"]]
    [:li [:a {:href "/contact"} "Contact"]]]])

(defn base-page [title content]
  (html5
    [:head
     [:title title]
     (include-css "/css/style.css")]
    [:body
     (navbar)
     [:div.content content]]))
```

### Security Considerations: Preventing XSS

Security is paramount when generating HTML content dynamically. Cross-Site Scripting (XSS) is a common vulnerability that occurs when untrusted data is included in web pages without proper validation or escaping.

#### Escaping User Input

Both Selmer and Hiccup provide mechanisms to escape user input, preventing XSS attacks.

- **Selmer**: Automatically escapes variables by default. You can disable escaping with the `|safe` filter, but use it cautiously.
- **Hiccup**: Automatically escapes strings, ensuring that user input is safe by default.

#### Best Practices for Security

- **Validate Input**: Always validate and sanitize user input before processing it.
- **Use HTTPS**: Ensure your application uses HTTPS to protect data in transit.
- **Regular Security Audits**: Conduct regular security audits and keep dependencies up to date.

### Conclusion

Serving static content and generating dynamic HTML pages are essential skills for building robust web applications in Clojure. By leveraging middleware for static files and templating libraries like Selmer and Hiccup, you can create efficient, secure, and maintainable web applications. Remember to organize your templates for reuse and prioritize security to protect your application from vulnerabilities.

## Quiz Time!

{{< quizdown >}}

### What is the purpose of using middleware in a Clojure web application?

- [x] To process requests and responses, such as serving static files
- [ ] To compile Clojure code into Java bytecode
- [ ] To manage database connections
- [ ] To handle user authentication

> **Explanation:** Middleware acts as an intermediary layer that processes requests and responses, making it ideal for handling tasks like serving static files.

### Which Clojure library is inspired by Django's template language?

- [x] Selmer
- [ ] Hiccup
- [ ] Compojure
- [ ] Ring

> **Explanation:** Selmer is a templating engine for Clojure inspired by Django's template language.

### How does Hiccup represent HTML elements?

- [x] As Clojure vectors
- [ ] As JSON objects
- [ ] As XML strings
- [ ] As plain text

> **Explanation:** Hiccup represents HTML elements as Clojure vectors, allowing for a programmatic approach to generating HTML.

### What is a common practice for organizing templates in a Clojure web application?

- [x] Using partials for reusable template fragments
- [ ] Storing all templates in a single file
- [ ] Embedding templates directly in Java code
- [ ] Avoiding the use of templates altogether

> **Explanation:** Using partials—reusable template fragments—is a common practice for organizing templates in a maintainable way.

### How does Selmer prevent Cross-Site Scripting (XSS) attacks?

- [x] By automatically escaping variables by default
- [ ] By disabling JavaScript in the browser
- [ ] By encrypting all user input
- [ ] By using a custom HTML parser

> **Explanation:** Selmer automatically escapes variables by default, preventing XSS attacks by ensuring that user input is safe.

### Which function is used to render a Selmer template?

- [x] `selmer.parser/render-file`
- [ ] `hiccup.page/html5`
- [ ] `ring.middleware.resource/wrap-resource`
- [ ] `compojure.core/GET`

> **Explanation:** The `selmer.parser/render-file` function is used to render a Selmer template, taking a template file path and a map of variables.

### What is the role of the `wrap-resource` middleware in a Ring application?

- [x] To serve static files from a specified directory
- [ ] To manage user sessions
- [ ] To handle HTTP requests
- [ ] To compile Clojure code

> **Explanation:** The `wrap-resource` middleware is used to serve static files from a specified directory in a Ring application.

### Which templating library allows you to generate HTML using Clojure data structures?

- [x] Hiccup
- [ ] Selmer
- [ ] Ring
- [ ] Compojure

> **Explanation:** Hiccup allows you to generate HTML using Clojure data structures, providing a programmatic approach to HTML generation.

### What is a key security consideration when generating dynamic HTML content?

- [x] Preventing Cross-Site Scripting (XSS) attacks through proper escaping
- [ ] Using plain text for all user input
- [ ] Disabling all JavaScript functionality
- [ ] Storing HTML templates in a database

> **Explanation:** Preventing Cross-Site Scripting (XSS) attacks through proper escaping is a key security consideration when generating dynamic HTML content.

### True or False: Hiccup automatically escapes strings to prevent XSS attacks.

- [x] True
- [ ] False

> **Explanation:** True. Hiccup automatically escapes strings, ensuring that user input is safe and preventing XSS attacks.

{{< /quizdown >}}
