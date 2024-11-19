---
linkTitle: "7.2.2 Connecting from IDEs (Cursive, Emacs, VSCode)"
title: "Integrating Clojure REPL with IDEs: Cursive, Emacs, VSCode"
description: "Explore step-by-step instructions for connecting Clojure REPL with popular IDEs like Cursive, Emacs, and VSCode, enhancing your development workflow."
categories:
- Clojure Development
- IDE Integration
- Interactive Programming
tags:
- Clojure
- REPL
- Cursive
- Emacs
- VSCode
- Interactive Development
date: 2024-10-25
type: docs
nav_weight: 722000
canonical: "https://clojureforjava.com/2/7/2/2"
license: "© 2024 Tokenizer Inc. CC BY-NC-SA 4.0"
---

## 7.2.2 Connecting from IDEs (Cursive, Emacs, VSCode)

In the realm of Clojure development, the Read-Eval-Print Loop (REPL) is an indispensable tool that facilitates interactive programming. By integrating the REPL with your Integrated Development Environment (IDE), you can significantly enhance your productivity and streamline your workflow. This section provides a comprehensive guide on connecting the Clojure REPL with three popular IDEs: Cursive (IntelliJ IDEA), Emacs with CIDER, and Visual Studio Code (VSCode) with Calva. Each of these tools offers unique features and benefits, allowing you to choose the one that best fits your development style.

### Cursive (IntelliJ IDEA)

Cursive is a powerful Clojure plugin for IntelliJ IDEA, providing robust support for Clojure development. It seamlessly integrates with the REPL, allowing you to evaluate code directly from the editor.

#### Setting Up a REPL Run Configuration

1. **Install Cursive Plugin:**
   - Open IntelliJ IDEA and navigate to `File > Settings > Plugins`.
   - Search for "Cursive" and install the plugin.
   - Restart IntelliJ IDEA to activate the plugin.

2. **Create a New Project:**
   - Go to `File > New > Project`.
   - Select "Clojure" from the list of project types.
   - Follow the prompts to set up your project.

3. **Configure a REPL Run Configuration:**
   - Open the `Run/Debug Configurations` dialog from the toolbar or via `Run > Edit Configurations`.
   - Click the `+` button and select `Clojure REPL`.
   - Choose the appropriate module and set the REPL type (e.g., `Local` or `Remote`).

4. **Start the REPL:**
   - Click the `Run` button next to your REPL configuration.
   - The REPL console will open, ready for interaction.

#### Connecting to a Running REPL Process

- If you have a Clojure application running with a REPL server, you can connect to it:
  - Open the `Run/Debug Configurations` dialog.
  - Create a new `Remote` REPL configuration.
  - Enter the host and port details of the running REPL server.
  - Click `OK` and then `Run` to connect.

#### Evaluating Code Directly from the Editor

- **Evaluate Expressions:**
  - Place the cursor on the expression you want to evaluate.
  - Use the shortcut `Ctrl + Shift + P` (Windows/Linux) or `Cmd + Shift + P` (Mac) to evaluate the expression.
  - The result will appear in the REPL console.

- **Inline Evaluation:**
  - Cursive supports inline evaluation, allowing you to see results directly in the editor.
  - Use `Alt + Enter` to evaluate the current form and display the result inline.

### Emacs with CIDER

Emacs, combined with CIDER (Clojure Interactive Development Environment that Rocks), provides a powerful and customizable environment for Clojure development. CIDER enhances Emacs with features like code evaluation, debugging, and more.

#### Installing and Configuring CIDER

