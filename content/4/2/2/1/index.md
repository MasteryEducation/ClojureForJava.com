---
linkTitle: "2.2.1 Visual Studio Code with Calva"
title: "Visual Studio Code with Calva: A Comprehensive Guide for Clojure Development"
description: "Explore the integration of Visual Studio Code with Calva for Clojure development, including installation, basic usage, features, and customization."
categories:
- Clojure Development
- Integrated Development Environments (IDEs)
- Programming Tools
tags:
- Clojure
- Visual Studio Code
- Calva
- REPL
- Code Evaluation
date: 2024-10-25
type: docs
nav_weight: 221000
canonical: "https://clojureforjava.com/4/2/2/1"
license: "© 2024 Tokenizer Inc. CC BY-NC-SA 4.0"
---

## 2.2.1 Visual Studio Code with Calva

Visual Studio Code (VS Code) has become one of the most popular code editors due to its versatility, extensive plugin ecosystem, and ease of use. For Clojure developers, the Calva extension transforms VS Code into a powerful Clojure development environment. This section will guide you through installing Calva, using its features, and customizing it to suit your development workflow.

### Installing Calva Extension for Clojure Support

To begin using Clojure in Visual Studio Code, you need to install the Calva extension. Calva provides rich support for Clojure and ClojureScript development, including features like inline evaluation, REPL integration, and more.

#### Step-by-Step Installation Guide

1. **Open Visual Studio Code:**
   Launch VS Code on your machine. If you haven't installed it yet, download it from [Visual Studio Code's official website](https://code.visualstudio.com/).

2. **Access the Extensions Marketplace:**
   Click on the Extensions icon in the Activity Bar on the side of the window or press `Ctrl+Shift+X` (or `Cmd+Shift+X` on macOS) to open the Extensions view.

3. **Search for Calva:**
   In the search bar, type "Calva" to find the extension. The full name is "Calva: Clojure & ClojureScript Interactive Programming."

4. **Install Calva:**
   Click the "Install" button to add Calva to your VS Code setup. Once installed, you'll see a "Reload" button, which you should click to activate the extension.

5. **Verify Installation:**
   After reloading, you can verify that Calva is installed by checking the status bar at the bottom of VS Code, where you'll see Clojure-related icons and options.

### Basic Usage: Creating a New Clojure Project and Connecting to a REPL

With Calva installed, you can now create a new Clojure project and connect to a REPL (Read-Eval-Print Loop), which is essential for interactive development.

#### Creating a New Clojure Project

1. **Open the Terminal:**
   Use the integrated terminal in VS Code by selecting `Terminal > New Terminal` from the menu or pressing ``Ctrl+` `` (or ``Cmd+` `` on macOS).

2. **Generate a New Project:**
   Use Leiningen, a popular Clojure build tool, to create a new project. Run the following command in the terminal:
   ```bash
   lein new app my-clojure-app
   ```
   This command creates a new Clojure application named `my-clojure-app`.

3. **Open the Project:**
   Navigate to the newly created project directory:
   ```bash
   cd my-clojure-app
   ```
   Then open this directory in VS Code using the command:
   ```bash
   code .
   ```

#### Connecting to a REPL

1. **Start the REPL:**
   In the terminal, start a Clojure REPL by running:
   ```bash
   lein repl
   ```
   This command launches a REPL session, allowing you to interactively evaluate Clojure code.

2. **Connect Calva to the REPL:**
   With the REPL running, use Calva to connect to it. Click on the "Jack-in" button in the status bar or use the command palette (`Ctrl+Shift+P` or `Cmd+Shift+P`) and type "Calva: Start a Project REPL and Connect (a.k.a. Jack-in)".

3. **Select the Project Type:**
   Calva will prompt you to select the type of project. Choose "Leiningen" since you are using Leiningen to manage your project.

4. **Verify Connection:**
   Once connected, you can evaluate Clojure expressions directly from your source files. Highlight a piece of code and press `Ctrl+Enter` (or `Cmd+Enter` on macOS) to evaluate it in the REPL.

### Features Overview: Code Evaluation, Debugging, and Inline Result Viewing

Calva offers a suite of features that enhance the Clojure development experience in VS Code. Let's explore some of the key functionalities.

#### Code Evaluation

Calva allows you to evaluate Clojure code snippets directly within your editor. This feature is crucial for testing and debugging code in real-time.

- **Inline Evaluation:**
  Place your cursor on a Clojure expression and press `Ctrl+Enter` (or `Cmd+Enter` on macOS) to evaluate it. The result appears inline, right next to the code.

- **Evaluation of Selected Code:**
  Highlight a block of code and use the same key combination to evaluate the selection. This is useful for testing specific parts of your code without running the entire program.

#### Debugging

While Clojure's functional nature often reduces the need for traditional debugging, Calva provides tools to help you inspect and debug your code.

- **Breakpoints:**
  Although Clojure doesn't support breakpoints in the traditional sense, you can insert `println` statements or use the `tap>` function to log values at specific points in your code.

- **Stack Traces:**
  When an error occurs, Calva displays a stack trace in the terminal, helping you trace the source of the error.

#### Inline Result Viewing

One of Calva's standout features is the ability to view evaluation results inline. This feature enhances the interactive programming experience by providing immediate feedback.

- **Result Annotations:**
  After evaluating an expression, Calva annotates the result next to the code. This feature is particularly useful for understanding the output of complex expressions.

- **Result History:**
  Calva maintains a history of evaluated expressions and their results, allowing you to review past evaluations easily.

### Customization: Settings for Linting and Formatting

