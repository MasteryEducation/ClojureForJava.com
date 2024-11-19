---
linkTitle: "12.3.2 Creating Executable JARs"
title: "Creating Executable JARs with Clojure and Leiningen"
description: "Learn how to create executable JARs in Clojure using Leiningen, enabling seamless deployment and execution of your Clojure applications."
categories:
- Clojure Development
- Java Interoperability
- Build Tools
tags:
- Clojure
- Leiningen
- JAR
- Java
- Build Automation
date: 2024-10-25
type: docs
nav_weight: 1232000
canonical: "https://clojureforjava.com/1/12/3/2"
license: "© 2024 Tokenizer Inc. CC BY-NC-SA 4.0"
---

## 12.3.2 Creating Executable JARs with Clojure and Leiningen

Creating executable JARs is a crucial step in the process of deploying Clojure applications. This section will guide you through the process of packaging your Clojure applications into standalone JAR files using Leiningen, a popular build automation tool for Clojure. We will explore the benefits of using executable JARs, delve into the configuration and execution details, and provide practical examples to ensure you can confidently create and run your own JAR files.

### Understanding Executable JARs

An executable JAR (Java ARchive) file is a package that contains all the necessary components of a Java application, including compiled classes, resources, and metadata. For Clojure applications, an executable JAR allows you to bundle your Clojure code, dependencies, and a manifest file that specifies the entry point of the application. This makes it easy to distribute and run your application on any machine with a compatible Java Runtime Environment (JRE).

#### Benefits of Executable JARs

1. **Portability**: An executable JAR is platform-independent, allowing your application to run on any system with a JRE.
2. **Simplicity**: Users can execute your application with a simple command, without needing to manage dependencies or configurations.
3. **Deployment**: Packaging your application as a JAR simplifies deployment processes, especially in cloud environments or containerized applications.

### Setting Up Your Clojure Project

Before creating an executable JAR, ensure your Clojure project is properly set up with Leiningen. If you haven't already, create a new Leiningen project using the following command:

```shell
lein new app your-app
```

This command generates a basic project structure with the necessary files, including `project.clj`, which is the configuration file for your Leiningen project.

### Configuring `project.clj` for JAR Creation

The `project.clj` file is where you define your project's configuration, including dependencies, source paths, and build instructions. To create an executable JAR, you need to specify the `:main` namespace, which contains the entry point of your application. This is typically the namespace with the `-main` function.

Here's an example `project.clj` configuration:

```clojure
(defproject your-app "0.1.0-SNAPSHOT"
  :description "A sample Clojure application"
  :url "http://example.com/your-app"
  :license {:name "Eclipse Public License"
            :url "http://www.eclipse.org/legal/epl-v10.html"}
  :dependencies [[org.clojure/clojure "1.10.3"]]
  :main ^:skip-aot your-app.core
  :target-path "target/%s"
  :profiles {:uberjar {:aot :all}})
```

#### Key Configuration Elements

- **`:main`**: Specifies the namespace containing the `-main` function. The `^:skip-aot` metadata indicates that the namespace should not be ahead-of-time (AOT) compiled unless building an uberjar.
- **`:target-path`**: Defines the directory where compiled artifacts will be placed.
- **`:profiles`**: Contains build profiles. The `:uberjar` profile is used to configure settings specific to building an executable JAR, such as AOT compilation.

### Building the Executable JAR

With your `project.clj` configured, you can build the executable JAR using the `lein uberjar` command. This command compiles your Clojure code, resolves dependencies, and packages everything into a standalone JAR file.

```shell
lein uberjar
```

Upon successful execution, Leiningen creates the JAR file in the `target` directory, typically named `your-app-standalone.jar`.

### Running the Executable JAR

To run your application from the JAR file, use the `java -jar` command followed by the path to the JAR file:

```shell
java -jar target/your-app-standalone.jar
```

This command launches the Java Virtual Machine (JVM) and executes the `-main` function specified in your `:main` namespace.

### Practical Example: Building a Simple Clojure Application

Let's walk through a practical example of creating an executable JAR for a simple Clojure application. We'll build a basic "Hello, World!" application and package it into a JAR file.

#### Step 1: Create the Project

Create a new Leiningen project:

```shell
lein new app hello-world
```

#### Step 2: Implement the Application

Navigate to the `src/hello_world/core.clj` file and implement the `-main` function:

```clojure
(ns hello-world.core
  (:gen-class))

(defn -main
  "A simple Hello, World! application."
  [& args]
  (println "Hello, World!"))
```

#### Step 3: Configure `project.clj`

Edit the `project.clj` file to specify the `:main` namespace:

```clojure
(defproject hello-world "0.1.0-SNAPSHOT"
  :description "A simple Hello, World! application"
  :url "http://example.com/hello-world"
  :license {:name "Eclipse Public License"
            :url "http://www.eclipse.org/legal/epl-v10.html"}
  :dependencies [[org.clojure/clojure "1.10.3"]]
  :main ^:skip-aot hello-world.core
  :target-path "target/%s"
  :profiles {:uberjar {:aot :all}})
```

#### Step 4: Build the JAR

Run the `lein uberjar` command to build the executable JAR:

```shell
lein uberjar
```

#### Step 5: Execute the JAR

Run the application using the `java -jar` command:

```shell
java -jar target/hello-world-standalone.jar
```

You should see the output:

```
Hello, World!
```

### Advanced Configuration Options

Leiningen offers various configuration options to customize the JAR creation process. Here are some advanced options you might consider:

