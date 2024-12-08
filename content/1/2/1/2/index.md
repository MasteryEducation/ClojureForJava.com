---
canonical: "https://clojureforjava.com/1/2/1/2"
title: "Downloading and Installing Java for Clojure Development"
description: "Learn how to download and install Java for Clojure development on Windows, macOS, and Linux. This guide covers Oracle JDK, OpenJDK, and AdoptOpenJDK, with step-by-step instructions and best practices."
linkTitle: "2.1.2 Downloading and Installing Java"
tags:
- "Java Installation"
- "JDK"
- "OpenJDK"
- "Clojure Development"
- "Java Setup"
- "Oracle JDK"
- "AdoptOpenJDK"
- "Cross-Platform Installation"
date: 2024-11-25
type: docs
nav_weight: 21200
license: "© 2024 Tokenizer Inc. CC BY-NC-SA 4.0"
---

## 2.1.2 Downloading and Installing Java

As experienced Java developers transitioning to Clojure, setting up your development environment is crucial. Java Development Kit (JDK) is a prerequisite for running Clojure, as Clojure runs on the Java Virtual Machine (JVM). This section will guide you through downloading and installing the JDK on different operating systems, ensuring you have the right tools to start your Clojure journey.

### Choosing the Right JDK

Before diving into the installation process, it's important to choose the right JDK distribution. There are several options available:

- **Oracle JDK**: The official JDK from Oracle, often used in enterprise environments. It offers commercial support and long-term support (LTS) versions.
- **OpenJDK**: The open-source implementation of the Java Platform, Standard Edition. It is widely used and supported by the community.
- **AdoptOpenJDK**: Now part of the Eclipse Foundation as Adoptium, it provides prebuilt OpenJDK binaries with a focus on performance and security.

#### Selecting the Appropriate Version

When choosing a JDK version, consider the following:

- **LTS Versions**: These versions receive updates and support for an extended period, making them ideal for production environments. Examples include Java 11 and Java 17.
- **Standard Releases**: These are released every six months and may not have long-term support. They are suitable for testing new features.

For Clojure development, it's recommended to use an LTS version to ensure stability and compatibility.

### Downloading and Installing Java on Windows

#### Step 1: Download the JDK

