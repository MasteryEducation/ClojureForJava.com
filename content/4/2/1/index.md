---
linkTitle: "2.1 Installing Clojure and Leiningen"
title: "Installing Clojure and Leiningen: A Comprehensive Guide for Enterprise Integration"
description: "Learn how to install and configure Clojure and Leiningen on Windows, macOS, and Linux, including environment setup and troubleshooting tips."
categories:
- Clojure
- Installation
- Development
tags:
- Clojure Installation
- Leiningen
- Environment Setup
- Troubleshooting
- Java Developers
date: 2024-10-25
type: docs
nav_weight: 210000
canonical: "https://clojureforjava.com/4/2/1"
license: "© 2024 Tokenizer Inc. CC BY-NC-SA 4.0"
---

## 2.1 Installing Clojure and Leiningen

Clojure, a modern, dynamic, and functional dialect of the Lisp programming language, has gained significant traction in enterprise environments due to its robust features and seamless Java interoperability. To harness the power of Clojure for enterprise integration, it's crucial to set up a development environment that includes both Clojure and Leiningen, the de facto build automation tool for Clojure projects. This section provides a comprehensive guide to installing Clojure and Leiningen across different operating systems, configuring the necessary environment variables, verifying the installations, and troubleshooting common issues.

### Installation Steps

#### Installing Clojure and Leiningen on Windows

