---
linkTitle: "A.1.2 Installing on Windows"
title: "Installing Clojure on Windows: A Comprehensive Guide"
description: "Step-by-step guide to installing Clojure and Leiningen on Windows using Scoop and manual methods. Ideal for Java developers transitioning to Clojure."
categories:
- Clojure
- NoSQL
- Windows Installation
tags:
- Clojure Installation
- Windows
- Scoop
- Leiningen
- Java Developers
date: 2024-10-25
type: docs
nav_weight: 1812000
canonical: "https://clojureforjava.com/5/18/1/2"
license: "© 2024 Tokenizer Inc. CC BY-NC-SA 4.0"
---

## A.1.2 Installing on Windows

As a Java developer venturing into the world of Clojure, setting up your development environment on Windows is a crucial first step. This guide will walk you through the installation process using two methods: the recommended Scoop package manager and a manual installation approach. By the end of this guide, you'll have a fully functional Clojure environment ready for developing scalable data solutions with NoSQL databases.

### Why Clojure on Windows?

Windows remains a popular operating system for many developers, and setting up Clojure on Windows allows you to leverage your existing tools and workflows. Clojure's seamless integration with Java makes it an attractive choice for Java developers looking to explore functional programming and NoSQL data solutions.

### Prerequisites

Before diving into the installation process, ensure that you have the following:

- **Windows 10 or later**: This guide assumes you are using a modern version of Windows.
- **Administrator Access**: Some installation steps require administrative privileges.
- **Internet Connection**: Required for downloading installation packages and dependencies.

### Installing Clojure Using Scoop (Recommended)

Scoop is a command-line installer for Windows that simplifies the installation of development tools. It handles dependencies and ensures that your software is up to date.

#### Step 1: Install Scoop

1. **Open PowerShell as Administrator**: Right-click on the Start menu, select "Windows PowerShell (Admin)" to open PowerShell with administrative privileges.

2. **Set Execution Policy**: Run the following command to allow script execution, which is necessary for Scoop to function:

   ```powershell
   Set-ExecutionPolicy RemoteSigned -scope CurrentUser
   ```

   This command changes the execution policy for the current user, allowing you to run scripts that are signed by a trusted publisher.

3. **Install Scoop**: Execute the following command to install Scoop:

   ```powershell
   iwr -useb get.scoop.sh | iex
   ```

   This command downloads and executes the Scoop installation script. Once completed, Scoop will be installed and ready to use.

#### Step 2: Install Clojure

With Scoop installed, you can now install Clojure:

1. **Install Clojure**: Run the following command in PowerShell:

   ```powershell
   scoop install clojure
   ```

   Scoop will download and install the latest version of Clojure, along with any necessary dependencies.

#### Step 3: Install Leiningen

Leiningen is a build automation tool for Clojure, similar to Maven for Java. It simplifies project management and dependency handling.

1. **Install Leiningen**: Execute the following command:

   ```powershell
   scoop install leiningen
   ```

   This command installs Leiningen, enabling you to create and manage Clojure projects efficiently.

#### Step 4: Verify Installations

To ensure that Clojure and Leiningen are installed correctly, verify their versions:

1. **Check Clojure Version**: Run the following command:

   ```powershell
   clojure -M --version
   ```

   You should see the installed version of Clojure displayed in the terminal.

2. **Check Leiningen Version**: Execute:

   ```powershell
   lein -v
   ```

   This command displays the installed version of Leiningen, confirming that the installation was successful.

### Manual Installation of Clojure

If you prefer not to use Scoop, you can manually install Clojure and Leiningen. This method involves downloading and setting up the necessary files yourself.

#### Step 1: Download the Windows Installer

