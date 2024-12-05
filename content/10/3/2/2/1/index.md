---
linkTitle: "8.2.1 Using Leiningen and Deps.edn"
title: "Managing Clojure Dependencies with Leiningen and Deps.edn"
description: "Explore how to manage Clojure project dependencies using Leiningen and the deps.edn format, understanding their differences and best use cases."
categories:
- Clojure
- Dependency Management
- Software Development
tags:
- Clojure
- Leiningen
- Deps.edn
- Dependency Management
- Functional Programming
date: 2024-10-25
type: docs
nav_weight: 322100
canonical: "https://clojureforjava.com/10/3/2/2/1"
license: "© 2024 Tokenizer Inc. CC BY-NC-SA 4.0"
---

## 8.2.1 Using Leiningen and Deps.edn

In the world of Clojure development, managing dependencies is a critical task that ensures your projects are built efficiently and maintainably. Two primary tools for handling dependencies in Clojure are Leiningen and the newer `deps.edn` format. Each has its own strengths and use cases, and understanding how to leverage them effectively can significantly enhance your development workflow.

### Introduction to Leiningen

Leiningen, often referred to as "Lein," is a build automation tool for Clojure. It has been the de facto standard for Clojure projects for many years, providing a comprehensive suite of features beyond dependency management, including project scaffolding, testing, packaging, and more.

#### Key Features of Leiningen

- **Dependency Management**: Leiningen uses a `project.clj` file to specify project dependencies, repositories, and other configurations.
- **Build Automation**: Supports tasks such as compiling, running tests, and creating JAR files.
- **Plugin System**: Extensible through plugins, allowing for additional functionality tailored to specific needs.
- **REPL Integration**: Seamlessly integrates with the Clojure REPL for interactive development.

#### Setting Up Leiningen

