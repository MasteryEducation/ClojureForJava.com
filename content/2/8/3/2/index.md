---
linkTitle: "8.3.2 Automated Test Execution with Leiningen and Boot"
title: "Automated Test Execution with Leiningen and Boot for Clojure Projects"
description: "Explore how to effectively automate test execution in Clojure projects using Leiningen and Boot, including configuration, customization, and integration with CI pipelines."
categories:
- Clojure Development
- Automated Testing
- Continuous Integration
tags:
- Clojure
- Leiningen
- Boot
- Automated Testing
- CI/CD
date: 2024-10-25
type: docs
nav_weight: 832000
canonical: "https://clojureforjava.com/2/8/3/2"
license: "© 2024 Tokenizer Inc. CC BY-NC-SA 4.0"
---

## 8.3.2 Automated Test Execution with Leiningen and Boot

Automated testing is a cornerstone of modern software development, ensuring that code changes do not introduce regressions and that the software behaves as expected. In the Clojure ecosystem, Leiningen and Boot are two primary build tools that facilitate automated test execution. This section delves into how to leverage these tools to run tests efficiently, configure test paths, include or exclude tests based on metadata, and integrate test execution into continuous integration (CI) pipelines.

### Running Tests with Leiningen

Leiningen is a popular build automation tool for Clojure that simplifies project management, including running tests. The `lein test` command is the primary way to execute tests in a Leiningen-managed project.

#### Configuring Test Paths in `project.clj`

By default, Leiningen expects test files to reside in the `test` directory of your project. However, you can customize this behavior by specifying test paths in your `project.clj` file. Here's an example configuration:

```clojure
(defproject my-clojure-project "0.1.0-SNAPSHOT"
  :description "A sample Clojure project"
  :dependencies [[org.clojure/clojure "1.10.3"]]
  :test-paths ["test" "custom-test-dir"])
```

In this configuration, Leiningen will look for test files in both the `test` and `custom-test-dir` directories.

#### Running Tests with `lein test`

To execute tests, simply run the following command in your terminal:

```bash
lein test
```

This command will automatically discover and run all test namespaces in the specified test paths. Leiningen uses the `clojure.test` framework by default, which is included in the Clojure standard library.

#### Including or Excluding Tests Using Metadata and Selectors

Leiningen allows you to include or exclude tests based on metadata. This is useful for running a subset of tests, such as integration tests or tests marked as slow. You can add metadata to your tests using the `:test` metadata key:

```clojure
(ns my-clojure-project.core-test
  (:require [clojure.test :refer :all]))

(deftest ^:integration test-integration-feature
  (is (= 1 1)))

(deftest ^:unit test-unit-feature
  (is (= 2 2)))
```

To run only integration tests, use the `:only` option with `lein test`:

```bash
lein test :only :integration
```

Conversely, to exclude integration tests, use the `:exclude` option:

```bash
lein test :exclude :integration
```

### Running Tests with Boot

Boot is another powerful build tool for Clojure that offers a flexible pipeline architecture. Running tests in Boot involves using the `test` task, which can be customized to suit your needs.

#### Using the `test` Task

To run tests in a Boot project, you first need to include the `boot-test` dependency in your `build.boot` file:

```clojure
(set-env!
  :dependencies '[[org.clojure/clojure "1.10.3"]
                  [adzerk/boot-test "2.0.0"]])

(require '[adzerk.boot-test :refer [test]])

(deftask run-tests []
  (comp (test)))
```

With this setup, you can execute tests by running the following command:

```bash
boot run-tests
```

#### Customizing Test Runners

Boot allows you to customize test runners by specifying options in the `test` task. For example, you can run tests in parallel or specify a custom test reporter:

```clojure
(deftask run-tests []
  (comp (test :parallel true :reporter :junit)))
```

This configuration runs tests in parallel and uses the JUnit reporter for output.

### Integrating Test Execution into Build Scripts and CI Pipelines

Automated test execution is a critical component of continuous integration (CI) pipelines. Both Leiningen and Boot can be integrated into CI systems like Jenkins, Travis CI, and GitHub Actions.

#### Example: Integrating Leiningen with GitHub Actions

Here's a simple example of a GitHub Actions workflow that runs tests using Leiningen:

```yaml
name: Clojure CI

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v2
    - name: Set up JDK 11
      uses: actions/setup-java@v1
      with:
        java-version: '11'
    - name: Install Leiningen
      run: |
        curl https://raw.githubusercontent.com/technomancy/leiningen/stable/bin/lein > ~/bin/lein
        chmod +x ~/bin/lein
    - name: Run tests
      run: lein test
```

This workflow triggers on every push and pull request, ensuring that tests are run automatically.

#### Example: Integrating Boot with Jenkins

To integrate Boot with Jenkins, you can create a Jenkins pipeline script that includes a step to run Boot tests:

```groovy
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build and Test') {
            steps {
                sh 'boot run-tests'
            }
        }
    }
}
```

### Benefits of Continuous Testing During Development

Continuous testing provides several advantages:

- **Immediate Feedback:** Developers receive immediate feedback on code changes, allowing them to address issues quickly.
- **Increased Confidence:** Automated tests increase confidence in the codebase, reducing the likelihood of regressions.
- **Improved Code Quality:** Regular testing encourages better code practices and design.
- **Facilitates Collaboration:** Automated tests make it easier for teams to collaborate, as everyone can verify that changes do not break existing functionality.

### Conclusion

Automated test execution is an essential practice for maintaining robust and reliable Clojure applications. By leveraging Leiningen and Boot, developers can configure and run tests efficiently, integrate testing into CI pipelines, and enjoy the benefits of continuous testing. Whether you are working on a small project or a large enterprise application, these tools provide the flexibility and power needed to ensure your code meets the highest quality standards.

## Quiz Time!

{{< quizdown >}}

### What is the primary command to run tests in a Leiningen-managed project?

- [x] `lein test`
- [ ] `lein run`
- [ ] `lein build`
- [ ] `lein compile`

> **Explanation:** The `lein test` command is used to execute tests in a Leiningen-managed project.

### How can you specify custom test paths in a Leiningen project?

- [x] By adding `:test-paths` in `project.clj`
- [ ] By creating a `test-paths.edn` file
- [ ] By using a command-line option
- [ ] By modifying the `src` directory

> **Explanation:** Custom test paths can be specified in the `project.clj` file using the `:test-paths` key.

### What metadata key is used to categorize tests in Clojure?

- [x] `:test`
- [ ] `:category`
- [ ] `:type`
- [ ] `:group`

> **Explanation:** The `:test` metadata key is used to categorize tests in Clojure.

### Which Boot task is used to run tests?

- [x] `test`
- [ ] `build`
- [ ] `compile`
- [ ] `run`

> **Explanation:** The `test` task in Boot is used to execute tests.

### How can you run tests in parallel using Boot?

- [x] By setting the `:parallel` option to `true` in the `test` task
- [ ] By using a separate tool for parallel execution
- [ ] By modifying the `build.boot` file to include parallel code
- [ ] By running multiple Boot processes

> **Explanation:** The `:parallel` option in the `test` task allows tests to be run in parallel in Boot.

### What is a benefit of continuous testing?

- [x] Immediate feedback on code changes
- [ ] Increased build times
- [ ] Reduced code quality
- [ ] Less collaboration

> **Explanation:** Continuous testing provides immediate feedback on code changes, which is a significant benefit.

### Which CI tool is demonstrated for integrating Leiningen test execution?

- [x] GitHub Actions
- [ ] Jenkins
- [ ] Travis CI
- [ ] CircleCI

> **Explanation:** The example provided demonstrates integrating Leiningen with GitHub Actions.

### How do you exclude tests with specific metadata in Leiningen?

- [x] Using the `:exclude` option with `lein test`
- [ ] By deleting the test files
- [ ] By commenting out the test code
- [ ] By modifying the `project.clj` file

> **Explanation:** Tests can be excluded using the `:exclude` option with `lein test`.

### What is the purpose of the `boot-test` dependency in Boot?

- [x] To enable running tests
- [ ] To compile Clojure code
- [ ] To manage dependencies
- [ ] To build Docker images

> **Explanation:** The `boot-test` dependency is required to enable running tests in Boot.

### Continuous testing helps improve which aspect of software development?

- [x] Code quality
- [ ] Code obfuscation
- [ ] Code duplication
- [ ] Code deletion

> **Explanation:** Continuous testing helps improve code quality by ensuring that changes do not introduce regressions.

{{< /quizdown >}}
