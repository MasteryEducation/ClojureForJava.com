---
linkTitle: "2.2.1 Installing MongoDB on Different Platforms"
title: "Installing MongoDB on Different Platforms: Windows, macOS, and Linux"
description: "Comprehensive guide to installing MongoDB on Windows, macOS, and Linux, with detailed steps for setting up as a service and manual operation, and verification using the mongo shell."
categories:
- Database
- Installation
- NoSQL
tags:
- MongoDB
- Installation Guide
- Windows
- macOS
- Linux
date: 2024-10-25
type: docs
nav_weight: 221000
canonical: "https://clojureforjava.com/5/2/2/1"
license: "© 2024 Tokenizer Inc. CC BY-NC-SA 4.0"
---

## 2.2.1 Installing MongoDB on Different Platforms

MongoDB, a popular NoSQL database, is known for its flexibility, scalability, and ease of use. As a Java developer venturing into Clojure and NoSQL, understanding how to install MongoDB across different platforms is crucial. This section provides a comprehensive guide to installing MongoDB on Windows, macOS, and Linux. We'll also cover how to set up MongoDB as a service or run it manually, and verify the installation by connecting to MongoDB using the mongo shell.

### Installing MongoDB on Windows

#### Step 1: Download MongoDB

1. **Visit the MongoDB Download Center**: Go to the [MongoDB Download Center](https://www.mongodb.com/try/download/community) and select the Windows version.
2. **Choose the Version**: Select the latest stable release. Ensure you choose the correct version for your system architecture (x64).
3. **Download the Installer**: Click on the download button to get the `.msi` installer package.

#### Step 2: Install MongoDB

1. **Run the Installer**: Double-click the downloaded `.msi` file to start the installation process.
2. **Follow the Setup Wizard**:
   - **Setup Type**: Choose "Complete" for a full installation.
   - **Service Configuration**: Opt to install MongoDB as a service. This allows MongoDB to start automatically with your system. You can also specify the service name and data/log directories.
   - **Install MongoDB Compass**: This is optional but recommended for a GUI interface to interact with MongoDB.

#### Step 3: Configure Environment Variables

1. **Add MongoDB to PATH**: 
   - Open the System Properties (Right-click on 'This PC' -> Properties -> Advanced system settings).
   - Click on 'Environment Variables'.
   - Under 'System variables', find the 'Path' variable and click 'Edit'.
   - Add the path to the MongoDB `bin` directory (e.g., `C:\Program Files\MongoDB\Server\6.0\bin`).

#### Step 4: Verify the Installation

1. **Open Command Prompt**: Press `Win + R`, type `cmd`, and press Enter.
2. **Start MongoDB**: If installed as a service, it should start automatically. Otherwise, run `mongod` to start the MongoDB server.
3. **Connect using mongo shell**: Type `mongo` in the command prompt to connect to the MongoDB server. You should see a prompt indicating a successful connection.

### Installing MongoDB on macOS

#### Step 1: Install Homebrew

1. **Open Terminal**: You can find Terminal in Applications > Utilities.
2. **Install Homebrew**: If you don't have Homebrew installed, run the following command:
   ```bash
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```

#### Step 2: Install MongoDB

1. **Tap the MongoDB Formula**: Run the following command to add the MongoDB tap:
   ```bash
   brew tap mongodb/brew
   ```
2. **Install MongoDB**: Execute the following command to install MongoDB:
   ```bash
   brew install mongodb-community
   ```

#### Step 3: Run MongoDB

1. **Start MongoDB as a Service**: Use Homebrew to start MongoDB as a service:
   ```bash
   brew services start mongodb/brew/mongodb-community
   ```
2. **Run MongoDB Manually**: Alternatively, you can run MongoDB manually by executing:
   ```bash
   mongod --config /usr/local/etc/mongod.conf
   ```

#### Step 4: Verify the Installation

1. **Connect using mongo shell**: Open a new terminal window and type `mongo` to connect to the MongoDB server. You should see a prompt indicating a successful connection.

### Installing MongoDB on Linux

#### Step 1: Import the MongoDB Public Key

1. **Open Terminal**: Use the terminal application on your Linux distribution.
2. **Import the Key**: Run the following command to import the MongoDB public GPG key:
   ```bash
   wget -qO - https://www.mongodb.org/static/pgp/server-6.0.asc | sudo apt-key add -
   ```

#### Step 2: Create a List File for MongoDB

1. **Create the List File**: Use the following command to create a list file for MongoDB:
   ```bash
   echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/6.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-6.0.list
   ```

#### Step 3: Install MongoDB Packages

1. **Update Package Database**: Run the following command to update the local package database:
   ```bash
   sudo apt-get update
   ```
2. **Install MongoDB**: Execute the following command to install MongoDB:
   ```bash
   sudo apt-get install -y mongodb-org
   ```

#### Step 4: Start MongoDB

1. **Start MongoDB as a Service**: Use the following command to start MongoDB as a service:
   ```bash
   sudo systemctl start mongod
   ```
2. **Enable MongoDB to Start on Boot**: Run the following command to enable MongoDB to start on boot:
   ```bash
   sudo systemctl enable mongod
   ```

#### Step 5: Verify the Installation

1. **Check the Service Status**: Use the following command to check the status of the MongoDB service:
   ```bash
   sudo systemctl status mongod
   ```
   Ensure that the service is active and running.
2. **Connect using mongo shell**: Type `mongo` in the terminal to connect to the MongoDB server. You should see a prompt indicating a successful connection.

### Setting Up MongoDB as a Service

Setting up MongoDB as a service ensures that it starts automatically with your system, providing a seamless experience for development and production environments.

#### Windows

- During installation, choose the option to install MongoDB as a service.
- Use the `services.msc` utility to manage the MongoDB service.

#### macOS

- Use Homebrew services to manage MongoDB as a service with `brew services start mongodb/brew/mongodb-community`.

#### Linux

- Use `systemctl` to manage MongoDB as a service with `sudo systemctl enable mongod`.

### Running MongoDB Manually

Running MongoDB manually is useful for development environments or when you need more control over the MongoDB process.

#### Windows

- Open a command prompt and navigate to the MongoDB `bin` directory.
- Run `mongod` to start the MongoDB server.

#### macOS

- Use the terminal to run `mongod --config /usr/local/etc/mongod.conf`.

#### Linux

- Use the terminal to run `mongod` with the appropriate configuration file.

### Verifying the Installation

After installing MongoDB, it's important to verify that the installation was successful and that you can connect to the MongoDB server.

1. **Open the Mongo Shell**: Use the `mongo` command to open the MongoDB shell.
2. **Check the Connection**: Ensure that you see a prompt indicating a successful connection to the MongoDB server.
3. **Run Basic Commands**: Test the connection by running basic commands such as `show dbs` to list databases.

### Common Pitfalls and Troubleshooting

- **Port Conflicts**: Ensure that port 27017 is not being used by another application.
- **Firewall Settings**: Check firewall settings to ensure MongoDB can accept connections.
- **Service Permissions**: Ensure the MongoDB service has the necessary permissions to access data directories.

### Best Practices

- **Regular Updates**: Keep MongoDB updated to the latest stable version for security and performance improvements.
- **Backup and Restore**: Regularly backup your databases and test restore procedures.
- **Security Configurations**: Implement security best practices such as enabling authentication and using SSL/TLS for connections.

By following these detailed steps, you can successfully install MongoDB on Windows, macOS, and Linux, set it up as a service or run it manually, and verify the installation using the mongo shell. This foundational setup will enable you to leverage MongoDB's capabilities in your Clojure and NoSQL projects.

## Quiz Time!

{{< quizdown >}}

### Which command is used to start MongoDB as a service on macOS using Homebrew?

- [ ] mongod --config /usr/local/etc/mongod.conf
- [x] brew services start mongodb/brew/mongodb-community
- [ ] sudo systemctl start mongod
- [ ] mongo

> **Explanation:** The correct command to start MongoDB as a service on macOS using Homebrew is `brew services start mongodb/brew/mongodb-community`.

### What is the default port number for MongoDB?

- [x] 27017
- [ ] 8080
- [ ] 3306
- [ ] 5432

> **Explanation:** MongoDB uses port 27017 by default for connections.

### How can you verify the MongoDB installation on Windows?

- [x] By running the `mongo` command in the command prompt
- [ ] By checking the MongoDB Compass
- [ ] By opening the MongoDB website
- [ ] By running the `mongod` command

> **Explanation:** To verify the MongoDB installation, you can use the `mongo` command in the command prompt to connect to the MongoDB server.

### What is the purpose of the MongoDB public GPG key in Linux installation?

- [x] To verify the authenticity of the MongoDB packages
- [ ] To encrypt the MongoDB data
- [ ] To configure MongoDB services
- [ ] To set up MongoDB as a service

> **Explanation:** The MongoDB public GPG key is used to verify the authenticity of the MongoDB packages during installation.

### Which command is used to enable MongoDB to start on boot in Linux?

- [ ] sudo apt-get install -y mongodb-org
- [ ] mongod --config /usr/local/etc/mongod.conf
- [x] sudo systemctl enable mongod
- [ ] brew services start mongodb/brew/mongodb-community

> **Explanation:** The command `sudo systemctl enable mongod` is used to enable MongoDB to start on boot in Linux.

### What should you do if port 27017 is already in use during MongoDB installation?

- [x] Change the MongoDB port in the configuration file
- [ ] Uninstall MongoDB
- [ ] Restart the computer
- [ ] Disable the firewall

> **Explanation:** If port 27017 is already in use, you should change the MongoDB port in the configuration file to avoid conflicts.

### How can you add MongoDB to the PATH environment variable on Windows?

- [x] By editing the 'Path' variable in the System Properties
- [ ] By reinstalling MongoDB
- [ ] By running the `mongod` command
- [ ] By using the MongoDB Compass

> **Explanation:** You can add MongoDB to the PATH environment variable by editing the 'Path' variable in the System Properties on Windows.

### Which tool is recommended for a GUI interface to interact with MongoDB?

- [x] MongoDB Compass
- [ ] MongoDB Shell
- [ ] MongoDB CLI
- [ ] MongoDB Studio

> **Explanation:** MongoDB Compass is recommended for a GUI interface to interact with MongoDB.

### What is the command to install MongoDB on macOS using Homebrew?

- [ ] brew install mongodb
- [x] brew install mongodb-community
- [ ] sudo apt-get install mongodb
- [ ] brew tap mongodb/brew

> **Explanation:** The command to install MongoDB on macOS using Homebrew is `brew install mongodb-community`.

### True or False: MongoDB can only be installed as a service on Windows.

- [ ] True
- [x] False

> **Explanation:** False. MongoDB can be installed as a service on Windows, macOS, and Linux, but it can also be run manually on all these platforms.

{{< /quizdown >}}