To get started with Leiningen, you need to install it on your system. The installation process is straightforward and can be done via package managers or by downloading the script directly from the [Leiningen website](https://leiningen.org/).

```bash
brew install leiningen

curl https://raw.githubusercontent.com/technomancy/leiningen/stable/bin/lein > ~/bin/lein
chmod +x ~/bin/lein
```

Once installed, you can verify the installation by running:

```bash
lein version
```

### Understanding the `project.clj` File

The `project.clj` file is the heart of a Leiningen project. It defines the project metadata, dependencies, and various settings. Here's a basic example of a `project.clj` file:

```clojure
(defproject my-clojure-app "0.1.0-SNAPSHOT"
  :description "A sample Clojure project"
  :url "http://example.com/my-clojure-app"
  :license {:name "Eclipse Public License"
            :url "http://www.eclipse.org/legal/epl-v10.html"}
  :dependencies [[org.clojure/clojure "1.10.3"]
                 [ring/ring-core "1.9.0"]]
  :main ^:skip-aot my-clojure-app.core
  :target-path "target/%s"
  :profiles {:uberjar {:aot :all}})
```

#### Key Sections of `project.clj`

- **Project Metadata**: Includes the project name, version, description, and URL.
- **Dependencies**: A vector of dependencies, each specified by a group ID, artifact ID, and version.
- **Main Namespace**: Specifies the main entry point for the application.
- **Profiles**: Allows for different configurations, such as development and production profiles.

### Introduction to Deps.edn

The `deps.edn` format is a newer approach to dependency management in Clojure, introduced with the Clojure CLI tools. It provides a more declarative and flexible way to manage dependencies, focusing on simplicity and composability.

#### Key Features of Deps.edn

- **Simplicity**: A straightforward, data-driven approach to specifying dependencies.
- **Composability**: Supports dependency aliases and can easily compose multiple configurations.
- **Tool Agnostic**: Works seamlessly with various tools and editors, promoting a more integrated development experience.

#### Setting Up Deps.edn

To use `deps.edn`, you need the Clojure CLI tools installed. You can download and install them from the [official Clojure website](https://clojure.org/guides/getting_started).

```bash
brew install clojure/tools/clojure

clojure -M:version
```

### Understanding the `deps.edn` File

The `deps.edn` file is a simple EDN (Extensible Data Notation) file that defines dependencies and other configurations. Here's an example of a basic `deps.edn` file:

```clojure
{:deps {org.clojure/clojure {:mvn/version "1.10.3"}
        ring/ring-core {:mvn/version "1.9.0"}}
 :paths ["src" "resources"]
 :aliases {:dev {:extra-paths ["dev"]
                 :extra-deps {cider/cider-nrepl {:mvn/version "0.25.9"}}}}}
```

#### Key Sections of `deps.edn`

- **:deps**: A map of dependencies, each specified by a group ID, artifact ID, and version.
- **:paths**: Specifies the directories to include in the classpath.
- **:aliases**: Defines additional configurations, such as development dependencies or specific REPL configurations.

### Differences Between Leiningen and Deps.edn

While both Leiningen and `deps.edn` serve the purpose of managing dependencies, they differ in several key aspects:

1. **Complexity vs. Simplicity**: Leiningen offers a more comprehensive set of features, while `deps.edn` focuses on simplicity and composability.
2. **Build Automation**: Leiningen provides built-in support for tasks like building and testing, whereas `deps.edn` relies on external tools or custom scripts.
3. **Plugin System**: Leiningen has a mature plugin ecosystem, while `deps.edn` is more tool-agnostic, allowing for integration with various tools.
4. **Configuration Style**: `project.clj` is more verbose and feature-rich, while `deps.edn` is concise and declarative.

### Use Cases for Leiningen and Deps.edn

#### When to Use Leiningen

- **Complex Projects**: When you need advanced build automation and a rich set of features.
- **Existing Ecosystem**: If your project relies on existing Leiningen plugins or workflows.
- **Legacy Projects**: For maintaining older projects already using Leiningen.

#### When to Use Deps.edn

- **Simplicity**: For projects that prioritize simplicity and minimal configuration.
- **Tool Integration**: When you want seamless integration with various tools and editors.
- **Composability**: For projects that benefit from composable configurations and aliases.

### Practical Examples

#### Example 1: Setting Up a Simple Clojure Project with Leiningen

1. **Create a New Project**: Use Leiningen to scaffold a new project.

   ```bash
   lein new app my-clojure-app
   ```

2. **Add Dependencies**: Edit the `project.clj` file to add dependencies.

   ```clojure
   :dependencies [[org.clojure/clojure "1.10.3"]
                  [compojure "1.6.2"]]
   ```

3. **Run the Project**: Use Leiningen to run the project.

   ```bash
   lein run
   ```

4. **Build an Uberjar**: Package the project into an executable JAR.

   ```bash
   lein uberjar
   ```

#### Example 2: Setting Up a Simple Clojure Project with Deps.edn

1. **Create a New Project Directory**: Manually create a project directory and `deps.edn` file.

   ```bash
   mkdir my-clojure-app
   cd my-clojure-app
   touch deps.edn
   ```

2. **Add Dependencies**: Edit the `deps.edn` file to add dependencies.

   ```clojure
   {:deps {org.clojure/clojure {:mvn/version "1.10.3"}
           compojure {:mvn/version "1.6.2"}}}
   ```

3. **Run the Project**: Use the Clojure CLI to run the project.

   ```bash
   clojure -M -m my-clojure-app.core
   ```

4. **Create a Custom Alias**: Define an alias for development.

   ```clojure
   :aliases {:dev {:extra-paths ["dev"]
                   :extra-deps {cider/cider-nrepl {:mvn/version "0.25.9"}}}}
   ```

5. **Use the Alias**: Run the project with the development alias.

   ```bash
   clojure -M:dev
   ```

### Best Practices for Dependency Management

1. **Version Pinning**: Always specify exact versions for dependencies to ensure consistency across environments.
2. **Minimal Dependencies**: Keep your dependency list minimal to reduce potential conflicts and security vulnerabilities.
3. **Regular Updates**: Regularly update dependencies to benefit from bug fixes and performance improvements.
4. **Isolation**: Use aliases or profiles to isolate development dependencies from production code.
5. **Documentation**: Document your dependency choices and any specific configurations for future reference.

### Common Pitfalls and How to Avoid Them

1. **Dependency Conflicts**: Use tools like `lein deps :tree` or `clojure -Stree` to visualize and resolve conflicts.
2. **Overusing Plugins**: Avoid relying too heavily on plugins, which can complicate builds and introduce compatibility issues.
3. **Ignoring Security**: Regularly audit dependencies for known vulnerabilities using tools like [OWASP Dependency-Check](https://owasp.org/www-project-dependency-check/).
4. **Neglecting Documentation**: Ensure that your `project.clj` or `deps.edn` files are well-documented to aid future maintenance.

### Conclusion

Both Leiningen and `deps.edn` offer powerful ways to manage dependencies in Clojure projects, each with its own strengths and ideal use cases. By understanding the differences and best practices associated with each tool, you can choose the right approach for your project's needs, ensuring a smooth and efficient development process.

## Quiz Time!

{{< quizdown >}}

### What is the primary purpose of Leiningen in Clojure projects?

- [x] Build automation and dependency management
- [ ] Only dependency management
- [ ] Only build automation
- [ ] Code compilation

> **Explanation:** Leiningen is a build automation tool that also manages dependencies, providing a comprehensive suite of features for Clojure projects.

### Which file format does Leiningen use to specify project dependencies?

- [x] project.clj
- [ ] deps.edn
- [ ] pom.xml
- [ ] build.gradle

> **Explanation:** Leiningen uses the `project.clj` file to specify project dependencies and configurations.

### What is a key feature of the deps.edn format?

- [x] Simplicity and composability
- [ ] Complex build automation
- [ ] Extensive plugin ecosystem
- [ ] GUI-based configuration

> **Explanation:** The `deps.edn` format is known for its simplicity and composability, focusing on a straightforward approach to dependency management.

### How do you install Leiningen on macOS using Homebrew?

- [x] brew install leiningen
- [ ] brew install clojure
- [ ] brew install lein
- [ ] brew install clj

> **Explanation:** The correct command to install Leiningen on macOS using Homebrew is `brew install leiningen`.

### What is the purpose of the :aliases section in a deps.edn file?

- [x] To define additional configurations and dependencies
- [ ] To specify the main namespace
- [ ] To list all project dependencies
- [ ] To set the project version

> **Explanation:** The `:aliases` section in a `deps.edn` file is used to define additional configurations and dependencies, allowing for composable setups.

### Which tool is more suitable for complex projects with advanced build automation needs?

- [x] Leiningen
- [ ] Deps.edn
- [ ] Maven
- [ ] Gradle

> **Explanation:** Leiningen is more suitable for complex projects that require advanced build automation and a rich set of features.

### How can you visualize dependency conflicts in a Leiningen project?

- [x] lein deps :tree
- [ ] clojure -Stree
- [ ] lein show-deps
- [ ] clojure -M:tree

> **Explanation:** The command `lein deps :tree` is used to visualize dependency conflicts in a Leiningen project.

### What is a common pitfall when managing dependencies in Clojure projects?

- [x] Dependency conflicts
- [ ] Using too few dependencies
- [ ] Over-documenting dependencies
- [ ] Ignoring version numbers

> **Explanation:** Dependency conflicts are a common pitfall in managing dependencies, and tools like `lein deps :tree` can help resolve them.

### Which section of a project.clj file specifies the main entry point for the application?

- [x] :main
- [ ] :dependencies
- [ ] :profiles
- [ ] :description

> **Explanation:** The `:main` section of a `project.clj` file specifies the main entry point for the application.

### True or False: The deps.edn format is more verbose than project.clj.

- [ ] True
- [x] False

> **Explanation:** The `deps.edn` format is more concise and declarative compared to the more verbose `project.clj` format.

{{< /quizdown >}}
