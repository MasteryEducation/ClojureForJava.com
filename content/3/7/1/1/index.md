---
linkTitle: "A.1 Installing Clojure and Leiningen"
title: "Installing Clojure and Leiningen: A Comprehensive Guide for Java Professionals"
description: "Step-by-step installation guide for Clojure and Leiningen across various operating systems, tailored for Java professionals transitioning to Clojure."
categories:
- Clojure
- Installation
- Development Environment
tags:
- Clojure
- Leiningen
- Installation Guide
- Java Professionals
- Development Tools
date: 2024-10-25
type: docs
nav_weight: 711000
canonical: "https://clojureforjava.com/3/7/1/1"
license: "© 2024 Tokenizer Inc. CC BY-NC-SA 4.0"
---

## A.1 Installing Clojure and Leiningen

As a Java professional venturing into the world of Clojure, setting up your development environment is the first step towards mastering this powerful functional programming language. Clojure, being a dialect of Lisp, runs on the Java Virtual Machine (JVM), making it a natural choice for Java developers looking to explore functional programming paradigms. In this section, we will provide a detailed, step-by-step guide to installing Clojure and Leiningen, the build automation tool that simplifies Clojure project management, across different operating systems.

### Overview

Before diving into the installation process, let's briefly discuss what Clojure and Leiningen are and why they are essential for your development workflow.

- **Clojure**: A modern, dynamic, and functional programming language that emphasizes immutability and first-class functions. It is designed to be hosted on the JVM, providing seamless interoperability with Java.

- **Leiningen**: A build automation and dependency management tool for Clojure. It simplifies project setup, dependency management, and task automation, making it an indispensable tool for Clojure developers.

### Installation Prerequisites

Before installing Clojure and Leiningen, ensure that you have the following prerequisites:

1. **Java Development Kit (JDK)**: Clojure runs on the JVM, so you need to have a JDK installed. We recommend using JDK 8 or later. You can verify your Java installation by running `java -version` in your terminal.

2. **Internet Connection**: Both Clojure and Leiningen require downloading files from the internet, so ensure you have a stable internet connection.

3. **Administrator Privileges**: Some installation steps may require administrative access to your system.

### Installing Clojure and Leiningen on Windows

#### Step 1: Install Java Development Kit (JDK)

