## Question #: 01

**Question:**  
A company is designing the network for an online multi-player game. The game uses the UDP networking protocol and will be deployed in eight AWS Regions. The network architecture needs to minimize latency and packet loss to give end users a high-quality gaming experience.

**What solution will meet these requirements?**

**A.** Set up a transit gateway in each Region. Create inter-Region peering attachments between each transit gateway.  
**B.** Set up AWS Global Accelerator with UDP listeners and endpoint groups in each Region.  
**C.** Set up Amazon CloudFront with UDP turned on. Configure an origin in each Region.  
**D.** Set up a VPC peering mesh between each Region. Turn on UDP for each VPC.

---
<details>
<summary><strong>✅ Check Answer</strong></summary>

### ✅ Correct Answer: **B. Set up AWS Global Accelerator with UDP listeners and endpoint groups in each Region.**

---

### 📘 Explanation:

AWS **Global Accelerator** is specifically designed for applications that require **low latency**, **minimal packet loss**, and **high availability** — exactly what online multiplayer games demand. It uses the **AWS global network infrastructure**, allowing user requests to enter the AWS backbone at the nearest edge location and travel over the optimized network path.

#### Benefits of Global Accelerator:
- Supports **UDP** traffic (critical for real-time gaming).
- Automatically routes traffic to the **nearest healthy endpoint** in the designated Region.
- Provides **regional failover**, improving fault tolerance.
- Minimizes **internet hops**, improving performance compared to standard public internet routing.

---

### 🔗 References:

- AWS Global Accelerator official documentation:  
  https://docs.aws.amazon.com/global-accelerator/latest/dg/introduction-what-is-global-accelerator.html

- Related discussion on ExamTopics:  
  https://www.examtopics.com/discussions/amazon/view/100130-exam-aws-certified-solutions-architect-associate-saa-c03/  

</details>

## Question #: 02

**Question:**  
A company hosts a serverless application on AWS. The application uses Amazon API Gateway, AWS Lambda, and an Amazon RDS for PostgreSQL database. The company notices an increase in application errors that result from database connection timeouts during times of peak traffic or unpredictable traffic. The company needs a solution that reduces the application failures with the least amount of change to the code.

**What should a solutions architect do to meet these requirements?**

**A.** Reduce the Lambda concurrency rate.  
**B.** Enable RDS Proxy on the RDS DB instance.  
**C.** Resize the RDS DB instance class to accept more connections.  
**D.** Migrate the database to Amazon DynamoDB with on-demand scaling.

---
<details>
<summary><strong>✅ Check Answer</strong></summary>

### ✅ Correct Answer: **B. Enable RDS Proxy on the RDS DB instance.**

---

### 📘 Explanation:

When using AWS Lambda with Amazon RDS, a common challenge is **managing database connections**, especially during **traffic spikes**. Each Lambda invocation can potentially open a new database connection, quickly exhausting the connection pool of the RDS instance.

#### ✅ Why RDS Proxy is the best choice:
- **Manages and pools connections** efficiently.
- Helps avoid **connection exhaustion** during high concurrency.
- Requires **minimal code changes** (in most cases, just updating connection settings).
- **Improves database scalability and resilience** for serverless apps.

#### 🚫 Why not the others?
- **A. Reduce Lambda concurrency rate** – Might limit scalability and won't solve the root problem.
- **C. Resize RDS instance** – Helps temporarily but doesn't solve connection storming from Lambda.
- **D. Migrate to DynamoDB** – A large change in architecture; not minimal or quick.

---

### 🔗 References:

- AWS Docs – [Using Amazon RDS Proxy with AWS Lambda](https://docs.aws.amazon.com/lambda/latest/dg/services-rds.html)  
- AWS Docs – [Amazon RDS Proxy](https://docs.aws.amazon.com/rds/latest/UserGuide/rds-proxy.html)  
- ExamTopics Discussions - (https://www.examtopics.com/discussions/amazon/view/83199-exam-aws-certified-solutions-architect-associate-saa-c02/)


</details>

## Question #: 03

**Question:**  
A company has a Java application that uses Amazon Simple Queue Service (Amazon SQS) to parse messages. The application cannot parse messages that are larger than 256 KB in size. The company wants to implement a solution to give the application the ability to parse messages as large as 50 MB.

**Which solution will meet these requirements with the FEWEST changes to the code?**

**A.** Use the Amazon SQS Extended Client Library for Java to host messages that are larger than 256 KB in Amazon S3.  
**B.** Use Amazon EventBridge to post large messages from the application instead of Amazon SQS.  
**C.** Change the limit in Amazon SQS to handle messages that are larger than 256 KB.  
**D.** Store messages that are larger than 256 KB in Amazon Elastic File System (Amazon EFS). Configure Amazon SQS to reference this location in the messages.

---
<details>
<summary><strong>✅ Check Answer</strong></summary>

### ✅ Correct Answer: **A. Use the Amazon SQS Extended Client Library for Java to host messages that are larger than 256 KB in Amazon S3.**

---

### 📘 Explanation:

Amazon SQS has a **hard limit of 256 KB** for message size. If your application needs to send **larger messages (up to 2 GB)**, you must store the message payload **externally** and send a reference to it via SQS.

#### ✅ Why Option A is Correct:
- AWS provides the **Amazon SQS Extended Client Library for Java**, which seamlessly stores large message payloads in **Amazon S3**, and sends a pointer (reference) through SQS.
- This **minimizes code changes** and integrates smoothly into existing SQS-based Java applications.
- Allows messages up to **2 GB** in size (well above the 50 MB needed).

#### 🚫 Why not the others?
- **B. EventBridge** is not designed for large message payloads (limit is 256 KB as well).
- **C.** You **cannot change the 256 KB limit** on SQS — it’s a hard service limit.
- **D.** Amazon SQS cannot directly reference Amazon EFS files in its message body — this would require **custom logic** and **significant code changes**.

---

### 🔗 References:

- AWS Docs – [Amazon SQS Extended Client Library for Java](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-s3-messages.html)  
- ExamTopics Discussion - (https://www.examtopics.com/discussions/amazon/view/100202-exam-aws-certified-solutions-architect-associate-saa-c03/)

</details>

## Question #: 04

**Question:**  
A transaction processing company has weekly scripted batch jobs that run on Amazon EC2 instances. The EC2 instances are in an Auto Scaling group. The number of transactions can vary, but the baseline CPU utilization that is noted on each run is at least 60%. The company needs to provision the capacity 30 minutes before the jobs run.

Currently, engineers complete this task by manually modifying the Auto Scaling group parameters. The company does not have the resources to analyze the required capacity trends for the Auto Scaling group counts. The company needs an automated way to modify the Auto Scaling group’s desired capacity.

**Which solution will meet these requirements with the LEAST operational overhead?**

**A.** Create a dynamic scaling policy for the Auto Scaling group. Configure the policy to scale based on the CPU utilization metric. Set the target value for the metric to 60%.  
**B.** Create a scheduled scaling policy for the Auto Scaling group. Set the appropriate desired capacity, minimum capacity, and maximum capacity. Set the recurrence to weekly. Set the start time to 30 minutes before the batch jobs run.  
**C.** Create a predictive scaling policy for the Auto Scaling group. Configure the policy to scale based on forecast. Set the scaling metric to CPU utilization. Set the target value for the metric to 60%. In the policy, set the instances to pre-launch 30 minutes before the jobs run.  
**D.** Create an Amazon EventBridge event to invoke an AWS Lambda function when the CPU utilization metric value for the Auto Scaling group reaches 60%. Configure the Lambda function to increase the Auto Scaling group’s desired capacity and maximum capacity by 20%.

---

<details>
<summary><strong>✅ Check Answer</strong></summary>

---

### ✅ Correct Answer: **C. Create a predictive scaling policy for the Auto Scaling group. Configure the policy to scale based on forecast. Set the scaling metric to CPU utilization. Set the target value for the metric to 60%. In the policy, set the instances to pre-launch 30 minutes before the jobs run.**

---

### 📘 Explanation:

**Predictive scaling** in EC2 Auto Scaling uses machine learning to forecast future traffic trends and automatically adjusts capacity ahead of time. Since the batch jobs are **weekly and follow a consistent pattern**, predictive scaling is **ideal** because it can pre-launch instances **30 minutes before the jobs start**, without manual intervention or needing additional resources to analyze trends.

#### ✅ Why Option C is Correct:
- Predictive scaling is designed to detect patterns and launch instances in advance, minimizing latency or startup lag.
- Minimal operational overhead — no manual intervention is required once it's configured.
- Supports the use case where usage trends (like scheduled jobs) are predictable and repetitive.

#### 🚫 Why not the others?
- **A.** Dynamic scaling only reacts to real-time metrics and does not pre-launch instances.
- **B.** Scheduled scaling requires manual updates and is slightly less efficient than predictive.
- **D.** EventBridge + Lambda adds unnecessary complexity and overhead.

---

### 🔗 References:

- AWS Docs – [Predictive Scaling for EC2 Auto Scaling](https://docs.aws.amazon.com/autoscaling/ec2/userguide/ec2-auto-scaling-predictive-scaling.html)  
- ExamTopics Discussion - (https://www.examtopics.com/discussions/amazon/view/100204-exam-aws-certified-solutions-architect-associate-saa-c03/)


</details>

## Question #: 05

**Question:**  
A company is migrating an old application to AWS. The application runs a batch job every hour and is CPU intensive. The batch job takes 15 minutes on average with an on-premises server. The server has 64 virtual CPU (vCPU) and 512 GiB of memory.

**Which solution will run the batch job within 15 minutes with the LEAST operational overhead?**

**A.** Use AWS Lambda with functional scaling.  
**B.** Use Amazon Elastic Container Service (Amazon ECS) with AWS Fargate.  
**C.** Use Amazon Lightsail with AWS Auto Scaling.  
**D.** Use AWS Batch on Amazon EC2.

---

<details>
<summary><strong>✅ Check Answer</strong></summary>

---

### ✅ Correct Answer: **D. Use AWS Batch on Amazon EC2**

---

### 📘 Explanation:

#### ✅ Why Option D is Correct:
- **AWS Batch** is purpose-built for **batch processing** workloads.
- It supports high-performance EC2 instances (such as those with **64 vCPUs and 512 GiB RAM**), ensuring the job completes within 15 minutes as required.
- **Automatically provisions** and **scales compute resources**, reducing operational overhead.
- AWS Batch handles job queues, retry logic, scheduling, and execution — giving a **fully managed batch computing experience**.

#### 🚫 Why not the others?

- **A.** AWS Lambda is not suitable for **long-running CPU-intensive tasks**. It has a **maximum timeout of 15 minutes** and cannot support high resource requirements like 64 vCPUs or 512 GiB RAM.
- **B.** ECS with **Fargate** is serverless, but Fargate currently supports **only up to 4 vCPUs and 30 GiB RAM per task**, which is insufficient for this job.
- **C.** Amazon Lightsail is designed for simple workloads. It lacks the **customizability and scale** needed for CPU-intensive jobs of this magnitude.

---

### 🔗 References:

- AWS Docs – [AWS Batch Overview](https://docs.aws.amazon.com/batch/latest/userguide/what-is-batch.html)  
- AWS Compute Blog – [Choosing AWS Batch vs. Lambda for Compute Tasks](https://aws.amazon.com/blogs/compute/)

</details>


## Question #: 06

**Question:**  
A gaming company is moving its public scoreboard from a data center to the AWS Cloud. The company uses Amazon EC2 Windows Server instances behind an Application Load Balancer to host its dynamic application. The company needs a highly available storage solution for the application. The application consists of static files and dynamic server-side code.

**Which combination of steps should a solutions architect take to meet these requirements? (Choose two.)**

**A.** Store the static files on Amazon S3. Use Amazon CloudFront to cache objects at the edge.  
**B.** Store the static files on Amazon S3. Use Amazon ElastiCache to cache objects at the edge.  
**C.** Store the server-side code on Amazon Elastic File System (Amazon EFS). Mount the EFS volume on each EC2 instance to share the files.  
**D.** Store the server-side code on Amazon FSx for Windows File Server. Mount the FSx for Windows File Server volume on each EC2 instance to share the files.  
**E.** Store the server-side code on a General Purpose SSD (gp2) Amazon Elastic Block Store (Amazon EBS) volume. Mount the EBS volume on each EC2 instance to share the files.

---

<details>
<summary><strong>✅ Check Answer</strong></summary>

---

### ✅ Correct Answers:  
**A.** Store the static files on Amazon S3. Use Amazon CloudFront to cache objects at the edge.  
**D.** Store the server-side code on Amazon FSx for Windows File Server. Mount the FSx for Windows File Server volume on each EC2 instance to share the files.

---

### 📘 Explanation:

#### ✅ Why A is Correct:
- **Amazon S3** is ideal for hosting static content (HTML, CSS, JS, images).
- **Amazon CloudFront** is a content delivery network (CDN) that caches S3 content at edge locations, reducing latency and improving availability.

#### ✅ Why D is Correct:
- **Amazon FSx for Windows File Server** is a fully managed Windows-compatible file system, perfect for Windows EC2 instances.
- It supports Windows file sharing protocols like SMB and integrates well for server-side shared code needs.
- Highly available and scalable.

#### 🚫 Why not the others?

- **B.** Amazon ElastiCache is used for **in-memory caching** of frequently accessed data, not static files.
- **C.** Amazon EFS is a Linux-based solution, not ideal for **Windows EC2 instances**.
- **E.** Amazon EBS volumes **cannot be shared** across multiple EC2 instances, which defeats the purpose of sharing server-side code.

---

### 🔗 References:

- AWS Docs – [Amazon S3 with CloudFront](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/DownloadDistS3AndCustomOrigin.html)  
- AWS Docs – [Amazon FSx for Windows File Server](https://docs.aws.amazon.com/fsx/latest/WindowsGuide/what-is.html)

</details>

## Question #: 07

**Question:**  
A social media company runs its application on Amazon EC2 instances behind an Application Load Balancer (ALB). The ALB is the origin for an Amazon CloudFront distribution. The application has more than a billion images stored in an Amazon S3 bucket and processes thousands of images each second. The company wants to resize the images dynamically and serve appropriate formats to clients.

**Which solution will meet these requirements with the LEAST operational overhead?**

**A.** Install an external image management library on an EC2 instance. Use the image management library to process the images.  
**B.** Create a CloudFront origin request policy. Use the policy to automatically resize images and to serve the appropriate format based on the User-Agent HTTP header in the request.  
**C.** Use a Lambda@Edge function with an external image management library. Associate the Lambda@Edge function with the CloudFront behaviors that serve the images.  
**D.** Create a CloudFront response headers policy. Use the policy to automatically resize images and to serve the appropriate format based on the User-Agent HTTP header in the request.

---

<details>
<summary><strong>✅ Check Answer</strong></summary>

---

### ✅ Correct Answer:  
**C. Use a Lambda@Edge function with an external image management library. Associate the Lambda@Edge function with the CloudFront behaviors that serve the images.**

---

### 📘 Explanation:

#### ✅ Why C is Correct:
- **Lambda@Edge** allows running functions at AWS edge locations, enabling on-the-fly image manipulation (resize, reformat) close to users.
- This offloads the compute from your backend (EC2 or ALB) and **reduces latency** while improving scalability and operational simplicity.
- Many solutions (like AWS's [Serverless Image Handler](https://github.com/awslabs/serverless-image-handler)) use this approach.
- It **minimizes operational overhead** as you don’t need to manage EC2 instances or additional infrastructure.

#### 🚫 Why not the others?

- **A.** Installing image libraries on EC2 adds significant **operational overhead** — you’ll manage scaling, patching, and monitoring yourself.
- **B.** CloudFront **origin request policies** control what headers/cookies/query strings are forwarded — they **do not perform image resizing**.
- **D.** **Response headers policies** are used to set cache control, security headers, etc., and do **not support dynamic image manipulation**.

---

### 🔗 References:

- AWS – [Serverless Image Handler](https://github.com/awslabs/serverless-image-handler)  
- AWS Docs – [Lambda@Edge](https://docs.aws.amazon.com/lambda/latest/dg)
- ExamTopics Discussion - (https://www.examtopics.com/discussions/amazon/view/100231-exam-aws-certified-solutions-architect-associate-saa-c03/)
</details>

## Question #: 08

**Question:**  
A solutions architect is designing a company’s disaster recovery (DR) architecture. The company has a MySQL database that runs on an Amazon EC2 instance in a private subnet with scheduled backup. The DR design needs to include multiple AWS Regions.

**Which solution will meet these requirements with the LEAST operational overhead?**

**A.** Migrate the MySQL database to multiple EC2 instances. Configure a standby EC2 instance in the DR Region. Turn on replication.  
**B.** Migrate the MySQL database to Amazon RDS. Use a Multi-AZ deployment. Turn on read replication for the primary DB instance in the different Availability Zones.  
**C.** Migrate the MySQL database to an Amazon Aurora global database. Host the primary DB cluster in the primary Region. Host the secondary DB cluster in the DR Region.  
**D.** Store the scheduled backup of the MySQL database in an Amazon S3 bucket that is configured for S3 Cross-Region Replication (CRR). Use the data backup to restore the database in the DR Region.

---

<details>
<summary><strong>✅ Check Answer</strong></summary>

---

### ✅ Correct Answer:  
**C. Migrate the MySQL database to an Amazon Aurora global database. Host the primary DB cluster in the primary Region. Host the secondary DB cluster in the DR Region.**

---

### 📘 Explanation:

#### ✅ Why C is Correct:
- **Aurora global databases** are specifically designed for **multi-Region**, low-latency disaster recovery with **minimal operational overhead**.
- AWS handles **replication, failover**, and **synchronization**, reducing the need for manual configuration or maintenance.

#### 🚫 Why the other options are incorrect:

- **A.** Running MySQL on EC2 with manual replication introduces **high operational overhead** and requires **custom scripting and maintenance**.
- **B.** Amazon RDS Multi-AZ deployments are limited to **one Region**. You'd need **cross-Region replication**, which RDS does not support natively for Multi-AZ deployments.
- **D.** CRR-based backup and restore can work, but it is **not real-time** and has **longer RTO**, involving manual **restore steps**, which increases operational overhead.

---

### 🔗 References:
- [Aurora Global Databases](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/aurora-global-database.html)  
- [ExamTopics Discussion](https://www.examtopics.com/discussions/amazon/view/100204-exam-aws-certified-solutions-architect-associate-saa-c03/)

</details>

## Question #: 09

**Question:**
A company wants to migrate an Oracle database to AWS. The database consists of a single table that contains millions of geographic information systems (GIS) images that are high resolution and are identified by a geographic code.

When a natural disaster occurs, tens of thousands of images get updated every few minutes. Each geographic code has a single image or row that is associated with it. The company wants a solution that is highly available and scalable during such events.

**Which solution meets these requirements MOST cost-effectively?**

**A.** Store the images and geographic codes in a database table. Use Oracle running on an Amazon RDS Multi-AZ DB instance.  
**B.** Store the images in Amazon S3 buckets. Use Amazon DynamoDB with the geographic code as the key and the image S3 URL as the value.  
**C.** Store the images and geographic codes in an Amazon DynamoDB table. Configure DynamoDB Accelerator (DAX) during times of high load.  
**D.** Store the images in Amazon S3 buckets. Store geographic codes and image S3 URLs in a database table. Use Oracle running on an Amazon RDS Multi-AZ DB instance.

---

<details>
<summary><strong>✅ Check Answer</strong></summary>

---

### ✅ Correct Answer:  
**B. Store the images in Amazon S3 buckets. Use Amazon DynamoDB with the geographic code as the key and the image S3 URL as the value.**

---

### 📘 Explanation:

#### ✅ Why B is Correct:
- **Amazon S3** provides **cost-effective, durable, and scalable** storage for large image files.
- **Amazon DynamoDB** is **highly scalable**, serverless, and supports **rapid updates** during high-throughput scenarios such as disaster events.
- Storing **S3 URLs** in DynamoDB reduces data duplication and keeps image metadata easily accessible.
- This solution is **fully managed**, cost-effective, and **highly available**.

#### 🚫 Why the other options are incorrect:

- **A.** Using Oracle on RDS Multi-AZ is expensive and does not scale well for massive, frequent image updates.
- **C.** Storing large binary objects (images) directly in DynamoDB is not recommended due to cost and performance concerns.
- **D.** Oracle on RDS still brings operational overhead and doesn't scale or cost-optimize as well as DynamoDB + S3.

---

### 🔗 References:
- [Amazon DynamoDB Best Practices](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/best-practices.html)  
- [Amazon S3 Overview](https://docs.aws.amazon.com/s3/index.html)  
- [DynamoDB vs RDS](https://aws.amazon.com/nosql/dynamodb-vs-rds/)
- [ExamTopics Discussion](https://www.examtopics.com/discussions/amazon/view/102136-exam-aws-certified-solutions-architect-associate-saa-c03/)

</details>

## Question #: 10

**Question:**
A company hosts a frontend application that uses an Amazon API Gateway API backend that is integrated with AWS Lambda. When the API receives requests, the Lambda function loads many libraries. Then the Lambda function connects to an Amazon RDS database, processes the data, and returns the data to the frontend application. The company wants to ensure that response latency is as low as possible for all its users with the fewest number of changes to the company’s operations.

**Which solution will meet these requirements?**

**A.** Establish a connection between the frontend application and the database to make queries faster by bypassing the API.  
**B.** Configure provisioned concurrency for the Lambda function that handles the requests.  
**C.** Cache the results of the queries in Amazon S3 for faster retrieval of similar datasets.  
**D.** Increase the size of the database to increase the number of connections Lambda can establish at one time.

---

<details>
<summary><strong>✅ Check Answer</strong></summary>

---

### ✅ Correct Answer:  
**B. Configure provisioned concurrency for the Lambda function that handles the requests.**

---

### 📘 Explanation:

#### ✅ Why B is Correct:
- **Provisioned Concurrency** keeps Lambda function instances initialized and hyper-ready to respond to requests.
- This removes the **cold start latency** that occurs when a function must load large libraries or initialize connections.
- It’s the most effective way to reduce response time **without changing code** or architecture, which aligns with the requirement of minimal operational change.

#### 🚫 Why the other options are incorrect:

- **A.** Bypassing API Gateway and accessing RDS directly from the frontend breaks security best practices and adds complexity.  
- **C.** Caching results in S3 requires additional logic and does not address latency from Lambda cold starts.  
- **D.** Increasing DB size does not affect Lambda cold start latency, which is the main issue described.

---

### 🔗 References:
- [AWS Lambda – Provisioned Concurrency](https://docs.aws.amazon.com/lambda/latest/dg/configuration-concurrency.html)
- [Optimize AWS Lambda performance with Provisioned Concurrency](https://aws.amazon.com/blogs/compute/new-for-aws-lambda-predictable-start-up-latency-with-provisioned-concurrency/)
- [ExamTopics Discussion](https://www.examtopics.com/discussions/amazon/view/102144-exam-aws-certified-solutions-architect-associate-saa-c03/)


</details>

## Question #: 11

**Question:**  
A company hosts a three-tier web application that includes a PostgreSQL database. The database stores the metadata from documents. The company searches the metadata for key terms to retrieve documents that the company reviews in a report each month. The documents are stored in Amazon S3. The documents are usually written only once, but they are updated frequently.

The reporting process takes a few hours with the use of relational queries. The reporting process must not prevent any document modifications or the addition of new documents. A solutions architect needs to implement a solution to speed up the reporting process.

**Which solution will meet these requirements with the LEAST amount of change to the application code?**

**A.** Set up a new Amazon DocumentDB (with MongoDB compatibility) cluster that includes a read replica. Scale the read replica to generate the reports.  
**B.** Set up a new Amazon Aurora PostgreSQL DB cluster that includes an Aurora Replica. Issue queries to the Aurora Replica to generate the reports.  
**C.** Set up a new Amazon RDS for PostgreSQL Multi-AZ DB instance. Configure the reporting module to query the secondary RDS node so that the reporting module does not affect the primary node.  
**D.** Set up a new Amazon DynamoDB table to store the documents. Use a fixed write capacity to support new document entries. Automatically scale the read capacity to support the reports.

---

<details>
<summary><strong>✅ Check Answer</strong></summary>

---

### ✅ Correct Answer:  
**B. Set up a new Amazon Aurora PostgreSQL DB cluster that includes an Aurora Replica. Issue queries to the Aurora Replica to generate the reports.**

---

### 📘 Explanation:

#### ✅ Why B is Correct:
- Amazon **Aurora PostgreSQL** supports **read replicas**, which can be used to **offload read-heavy operations** such as reporting.
- Aurora Replicas are **synchronously replicated**, providing **low-latency** and **up-to-date** data access without interfering with the primary instance.
- This approach requires **minimal changes to application code**, typically only updating the reporting tool to point to the replica endpoint.

#### 🚫 Why the other options are incorrect:

- **A.** Amazon DocumentDB is **not compatible with PostgreSQL** and would require a **complete data migration and application rewrite**.
- **C.** RDS Multi-AZ is for **high availability**, **not for read scaling**. The standby instance **cannot be used for reads**.
- **D.** DynamoDB is a **NoSQL database**, which is not suitable for relational query processing without **major changes** to the schema and application logic.

---

### 🔗 References:
- [Amazon Aurora Replicas](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/Aurora.Replica.html)  
- [Aurora PostgreSQL](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/aurora-postgresql.html)  
- [RDS Multi-AZ vs Read Replica](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Concepts.MultiAZ.html)
- [ExamTopics Discussion](https://www.examtopics.com/discussions/amazon/view/102147-exam-aws-certified-solutions-architect-associate-saa-c03/)

</details>

## Question #: 12

**Question:**  
An ecommerce company is running a multi-tier application on AWS. The front-end and backend tiers both run on Amazon EC2, and the database runs on Amazon RDS for MySQL. The backend tier communicates with the RDS instance. There are frequent calls to return identical datasets from the database that are causing performance slowdowns.

**Which action should be taken to improve the performance of the backend?**

**A.** Implement Amazon SNS to store the database calls.  
**B.** Implement Amazon ElastiCache to cache the large datasets.  
**C.** Implement an RDS for MySQL read replica to cache database calls.  
**D.** Implement Amazon Kinesis Data Firehose to stream the calls to the database.

---

<details>
<summary><strong>✅ Check Answer</strong></summary>

---

### ✅ Correct Answer:  
**B. Implement Amazon ElastiCache to cache the large datasets.**

---

### 📘 Explanation:

#### ✅ Why B is Correct:
- **Amazon ElastiCache** (Redis or Memcached) is a highly efficient in-memory data store that can cache frequent and repetitive read-heavy queries.
- Caching improves **latency and application performance** by reducing the load on the database.
- This approach is ideal for situations where **identical datasets are repeatedly requested**, as described.

#### 🚫 Why the other options are incorrect:

- **A.** Amazon SNS is a messaging service, not a caching mechanism. It cannot be used to cache or store datasets.
- **C.** Read replicas help with read scalability but **do not cache results**. Each query still hits the database engine.
- **D.** Amazon Kinesis Data Firehose is used for **data streaming and delivery**, not for database querying or caching.

---

### 🔗 References:
- [Amazon ElastiCache Overview](https://docs.aws.amazon.com/elasticache/latest/mem-ug/WhatIs.html)
- [Best Practices for Caching with ElastiCache](https://aws.amazon.com/caching/)
- [ExamTopics Discussion](https://www.examtopics.com/discussions/amazon/view/102154-exam-aws-certified-solutions-architect-associate-saa-c03/)

</details>

## Question #: 13

**Question:**  
A company has a large dataset for its online advertising business stored in an Amazon RDS for MySQL DB instance in a single Availability Zone. The company wants business reporting queries to run without impacting the write operations to the production DB instance.

**Which solution meets these requirements?**

**A.** Deploy RDS read replicas to process the business reporting queries.  
**B.** Scale out the DB instance horizontally by placing it behind an Elastic Load Balancer.  
**C.** Scale up the DB instance to a larger instance type to handle write operations and queries.  
**D.** Deploy the DB instance in multiple Availability Zones to process the business reporting queries.

---

<details>
<summary><strong>✅ Check Answer</strong></summary>

---

### ✅ Correct Answer:  
**A. Deploy RDS read replicas to process the business reporting queries.**

---

### 📘 Explanation:

- Amazon RDS **read replicas** allow you to offload **read-heavy workloads** (like business reporting queries) from the primary database, which handles **write operations**.
- This improves performance and minimizes the impact of long-running queries on transactional workloads.
- Read replicas are **asynchronous** and designed specifically to support this use case.

**Why the other options are incorrect:**

- **B.** RDS does not support horizontal scaling through an Elastic Load Balancer like EC2. RDS cannot be placed behind an ELB.
- **C.** Scaling vertically (upgrading instance type) might help, but it doesn't separate read and write workloads and can still lead to contention.
- **D.** Multi-AZ deployments improve **availability and failover**, not performance. The standby replica cannot be queried.

---

### 🔗 Reference:
- [Amazon RDS Read Replicas](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_ReadRepl.html)
- [ExamTopics Discussion](https://www.examtopics.com/discussions/amazon/view/102157-exam-aws-certified-solutions-architect-associate-saa-c03/)
</details>