#### Customizing the Manifest File

The manifest file in a JAR specifies metadata about the JAR and its contents. You can customize the manifest by adding a `:manifest` entry to your `project.clj`:

```clojure
:manifest {"Main-Class" "hello_world.core"
           "Implementation-Version" "0.1.0"}
```

#### Including Additional Resources

If your application requires additional resources (e.g., configuration files, images), you can include them in the JAR by placing them in the `resources` directory of your project. Leiningen automatically includes this directory in the JAR.

#### Excluding Unnecessary Files

To exclude specific files or directories from the JAR, use the `:uberjar-exclusions` key in your `project.clj`:

```clojure
:uberjar-exclusions [#"^log4j.properties$"]
```

### Best Practices for Creating Executable JARs

1. **Keep Dependencies Updated**: Regularly update your dependencies to ensure compatibility and security.
2. **Use AOT Compilation Wisely**: While AOT compilation can improve startup time, it increases the JAR size. Use it judiciously.
3. **Test Thoroughly**: Test your application in various environments to ensure it runs smoothly from the JAR.
4. **Optimize for Performance**: Profile your application and optimize performance-critical sections before packaging.

### Common Pitfalls and Troubleshooting

#### ClassNotFoundException

If you encounter a `ClassNotFoundException`, ensure that all necessary dependencies are included in your `project.clj` and that the `:main` namespace is correctly specified.

#### Incorrect Entry Point

If your application doesn't start as expected, verify that the `:main` namespace contains a valid `-main` function and that the namespace is correctly specified in `project.clj`.

#### Large JAR Size

If your JAR is excessively large, review your dependencies and exclude unnecessary files using `:uberjar-exclusions`.

### Conclusion

Creating executable JARs is an essential skill for deploying Clojure applications. By leveraging Leiningen's powerful build automation capabilities, you can efficiently package your applications into standalone JARs, simplifying distribution and execution. With the knowledge and examples provided in this section, you are well-equipped to create and manage executable JARs for your Clojure projects.

## Quiz Time!

{{< quizdown >}}

### What is the primary purpose of an executable JAR?

- [x] To package a Java application into a single file for easy distribution and execution
- [ ] To compile Java source code into bytecode
- [ ] To provide a graphical user interface for Java applications
- [ ] To manage Java application dependencies

> **Explanation:** An executable JAR packages all necessary components of a Java application, including compiled classes and resources, into a single file for easy distribution and execution.

### Which command is used to build an executable JAR with Leiningen?

- [x] `lein uberjar`
- [ ] `lein jar`
- [ ] `lein build`
- [ ] `lein package`

> **Explanation:** The `lein uberjar` command is used to build an executable JAR in Leiningen, packaging the application and its dependencies.

### What is the role of the `:main` key in `project.clj`?

- [x] It specifies the namespace containing the entry point of the application.
- [ ] It defines the version of the Clojure language to use.
- [ ] It lists the dependencies required by the project.
- [ ] It sets the target directory for compiled artifacts.

> **Explanation:** The `:main` key specifies the namespace containing the `-main` function, which serves as the entry point for the application.

### How do you run an executable JAR from the command line?

- [x] `java -jar target/your-app-standalone.jar`
- [ ] `lein run target/your-app-standalone.jar`
- [ ] `java -cp target/your-app-standalone.jar`
- [ ] `lein exec target/your-app-standalone.jar`

> **Explanation:** The `java -jar` command is used to run an executable JAR file from the command line.

### What is the purpose of AOT compilation in Clojure?

- [x] To improve startup time by compiling Clojure code to Java bytecode ahead of time
- [ ] To reduce the size of the JAR file
- [ ] To enable dynamic typing in Clojure
- [ ] To provide a graphical user interface for Clojure applications

> **Explanation:** AOT (Ahead-of-Time) compilation improves startup time by compiling Clojure code to Java bytecode before runtime.

### Which directory should additional resources be placed in to be included in the JAR?

- [x] `resources`
- [ ] `src`
- [ ] `lib`
- [ ] `bin`

> **Explanation:** Additional resources should be placed in the `resources` directory, which Leiningen automatically includes in the JAR.

### How can you exclude specific files from the JAR?

- [x] Use the `:uberjar-exclusions` key in `project.clj`
- [ ] Use the `:exclude` key in `project.clj`
- [ ] Use the `:ignore` key in `project.clj`
- [ ] Use the `:omit` key in `project.clj`

> **Explanation:** The `:uberjar-exclusions` key in `project.clj` allows you to specify files or directories to exclude from the JAR.

### What should you do if you encounter a `ClassNotFoundException`?

- [x] Ensure all necessary dependencies are included in `project.clj` and the `:main` namespace is correctly specified.
- [ ] Reinstall Leiningen and try again.
- [ ] Increase the JVM heap size.
- [ ] Use a different version of Java.

> **Explanation:** A `ClassNotFoundException` often indicates missing dependencies or an incorrectly specified `:main` namespace.

### Why is it important to test your application in various environments?

- [x] To ensure it runs smoothly from the JAR across different systems
- [ ] To reduce the size of the JAR file
- [ ] To improve the graphical user interface
- [ ] To enable dynamic typing in Clojure

> **Explanation:** Testing in various environments ensures that your application runs smoothly from the JAR across different systems and configurations.

### True or False: An executable JAR is platform-independent.

- [x] True
- [ ] False

> **Explanation:** An executable JAR is platform-independent, allowing it to run on any system with a compatible Java Runtime Environment (JRE).

{{< /quizdown >}}
