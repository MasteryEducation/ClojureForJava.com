---
linkTitle: "13.4.2 Using Exclusions and Overrides"
title: "Dependency Management in Clojure: Using Exclusions and Overrides"
description: "Master the art of managing dependencies in Clojure by learning how to effectively use exclusions and overrides to resolve conflicts and optimize your project."
categories:
- Clojure
- Dependency Management
- Software Development
tags:
- Clojure
- Leiningen
- Deps.edn
- Dependency Exclusions
- Dependency Overrides
date: 2024-10-25
type: docs
nav_weight: 414200
canonical: "https://clojureforjava.com/3/4/1/4/2"
license: "© 2024 Tokenizer Inc. CC BY-NC-SA 4.0"
---

## 13.4.2 Using Exclusions and Overrides

In the world of software development, managing dependencies is a critical task that can significantly impact the stability and performance of your applications. For Clojure developers, especially those transitioning from Java, understanding how to handle dependency conflicts and optimize your project's dependency tree is essential. This section delves into the intricacies of using exclusions and overrides in Clojure, providing you with the knowledge and tools to manage dependencies effectively.

### Understanding Dependency Conflicts

Dependency conflicts occur when different libraries in your project require different versions of the same dependency. This can lead to a range of issues, from subtle bugs to outright application failures. In Clojure, as in many other languages, dependencies are often managed through tools like Leiningen or the Clojure CLI, which use `project.clj` and `deps.edn` files, respectively.

#### The Nature of Transitive Dependencies

Transitive dependencies are those that your direct dependencies rely on. While they can simplify dependency management by automatically including necessary libraries, they can also introduce conflicts. For instance, if two libraries depend on different versions of the same transitive dependency, it can lead to version clashes.

### Exclusions: Preventing Unwanted Dependencies

Exclusions allow you to prevent certain transitive dependencies from being included in your project. This is particularly useful when a transitive dependency is causing conflicts or is unnecessary for your application.

#### Specifying Exclusions in `project.clj`

Leiningen uses the `project.clj` file to manage dependencies. To exclude a transitive dependency, you can specify it directly within your dependency vector. Here's how you can do it:

```clojure
(defproject my-project "0.1.0-SNAPSHOT"
  :dependencies [[org.clojure/clojure "1.10.3"]
                 [com.example/library "2.0.0" :exclusions [org.clojure/tools.logging]]])
```

In this example, `com.example/library` is a dependency that normally brings in `org.clojure/tools.logging` as a transitive dependency. By specifying `:exclusions [org.clojure/tools.logging]`, we prevent it from being included.

#### Specifying Exclusions in `deps.edn`

For projects using the Clojure CLI, dependencies are managed through the `deps.edn` file. Exclusions can be specified similarly:

```clojure
{:deps {org.clojure/clojure {:mvn/version "1.10.3"}
        com.example/library {:mvn/version "2.0.0"
                             :exclusions [org.clojure/tools.logging]}}}
```

Here, the exclusion is specified within the map for `com.example/library`, ensuring that `org.clojure/tools.logging` is not included as a transitive dependency.

### Overrides: Ensuring Compatibility

Overrides are used to enforce a specific version of a dependency across your entire project, regardless of what versions are specified by your direct or transitive dependencies. This is particularly useful for ensuring compatibility and stability.

#### Using Overrides in `project.clj`

Leiningen allows you to specify overrides in the `:managed-dependencies` section of your `project.clj`:

```clojure
(defproject my-project "0.1.0-SNAPSHOT"
  :dependencies [[org.clojure/clojure "1.10.3"]
                 [com.example/library "2.0.0"]]
  :managed-dependencies [[org.clojure/tools.logging "1.1.0"]])
```

In this setup, `org.clojure/tools.logging` is enforced to be version `1.1.0` throughout the project, overriding any other version specified by dependencies.

#### Using Overrides in `deps.edn`

In `deps.edn`, you can use the `:override-deps` key to enforce specific versions:

```clojure
{:deps {org.clojure/clojure {:mvn/version "1.10.3"}
        com.example/library {:mvn/version "2.0.0"}}
 :override-deps {org.clojure/tools.logging {:mvn/version "1.1.0"}}}
```

