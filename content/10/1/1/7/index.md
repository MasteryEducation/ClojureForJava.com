---
linkTitle: "1.7 Setting Up the Clojure Development Environment"
title: "Setting Up the Clojure Development Environment: A Comprehensive Guide for Java Professionals"
description: "Learn how to set up a Clojure development environment with step-by-step instructions for installing Java, Leiningen, and configuring popular IDEs like IntelliJ IDEA with Cursive, Emacs with CIDER, and VSCode with Calva."
categories:
- Clojure
- Development
- Programming
tags:
- Clojure
- Java
- Leiningen
- IDE
- REPL
date: 2024-10-25
type: docs
nav_weight: 117000
canonical: "https://clojureforjava.com/10/1/1/7"
license: "© 2024 Tokenizer Inc. CC BY-NC-SA 4.0"
---

## 1.7 Setting Up the Clojure Development Environment

As a Java professional venturing into the world of Clojure, setting up your development environment is a crucial first step. This guide will walk you through the process of installing the necessary tools and configuring your environment to maximize productivity. We'll cover the installation of Java, Leiningen (Clojure's build tool), and setting up popular IDEs or text editors such as IntelliJ IDEA with Cursive, Emacs with CIDER, and VSCode with Calva. Additionally, we'll provide tips for configuring the REPL (Read-Eval-Print Loop) for interactive development.

### Step 1: Installing Java

Clojure runs on the Java Virtual Machine (JVM), so having Java installed is a prerequisite. Here's how you can set it up:

#### 1.1 Checking for Java Installation

Before installing Java, check if it's already installed on your system:

```bash
java -version
```

If Java is installed, this command will display the version number. Ensure you have Java 8 or later.

#### 1.2 Installing Java on Windows