1. **Download JDK**: Visit the [Oracle JDK download page](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html) or [AdoptOpenJDK](https://adoptopenjdk.net/) for an open-source alternative. Download the installer for your Windows version.

2. **Install JDK**: Run the installer and follow the on-screen instructions. Ensure you set the JAVA_HOME environment variable to the JDK installation path.

3. **Verify Installation**: Open Command Prompt and run `java -version` to verify the installation. You should see the Java version details.

#### Step 2: Install Clojure

1. **Download Clojure Tools**: Visit the [Clojure download page](https://clojure.org/guides/getting_started) and download the Windows installer.

2. **Run the Installer**: Execute the downloaded installer and follow the instructions. This will install the Clojure CLI tools.

3. **Verify Installation**: Open Command Prompt and run `clj -h`. You should see the Clojure command-line help output.

#### Step 3: Install Leiningen

1. **Download Leiningen Script**: Download the `lein.bat` script from the [Leiningen website](https://leiningen.org/).

2. **Place the Script**: Move the `lein.bat` file to a directory included in your system's PATH, such as `C:\Program Files\Leiningen`.

3. **Run Leiningen**: Open Command Prompt and run `lein`. This will download the Leiningen jar file and set up the necessary environment.

4. **Verify Installation**: Run `lein -v` to verify the installation. You should see the Leiningen version number.

### Installing Clojure and Leiningen on macOS

#### Step 1: Install Homebrew

1. **Open Terminal**: Launch the Terminal application.

2. **Install Homebrew**: Run the following command to install Homebrew, a package manager for macOS:

   ```bash
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```

3. **Verify Installation**: Run `brew -v` to verify Homebrew installation.

#### Step 2: Install Java Development Kit (JDK)

1. **Install JDK via Homebrew**: Run the following command to install the latest JDK:

   ```bash
   brew install openjdk
   ```

2. **Set JAVA_HOME**: Add the following line to your `.bash_profile` or `.zshrc` file to set the JAVA_HOME environment variable:

   ```bash
   export JAVA_HOME=$(/usr/libexec/java_home)
   ```

3. **Verify Installation**: Run `java -version` in Terminal to verify the installation.

#### Step 3: Install Clojure

1. **Install Clojure via Homebrew**: Run the following command to install Clojure:

   ```bash
   brew install clojure/tools/clojure
   ```

2. **Verify Installation**: Run `clj -h` to verify the installation. You should see the Clojure command-line help output.

#### Step 4: Install Leiningen

1. **Install Leiningen via Homebrew**: Run the following command to install Leiningen:

   ```bash
   brew install leiningen
   ```

2. **Verify Installation**: Run `lein -v` to verify the installation. You should see the Leiningen version number.

### Installing Clojure and Leiningen on Linux

#### Step 1: Install Java Development Kit (JDK)

1. **Open Terminal**: Launch your terminal application.

2. **Update Package Index**: Run the following command to update your package index:

   ```bash
   sudo apt update
   ```

3. **Install JDK**: Run the following command to install the default JDK:

   ```bash
   sudo apt install default-jdk
   ```

4. **Verify Installation**: Run `java -version` to verify the installation.

#### Step 2: Install Clojure

1. **Download Clojure Installer Script**: Run the following command to download the Clojure installer script:

   ```bash
   curl -O https://download.clojure.org/install/linux-install-1.10.3.1029.sh
   ```

2. **Make the Script Executable**: Run the following command to make the script executable:

   ```bash
   chmod +x linux-install-1.10.3.1029.sh
   ```

3. **Run the Installer**: Execute the installer script with the following command:

   ```bash
   sudo ./linux-install-1.10.3.1029.sh
   ```

4. **Verify Installation**: Run `clj -h` to verify the installation.

#### Step 3: Install Leiningen

1. **Download Leiningen Script**: Run the following command to download the Leiningen script:

   ```bash
   wget https://raw.githubusercontent.com/technomancy/leiningen/stable/bin/lein
   ```

2. **Make the Script Executable**: Run the following command to make the script executable:

   ```bash
   chmod +x lein
   ```

3. **Move the Script to a Directory in PATH**: Run the following command to move the script to a directory in your PATH:

   ```bash
   sudo mv lein /usr/local/bin/
   ```

4. **Run Leiningen**: Execute `lein` in the terminal. This will download the Leiningen jar file and set up the necessary environment.

5. **Verify Installation**: Run `lein -v` to verify the installation.

### Verification and Troubleshooting

After completing the installation steps, it's crucial to verify that both Clojure and Leiningen are functioning correctly. Here are some common verification steps and troubleshooting tips:

#### Verification Steps

1. **Clojure REPL**: Start a Clojure REPL by running `clj` in your terminal. You should see a prompt indicating that the REPL is ready for input.

2. **Leiningen Project**: Create a new Leiningen project by running `lein new app myapp`. This should create a new directory named `myapp` with a basic Clojure application structure.

3. **Run the Application**: Navigate to the `myapp` directory and run `lein run`. You should see output indicating that the application is running.

#### Troubleshooting Tips

1. **JAVA_HOME Not Set**: Ensure that the JAVA_HOME environment variable is set correctly. This is a common issue that can prevent Clojure and Leiningen from running.

2. **Network Issues**: If you encounter network-related errors, ensure that your internet connection is stable and that there are no firewall restrictions blocking downloads.

3. **Permission Denied**: If you receive permission errors, try running the commands with `sudo` (Linux/macOS) or as an administrator (Windows).

4. **Path Issues**: Ensure that the directories containing the `clj` and `lein` executables are included in your system's PATH environment variable.

### Best Practices and Optimization Tips

1. **Use a Version Manager**: Consider using a version manager like SDKMAN! to manage multiple versions of Java and Clojure. This can be particularly useful if you work on projects with different version requirements.

2. **Regular Updates**: Keep your Clojure and Leiningen installations up to date to benefit from the latest features and security patches.

3. **Environment Isolation**: Use tools like Docker to create isolated environments for your Clojure projects, ensuring consistent setups across different machines.

4. **IDE Integration**: Integrate Clojure and Leiningen with your preferred IDE (e.g., IntelliJ IDEA with Cursive) for enhanced development productivity and features like code completion and debugging.

5. **Community Resources**: Engage with the Clojure community through forums, mailing lists, and open-source projects to stay informed about best practices and new developments.

### Conclusion

Installing Clojure and Leiningen is a straightforward process that sets the foundation for your journey into functional programming. By following the steps outlined in this guide, you can ensure a smooth setup across different operating systems, allowing you to focus on learning and applying Clojure's powerful features. Remember to verify your installation and troubleshoot any issues promptly to maintain an efficient development environment.

## Quiz Time!

{{< quizdown >}}

### What is the primary role of Leiningen in Clojure development?

- [x] Build automation and dependency management
- [ ] Code compilation
- [ ] Syntax highlighting
- [ ] Version control

> **Explanation:** Leiningen is a build automation and dependency management tool for Clojure, simplifying project setup and task automation.

### Which command verifies the installation of Clojure on Windows?

- [x] `clj -h`
- [ ] `lein -v`
- [ ] `java -version`
- [ ] `clojure -version`

> **Explanation:** The `clj -h` command provides help output for the Clojure CLI, confirming its installation.

### What is the recommended method to install Clojure on macOS?

- [x] Using Homebrew
- [ ] Downloading a tarball
- [ ] Using MacPorts
- [ ] Compiling from source

> **Explanation:** Homebrew is a popular package manager for macOS, making it easy to install Clojure and manage updates.

### What environment variable must be set for Java to work correctly with Clojure?

- [x] JAVA_HOME
- [ ] PATH
- [ ] CLASSPATH
- [ ] JDK_HOME

> **Explanation:** The JAVA_HOME environment variable points to the JDK installation directory, which is necessary for Java applications.

### Which command is used to create a new Leiningen project?

- [x] `lein new app myapp`
- [ ] `lein create project myapp`
- [ ] `clj new app myapp`
- [ ] `java new app myapp`

> **Explanation:** The `lein new app myapp` command generates a new Clojure application project using Leiningen.

### How can you verify that Leiningen is installed correctly?

- [x] Run `lein -v`
- [ ] Run `lein help`
- [ ] Run `lein check`
- [ ] Run `lein verify`

> **Explanation:** Running `lein -v` displays the version of Leiningen, confirming its installation.

### What tool can be used to manage multiple versions of Java and Clojure?

- [x] SDKMAN!
- [ ] NVM
- [ ] RVM
- [ ] Pyenv

> **Explanation:** SDKMAN! is a tool for managing parallel versions of multiple Software Development Kits, including Java and Clojure.

### What should you do if you encounter "Permission Denied" errors during installation?

- [x] Run commands with `sudo` or as an administrator
- [ ] Restart your computer
- [ ] Reinstall Java
- [ ] Disable your firewall

> **Explanation:** Running commands with `sudo` (Linux/macOS) or as an administrator (Windows) can resolve permission issues.

### Which command is used to start a Clojure REPL?

- [x] `clj`
- [ ] `lein repl`
- [ ] `java repl`
- [ ] `clojure start`

> **Explanation:** The `clj` command starts a Clojure REPL, allowing you to interactively evaluate Clojure code.

### True or False: Clojure can run on the JVM, making it compatible with Java libraries.

- [x] True
- [ ] False

> **Explanation:** Clojure is designed to run on the JVM, providing seamless interoperability with Java libraries and tools.

{{< /quizdown >}}
