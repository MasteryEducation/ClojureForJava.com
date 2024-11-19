---
linkTitle: "16.3.1 Packaging as Standalone JARs"
title: "Packaging Standalone JARs with Leiningen: A Comprehensive Guide"
description: "Explore the process of packaging Clojure applications as standalone JARs using Leiningen's uberjar task, detailing the benefits for deployment and providing step-by-step instructions."
categories:
- Clojure
- Java
- Software Development
tags:
- Clojure
- Leiningen
- JAR
- Deployment
- Java
date: 2024-10-25
type: docs
nav_weight: 523100
canonical: "https://clojureforjava.com/3/5/2/3/1"
license: "© 2024 Tokenizer Inc. CC BY-NC-SA 4.0"
---

## 16.3.1 Packaging Standalone JARs with Leiningen: A Comprehensive Guide

In the world of software development, deploying applications efficiently and reliably is crucial. For Java professionals transitioning to Clojure, understanding how to package applications as standalone JAR files is an essential skill. This section explores the process of building standalone JAR files using Leiningen, a popular build automation tool for Clojure projects. We'll delve into the advantages of using an uberjar for deployment, provide detailed instructions on creating one, and discuss best practices to ensure your application runs smoothly in production environments.

### Understanding the Standalone JAR

A standalone JAR, often referred to as an "uberjar," is a JAR (Java Archive) file that contains not only your compiled code but also all the dependencies your application needs to run. This packaging method simplifies deployment by bundling everything into a single file, making it easy to distribute and execute on any system with a Java Runtime Environment (JRE).

#### Advantages of Using an Uberjar

1. **Simplicity in Deployment**: With all dependencies included, deploying your application becomes a matter of copying a single file to the target environment and executing it with a simple command.

2. **Consistency Across Environments**: By packaging dependencies, you ensure that the same versions are used in development, testing, and production, reducing the risk of "it works on my machine" issues.

3. **Reduced Configuration Overhead**: There's no need to manage classpaths or install dependencies separately on the target machine, as everything is self-contained within the JAR.

4. **Portability**: As long as the target system has a compatible JRE, your application can run without additional setup, making it ideal for cloud deployments or environments where you have limited control over the system configuration.

### Setting Up Leiningen

Before we dive into creating an uberjar, ensure that you have Leiningen installed. Leiningen is a build automation tool specifically designed for Clojure projects, similar to Maven or Gradle in the Java ecosystem.

#### Installing Leiningen

