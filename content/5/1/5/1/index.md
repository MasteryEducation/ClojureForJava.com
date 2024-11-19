---
linkTitle: "1.5.1 Installing Clojure and Leiningen"
title: "Installing Clojure and Leiningen: A Comprehensive Guide for Java Developers"
description: "Step-by-step guide to installing Clojure CLI tools and Leiningen on Windows, macOS, and Linux, with verification through simple Clojure programs."
categories:
- Clojure
- NoSQL
- Java Development
tags:
- Clojure Installation
- Leiningen
- Java Developers
- Cross-Platform Setup
- Functional Programming
date: 2024-10-25
type: docs
nav_weight: 151000
canonical: "https://clojureforjava.com/5/1/5/1"
license: "© 2024 Tokenizer Inc. CC BY-NC-SA 4.0"
---

## 1.5.1 Installing Clojure and Leiningen

As a Java developer venturing into the world of Clojure, setting up your development environment is a crucial first step. This section provides a detailed guide to installing Clojure CLI tools and Leiningen across different operating systems: Windows, macOS, and Linux. We will also verify the installation by running simple Clojure programs, ensuring your setup is ready for development.

### Introduction to Clojure CLI Tools

Clojure CLI tools provide a robust command-line interface for managing Clojure projects. They facilitate tasks such as running REPLs, managing dependencies, and executing scripts. The CLI tools are designed to be lightweight and integrate seamlessly with existing development workflows.

### Installing Clojure CLI Tools

#### Windows Installation