This ensures that `org.clojure/tools.logging` is always version `1.1.0`, resolving any potential conflicts.

### Practical Examples and Use Cases

To illustrate the practical application of exclusions and overrides, let's consider a scenario where a project depends on multiple libraries that, in turn, depend on different versions of a common library.

#### Scenario: Resolving Conflicts in a Web Application

Imagine you are developing a web application that uses both `ring` and `compojure`. Both libraries depend on `ring/ring-core`, but they require different versions. This can lead to conflicts that need to be resolved.

##### Step 1: Identify the Conflict

First, you need to identify the conflicting versions. You can do this by running the dependency tree command in Leiningen:

```bash
lein deps :tree
```

Or with the Clojure CLI:

```bash
clj -Stree
```

This will output a tree of dependencies, allowing you to spot where the conflicts occur.

##### Step 2: Apply Exclusions

Once you've identified the conflicting transitive dependencies, you can apply exclusions to prevent the unwanted versions from being included:

```clojure
(defproject my-webapp "0.1.0-SNAPSHOT"
  :dependencies [[org.clojure/clojure "1.10.3"]
                 [ring/ring-core "1.9.0" :exclusions [ring/ring-core]]
                 [compojure "1.6.2" :exclusions [ring/ring-core]]])
```

In this example, both `ring` and `compojure` are instructed to exclude their transitive dependency on `ring/ring-core`, allowing you to specify the desired version directly.

##### Step 3: Use Overrides for Consistency

To ensure that the desired version of `ring/ring-core` is used consistently, you can specify it in the `:managed-dependencies` or `:override-deps`:

```clojure
(defproject my-webapp "0.1.0-SNAPSHOT"
  :dependencies [[org.clojure/clojure "1.10.3"]
                 [ring/ring-core "1.9.0"]
                 [compojure "1.6.2"]]
  :managed-dependencies [[ring/ring-core "1.9.0"]])
```

Or in `deps.edn`:

```clojure
{:deps {org.clojure/clojure {:mvn/version "1.10.3"}
        ring/ring-core {:mvn/version "1.9.0"}
        compojure {:mvn/version "1.6.2"}}
 :override-deps {ring/ring-core {:mvn/version "1.9.0"}}}
```

### Best Practices for Dependency Management

Managing dependencies effectively requires a strategic approach. Here are some best practices to consider:

1. **Regularly Audit Dependencies**: Regularly review your project's dependencies to identify potential conflicts and unnecessary libraries.

2. **Use Exclusions Sparingly**: While exclusions are powerful, overusing them can lead to maintenance challenges. Use them judiciously to resolve specific conflicts.

3. **Prefer Overrides for Critical Libraries**: For critical libraries that need to be consistent across your project, use overrides to enforce specific versions.

4. **Keep Dependencies Up-to-Date**: Regularly update your dependencies to benefit from the latest features and security patches.

5. **Document Your Decisions**: Clearly document why certain exclusions or overrides are in place to help future developers understand the rationale behind these decisions.

### Common Pitfalls and How to Avoid Them

Despite best efforts, dependency management can sometimes go awry. Here are some common pitfalls and how to avoid them:

- **Ignoring Transitive Dependencies**: Always be aware of the transitive dependencies your project is pulling in. Use tools to visualize and analyze your dependency tree.

- **Overriding Without Understanding**: Before applying an override, ensure you understand the implications of forcing a specific version, especially if it differs from what your dependencies expect.

- **Neglecting Security Updates**: Outdated dependencies can introduce security vulnerabilities. Make it a habit to check for and apply security updates regularly.

- **Lack of Testing After Changes**: After modifying exclusions or overrides, thoroughly test your application to ensure that the changes haven't introduced new issues.

### Tools and Resources

Several tools and resources can assist you in managing dependencies effectively:

- **Leiningen**: A popular build automation tool for Clojure that simplifies dependency management. [Leiningen Official Site](https://leiningen.org/)

- **Clojure CLI**: Provides a robust mechanism for managing dependencies through `deps.edn`. [Clojure CLI Documentation](https://clojure.org/guides/deps_and_cli)

- **Maven Central**: A repository of open-source libraries that can be used in Clojure projects. [Maven Central Repository](https://search.maven.org/)

- **Clojars**: A community repository for Clojure libraries. [Clojars Repository](https://clojars.org/)

- **Dependency Graph Tools**: Tools like `lein-ancient` and `lein-depgraph` can help visualize and analyze your project's dependencies.

### Conclusion

Effectively managing dependencies in Clojure is a vital skill that can significantly impact your project's success. By understanding and utilizing exclusions and overrides, you can resolve conflicts, ensure compatibility, and maintain a clean and efficient dependency tree. As you continue to develop in Clojure, these techniques will become an invaluable part of your toolkit, enabling you to build robust and reliable applications.

## Quiz Time!

{{< quizdown >}}

### What is the primary purpose of using exclusions in Clojure dependency management?

- [x] To prevent unwanted transitive dependencies from being included.
- [ ] To enforce a specific version of a dependency.
- [ ] To automatically update dependencies to the latest version.
- [ ] To remove all dependencies from a project.

> **Explanation:** Exclusions are used to prevent certain transitive dependencies from being included in your project, helping to avoid conflicts and unnecessary libraries.

### In a `project.clj` file, where do you specify exclusions for a dependency?

- [x] Within the dependency vector using `:exclusions`.
- [ ] In the `:managed-dependencies` section.
- [ ] In the `:repositories` section.
- [ ] In the `:profiles` section.

> **Explanation:** Exclusions are specified within the dependency vector using the `:exclusions` keyword in a `project.clj` file.

### How can you enforce a specific version of a dependency across your entire project in `deps.edn`?

- [x] By using the `:override-deps` key.
- [ ] By specifying the version in the `:deps` map.
- [ ] By using the `:exclusions` key.
- [ ] By adding the version to the `:repositories` section.

> **Explanation:** The `:override-deps` key is used in `deps.edn` to enforce a specific version of a dependency across the entire project.

### What is a common pitfall when using overrides in dependency management?

- [x] Overriding without understanding the implications.
- [ ] Using the latest version of all dependencies.
- [ ] Excluding too many dependencies.
- [ ] Not documenting the project's dependencies.

> **Explanation:** Overriding without understanding the implications can lead to compatibility issues, as it forces a specific version that may not be compatible with all dependencies.

### Which tool can help visualize and analyze your project's dependencies in Clojure?

- [x] `lein-depgraph`
- [ ] `lein-ancient`
- [ ] `cljfmt`
- [ ] `codox`

> **Explanation:** `lein-depgraph` is a tool that helps visualize and analyze your project's dependencies, making it easier to identify conflicts and unnecessary libraries.

### True or False: Exclusions should be used sparingly to avoid maintenance challenges.

- [x] True
- [ ] False

> **Explanation:** True. Overusing exclusions can lead to maintenance challenges, so they should be used judiciously to resolve specific conflicts.

### What is the benefit of keeping dependencies up-to-date?

- [x] To benefit from the latest features and security patches.
- [ ] To reduce the size of the dependency tree.
- [ ] To automatically resolve all conflicts.
- [ ] To eliminate the need for exclusions and overrides.

> **Explanation:** Keeping dependencies up-to-date ensures that you benefit from the latest features and security patches, enhancing the stability and security of your project.

### In `project.clj`, where do you specify overrides for dependency versions?

- [x] In the `:managed-dependencies` section.
- [ ] Within the dependency vector using `:exclusions`.
- [ ] In the `:repositories` section.
- [ ] In the `:profiles` section.

> **Explanation:** Overrides for dependency versions are specified in the `:managed-dependencies` section of a `project.clj` file.

### Which of the following is NOT a best practice for dependency management?

- [ ] Regularly audit dependencies.
- [ ] Use exclusions sparingly.
- [ ] Prefer overrides for critical libraries.
- [x] Ignore transitive dependencies.

> **Explanation:** Ignoring transitive dependencies is not a best practice. It's important to be aware of and manage transitive dependencies to avoid conflicts and unnecessary libraries.

### True or False: After modifying exclusions or overrides, it's important to thoroughly test your application.

- [x] True
- [ ] False

> **Explanation:** True. Thorough testing is essential after modifying exclusions or overrides to ensure that the changes haven't introduced new issues.

{{< /quizdown >}}
