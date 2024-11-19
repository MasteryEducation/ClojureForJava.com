---
linkTitle: "4.2.1 Creating Tables with Provisioned and On-Demand Capacity Modes"
title: "Creating Tables with Provisioned and On-Demand Capacity Modes in DynamoDB"
description: "Explore the intricacies of creating DynamoDB tables with provisioned and on-demand capacity modes, including step-by-step instructions and best practices for Java and Clojure developers."
categories:
- NoSQL
- Clojure
- DynamoDB
tags:
- DynamoDB
- NoSQL
- Clojure
- AWS
- Capacity Modes
date: 2024-10-25
type: docs
nav_weight: 421000
canonical: "https://clojureforjava.com/5/4/2/1"
license: "© 2024 Tokenizer Inc. CC BY-NC-SA 4.0"
---

## 4.2.1 Creating Tables with Provisioned and On-Demand Capacity Modes

Amazon DynamoDB is a fully managed NoSQL database service that provides fast and predictable performance with seamless scalability. One of the key features of DynamoDB is its flexible capacity modes, which allow you to optimize costs and performance based on your application's workload patterns. In this section, we will delve into the details of creating tables with both provisioned and on-demand capacity modes, providing comprehensive guidance for Java and Clojure developers.

### Understanding Capacity Modes in DynamoDB

Before diving into the technical details, it's crucial to understand the fundamental differences between provisioned throughput and on-demand capacity modes.

#### Provisioned Throughput Mode

Provisioned throughput mode allows you to specify the number of read and write capacity units required for your application. This mode is ideal for applications with predictable traffic patterns, where you can anticipate the workload and allocate resources accordingly. The key characteristics of provisioned throughput mode include:

- **Cost Efficiency:** By allocating a fixed number of capacity units, you can optimize costs for predictable workloads.
- **Predictability:** Ensures consistent performance by reserving the necessary resources.
- **Auto Scaling:** You can enable auto-scaling to automatically adjust capacity based on traffic patterns.

#### On-Demand Capacity Mode

On-demand capacity mode, on the other hand, is designed for applications with unpredictable or variable traffic patterns. This mode automatically scales to accommodate the workload, eliminating the need for manual capacity planning. Key features of on-demand capacity mode include:

- **Flexibility:** Automatically scales to handle any level of request traffic.
- **Simplicity:** No need to specify capacity units, making it easy to manage.
- **Cost:** You pay for the actual read and write requests, which can be more cost-effective for sporadic workloads.

### Creating a DynamoDB Table via AWS Console

Let's start by creating a DynamoDB table using the AWS Management Console. Follow these steps:

1. **Sign in to the AWS Management Console** and open the DynamoDB console at [https://console.aws.amazon.com/dynamodb](https://console.aws.amazon.com/dynamodb).

2. **Click on "Create Table."** This will open the table creation wizard.

3. **Enter the Table Name and Primary Key.** For example, you might create a table named `Orders` with a primary key `OrderId` of type `String`.

4. **Select Capacity Mode:**
   - Choose **Provisioned** if you have predictable traffic and want to specify read and write capacity units.
   - Choose **On-Demand** if your traffic is unpredictable or you prefer automatic scaling.

5. **Configure Additional Settings:**
   - For provisioned mode, specify the read and write capacity units.
   - Optionally, enable auto-scaling for provisioned mode.
   - Configure additional settings such as encryption, tags, and global secondary indexes if needed.

6. **Review and Create:**
   - Review your settings and click **Create** to create the table.

### Creating a DynamoDB Table via AWS CLI

For developers who prefer command-line interfaces, the AWS CLI provides a powerful way to create DynamoDB tables. Here's how you can do it:

1. **Open your terminal** and ensure that the AWS CLI is installed and configured with your credentials.

2. **Create a Table with Provisioned Capacity:**

   ```bash
   aws dynamodb create-table \
       --table-name Orders \
       --attribute-definitions AttributeName=OrderId,AttributeType=S \
       --key-schema AttributeName=OrderId,KeyType=HASH \
       --provisioned-throughput ReadCapacityUnits=5,WriteCapacityUnits=5
   ```

3. **Create a Table with On-Demand Capacity:**

   ```bash
   aws dynamodb create-table \
       --table-name Orders \
       --attribute-definitions AttributeName=OrderId,AttributeType=S \
       --key-schema AttributeName=OrderId,KeyType=HASH \
       --billing-mode PAY_PER_REQUEST
   ```

### Best Practices for Selecting Capacity Modes

Choosing the right capacity mode is crucial for optimizing both performance and cost. Here are some best practices to consider:

- **Analyze Traffic Patterns:** Use historical data to understand your application's traffic patterns. If your workload is predictable, provisioned mode with auto-scaling might be more cost-effective.

- **Start with On-Demand:** For new applications or those with unpredictable workloads, start with on-demand mode. This allows you to gather data on traffic patterns without the risk of under-provisioning.

- **Monitor and Adjust:** Regularly monitor your application's performance and costs. Use AWS CloudWatch to track metrics and adjust capacity modes as needed.

- **Consider Auto Scaling:** If you choose provisioned mode, enable auto-scaling to automatically adjust capacity based on demand, reducing the risk of throttling.

### Switching Between Capacity Modes

There may be scenarios where you need to switch between capacity modes. For example, an application that starts with on-demand mode might switch to provisioned mode as traffic stabilizes. Here's how you can switch modes:

1. **Open the DynamoDB Console** and navigate to the table you want to modify.

2. **Select the "Capacity" tab** and click on "Manage Capacity."

3. **Switch Capacity Mode:**
   - To switch to provisioned mode, specify the desired read and write capacity units.
   - To switch to on-demand mode, select the "On-Demand" option.

4. **Save Changes** to apply the new capacity mode.

### Conclusion

Creating DynamoDB tables with the appropriate capacity mode is a critical step in designing scalable and cost-effective data solutions. By understanding the differences between provisioned and on-demand capacity modes, and following best practices for selecting and switching modes, you can optimize your application's performance and costs.

In the next section, we will explore how to access DynamoDB from Clojure using the Amazonica library, enabling seamless integration with your Clojure applications.

## Quiz Time!

{{< quizdown >}}

### What is the primary advantage of using on-demand capacity mode in DynamoDB?

- [x] It automatically scales to handle any level of request traffic.
- [ ] It requires manual capacity planning.
- [ ] It is always more cost-effective than provisioned mode.
- [ ] It provides fixed performance levels.

> **Explanation:** On-demand capacity mode automatically scales to accommodate workload variations, making it ideal for unpredictable traffic patterns.

### Which AWS CLI command creates a DynamoDB table with provisioned capacity?

- [x] `aws dynamodb create-table --table-name Orders --attribute-definitions AttributeName=OrderId,AttributeType=S --key-schema AttributeName=OrderId,KeyType=HASH --provisioned-throughput ReadCapacityUnits=5,WriteCapacityUnits=5`
- [ ] `aws dynamodb create-table --table-name Orders --attribute-definitions AttributeName=OrderId,AttributeType=S --key-schema AttributeName=OrderId,KeyType=HASH --billing-mode PAY_PER_REQUEST`
- [ ] `aws dynamodb create-table --table-name Orders --billing-mode PROVISIONED`
- [ ] `aws dynamodb create-table --table-name Orders --provisioned-throughput ReadCapacityUnits=5,WriteCapacityUnits=5`

> **Explanation:** The command specifies the table name, attribute definitions, key schema, and provisioned throughput, which are necessary for creating a table with provisioned capacity.

### What is a key consideration when choosing between provisioned and on-demand capacity modes?

- [x] Analyzing traffic patterns to determine predictability.
- [ ] Always starting with provisioned mode.
- [ ] On-demand mode is always cheaper.
- [ ] Provisioned mode is only for large-scale applications.

> **Explanation:** Analyzing traffic patterns helps determine whether your workload is predictable, guiding the choice between provisioned and on-demand modes.

### How can you switch a DynamoDB table from provisioned to on-demand capacity mode?

- [x] Use the DynamoDB console to manage capacity and select the "On-Demand" option.
- [ ] Use AWS CLI to delete and recreate the table.
- [ ] Change the table's primary key.
- [ ] Modify the table's encryption settings.

> **Explanation:** The DynamoDB console allows you to manage capacity settings and switch between capacity modes without recreating the table.

### Which of the following is a benefit of using provisioned throughput mode?

- [x] Cost efficiency for predictable workloads.
- [ ] Automatic scaling without manual intervention.
- [ ] No need to specify capacity units.
- [ ] Pay-per-request billing.

> **Explanation:** Provisioned throughput mode allows you to specify capacity units, optimizing costs for predictable workloads.

### What is the AWS CLI command to create a table with on-demand capacity?

- [x] `aws dynamodb create-table --table-name Orders --attribute-definitions AttributeName=OrderId,AttributeType=S --key-schema AttributeName=OrderId,KeyType=HASH --billing-mode PAY_PER_REQUEST`
- [ ] `aws dynamodb create-table --table-name Orders --attribute-definitions AttributeName=OrderId,AttributeType=S --key-schema AttributeName=OrderId,KeyType=HASH --provisioned-throughput ReadCapacityUnits=5,WriteCapacityUnits=5`
- [ ] `aws dynamodb create-table --table-name Orders --billing-mode PROVISIONED`
- [ ] `aws dynamodb create-table --table-name Orders --billing-mode ON_DEMAND`

> **Explanation:** The command specifies the billing mode as PAY_PER_REQUEST, which is required for creating a table with on-demand capacity.

### What should you do if your application's workload becomes more predictable over time?

- [x] Consider switching from on-demand to provisioned capacity mode.
- [ ] Always keep the application in on-demand mode.
- [ ] Increase the read and write capacity units in on-demand mode.
- [ ] Disable auto-scaling for provisioned mode.

> **Explanation:** If the workload becomes predictable, switching to provisioned mode can optimize costs and performance.

### Which tool can you use to monitor your DynamoDB table's performance and costs?

- [x] AWS CloudWatch
- [ ] AWS Lambda
- [ ] AWS S3
- [ ] AWS EC2

> **Explanation:** AWS CloudWatch provides metrics and logs for monitoring DynamoDB performance and costs.

### True or False: On-demand capacity mode requires you to specify read and write capacity units.

- [ ] True
- [x] False

> **Explanation:** On-demand capacity mode automatically scales without the need to specify capacity units.

### What is a potential drawback of using on-demand capacity mode for high-traffic applications?

- [x] It may be more expensive than provisioned mode for consistently high traffic.
- [ ] It requires manual scaling.
- [ ] It does not support auto-scaling.
- [ ] It limits the number of global secondary indexes.

> **Explanation:** On-demand mode charges per request, which can be more expensive than provisioned mode for applications with consistently high traffic.

{{< /quizdown >}}
