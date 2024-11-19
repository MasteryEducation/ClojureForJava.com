---
linkTitle: "4.4.1 Server-Side Rendering with Selmer"
title: "Server-Side Rendering with Selmer: A Comprehensive Guide for Clojure Developers"
description: "Explore the power of server-side rendering with Selmer in Clojure, including templating syntax, template inheritance, dynamic content, and internationalization support."
categories:
- Clojure
- Web Development
- Templating
tags:
- Selmer
- Server-Side Rendering
- Clojure
- Templating
- Internationalization
date: 2024-10-25
type: docs
nav_weight: 441000
canonical: "https://clojureforjava.com/4/4/4/1"
license: "© 2024 Tokenizer Inc. CC BY-NC-SA 4.0"
---

## 4.4.1 Server-Side Rendering with Selmer

In the realm of web development, server-side rendering (SSR) plays a crucial role in delivering dynamic, SEO-friendly content to users. For Clojure developers, Selmer stands out as a robust templating engine that facilitates SSR by allowing you to generate HTML on the server side. This section delves into the intricacies of using Selmer for server-side rendering, covering its syntax, template inheritance, dynamic content handling, and internationalization support.

### Introduction to Selmer

Selmer is a Clojure library inspired by Django's templating engine, designed to render HTML templates with embedded Clojure expressions. It provides a straightforward way to separate your application's logic from its presentation, making your codebase more maintainable and scalable.

#### Why Use Selmer?

- **Familiar Syntax:** If you're coming from a background in web development with Django or similar frameworks, Selmer's syntax will feel intuitive.
- **Flexibility:** Selmer allows you to embed Clojure code within your templates, offering powerful customization options.
- **Performance:** By rendering HTML on the server, Selmer can improve the perceived performance of your application, particularly for users with slower devices or connections.

### Selmer Syntax

Selmer's syntax is both powerful and easy to learn, featuring tags, filters, and expressions that allow you to manipulate data and control the flow of your templates.

#### Basic Syntax

At its core, Selmer uses double curly braces (`{{ }}`) to denote expressions and `{% %}` for control structures. Here's a simple example:

```html
<!DOCTYPE html>
<html>
<head>
    <title>{{ title }}</title>
</head>
<body>
    <h1>Welcome, {{ user.name }}!</h1>
    {% if user.admin %}
    <p>You have administrative privileges.</p>
    {% else %}
    <p>You are a regular user.</p>
    {% endif %}
</body>
</html>
```

In this example, `{{ title }}` and `{{ user.name }}` are expressions that will be replaced with values from your data model, while the `{% if %}` tag is used for conditional logic.

#### Filters

Selmer supports filters, which are functions that transform data before it's rendered. You can chain filters using the pipe (`|`) character:

```html
<p>The price is {{ price | number_format:2 }}</p>
```

Here, `number_format:2` formats the `price` variable to two decimal places.

### Template Inheritance

Template inheritance is a powerful feature that allows you to define a base template and extend it in other templates. This promotes reusability and consistency across your application.

#### Creating a Base Template

A base template typically contains the common structure of your web pages, such as the header, footer, and navigation bar. You can define blocks that child templates can override:

```html
<!DOCTYPE html>
<html>
<head>
    <title>{% block title %}My Application{% endblock %}</title>
</head>
<body>
    <header>
        <h1>My Application</h1>
    </header>
    <nav>
        <!-- Navigation links -->
    </nav>
    <main>
        {% block content %}
        <!-- Default content -->
        {% endblock %}
    </main>
    <footer>
        <p>&copy; 2024 My Application</p>
    </footer>
</body>
</html>
```

#### Extending the Base Template

Child templates can extend the base template and provide specific content for each block:

```html
{% extends "base.html" %}

{% block title %}Home Page{% endblock %}

{% block content %}
<h2>Welcome to the Home Page</h2>
<p>This is the main content of the home page.</p>
{% endblock %}
```

This approach ensures that any changes to the base template automatically propagate to all child templates, reducing duplication and maintenance effort.

### Dynamic Content

One of the key aspects of server-side rendering is the ability to inject dynamic content into your templates. Selmer makes this straightforward by allowing you to pass data from your Clojure handlers to the templates.

#### Passing Data to Templates

In a typical Clojure web application, you define handlers that process requests and return responses. To render a Selmer template, you pass a map of data to the `selmer.parser/render` function:

```clojure
(ns myapp.handler
  (:require [selmer.parser :as parser]))

(defn home-page-handler [request]
  (let [user {:name "Alice" :admin true}
        title "Home Page"]
    (parser/render-file "templates/home.html" {:user user :title title})))
```

In this example, the `home-page-handler` function renders the `home.html` template, passing the `user` and `title` data to it. The template can then access these values using the syntax described earlier.

#### Handling Complex Data Structures

Selmer can handle complex data structures, such as nested maps and sequences. You can iterate over collections using the `{% for %}` tag:

```html
<ul>
{% for item in items %}
    <li>{{ item.name }}: {{ item.price | number_format:2 }}</li>
{% endfor %}
</ul>
```

This template snippet iterates over a collection of `items`, rendering each item's name and price.

### Internationalization (i18n)

