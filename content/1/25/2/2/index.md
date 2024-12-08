---
canonical: "https://clojureforjava.com/1/25/2/2"
title: "Clojure Linting and Static Analysis Tools: Enhance Code Quality with clj-kondo, eastwood, and kibit"
description: "Explore essential linting and static analysis tools for Clojure, including clj-kondo, eastwood, and kibit. Learn how to integrate these tools into your development workflow to maintain high code quality and enforce coding standards."
linkTitle: "C.2.2 Linting and Static Analysis Tools"
tags:
- "Clojure"
- "Linting"
- "Static Analysis"
- "clj-kondo"
- "eastwood"
- "kibit"
- "Code Quality"
- "Functional Programming"
date: 2024-11-25
type: docs
nav_weight: 252200
license: "© 2024 Tokenizer Inc. CC BY-NC-SA 4.0"
---

## C.2.2 Linting and Static Analysis Tools

As experienced Java developers transitioning to Clojure, maintaining code quality is paramount. Just as Java developers rely on tools like Checkstyle, PMD, and FindBugs, Clojure offers powerful linting and static analysis tools to ensure your code is clean, idiomatic, and free of common pitfalls. In this section, we'll explore three essential tools: **clj-kondo**, **eastwood**, and **kibit**. We'll also discuss how to integrate these tools into your development environment and CI pipelines to enforce coding standards effectively.

### Why Linting and Static Analysis?

Before diving into specific tools, let's briefly discuss why linting and static analysis are crucial:

- **Code Quality**: These tools help identify potential errors, bad practices, and non-idiomatic code, leading to more maintainable and robust applications.
- **Consistency**: Enforcing coding standards across your team ensures consistency, making the codebase easier to understand and navigate.
- **Early Error Detection**: Catching issues early in the development process reduces the cost and effort of fixing bugs later.
- **Learning and Improvement**: Tools like kibit suggest idiomatic replacements, helping developers learn and adopt best practices.

### clj-kondo: Real-Time Feedback and Static Analysis

**clj-kondo** is a popular linter and static analyzer for Clojure. It provides real-time feedback as you write code, integrating seamlessly with various editors. Let's explore its features and how to set it up.

#### Key Features of clj-kondo

- **Real-Time Feedback**: Provides instant feedback in your editor, highlighting issues as you type.
- **Customizable**: Supports custom configurations to tailor linting rules to your project's needs.
- **Fast and Lightweight**: Designed to be fast, making it suitable for large codebases.
- **Editor Integration**: Works with popular editors like Emacs, IntelliJ IDEA, and Visual Studio Code.

#### Setting Up clj-kondo

To get started with clj-kondo, follow these steps:

1. **Installation**: You can install clj-kondo via Homebrew on macOS, or download the binary for your operating system from the [official GitHub repository](https://github.com/clj-kondo/clj-kondo).

   ```bash
   # Install via Homebrew
   brew install borkdude/brew/clj-kondo
   ```

2. **Editor Integration**: Integrate clj-kondo with your preferred editor. For example, in Visual Studio Code, you can use the Calva extension, which supports clj-kondo out of the box.

3. **Configuration**: Create a `.clj-kondo/config.edn` file in your project to customize linting rules. Here's a sample configuration:

   ```clojure
   ;; .clj-kondo/config.edn
   {:linters {:unused-var {:level :warning}
              :missing-docstring {:level :info}}}
   ```

4. **Running clj-kondo**: You can run clj-kondo manually to lint your codebase:

   ```bash
   clj-kondo --lint src
   ```

#### Example: Using clj-kondo

Consider the following Clojure code snippet:

```clojure
(defn add [x y]
  (+ x y))

(defn unused-fn []
  (println "This function is never used"))
```

When you run clj-kondo, it will highlight that `unused-fn` is defined but never used, helping you keep your code clean.

### eastwood: Deep Code Analysis

**eastwood** is another powerful tool for static analysis in Clojure. It goes beyond simple linting, performing deeper code analysis to detect potential errors and bad practices.

#### Key Features of eastwood

- **Comprehensive Analysis**: Detects a wide range of issues, including potential bugs, performance problems, and style violations.
- **Customizable**: Allows you to enable or disable specific checks based on your project's requirements.
- **Integration with CI**: Can be integrated into your CI pipeline to enforce coding standards automatically.

#### Setting Up eastwood

To set up eastwood, follow these steps:

1. **Add Dependency**: Add eastwood as a dependency in your `project.clj` file:

   ```clojure
   ;; project.clj
   :plugins [[jonase/eastwood "0.9.9"]]
   ```

2. **Running eastwood**: Use Leiningen to run eastwood on your project:

   ```bash
   lein eastwood
   ```

3. **Configuration**: Customize eastwood's behavior by creating an `eastwood.clj` file in your project. Here's an example configuration:

   ```clojure
   ;; eastwood.clj
   {:linters [:unused-vars :constant-test]
    :exclude-namespaces [my.project.generated]}
   ```

#### Example: Using eastwood

Let's analyze a simple Clojure function with eastwood:

```clojure
(defn divide [x y]
  (if (zero? y)
    (throw (IllegalArgumentException. "Division by zero"))
    (/ x y)))
```

Running eastwood might reveal that the exception handling could be improved, prompting you to refine your code.

### kibit: Suggesting Idiomatic Code

**kibit** is a tool that suggests idiomatic replacements and refactorings for your Clojure code. It helps you write more idiomatic and concise code by identifying patterns that can be simplified.

#### Key Features of kibit

- **Idiomatic Suggestions**: Provides suggestions for refactoring code to be more idiomatic.
- **Easy to Use**: Simple command-line interface for analyzing your codebase.
- **Educational**: Helps developers learn idiomatic Clojure patterns.

#### Setting Up kibit

To set up kibit, follow these steps:

1. **Add Dependency**: Add kibit as a dependency in your `project.clj` file:

   ```clojure
   ;; project.clj
   :plugins [[lein-kibit "0.1.8"]]
   ```

2. **Running kibit**: Use Leiningen to run kibit on your project:

   ```bash
   lein kibit
   ```

#### Example: Using kibit

Consider the following Clojure code:

```clojure
(if (not (empty? coll))
  (first coll)
  nil)
```

kibit will suggest replacing this with the more idiomatic `first` function:

```clojure
(first coll)
```

### Integrating Linting and Analysis Tools into Your Workflow

Integrating these tools into your development workflow ensures that code quality is maintained consistently. Here are some strategies:

#### Editor Integration

- **Visual Studio Code**: Use the Calva extension for clj-kondo integration.
- **IntelliJ IDEA**: Use the Cursive plugin, which supports clj-kondo.
- **Emacs**: Integrate clj-kondo with CIDER for real-time feedback.

#### Continuous Integration (CI)

- **Automate Checks**: Configure your CI pipeline to run clj-kondo, eastwood, and kibit on every commit, ensuring that code quality is enforced automatically.
- **Fail Builds on Errors**: Set up your CI to fail builds if any linting or analysis errors are detected, preventing problematic code from being merged.

### Comparing Clojure Tools with Java

Let's compare these Clojure tools with their Java counterparts to highlight similarities and differences:

| Feature        | clj-kondo (Clojure) | Checkstyle (Java) |
|----------------|---------------------|-------------------|
| Real-Time Feedback | Yes                 | No                |
| Customizable  | Yes                 | Yes               |
| Editor Integration | Yes                 | Yes               |

| Feature        | eastwood (Clojure) | PMD (Java)        |
|----------------|--------------------|-------------------|
| Comprehensive Analysis | Yes                | Yes               |
| Customizable  | Yes                | Yes               |
| CI Integration | Yes                | Yes               |

| Feature        | kibit (Clojure)   | SonarLint (Java)  |
|----------------|-------------------|-------------------|
| Idiomatic Suggestions | Yes               | Yes               |
| Educational   | Yes               | Yes               |
| Easy to Use   | Yes               | Yes               |

### Try It Yourself

To get hands-on experience, try the following exercises:

1. **Install clj-kondo** and integrate it with your editor. Write a simple Clojure function and observe the real-time feedback.
2. **Run eastwood** on a Clojure project and analyze the output. Identify any potential improvements in your code.
3. **Use kibit** to refactor a piece of Clojure code. Compare the original and refactored versions to understand the idiomatic changes.

### Exercises

1. **Exercise 1**: Write a Clojure function with unused variables and run clj-kondo to identify them.
2. **Exercise 2**: Create a Clojure project with potential performance issues and use eastwood to detect them.
3. **Exercise 3**: Write non-idiomatic Clojure code and use kibit to refactor it.

### Summary and Key Takeaways

- **clj-kondo** provides real-time feedback and is highly customizable, making it an essential tool for maintaining code quality.
- **eastwood** offers deep code analysis, helping you detect potential errors and bad practices.
- **kibit** suggests idiomatic replacements, aiding in writing concise and idiomatic Clojure code.
- Integrating these tools into your development workflow and CI pipeline ensures consistent code quality and adherence to coding standards.

By leveraging these tools, you can maintain high code quality, enforce coding standards, and write idiomatic Clojure code, making your transition from Java to Clojure smoother and more effective.

## Quiz: Test Your Knowledge on Clojure Linting and Static Analysis Tools

{{< quizdown >}}

### Which tool provides real-time feedback in your editor for Clojure code?

- [x] clj-kondo
- [ ] eastwood
- [ ] kibit
- [ ] Checkstyle

> **Explanation:** clj-kondo provides real-time feedback as you write code, integrating seamlessly with various editors.

### What is the primary purpose of eastwood in Clojure development?

- [ ] Suggesting idiomatic code replacements
- [x] Performing deep code analysis
- [ ] Providing real-time feedback
- [ ] Managing dependencies

> **Explanation:** eastwood performs deep code analysis to detect potential errors and bad practices.

### Which tool is used for suggesting idiomatic replacements in Clojure code?

- [ ] clj-kondo
- [ ] eastwood
- [x] kibit
- [ ] PMD

> **Explanation:** kibit suggests idiomatic replacements and refactorings for Clojure code.

### How can clj-kondo be integrated into a CI pipeline?

- [x] By configuring the CI pipeline to run clj-kondo on every commit
- [ ] By using it only in the editor
- [ ] By manually running it after code is merged
- [ ] By integrating it with Maven

> **Explanation:** clj-kondo can be integrated into a CI pipeline to run on every commit, ensuring code quality is enforced automatically.

### Which of the following is a feature of kibit?

- [x] Idiomatic Suggestions
- [ ] Real-Time Feedback
- [ ] Deep Code Analysis
- [ ] Dependency Management

> **Explanation:** kibit provides idiomatic suggestions for refactoring Clojure code.

### What is a common feature between clj-kondo and Checkstyle?

- [x] Customizable linting rules
- [ ] Real-time feedback
- [ ] Deep code analysis
- [ ] Suggesting idiomatic replacements

> **Explanation:** Both clj-kondo and Checkstyle allow for customizable linting rules.

### Which tool would you use to detect unused variables in Clojure?

- [x] clj-kondo
- [ ] eastwood
- [ ] kibit
- [ ] SonarLint

> **Explanation:** clj-kondo can detect unused variables and provide feedback.

### What is the main advantage of integrating linting tools into your CI pipeline?

- [x] Ensuring consistent code quality
- [ ] Reducing build time
- [ ] Automating deployment
- [ ] Managing dependencies

> **Explanation:** Integrating linting tools into your CI pipeline ensures consistent code quality across the codebase.

### Which tool is known for its educational value in suggesting idiomatic Clojure patterns?

- [ ] clj-kondo
- [ ] eastwood
- [x] kibit
- [ ] PMD

> **Explanation:** kibit is known for its educational value in suggesting idiomatic Clojure patterns.

### True or False: eastwood can be used to enforce coding standards automatically in a CI pipeline.

- [x] True
- [ ] False

> **Explanation:** eastwood can be integrated into a CI pipeline to enforce coding standards automatically.

{{< /quizdown >}}