1. **Visit the Official JDK Website**: Go to the [Oracle JDK](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html) or [AdoptOpenJDK](https://adoptopenjdk.net/) website.
2. **Select the Version**: Choose the appropriate JDK version (e.g., Java 11 LTS) and click on the download link for Windows.
3. **Choose the Installer**: Download the `.exe` installer for Windows.

#### Step 2: Install the JDK

1. **Run the Installer**: Double-click the downloaded `.exe` file to start the installation process.
2. **Follow the Installation Wizard**: Accept the license agreement and choose the installation directory. The default path is usually `C:\Program Files\Java\jdk-<version>`.
3. **Complete the Installation**: Click "Next" and "Finish" to complete the installation.

#### Step 3: Set Environment Variables

1. **Open System Properties**: Right-click on "This PC" or "My Computer" and select "Properties".
2. **Access Environment Variables**: Click on "Advanced system settings" and then "Environment Variables".
3. **Add JAVA_HOME**: Under "System variables", click "New" and add `JAVA_HOME` with the path to your JDK installation (e.g., `C:\Program Files\Java\jdk-<version>`).
4. **Update PATH Variable**: Find the "Path" variable, click "Edit", and add `%JAVA_HOME%\bin`.

#### Step 4: Verify the Installation

1. **Open Command Prompt**: Press `Win + R`, type `cmd`, and press Enter.
2. **Check Java Version**: Type `java -version` and `javac -version` to verify the installation.

```shell
java -version
javac -version
```

### Downloading and Installing Java on macOS

#### Step 1: Download the JDK

1. **Visit the Official JDK Website**: Go to the [Oracle JDK](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html) or [AdoptOpenJDK](https://adoptopenjdk.net/) website.
2. **Select the Version**: Choose the appropriate JDK version (e.g., Java 11 LTS) and click on the download link for macOS.
3. **Choose the Installer**: Download the `.dmg` installer for macOS.

#### Step 2: Install the JDK

1. **Open the Installer**: Double-click the downloaded `.dmg` file to mount it.
2. **Run the Package Installer**: Double-click the `.pkg` file to start the installation process.
3. **Follow the Installation Wizard**: Accept the license agreement and follow the prompts to complete the installation.

#### Step 3: Set Environment Variables

1. **Open Terminal**: Press `Cmd + Space`, type `Terminal`, and press Enter.
2. **Edit Profile**: Open your profile file (`~/.bash_profile`, `~/.zshrc`, or `~/.bashrc`) in a text editor.
3. **Add JAVA_HOME**: Add the following line to set the `JAVA_HOME` environment variable:

```shell
export JAVA_HOME=$(/usr/libexec/java_home)
```

4. **Update PATH Variable**: Add the following line to update the `PATH` variable:

```shell
export PATH=$JAVA_HOME/bin:$PATH
```

5. **Apply Changes**: Save the file and run `source ~/.bash_profile` (or the equivalent for your shell) to apply the changes.

#### Step 4: Verify the Installation

1. **Check Java Version**: In Terminal, type `java -version` and `javac -version` to verify the installation.

```shell
java -version
javac -version
```

### Downloading and Installing Java on Linux

#### Step 1: Download the JDK

1. **Visit the Official JDK Website**: Go to the [Oracle JDK](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html) or [AdoptOpenJDK](https://adoptopenjdk.net/) website.
2. **Select the Version**: Choose the appropriate JDK version (e.g., Java 11 LTS) and click on the download link for Linux.
3. **Choose the Package**: Download the `.tar.gz` archive or the `.deb`/`.rpm` package for your distribution.

#### Step 2: Install the JDK

For Debian-based systems (e.g., Ubuntu):

1. **Open Terminal**: Press `Ctrl + Alt + T` to open Terminal.
2. **Install the Package**: Use `dpkg` to install the downloaded package:

```shell
sudo dpkg -i <package-name>.deb
```

For Red Hat-based systems (e.g., Fedora, CentOS):

1. **Open Terminal**: Press `Ctrl + Alt + T` to open Terminal.
2. **Install the Package**: Use `rpm` to install the downloaded package:

```shell
sudo rpm -ivh <package-name>.rpm
```

For other distributions:

1. **Extract the Archive**: Use `tar` to extract the `.tar.gz` archive:

```shell
tar -xvf <package-name>.tar.gz
```

2. **Move to /opt**: Move the extracted directory to `/opt`:

```shell
sudo mv jdk-<version> /opt/
```

#### Step 3: Set Environment Variables

1. **Edit Profile**: Open your profile file (`~/.bashrc`, `~/.zshrc`, or `~/.bash_profile`) in a text editor.
2. **Add JAVA_HOME**: Add the following line to set the `JAVA_HOME` environment variable:

```shell
export JAVA_HOME=/opt/jdk-<version>
```

3. **Update PATH Variable**: Add the following line to update the `PATH` variable:

```shell
export PATH=$JAVA_HOME/bin:$PATH
```

4. **Apply Changes**: Save the file and run `source ~/.bashrc` (or the equivalent for your shell) to apply the changes.

#### Step 4: Verify the Installation

1. **Check Java Version**: In Terminal, type `java -version` and `javac -version` to verify the installation.

```shell
java -version
javac -version
```

### Troubleshooting Common Issues

- **Java Version Conflicts**: Ensure that the `JAVA_HOME` and `PATH` variables point to the correct JDK version.
- **Permission Errors**: Use `sudo` for commands that require administrative privileges.
- **Incomplete Installation**: Re-download the installer if the installation fails.

### Try It Yourself

To solidify your understanding, try the following:

- **Experiment with Different JDK Versions**: Install both Java 11 and Java 17, and switch between them using the `JAVA_HOME` variable.
- **Automate the Installation**: Write a shell script to automate the JDK installation and environment variable setup.

### Summary and Key Takeaways

- **Choose the Right JDK**: Select an LTS version for stability and long-term support.
- **Follow Platform-Specific Instructions**: Each operating system has unique steps for installation.
- **Verify Your Installation**: Always check the Java version to ensure the installation was successful.

By following these steps, you'll have a robust Java environment ready for Clojure development. Now that you've set up Java, you're one step closer to mastering Clojure's functional programming paradigm.

## Quiz Time!

{{< quizdown >}}

### Which JDK version is recommended for Clojure development?

- [x] Long-Term Support (LTS) version
- [ ] Latest standard release
- [ ] Any version
- [ ] Beta version

> **Explanation:** LTS versions provide stability and long-term support, making them ideal for development environments.


### What is the default installation path for JDK on Windows?

- [x] C:\Program Files\Java\jdk-<version>
- [ ] C:\Java\jdk-<version>
- [ ] C:\Windows\Java\jdk-<version>
- [ ] C:\Users\Java\jdk-<version>

> **Explanation:** The default installation path for JDK on Windows is typically `C:\Program Files\Java\jdk-<version>`.


### How do you set the JAVA_HOME environment variable on macOS?

- [x] export JAVA_HOME=$(/usr/libexec/java_home)
- [ ] export JAVA_HOME=/usr/local/java
- [ ] export JAVA_HOME=/opt/java
- [ ] export JAVA_HOME=/usr/bin/java

> **Explanation:** The command `export JAVA_HOME=$(/usr/libexec/java_home)` dynamically sets the JAVA_HOME variable to the installed JDK location on macOS.


### Which command verifies the Java installation on Linux?

- [x] java -version
- [ ] java --check
- [ ] java --verify
- [ ] java --info

> **Explanation:** The `java -version` command is used to verify the Java installation and check the installed version.


### What is the purpose of setting the PATH variable?

- [x] To include the JDK binaries in the system path
- [ ] To set the default Java editor
- [ ] To configure Java security settings
- [ ] To manage Java libraries

> **Explanation:** Setting the PATH variable ensures that the JDK binaries are accessible from the command line.


### Which JDK distribution is open-source?

- [x] OpenJDK
- [ ] Oracle JDK
- [ ] IBM JDK
- [ ] Microsoft JDK

> **Explanation:** OpenJDK is the open-source implementation of the Java Platform, Standard Edition.


### What command is used to apply changes to the profile file in Linux?

- [x] source ~/.bashrc
- [ ] apply ~/.bashrc
- [ ] run ~/.bashrc
- [ ] exec ~/.bashrc

> **Explanation:** The `source ~/.bashrc` command applies changes made to the profile file by reloading it.


### Which tool is used for installing JDK on Debian-based systems?

- [x] dpkg
- [ ] rpm
- [ ] apt-get
- [ ] yum

> **Explanation:** The `dpkg` tool is used for installing `.deb` packages on Debian-based systems.


### What is the role of AdoptOpenJDK?

- [x] Provides prebuilt OpenJDK binaries
- [ ] Offers commercial support for Java
- [ ] Develops proprietary Java features
- [ ] Manages Java licensing

> **Explanation:** AdoptOpenJDK provides prebuilt OpenJDK binaries with a focus on performance and security.


### True or False: Java 17 is a Long-Term Support (LTS) version.

- [x] True
- [ ] False

> **Explanation:** Java 17 is indeed a Long-Term Support (LTS) version, offering extended support and stability.

{{< /quizdown >}}