1. **Visit the Clojure Website**: Go to the [Clojure Tools for Windows](https://clojure.org/guides/install_clojure#_windows) page.

2. **Download the Installer**: Click on the link to download the Clojure installer for Windows. This installer includes the Clojure CLI tools.

3. **Run the Installer**: Double-click the downloaded file to start the installation process. Follow the on-screen instructions to complete the installation.

#### Step 2: Install Leiningen

Leiningen is not included in the Clojure installer, so you need to set it up separately.

1. **Download `leiningen.bat`**: Visit the [Leiningen GitHub repository](https://github.com/technomancy/leiningen) and download the `leiningen.bat` file.

2. **Add to PATH**: Place the `leiningen.bat` file in a directory that is included in your system's `PATH` environment variable. This allows you to run Leiningen from any command prompt.

3. **Run Self-Install**: Open a command prompt and run the following command:

   ```shell
   lein self-install
   ```

   This command downloads the necessary Leiningen files and sets up your environment.

#### Step 3: Verify Installations

To confirm that everything is set up correctly, check the versions of Clojure and Leiningen:

1. **Check Clojure Version**: Open a command prompt and run:

   ```shell
   clojure -M --version
   ```

2. **Check Leiningen Version**: Execute:

   ```shell
   lein -v
   ```

   Both commands should display the respective version numbers, indicating successful installation.

### Best Practices for Clojure Development on Windows

- **Use a Modern IDE**: Consider using an IDE with Clojure support, such as IntelliJ IDEA with the Cursive plugin, to enhance your development experience.
- **Leverage REPL**: Take advantage of Clojure's interactive REPL for rapid prototyping and testing.
- **Version Control**: Use Git for version control to manage your Clojure projects effectively.
- **Regular Updates**: Keep your tools and libraries updated to benefit from the latest features and security patches.

### Common Pitfalls and Troubleshooting

- **Execution Policy Errors**: If you encounter issues with script execution, ensure that the execution policy is set correctly using `Set-ExecutionPolicy`.
- **PATH Configuration**: Double-check that `leiningen.bat` is in a directory included in your `PATH`. Incorrect PATH settings can lead to command not found errors.
- **Network Issues**: If downloads fail, verify your internet connection and try again.

### Conclusion

Setting up Clojure on Windows is a straightforward process, whether you choose the convenience of Scoop or prefer manual installation. With your environment ready, you're equipped to explore the powerful combination of Clojure and NoSQL databases, leveraging your Java expertise to build scalable data solutions.

## Quiz Time!

{{< quizdown >}}

### What is the recommended tool for installing Clojure on Windows?

- [x] Scoop
- [ ] Chocolatey
- [ ] Homebrew
- [ ] npm

> **Explanation:** Scoop is recommended for installing Clojure on Windows due to its simplicity and ability to manage dependencies.

### Which command is used to set the execution policy in PowerShell?

- [x] Set-ExecutionPolicy RemoteSigned -scope CurrentUser
- [ ] Set-Policy RemoteSigned
- [ ] Set-Execution RemoteSigned
- [ ] Set-PolicyExecution RemoteSigned -scope CurrentUser

> **Explanation:** The `Set-ExecutionPolicy RemoteSigned -scope CurrentUser` command allows the execution of scripts signed by a trusted publisher for the current user.

### How do you verify the installation of Clojure using Scoop?

- [x] clojure -M --version
- [ ] clojure --check
- [ ] clojure -v
- [ ] clojure --verify

> **Explanation:** Running `clojure -M --version` displays the installed version of Clojure, confirming the installation.

### What is the purpose of the `lein self-install` command?

- [x] To download and set up Leiningen
- [ ] To update Leiningen to the latest version
- [ ] To uninstall Leiningen
- [ ] To verify Leiningen installation

> **Explanation:** The `lein self-install` command downloads the necessary Leiningen files and completes the setup process.

### Which file must be downloaded for manual installation of Leiningen?

- [x] leiningen.bat
- [ ] lein.bat
- [ ] lein.exe
- [ ] lein.sh

> **Explanation:** The `leiningen.bat` file is required for setting up Leiningen manually on Windows.

### What should you do if you encounter script execution errors in PowerShell?

- [x] Check and set the execution policy
- [ ] Reinstall PowerShell
- [ ] Use Command Prompt instead
- [ ] Disable script execution

> **Explanation:** Setting the execution policy correctly resolves script execution errors in PowerShell.

### Where should `leiningen.bat` be placed for manual installation?

- [x] In a directory included in the PATH
- [ ] In the Windows System32 folder
- [ ] In the Clojure installation directory
- [ ] In the user's Documents folder

> **Explanation:** Placing `leiningen.bat` in a directory included in the PATH allows it to be executed from any command prompt.

### What is the primary advantage of using Scoop for installation?

- [x] Simplifies dependency management
- [ ] Provides a graphical user interface
- [ ] Offers more installation options
- [ ] Integrates with Visual Studio

> **Explanation:** Scoop simplifies dependency management and ensures that software is up to date, making it ideal for command-line installations.

### True or False: Clojure can only be installed on Windows using Scoop.

- [ ] True
- [x] False

> **Explanation:** Clojure can be installed manually on Windows without using Scoop, although Scoop is recommended for its simplicity.

### Which IDE is recommended for Clojure development on Windows?

- [x] IntelliJ IDEA with Cursive
- [ ] Visual Studio Code
- [ ] Eclipse
- [ ] NetBeans

> **Explanation:** IntelliJ IDEA with the Cursive plugin is recommended for Clojure development due to its robust support for Clojure features.

{{< /quizdown >}}