1. **Install Emacs:**
   - Download and install Emacs from [GNU Emacs](https://www.gnu.org/software/emacs/).

2. **Install CIDER:**
   - Open Emacs and enter the package manager with `M-x package-list-packages`.
   - Search for "cider" and install it.

3. **Configure CIDER:**
   - Add the following to your Emacs configuration file (`~/.emacs` or `~/.emacs.d/init.el`):
     ```elisp
     (require 'cider)
     ```

#### Starting a REPL Session and Connecting

- **Start a REPL:**
  - Open a Clojure file in Emacs.
  - Use `M-x cider-jack-in` to start a REPL session.
  - CIDER will automatically start a REPL and connect to it.

- **Connect to an Existing REPL:**
  - Use `M-x cider-connect`.
  - Enter the host and port of the running REPL server.

#### Using Keybindings to Send Code to the REPL

- **Evaluate Code:**
  - Place the cursor on the expression and use `C-x C-e` to evaluate it.
  - The result will be displayed in the minibuffer.

- **Evaluate Buffer or Region:**
  - Use `C-c C-k` to evaluate the entire buffer.
  - Use `C-c C-r` to evaluate a selected region.

### VSCode with Calva

Visual Studio Code, with the Calva extension, offers a modern and user-friendly environment for Clojure development. Calva provides features like inline evaluation, syntax highlighting, and more.

#### Installing the Calva Extension

1. **Install Visual Studio Code:**
   - Download and install VSCode from [Visual Studio Code](https://code.visualstudio.com/).

2. **Install Calva:**
   - Open the Extensions view in VSCode (`Ctrl + Shift + X`).
   - Search for "Calva" and install it.

#### Initializing a REPL Session

- **Start a REPL:**
  - Open a Clojure file in VSCode.
  - Use the command palette (`Ctrl + Shift + P`) and run `Calva: Start a Project REPL and Connect`.
  - Choose the appropriate project type and follow the prompts.

- **Connect to an Existing REPL:**
  - Use the command palette and run `Calva: Connect to a Running REPL Server`.
  - Enter the host and port details.

#### Interactively Evaluating Code and Viewing Results Inline

- **Evaluate Code:**
  - Place the cursor on the expression and use `Ctrl + Enter` to evaluate it.
  - The result will be displayed inline next to the code.

- **Evaluate Top-Level Form:**
  - Use `Alt + Enter` to evaluate the top-level form containing the cursor.

### Benefits of Editor Integration

Integrating the REPL with your IDE offers numerous benefits:

- **Inline Results:**
  - See results directly in the editor, reducing context switching and improving focus.

- **Better Navigation:**
  - Jump to definitions, find references, and navigate code more efficiently.

- **Enhanced Productivity:**
  - Quickly test and iterate on code, leading to faster development cycles.

- **Error Feedback:**
  - Immediate feedback on errors and exceptions, allowing for quicker debugging.

### Experimentation and Personalization

While each IDE offers unique features, the best choice depends on your personal preferences and workflow. Experiment with different tools to find the one that aligns with your development style. Whether you prefer the robust features of Cursive, the customizability of Emacs, or the modern interface of VSCode, integrating the REPL will undoubtedly enhance your Clojure development experience.

## Quiz Time!

{{< quizdown >}}

### Which plugin is used to integrate Clojure with IntelliJ IDEA?

- [x] Cursive
- [ ] CIDER
- [ ] Calva
- [ ] Leiningen

> **Explanation:** Cursive is the plugin used to integrate Clojure with IntelliJ IDEA, providing robust support for Clojure development.

### What command is used to start a REPL session in Emacs with CIDER?

- [ ] M-x package-install
- [x] M-x cider-jack-in
- [ ] M-x start-repl
- [ ] M-x connect-repl

> **Explanation:** `M-x cider-jack-in` is the command used in Emacs with CIDER to start a REPL session.

### How can you evaluate a Clojure expression inline in VSCode with Calva?

- [ ] Use the command palette
- [x] Ctrl + Enter
- [ ] Alt + Enter
- [ ] Shift + Enter

> **Explanation:** In VSCode with Calva, `Ctrl + Enter` is used to evaluate a Clojure expression inline.

### What is the benefit of integrating the REPL with an IDE?

- [x] Inline results and better navigation
- [ ] Slower code execution
- [ ] Increased memory usage
- [ ] Limited code evaluation

> **Explanation:** Integrating the REPL with an IDE provides benefits like inline results and better navigation, enhancing productivity.

### Which keybinding evaluates the entire buffer in Emacs with CIDER?

- [ ] C-x C-e
- [x] C-c C-k
- [ ] C-c C-r
- [ ] C-c C-c

> **Explanation:** `C-c C-k` evaluates the entire buffer in Emacs with CIDER.

### What is the primary purpose of the REPL in Clojure development?

- [x] Interactive programming and testing
- [ ] Compiling code
- [ ] Managing dependencies
- [ ] Formatting code

> **Explanation:** The primary purpose of the REPL in Clojure development is interactive programming and testing.

### Which IDE uses Calva for Clojure integration?

- [ ] IntelliJ IDEA
- [ ] Emacs
- [x] Visual Studio Code
- [ ] Sublime Text

> **Explanation:** Visual Studio Code uses Calva for Clojure integration, providing features like inline evaluation.

### How do you connect to a running REPL server in Cursive?

- [ ] Use the command palette
- [ ] M-x connect-repl
- [x] Create a Remote REPL configuration
- [ ] Use the REPL console

> **Explanation:** In Cursive, you connect to a running REPL server by creating a Remote REPL configuration.

### What is the keybinding for evaluating a region in Emacs with CIDER?

- [ ] C-x C-e
- [ ] C-c C-k
- [x] C-c C-r
- [ ] C-c C-c

> **Explanation:** `C-c C-r` is the keybinding for evaluating a region in Emacs with CIDER.

### True or False: Integrating the REPL with an IDE can lead to faster development cycles.

- [x] True
- [ ] False

> **Explanation:** True. Integrating the REPL with an IDE allows for quick testing and iteration, leading to faster development cycles.

{{< /quizdown >}}