1. **Prerequisites**: Ensure you have Java Development Kit (JDK) installed. Clojure requires Java to run. You can download the latest JDK from [Oracle's official website](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html).

2. **Download and Install Scoop**: Scoop is a command-line installer for Windows, which simplifies the installation of Clojure CLI tools.
   - Open PowerShell as an Administrator and execute the following command:
     ```powershell
     Set-ExecutionPolicy RemoteSigned -scope CurrentUser
     iwr -useb get.scoop.sh | iex
     ```

3. **Install Clojure**: With Scoop installed, you can now install Clojure by running:
   ```powershell
   scoop install clojure
   ```

4. **Verify Installation**: To verify the installation, open a new terminal window and run:
   ```powershell
   clojure -M -e "(println \"Hello, Clojure!\")"
   ```
   You should see the output `Hello, Clojure!`.

#### macOS Installation

1. **Prerequisites**: Ensure you have Homebrew installed. Homebrew is a package manager for macOS that simplifies software installation. If not installed, you can do so by running:
   ```bash
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```

2. **Install Clojure**: With Homebrew, installing Clojure is straightforward:
   ```bash
   brew install clojure/tools/clojure
   ```

3. **Verify Installation**: Open a terminal and execute:
   ```bash
   clojure -M -e "(println \"Hello, Clojure!\")"
   ```
   The output should be `Hello, Clojure!`.

#### Linux Installation

1. **Prerequisites**: Ensure your system has Java installed. You can install OpenJDK using your package manager. For example, on Ubuntu:
   ```bash
   sudo apt update
   sudo apt install openjdk-11-jdk
   ```

2. **Install Clojure**: Use the following script to install Clojure CLI tools:
   ```bash
   curl -O https://download.clojure.org/install/linux-install-1.10.3.1029.sh
   chmod +x linux-install-1.10.3.1029.sh
   sudo ./linux-install-1.10.3.1029.sh
   ```

3. **Verify Installation**: Run the following command in your terminal:
   ```bash
   clojure -M -e "(println \"Hello, Clojure!\")"
   ```
   You should see `Hello, Clojure!` as the output.

### Introduction to Leiningen

Leiningen is a build automation tool for Clojure, akin to Maven for Java. It simplifies project management, dependency resolution, and builds processes. Leiningen is essential for Clojure developers as it streamlines the creation and management of Clojure projects.

### Installing Leiningen

#### Cross-Platform Installation

1. **Download Leiningen Script**: The installation process for Leiningen is similar across all platforms. Start by downloading the Leiningen script:
   ```bash
   curl https://raw.githubusercontent.com/technomancy/leiningen/stable/bin/lein -o lein
   ```

2. **Make the Script Executable**: Change the permissions to make the script executable:
   ```bash
   chmod +x lein
   ```

3. **Move to a Directory in Your PATH**: Move the script to a directory that's in your system's PATH, such as `/usr/local/bin`:
   ```bash
   sudo mv lein /usr/local/bin/
   ```

4. **Run Leiningen**: Execute the following command to download Leiningen's self-installing package:
   ```bash
   lein
   ```
   This command will download the necessary files and set up Leiningen for use.

5. **Verify Installation**: To verify, create a new Clojure project:
   ```bash
   lein new app my-clojure-app
   cd my-clojure-app
   lein run
   ```
   You should see output indicating that the application is running, typically printing "Hello, World!".

### Running Simple Clojure Programs

Once Clojure and Leiningen are installed, it's beneficial to run a few simple programs to ensure everything is functioning correctly.

#### Example 1: Basic Arithmetic

Create a file named `arithmetic.clj` with the following content:

```clojure
(ns arithmetic)

(defn add [a b]
  (+ a b))

(println "Sum of 5 and 3 is:" (add 5 3))
```

Run the program using the Clojure CLI:

```bash
clojure -M arithmetic.clj
```

You should see the output `Sum of 5 and 3 is: 8`.

#### Example 2: Using Leiningen

Navigate to your project directory and edit the `src/my_clojure_app/core.clj` file:

```clojure
(ns my-clojure-app.core)

(defn -main
  "A simple program that prints a greeting."
  [& args]
  (println "Welcome to Clojure with Leiningen!"))
```

Run the program using Leiningen:

```bash
lein run
```

The output should be `Welcome to Clojure with Leiningen!`.

### Best Practices and Common Pitfalls

- **Java Compatibility**: Ensure your Java version is compatible with Clojure. Clojure typically supports a range of Java versions, but it's best to use a stable release like Java 11.
- **Environment Variables**: On Windows, ensure your PATH variable includes the directories for Java, Clojure, and Leiningen.
- **Leiningen Profiles**: Utilize Leiningen profiles to manage different environments (e.g., development, testing, production).
- **Dependency Management**: Regularly update your dependencies to avoid security vulnerabilities and ensure compatibility.

### Conclusion

Installing Clojure and Leiningen sets the foundation for your journey into functional programming with Clojure. With these tools, you can efficiently manage projects, dependencies, and build processes, leveraging Clojure's powerful features for scalable data solutions. As you continue, explore more advanced topics and integrate Clojure with NoSQL databases to build robust applications.

## Quiz Time!

{{< quizdown >}}

### What is the primary purpose of Clojure CLI tools?

- [x] To manage Clojure projects and dependencies
- [ ] To compile Java programs
- [ ] To create graphical user interfaces
- [ ] To manage network configurations

> **Explanation:** Clojure CLI tools provide a command-line interface for managing Clojure projects, running REPLs, and handling dependencies.

### Which command installs Clojure on macOS using Homebrew?

- [x] `brew install clojure/tools/clojure`
- [ ] `apt-get install clojure`
- [ ] `scoop install clojure`
- [ ] `yum install clojure`

> **Explanation:** Homebrew is the package manager used on macOS, and the command `brew install clojure/tools/clojure` installs Clojure.

### What is the role of Leiningen in Clojure development?

- [x] Project automation and dependency management
- [ ] Compiling Clojure to native code
- [ ] Managing network connections
- [ ] Creating database schemas

> **Explanation:** Leiningen is a build automation tool for Clojure, similar to Maven for Java, used for project management and dependency resolution.

### How do you verify Clojure installation on Windows?

- [x] Run `clojure -M -e "(println \"Hello, Clojure!\")"`
- [ ] Run `java -version`
- [ ] Run `lein version`
- [ ] Run `clojure --help`

> **Explanation:** Running `clojure -M -e "(println \"Hello, Clojure!\")"` checks if Clojure is installed correctly by executing a simple program.

### What is the first step in installing Leiningen?

- [x] Download the Leiningen script
- [ ] Install Java
- [ ] Configure the PATH variable
- [ ] Install a text editor

> **Explanation:** The first step is to download the Leiningen script, which is then made executable and moved to a directory in the PATH.

### Which command is used to create a new Clojure project with Leiningen?

- [x] `lein new app my-clojure-app`
- [ ] `clojure new project`
- [ ] `mvn create clojure-app`
- [ ] `gradle init clojure-app`

> **Explanation:** `lein new app my-clojure-app` is the command used to create a new Clojure project using Leiningen.

### What is the output of the command `lein run` in a new Leiningen project?

- [x] "Hello, World!"
- [ ] "Clojure is running"
- [ ] "Project initialized"
- [ ] "Welcome to Leiningen"

> **Explanation:** By default, a new Leiningen project prints "Hello, World!" when `lein run` is executed.

### What should you ensure before installing Clojure on Linux?

- [x] Java is installed
- [ ] Python is installed
- [ ] Node.js is installed
- [ ] Docker is installed

> **Explanation:** Clojure requires Java to run, so it's essential to have Java installed before setting up Clojure.

### Which tool is recommended for installing Clojure on Windows?

- [x] Scoop
- [ ] Homebrew
- [ ] apt-get
- [ ] Chocolatey

> **Explanation:** Scoop is a command-line installer for Windows that simplifies the installation of Clojure CLI tools.

### True or False: Leiningen is only used for dependency management in Clojure projects.

- [ ] True
- [x] False

> **Explanation:** False. Leiningen is used for project automation, dependency management, and build processes, among other tasks.

{{< /quizdown >}}