Supporting multiple languages is crucial for applications targeting a global audience. Selmer provides mechanisms to facilitate internationalization (i18n), allowing you to render templates in different languages based on user preferences or locale settings.

#### Setting Up i18n

To enable i18n in your Selmer templates, you'll need to integrate a library like `clj-i18n` or `tufte` to manage translations. These libraries typically use resource bundles or translation files to store localized strings.

#### Using Translation Keys

Once you've set up your translation infrastructure, you can use translation keys in your templates. Here's an example using a hypothetical translation function:

```html
<p>{{ t "welcome.message" }}</p>
```

In this example, `t` is a function that retrieves the translated string for the key `welcome.message` based on the current locale.

#### Handling Plurals and Gender

Advanced i18n support includes handling plurals and gender-specific translations. This often involves defining multiple translation keys and using conditional logic to select the appropriate one.

### Best Practices for Using Selmer

- **Keep Logic Out of Templates:** While Selmer allows you to embed Clojure code, it's best to keep complex logic in your handlers or service layer. Templates should focus on presentation.
- **Use Template Inheritance:** Leverage template inheritance to promote DRY (Don't Repeat Yourself) principles and maintain consistency across your application.
- **Optimize for Performance:** Consider caching rendered templates or using partials for frequently repeated sections to improve performance.
- **Test Your Templates:** Ensure your templates render correctly by writing tests that verify the output for different data scenarios.

### Common Pitfalls and Optimization Tips

- **Avoid Overusing Filters:** While filters are powerful, overusing them can lead to performance issues. Consider pre-processing data in your handlers if complex transformations are needed.
- **Watch for Missing Variables:** Selmer will throw an error if a template references a variable that isn't provided. Use default values or conditionals to handle optional data gracefully.
- **Profile Rendering Performance:** Use tools like VisualVM or YourKit to profile your application's performance and identify bottlenecks in template rendering.

### Conclusion

Selmer is a versatile and efficient tool for server-side rendering in Clojure applications. By mastering its syntax, leveraging template inheritance, and supporting internationalization, you can build dynamic, user-friendly web applications that cater to a global audience. As you integrate Selmer into your projects, keep best practices in mind to ensure your templates are maintainable, performant, and easy to understand.

## Quiz Time!

{{< quizdown >}}

### What is the primary purpose of Selmer in Clojure web applications?

- [x] To render HTML templates with embedded Clojure expressions
- [ ] To manage database connections
- [ ] To handle HTTP requests and responses
- [ ] To provide client-side interactivity

> **Explanation:** Selmer is a templating engine used for rendering HTML with embedded Clojure expressions, separating logic from presentation.

### How do you denote expressions in Selmer templates?

- [x] {{ }}
- [ ] [[ ]]
- [ ] << >>
- [ ] (( ))

> **Explanation:** Selmer uses double curly braces `{{ }}` to denote expressions within templates.

### What is the purpose of template inheritance in Selmer?

- [x] To define a base template and extend it in other templates
- [ ] To include JavaScript files in templates
- [ ] To manage CSS styles
- [ ] To connect to external APIs

> **Explanation:** Template inheritance allows you to define a base template and extend it in other templates, promoting reusability and consistency.

### How can you pass data from a Clojure handler to a Selmer template?

- [x] By passing a map of data to `selmer.parser/render`
- [ ] By using global variables
- [ ] By embedding data directly in the HTML
- [ ] By using a separate configuration file

> **Explanation:** Data is passed from a Clojure handler to a Selmer template by providing a map of data to the `selmer.parser/render` function.

### Which tag is used for conditional logic in Selmer templates?

- [x] {% if %}
- [ ] {{ if }}
- [ ] [[ if ]]
- [ ] (( if ))

> **Explanation:** The `{% if %}` tag is used for conditional logic in Selmer templates.

### What is the benefit of using filters in Selmer templates?

- [x] To transform data before rendering
- [ ] To connect to databases
- [ ] To manage user sessions
- [ ] To handle HTTP requests

> **Explanation:** Filters in Selmer templates are used to transform data before rendering, such as formatting numbers or dates.

### How can you support multiple languages in Selmer templates?

- [x] By using translation keys and a translation library
- [ ] By writing separate templates for each language
- [ ] By using inline translations
- [ ] By storing translations in a database

> **Explanation:** Supporting multiple languages in Selmer templates involves using translation keys and a translation library to manage localized strings.

### What is a common pitfall when using Selmer templates?

- [x] Referencing variables that aren't provided
- [ ] Using too many CSS styles
- [ ] Including JavaScript in templates
- [ ] Using too many HTML tags

> **Explanation:** A common pitfall is referencing variables in Selmer templates that aren't provided, which can lead to errors.

### How can you optimize the performance of Selmer templates?

- [x] By caching rendered templates or using partials
- [ ] By increasing server memory
- [ ] By using more CSS styles
- [ ] By reducing the number of HTML tags

> **Explanation:** Optimizing performance can be achieved by caching rendered templates or using partials for frequently repeated sections.

### True or False: Selmer templates should contain complex business logic.

- [ ] True
- [x] False

> **Explanation:** Selmer templates should focus on presentation and avoid complex business logic, which should be handled in the application's logic layer.

{{< /quizdown >}}