1. **Download the Leiningen Script**: Visit the [Leiningen website](https://leiningen.org/) and download the `lein` script.

2. **Make the Script Executable**: Open your terminal and navigate to the directory where you downloaded the script. Run the following command to make it executable:

   ```bash
   chmod +x lein
   ```

3. **Move the Script to Your PATH**: Move the script to a directory that's in your system's PATH, such as `/usr/local/bin` on Unix-based systems:

   ```bash
   mv lein /usr/local/bin/
   ```

4. **Verify the Installation**: Run `lein` in your terminal to verify that it's installed correctly. Leiningen will download and install its dependencies on the first run.

### Creating a Clojure Project

Let's create a simple Clojure project to demonstrate the process of building an uberjar.

1. **Create a New Project**: Use Leiningen to create a new project:

   ```bash
   lein new app my-clojure-app
   ```

   This command creates a new directory named `my-clojure-app` with a basic project structure.

2. **Navigate to the Project Directory**: Change into the newly created project directory:

   ```bash
   cd my-clojure-app
   ```

3. **Project Structure**: The project structure should look like this:

   ```
   my-clojure-app/
   ├── README.md
   ├── project.clj
   ├── resources/
   ├── src/
   │   └── my_clojure_app/
   │       └── core.clj
   ├── target/
   └── test/
   ```

   The `project.clj` file is the configuration file for your project, where you specify dependencies, build configurations, and more.

### Configuring `project.clj` for Uberjar

Open the `project.clj` file in your favorite text editor. It should look something like this:

```clojure
(defproject my-clojure-app "0.1.0-SNAPSHOT"
  :description "A simple Clojure application"
  :url "http://example.com/FIXME"
  :license {:name "Eclipse Public License"
            :url "http://www.eclipse.org/legal/epl-v10.html"}
  :dependencies [[org.clojure/clojure "1.10.3"]]
  :main ^:skip-aot my-clojure-app.core
  :target-path "target/%s"
  :profiles {:uberjar {:aot :all}})
```

#### Key Elements in `project.clj`

- **`:main`**: Specifies the namespace containing the `-main` function, which acts as the entry point of your application. In this case, it's `my-clojure-app.core`.

- **`:target-path`**: Defines where the compiled files and the final JAR will be placed.

- **`:profiles`**: Contains build profiles. The `:uberjar` profile is used to specify settings for building the uberjar. The `:aot :all` option indicates that all namespaces should be Ahead-Of-Time (AOT) compiled, which is necessary for creating an executable JAR.

### Implementing the Main Function

Open `src/my_clojure_app/core.clj` and implement a simple `-main` function:

```clojure
(ns my-clojure-app.core
  (:gen-class))

(defn -main
  [& args]
  (println "Hello, World!"))
```

The `-main` function is the entry point of your application. The `:gen-class` directive is necessary for generating a Java class file that can be executed.

### Building the Uberjar

With the project configured and the main function implemented, you're ready to build the uberjar.

1. **Run the Uberjar Task**: Execute the following command in the terminal:

   ```bash
   lein uberjar
   ```

   Leiningen will compile your code, resolve dependencies, and package everything into a standalone JAR file. The output will be placed in the `target` directory.

2. **Locate the Uberjar**: After the build completes, you should see a file named something like `my-clojure-app-0.1.0-SNAPSHOT-standalone.jar` in the `target` directory.

### Running the Uberjar

To run your standalone JAR, use the `java` command:

```bash
java -jar target/my-clojure-app-0.1.0-SNAPSHOT-standalone.jar
```

You should see the output `Hello, World!` in your terminal, indicating that your application is running successfully.

### Best Practices for Building Uberjars

1. **Optimize Dependencies**: Ensure that your `project.clj` only includes necessary dependencies to minimize the size of the uberjar.

2. **Use AOT Compilation Judiciously**: While AOT compilation is required for the main namespace, avoid AOT compiling all namespaces unless necessary, as it can increase build times and jar size.

3. **Externalize Configuration**: For production applications, consider externalizing configuration files to avoid hardcoding environment-specific settings in your code.

4. **Security Considerations**: Be mindful of including sensitive information in your JAR, such as API keys or passwords. Use environment variables or configuration files to manage sensitive data.

5. **Testing Before Deployment**: Always test your uberjar in an environment that mirrors production as closely as possible to catch any issues related to dependencies or environment differences.

### Common Pitfalls and Troubleshooting

- **Classpath Conflicts**: Ensure that there are no conflicting versions of dependencies included in your project. Use tools like `lein deps :tree` to visualize dependency trees and resolve conflicts.

- **Missing Dependencies**: If your application fails to start due to missing dependencies, double-check your `project.clj` to ensure all required libraries are included.

- **AOT Compilation Errors**: If you encounter errors during AOT compilation, verify that all namespaces are correctly defined and that there are no circular dependencies.

### Advanced Topics

#### Customizing the Uberjar Manifest

The JAR manifest file can be customized to include additional metadata or specify a different main class. This can be done by adding a `:manifest` key to the `:uberjar` profile in `project.clj`.

#### Using Leiningen Plugins

Leiningen supports a variety of plugins that can enhance the build process. For example, the `lein-ring` plugin can be used to package web applications with embedded servers.

#### Continuous Integration and Deployment

Integrating the uberjar build process into a CI/CD pipeline ensures that your application is consistently packaged and ready for deployment. Tools like Jenkins, Travis CI, or GitHub Actions can automate the build and deployment process.

### Conclusion

Packaging Clojure applications as standalone JARs using Leiningen's uberjar task is a powerful technique that simplifies deployment and ensures consistency across environments. By following best practices and understanding the nuances of the uberjar process, you can create robust, portable applications that are easy to distribute and run. Whether you're deploying to a cloud environment or a local server, the uberjar approach provides a streamlined solution for Clojure application deployment.

## Quiz Time!

{{< quizdown >}}

### What is a standalone JAR file?

- [x] A JAR file that contains both the application code and all its dependencies.
- [ ] A JAR file that only contains the application code.
- [ ] A JAR file that only contains the application's dependencies.
- [ ] A JAR file that requires external configuration files to run.

> **Explanation:** A standalone JAR, or uberjar, includes both the application code and all its dependencies, making it self-contained and easy to deploy.

### Which command is used to create an uberjar in Leiningen?

- [x] `lein uberjar`
- [ ] `lein jar`
- [ ] `lein build`
- [ ] `lein package`

> **Explanation:** The `lein uberjar` command compiles the application and packages it along with its dependencies into a standalone JAR file.

### What is the purpose of the `:main` key in `project.clj`?

- [x] To specify the namespace containing the `-main` function, which acts as the entry point of the application.
- [ ] To define the main dependency of the project.
- [ ] To indicate the primary library used in the project.
- [ ] To set the main configuration file for the project.

> **Explanation:** The `:main` key specifies the namespace with the `-main` function, which is the entry point when the JAR is executed.

### What does AOT stand for in the context of Clojure?

- [x] Ahead-Of-Time
- [ ] After-Operation-Time
- [ ] Asynchronous-Operation-Time
- [ ] Application-Optimization-Time

> **Explanation:** AOT stands for Ahead-Of-Time compilation, which compiles Clojure code into Java bytecode before runtime.

### Why is it beneficial to package applications as standalone JARs?

- [x] Simplifies deployment by bundling all dependencies.
- [x] Ensures consistency across different environments.
- [ ] Increases the need for manual configuration.
- [ ] Requires additional setup on the target machine.

> **Explanation:** Standalone JARs simplify deployment by including all dependencies and ensure consistency across environments without additional setup.

### What should you do if you encounter classpath conflicts?

- [x] Use tools like `lein deps :tree` to visualize and resolve conflicts.
- [ ] Ignore the conflicts and proceed with the build.
- [ ] Manually edit the classpath file.
- [ ] Remove all dependencies and start over.

> **Explanation:** Tools like `lein deps :tree` help visualize dependency trees and resolve conflicts by identifying conflicting versions.

### What is the role of the `:profiles` key in `project.clj`?

- [x] To define different build configurations, such as for development or production.
- [ ] To list all dependencies of the project.
- [ ] To specify the project's main namespace.
- [ ] To configure the project's logging settings.

> **Explanation:** The `:profiles` key allows defining different build configurations, such as development, testing, or production settings.

### How can you run a standalone JAR file?

- [x] Using the command `java -jar <jar-file>`
- [ ] Using the command `lein run <jar-file>`
- [ ] Using the command `lein exec <jar-file>`
- [ ] Using the command `java -cp <jar-file>`

> **Explanation:** The `java -jar <jar-file>` command is used to execute a standalone JAR file.

### What is a common pitfall when building uberjars?

- [x] Classpath conflicts due to conflicting dependency versions.
- [ ] Including too few dependencies.
- [ ] Using too many plugins.
- [ ] Not specifying a target path.

> **Explanation:** Classpath conflicts can occur when different dependencies have conflicting versions, leading to runtime errors.

### True or False: An uberjar requires additional setup on the target machine to run.

- [ ] True
- [x] False

> **Explanation:** False. An uberjar is self-contained and does not require additional setup on the target machine, as it includes all necessary dependencies.

{{< /quizdown >}}