Calva is highly customizable, allowing you to tailor the development environment to your preferences, particularly in terms of linting and formatting.

#### Configuring Linting

Linting helps maintain code quality by highlighting potential errors and enforcing coding standards.

- **Clojure Linting:**
  Calva integrates with clj-kondo, a popular linter for Clojure. To enable linting, ensure that clj-kondo is installed on your system. You can install it via Homebrew on macOS:
  ```bash
  brew install borkdude/brew/clj-kondo
  ```

- **Customizing Linting Rules:**
  You can customize linting rules by creating a `.clj-kondo/config.edn` file in your project directory. This file allows you to enable or disable specific linting checks.

#### Formatting Code

Consistent code formatting improves readability and maintainability.

- **Calva Formatter:**
  Calva includes a built-in formatter that adheres to community standards. To format your code, use the command palette and select "Format Document" or press `Shift+Alt+F` (or `Shift+Option+F` on macOS).

- **Customizing Formatting:**
  You can customize the formatting settings by modifying the `settings.json` file in your VS Code configuration. For example, you can adjust indentation levels or line length.

### Best Practices and Common Pitfalls

As you integrate Calva into your Clojure development workflow, keep the following best practices and common pitfalls in mind:

#### Best Practices

- **Regularly Update Extensions:**
  Keep Calva and other extensions up to date to benefit from the latest features and bug fixes.

- **Use REPL-Driven Development:**
  Embrace REPL-driven development by frequently evaluating code snippets and iterating quickly.

- **Leverage Inline Results:**
  Use inline results to gain immediate feedback on code changes, enhancing your understanding of complex logic.

#### Common Pitfalls

- **Ignoring Linting Warnings:**
  Pay attention to linting warnings, as they can help you catch potential issues early in the development process.

- **Overlooking Configuration:**
  Spend time configuring Calva to suit your workflow. Proper configuration can significantly enhance productivity.

### Conclusion

Visual Studio Code, combined with the Calva extension, offers a robust environment for Clojure development. From installation to customization, this guide has covered the essential aspects of using Calva effectively. By leveraging its features, such as code evaluation, debugging, and inline result viewing, you can enhance your productivity and streamline your Clojure development workflow.

## Quiz Time!

{{< quizdown >}}

### What is the primary purpose of the Calva extension in Visual Studio Code?

- [x] To provide Clojure and ClojureScript support in VS Code
- [ ] To enhance Java development in VS Code
- [ ] To manage project dependencies
- [ ] To create Docker containers

> **Explanation:** Calva is specifically designed to add Clojure and ClojureScript support to Visual Studio Code, enhancing the development experience for these languages.

### How do you install the Calva extension in Visual Studio Code?

- [x] Through the Extensions Marketplace in VS Code
- [ ] By downloading it from the Calva website
- [ ] By installing it via npm
- [ ] By using a command-line tool

> **Explanation:** The Calva extension can be installed directly from the Extensions Marketplace within Visual Studio Code.

### What command is used to create a new Clojure project with Leiningen?

- [x] `lein new app my-clojure-app`
- [ ] `lein create project my-clojure-app`
- [ ] `lein init my-clojure-app`
- [ ] `lein start my-clojure-app`

> **Explanation:** The command `lein new app my-clojure-app` is used to generate a new Clojure application project using Leiningen.

### Which key combination is used to evaluate a Clojure expression inline in Calva?

- [x] `Ctrl+Enter` (or `Cmd+Enter` on macOS)
- [ ] `Alt+Enter`
- [ ] `Shift+Enter`
- [ ] `Ctrl+Shift+Enter`

> **Explanation:** In Calva, `Ctrl+Enter` (or `Cmd+Enter` on macOS) is the key combination used to evaluate a Clojure expression inline.

### What tool does Calva integrate with for linting Clojure code?

- [x] clj-kondo
- [ ] ESLint
- [ ] JSHint
- [ ] Prettier

> **Explanation:** Calva integrates with clj-kondo, a popular linter for Clojure, to provide linting capabilities.

### How can you customize linting rules in a Clojure project using Calva?

- [x] By creating a `.clj-kondo/config.edn` file
- [ ] By modifying the `settings.json` file in VS Code
- [ ] By installing additional VS Code extensions
- [ ] By changing the `project.clj` file

> **Explanation:** Linting rules can be customized by creating a `.clj-kondo/config.edn` file in the project directory.

### Which feature of Calva allows you to view evaluation results directly next to your code?

- [x] Inline Result Viewing
- [ ] Code Snippets
- [ ] Syntax Highlighting
- [ ] Code Folding

> **Explanation:** Inline Result Viewing in Calva allows developers to see the results of evaluated expressions directly next to the code.

### What is the benefit of using REPL-driven development in Clojure?

- [x] It allows for interactive testing and rapid iteration
- [ ] It automates code deployment
- [ ] It simplifies version control
- [ ] It enhances code security

> **Explanation:** REPL-driven development enables interactive testing and rapid iteration, which is a key advantage in Clojure development.

### How can you format Clojure code in Visual Studio Code using Calva?

- [x] By using the "Format Document" command or pressing `Shift+Alt+F` (or `Shift+Option+F` on macOS)
- [ ] By running a shell script
- [ ] By editing the `project.clj` file
- [ ] By using a third-party application

> **Explanation:** Calva provides a built-in formatter that can be accessed via the "Format Document" command or the specified key combination.

### True or False: Calva requires a separate installation of a REPL to function.

- [x] True
- [ ] False

> **Explanation:** Calva requires an external REPL, such as one provided by Leiningen, to function properly and connect for interactive development.

{{< /quizdown >}}