1. **Download the JDK**: Visit the [Oracle JDK download page](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html) or [AdoptOpenJDK](https://adoptopenjdk.net/) for an open-source alternative.
2. **Install the JDK**: Run the installer and follow the on-screen instructions.
3. **Set Environment Variables**:
   - Open the Start menu, search for "Environment Variables," and select "Edit the system environment variables."
   - Under "System Properties," click "Environment Variables."
   - Add a new system variable `JAVA_HOME` with the path to your JDK installation.
   - Append `%JAVA_HOME%\bin` to the `Path` variable.

#### 1.3 Installing Java on macOS

1. **Using Homebrew**: Open Terminal and run:

   ```bash
   brew install openjdk@11
   ```

2. **Set JAVA_HOME**: Add the following to your `.bash_profile` or `.zshrc`:

   ```bash
   export JAVA_HOME=$(/usr/libexec/java_home -v 11)
   ```

3. **Verify Installation**:

   ```bash
   java -version
   ```

#### 1.4 Installing Java on Linux

1. **Using APT (Debian/Ubuntu)**:

   ```bash
   sudo apt update
   sudo apt install openjdk-11-jdk
   ```

2. **Using YUM (CentOS/RHEL)**:

   ```bash
   sudo yum install java-11-openjdk-devel
   ```

3. **Set JAVA_HOME**: Add the following to your `.bashrc` or `.bash_profile`:

   ```bash
   export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
   ```

4. **Verify Installation**:

   ```bash
   java -version
   ```

### Step 2: Installing Leiningen

Leiningen is the build automation tool for Clojure, similar to Maven or Gradle for Java. It simplifies project management and dependency handling.

#### 2.1 Installing Leiningen on All Platforms

1. **Download the Leiningen Script**: Open a terminal and run:

   ```bash
   curl https://raw.githubusercontent.com/technomancy/leiningen/stable/bin/lein -o lein
   ```

2. **Make the Script Executable**:

   ```bash
   chmod +x lein
   ```

3. **Move the Script to a Directory in Your PATH**:

   ```bash
   sudo mv lein /usr/local/bin/
   ```

4. **Run Leiningen**: Execute the following command to download the Leiningen self-install package:

   ```bash
   lein
   ```

   This command will download the necessary files and set up Leiningen.

### Step 3: Setting Up Your IDE or Text Editor

Choosing the right IDE or text editor can significantly enhance your productivity. Here, we'll cover setup instructions for IntelliJ IDEA with Cursive, Emacs with CIDER, and VSCode with Calva.

#### 3.1 IntelliJ IDEA with Cursive

IntelliJ IDEA is a popular choice among Java developers, and the Cursive plugin adds excellent support for Clojure.

1. **Install IntelliJ IDEA**: Download and install [IntelliJ IDEA](https://www.jetbrains.com/idea/download/).

2. **Install the Cursive Plugin**:
   - Open IntelliJ IDEA and navigate to `File > Settings > Plugins`.
   - Search for "Cursive" and click "Install."

3. **Create a New Clojure Project**:
   - Go to `File > New > Project`.
   - Select "Clojure" from the list of project types.
   - Follow the prompts to configure your project.

4. **Configure the REPL**:
   - Open the `Run` menu and select `Edit Configurations`.
   - Add a new "Clojure REPL" configuration.
   - Set the module and working directory as needed.

#### 3.2 Emacs with CIDER

Emacs is a powerful text editor favored by many developers for its extensibility. CIDER is the Clojure Interactive Development Environment that integrates with Emacs.

1. **Install Emacs**: Follow the instructions on the [GNU Emacs website](https://www.gnu.org/software/emacs/download.html) to install Emacs on your system.

2. **Install CIDER**:
   - Open Emacs and add the following to your `.emacs` or `init.el` file:

     ```lisp
     (require 'package)
     (add-to-list 'package-archives
                  '("melpa" . "https://melpa.org/packages/") t)
     (package-initialize)
     ```

   - Install CIDER by running `M-x package-refresh-contents` followed by `M-x package-install RET cider RET`.

3. **Create a Clojure Project**:
   - Use Leiningen to create a new project:

     ```bash
     lein new app my-clojure-app
     ```

   - Open the project in Emacs.

4. **Start the REPL**:
   - Open a Clojure file and run `M-x cider-jack-in` to start the REPL.

#### 3.3 VSCode with Calva

Visual Studio Code is a lightweight, versatile editor with robust support for Clojure through the Calva extension.

1. **Install Visual Studio Code**: Download and install [VSCode](https://code.visualstudio.com/).

2. **Install the Calva Extension**:
   - Open VSCode and navigate to the Extensions view (`Ctrl+Shift+X`).
   - Search for "Calva" and click "Install."

3. **Create a Clojure Project**:
   - Use Leiningen to create a new project:

     ```bash
     lein new app my-clojure-app
     ```

   - Open the project folder in VSCode.

4. **Configure the REPL**:
   - Open a Clojure file and use the command palette (`Ctrl+Shift+P`) to run `Calva: Start a Project REPL and Connect`.

### Step 4: Configuring the REPL

The REPL (Read-Eval-Print Loop) is a powerful tool for interactive development in Clojure. Here's how to configure it for optimal use:

#### 4.1 Understanding the REPL

The REPL allows you to evaluate Clojure expressions interactively, providing immediate feedback. It's an essential tool for exploring code, testing functions, and debugging.

#### 4.2 Starting the REPL

- **Leiningen**: Run `lein repl` in your project directory to start the REPL.
- **IDE Integration**: Use the REPL integration features in your chosen IDE or editor (as described in the setup instructions above).

#### 4.3 Using the REPL Effectively

- **Evaluate Code**: Send code from your editor to the REPL for evaluation. Most IDEs and editors provide shortcuts for this.
- **Explore Libraries**: Load and test libraries in the REPL to understand their functionality.
- **Debugging**: Use the REPL to test small code snippets and debug issues interactively.

#### 4.4 REPL Best Practices

- **Keep the REPL Running**: Maintain a persistent REPL session to avoid the overhead of restarting it frequently.
- **Use Namespaces**: Organize your code into namespaces and switch between them in the REPL as needed.
- **Leverage REPL History**: Use the REPL's command history to recall and edit previous commands.

### Step 5: Additional Tools and Tips

To further enhance your Clojure development experience, consider the following tools and tips:

#### 5.1 Linter and Formatter

- **clj-kondo**: A linter for Clojure that helps identify potential issues in your code. Install it via Homebrew or download it from [GitHub](https://github.com/clj-kondo/clj-kondo).
- **cljfmt**: A formatter for Clojure code. Integrate it with your editor to maintain consistent code style.

#### 5.2 Version Control

- **Git**: Use Git for version control to track changes and collaborate with others. Ensure your project is initialized as a Git repository.

#### 5.3 Continuous Integration

- **CircleCI or GitHub Actions**: Set up continuous integration pipelines to automate testing and deployment.

#### 5.4 Documentation

- **Codox**: Generate API documentation for your Clojure projects using Codox. It integrates with Leiningen for easy setup.

### Conclusion

Setting up a Clojure development environment involves installing Java, Leiningen, and configuring your preferred IDE or text editor. By following the steps outlined in this guide, you'll be well-equipped to start developing Clojure applications efficiently. Remember to leverage the REPL for interactive development and explore additional tools to enhance your productivity.

With your environment set up, you're ready to dive deeper into Clojure and explore the functional programming paradigms that set it apart from traditional object-oriented languages like Java.

## Quiz Time!

{{< quizdown >}}

### What is the primary build tool for Clojure?

- [x] Leiningen
- [ ] Maven
- [ ] Gradle
- [ ] Ant

> **Explanation:** Leiningen is the primary build tool for Clojure, similar to Maven or Gradle for Java.

### Which Java version is required at a minimum for running Clojure?

- [ ] Java 6
- [ ] Java 7
- [x] Java 8
- [ ] Java 11

> **Explanation:** Clojure requires at least Java 8 to run, as it relies on features introduced in this version.

### Which IDE plugin is recommended for Clojure development in IntelliJ IDEA?

- [ ] Eclipse Clojure
- [x] Cursive
- [ ] Calva
- [ ] CIDER

> **Explanation:** Cursive is the recommended plugin for Clojure development in IntelliJ IDEA, providing comprehensive support for the language.

### What command is used to start a REPL in a Leiningen project?

- [ ] lein start
- [x] lein repl
- [ ] lein run
- [ ] lein init

> **Explanation:** The `lein repl` command is used to start a REPL session in a Leiningen project.

### Which extension is used for Clojure development in VSCode?

- [ ] CIDER
- [ ] Paredit
- [x] Calva
- [ ] Spacemacs

> **Explanation:** Calva is the extension used for Clojure development in Visual Studio Code, offering features like REPL integration and syntax highlighting.

### How can you make the Leiningen script executable on Unix-like systems?

- [x] chmod +x lein
- [ ] chmod 777 lein
- [ ] chown lein
- [ ] ln -s lein

> **Explanation:** The `chmod +x lein` command makes the Leiningen script executable on Unix-like systems.

### What is the purpose of the `JAVA_HOME` environment variable?

- [ ] To specify the Java version
- [x] To point to the Java installation directory
- [ ] To configure the Java compiler
- [ ] To set the Java classpath

> **Explanation:** The `JAVA_HOME` environment variable is used to specify the path to the Java installation directory.

### Which tool is recommended for linting Clojure code?

- [ ] ESLint
- [ ] Prettier
- [x] clj-kondo
- [ ] Checkstyle

> **Explanation:** clj-kondo is a linter for Clojure that helps identify potential issues in your code.

### What is the primary benefit of using a REPL in Clojure development?

- [ ] Faster compilation
- [ ] Easier debugging
- [x] Interactive code evaluation
- [ ] Automated testing

> **Explanation:** The primary benefit of using a REPL in Clojure development is the ability to interactively evaluate code and receive immediate feedback.

### True or False: Clojure can only be developed using Emacs.

- [ ] True
- [x] False

> **Explanation:** False. Clojure can be developed using various IDEs and editors, including IntelliJ IDEA with Cursive, VSCode with Calva, and Emacs with CIDER.

{{< /quizdown >}}