1. **Prerequisites:**
   - Ensure you have Java Development Kit (JDK) installed. Clojure requires Java 8 or later. You can download it from [Oracle's official site](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html) or use an open-source alternative like [AdoptOpenJDK](https://adoptopenjdk.net/).

2. **Install Clojure:**
   - Download the Windows installer from the [Clojure official website](https://clojure.org/guides/getting_started).
   - Run the installer and follow the on-screen instructions. The installer will add the `clojure` command to your system PATH.

3. **Install Leiningen:**
   - Download the `lein.bat` script from the [Leiningen website](https://leiningen.org/).
   - Place `lein.bat` in a directory included in your system PATH, such as `C:\Program Files\Leiningen`.
   - Open a command prompt and run `lein self-install`. This command downloads the necessary Leiningen jar files.

4. **Environment Configuration:**
   - Set the `JAVA_HOME` environment variable to point to your JDK installation directory. For example:
     ```shell
     setx JAVA_HOME "C:\Program Files\Java\jdk-11.0.10"
     ```
   - Ensure the `PATH` environment variable includes the directories for Java, Clojure, and Leiningen.

#### Installing Clojure and Leiningen on macOS

1. **Prerequisites:**
   - macOS comes with a pre-installed version of Java, but it's advisable to install the latest JDK using [Homebrew](https://brew.sh/). Run the following command:
     ```shell
     brew install openjdk
     ```

2. **Install Clojure:**
   - Use Homebrew to install Clojure:
     ```shell
     brew install clojure/tools/clojure
     ```

3. **Install Leiningen:**
   - Again, use Homebrew:
     ```shell
     brew install leiningen
     ```

4. **Environment Configuration:**
   - Set the `JAVA_HOME` environment variable by adding the following line to your `~/.bash_profile` or `~/.zshrc` file:
     ```shell
     export JAVA_HOME=$(/usr/libexec/java_home)
     ```
   - Ensure the `PATH` includes `/usr/local/bin` where Homebrew installs binaries.

#### Installing Clojure and Leiningen on Linux

1. **Prerequisites:**
   - Install the JDK. For Ubuntu, you can use:
     ```shell
     sudo apt update
     sudo apt install openjdk-11-jdk
     ```

2. **Install Clojure:**
   - Download and run the installation script:
     ```shell
     curl -O https://download.clojure.org/install/linux-install-1.10.3.1029.sh
     chmod +x linux-install-1.10.3.1029.sh
     sudo ./linux-install-1.10.3.1029.sh
     ```

3. **Install Leiningen:**
   - Download the `lein` script:
     ```shell
     curl -O https://raw.githubusercontent.com/technomancy/leiningen/stable/bin/lein
     chmod +x lein
     sudo mv lein /usr/local/bin/
     ```
   - Run `lein` to complete the installation:
     ```shell
     lein
     ```

4. **Environment Configuration:**
   - Add the following lines to your `~/.bashrc` or `~/.zshrc` file:
     ```shell
     export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
     export PATH=$PATH:/usr/local/bin
     ```

### Verification

After installation, it's essential to verify that both Clojure and Leiningen are correctly installed and accessible from the command line.

- **Verify Clojure Installation:**
  ```shell
  clojure -M
  ```
  This command should start a Clojure REPL (Read-Eval-Print Loop), indicating that Clojure is installed correctly.

- **Verify Leiningen Installation:**
  ```shell
  lein --version
  ```
  This command should output the version of Leiningen installed, confirming a successful installation.

### Troubleshooting Tips

Even with careful installation, you might encounter issues. Here are some common problems and their solutions:

1. **Java Not Found:**
   - Ensure that the `JAVA_HOME` environment variable is set correctly and that the JDK's `bin` directory is included in your `PATH`.

2. **Clojure Command Not Found:**
   - Verify that the Clojure installation directory is included in your `PATH`.

3. **Leiningen Fails to Download Dependencies:**
   - Check your internet connection and ensure that your firewall or proxy settings allow access to external Maven repositories.

4. **Permission Issues on Linux:**
   - Ensure that the `lein` script is executable and located in a directory included in your `PATH`.

5. **Version Conflicts:**
   - If multiple versions of Java or Clojure are installed, ensure that the correct version is prioritized in your `PATH`.

### Conclusion

Setting up Clojure and Leiningen is a crucial step in leveraging the full potential of Clojure for enterprise integration. By following the detailed installation instructions provided for Windows, macOS, and Linux, configuring the necessary environment variables, and verifying the installations, you can ensure a smooth development experience. Additionally, the troubleshooting tips will help you resolve common issues, allowing you to focus on building robust and scalable applications with Clojure.

## Quiz Time!

{{< quizdown >}}

### What is the minimum Java version required for Clojure installation?

- [ ] Java 6
- [ ] Java 7
- [x] Java 8
- [ ] Java 9

> **Explanation:** Clojure requires Java 8 or later for installation and execution.

### Which command is used to verify the installation of Leiningen?

- [x] `lein --version`
- [ ] `lein check`
- [ ] `lein install`
- [ ] `lein verify`

> **Explanation:** The `lein --version` command outputs the installed version of Leiningen, confirming its installation.

### On macOS, which package manager is recommended for installing Clojure and Leiningen?

- [ ] MacPorts
- [x] Homebrew
- [ ] Fink
- [ ] Nix

> **Explanation:** Homebrew is a popular package manager for macOS, making it easy to install and manage software like Clojure and Leiningen.

### What environment variable needs to be set to point to the JDK installation directory?

- [x] `JAVA_HOME`
- [ ] `JDK_HOME`
- [ ] `JAVA_PATH`
- [ ] `JDK_PATH`

> **Explanation:** The `JAVA_HOME` environment variable should be set to the JDK installation directory to ensure Java applications can locate the JDK.

### Which command starts a Clojure REPL to verify its installation?

- [x] `clojure -M`
- [ ] `clojure -R`
- [ ] `clojure -C`
- [ ] `clojure -V`

> **Explanation:** The `clojure -M` command initiates a Clojure REPL, verifying that Clojure is installed correctly.

### What is the purpose of the `lein self-install` command on Windows?

- [x] To download necessary Leiningen jar files
- [ ] To update the Leiningen script
- [ ] To uninstall Leiningen
- [ ] To verify the Leiningen installation

> **Explanation:** The `lein self-install` command downloads the necessary jar files for Leiningen, completing the installation process.

### Which directory should the `lein` script be placed in on Linux for global access?

- [ ] `/usr/bin/`
- [ ] `/bin/`
- [x] `/usr/local/bin/`
- [ ] `/opt/bin/`

> **Explanation:** Placing the `lein` script in `/usr/local/bin/` allows it to be accessible globally on Linux systems.

### What might cause the error "Clojure command not found"?

- [x] Clojure installation directory not in `PATH`
- [ ] Incorrect Java version
- [ ] Missing `lein` script
- [ ] Incorrect `JAVA_HOME` setting

> **Explanation:** If the Clojure installation directory is not included in the `PATH`, the system cannot locate the `clojure` command.

### What should you do if Leiningen fails to download dependencies?

- [x] Check internet connection and firewall settings
- [ ] Reinstall Java
- [ ] Update the `lein` script
- [ ] Change the `JAVA_HOME` variable

> **Explanation:** Ensuring a stable internet connection and proper firewall settings can resolve issues with downloading dependencies.

### True or False: Clojure can be installed without Java.

- [ ] True
- [x] False

> **Explanation:** Clojure requires Java to run, so Java must be installed before installing Clojure.

{{< /quizdown >}}
