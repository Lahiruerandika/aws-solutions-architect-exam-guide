## Question #: 01

**Question:**  
A company has an aging network-attached storage (NAS) array in its data center. The NAS array presents SMB shares and NFS shares to client workstations. The company does not want to purchase a new NAS array. The company also does not want to incur the cost of renewing the NAS array’s support contract. Some of the data is accessed frequently, but much of the data is inactive.

A solutions architect needs to implement a solution that migrates the data to Amazon S3, uses S3 Lifecycle policies, and maintains the same look and feel for the client workstations. The solutions architect has identified AWS Storage Gateway as part of the solution.

**Which type of storage gateway should the solutions architect provision to meet these requirements?**

**A.** Volume Gateway  
**B.** Tape Gateway  
**C.** Amazon FSx File Gateway  
**D.** Amazon S3 File Gateway

---

<details>
<summary><strong>✅ Check Answer</strong></summary>

---

### ✅ Correct Answer: **D. Amazon S3 File Gateway**

---

### 📘 Explanation:

**Amazon S3 File Gateway** is the ideal choice for this scenario. It presents a file interface (NFS or SMB) to on-premises clients, but stores the actual data in **Amazon S3**. This meets the need to:

- Maintain the same interface (NFS/SMB) for client workstations.
- Use **S3 Lifecycle policies** to manage storage costs by transitioning older data to cheaper storage classes like **S3 Glacier**.
- Avoid purchasing new on-premises storage or renewing support contracts.

#### ✅ Why Option D is Correct:
- **S3 File Gateway** enables access to objects in Amazon S3 as files through standard NFS and SMB protocols.
- Files are cached locally for low-latency access and can be accessed by multiple clients.
- Works well for replacing legacy NAS systems and allows seamless migration.

#### 🚫 Why not the others?
- **A. Volume Gateway** exposes block storage (iSCSI), not suitable for file-based workloads.
- **B. Tape Gateway** is for backup/archive workflows using virtual tapes — not appropriate for regular file access.
- **C. Amazon FSx File Gateway** is not a valid service — likely a confusion with **Amazon FSx for Windows/Linux**, which is a managed file system, not a Storage Gateway type.

---

### 🔗 References:

- AWS Docs – [Amazon S3 File Gateway](https://docs.aws.amazon.com/filegateway/latest/filefsxw/what-is-file-gateway.html)  
- [ExamTopics Discussion](https://www.examtopics.com/discussions/amazon/view/100220-exam-aws-certified-solutions-architect-associate-saa-c03/)

</details>

## Question #: 02

**Question:**  
A company hosts a three-tier web application on Amazon EC2 instances in a single Availability Zone. The web application uses a self-managed MySQL database that is hosted on an EC2 instance to store data in an Amazon Elastic Block Store (Amazon EBS) volume. The MySQL database currently uses a 1 TB Provisioned IOPS SSD (io2) EBS volume. The company expects traffic of 1,000 IOPS for both reads and writes at peak traffic.

The company wants to minimize any disruptions, stabilize performance, and reduce costs while retaining the capacity for double the IOPS. The company wants to move the database tier to a fully managed solution that is highly available and fault tolerant.

**Which solution will meet these requirements MOST cost-effectively?**

**A.** Use a Multi-AZ deployment of an Amazon RDS for MySQL DB instance with an io2 Block Express EBS volume.  
**B.** Use a Multi-AZ deployment of an Amazon RDS for MySQL DB instance with a General Purpose SSD (gp2) EBS volume.  
**C.** Use Amazon S3 Intelligent-Tiering access tiers.  
**D.** Use two large EC2 instances to host the database in active-passive mode.

---

<details>
<summary><strong>✅ Check Answer</strong></summary>

---

### ✅ Correct Answer: **B. Use a Multi-AZ deployment of an Amazon RDS for MySQL DB instance with a General Purpose SSD (gp2) EBS volume.**

---

### 📘 Explanation:

#### ✅ Why Option B is Correct:
- **Amazon RDS** in **Multi-AZ deployment** provides high availability and fault tolerance.
- **General Purpose SSD (gp2)** volumes can provide **up to 3,000 IOPS** per volume, depending on
### ✅ Correct Answer: **B. Use a Multi-AZ deployment of an Amazon RDS for MySQL DB instance with a General Purpose SSD (gp2) EBS volume.**

---

### 📘 Explanation:

#### ✅ Why Option B is Correct:
- **Amazon RDS** in **Multi-AZ deployment** provides high availability and fault tolerance.
- **General Purpose SSD (gp2)** volumes can provide **up to 3,000 IOPS** per volume, depending on the size (you get 3 IOPS per GB). A 1 TB gp2 volume can provide **3,000 IOPS**, which is enough to handle **1,000 IOPS** read/write traffic and allows for future growth up to **double the current workload**.
- This option also **reduces costs significantly** compared to using **Provisioned IOPS (io2)**.

#### 🚫 Why not the others?

- **A.** io2 Block Express is very high performance and low latency, but it's **more expensive** than gp2. Not needed for this IOPS level if cost is a concern.
- **C.** Amazon S3 Intelligent-Tiering is **not suitable for databases**, as it’s designed for object storage and archival—not live transactional workloads.
- **D.** Hosting a MySQL cluster on EC2 in an active-passive configuration increases operational complexity, lacks managed features, and is **not fault-tolerant by default** without additional setup and tooling.

---

### 🔗 References:

- AWS Docs – [Amazon RDS Multi-AZ](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Concepts.MultiAZ.html)  
- AWS Docs – [EBS Volume Types](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-volume-types.html)  

</details>

## Question #: 03

**Question:**  
A company is moving its data management application to AWS. The company wants to transition to an event-driven architecture. The architecture needs to be more distributed and to use serverless concepts while performing the different aspects of the workflow. The company also wants to minimize operational overhead.

**Which solution will meet these requirements?**

**A.** Build out the workflow in AWS Glue. Use AWS Glue to invoke AWS Lambda functions to process the workflow steps.  
**B.** Build out the workflow in AWS Step Functions. Deploy the application on Amazon EC2 instances. Use Step Functions to invoke the workflow steps on the EC2 instances.  
**C.** Build out the workflow in Amazon EventBridge. Use EventBridge to invoke AWS Lambda functions on a schedule to process the workflow steps.  
**D.** Build out the workflow in AWS Step Functions. Use Step Functions to create a state machine. Use the state machine to invoke AWS Lambda functions to process the workflow steps.

---

<details>
<summary><strong>✅ Check Answer</strong></summary>

---

### ✅ Correct Answer:  
**D. Build out the workflow in AWS Step Functions. Use Step Functions to create a state machine. Use the state machine to invoke AWS Lambda functions to process the workflow steps.**

---

### 📘 Explanation:

#### ✅ Why D is Correct:
- **AWS Step Functions** allow the creation of a **serverless, event-driven workflow** that coordinates components, ensuring minimal operational overhead.
- You can design a **state machine** that defines the sequence of steps in the workflow.
- **AWS Lambda** functions are invoked by Step Functions at each step, making the architecture **highly distributed, serverless, and event-driven**.
- This approach is **cost-effective**, **scalable**, and **requires minimal maintenance**.

#### 🚫 Why the other options are incorrect:

- **A.** AWS Glue is primarily for **ETL jobs**, not general event-driven workflow management.
- **B.** Running applications on EC2 instances **increases operational overhead**, which goes against the goal of using serverless concepts.
- **C.** EventBridge is good for **event routing**, but **it doesn't inherently model complex workflows** like Step Functions does. Scheduling is not the primary requirement here.

---

### 🔗 References:
- [AWS Step Functions Documentation](https://docs.aws.amazon.com/step-functions/latest/dg/welcome.html)  
- [AWS Lambda Overview](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html)  
- [FreeCram Discussion](https://www.freecram.net/question/Amazon.AWS-Solutions-Associate.v2023-10-17.q198/a-company-is-moving-its-data-management-application-to-aws-the-company-wants-to-transition-to-an-event-dr)

</details>

## Question #: 04  

**Question:**  
A company hosts a multiplayer gaming application on AWS. The company wants the application to read data with sub-millisecond latency and run one-time queries on historical data.

**Which solution will meet these requirements with the LEAST operational overhead?**

**A.** Use Amazon RDS for data that is frequently accessed. Run a periodic custom script to export the data to an Amazon S3 bucket.  
**B.** Store the data directly in an Amazon S3 bucket. Implement an S3 Lifecycle policy to move older data to S3 Glacier Deep Archive for long-term storage. Run one-time queries on the data in Amazon S3 by using Amazon Athena.  
**C.** Use Amazon DynamoDB with DynamoDB Accelerator (DAX) for data that is frequently accessed. Export the data to an Amazon S3 bucket by using DynamoDB table export. Run one-time queries on the data in Amazon S3 by using Amazon Athena.  
**D.** Use Amazon DynamoDB for data that is frequently accessed. Turn on streaming to Amazon Kinesis Data Streams. Use Amazon Kinesis Data Firehose to read the data from Kinesis Data Streams. Store the records in an Amazon S3 bucket.

---

<details>
<summary><strong>✅ Check Answer</strong></summary>

---

### ✅ Correct Answer:  
**C. Use Amazon DynamoDB with DynamoDB Accelerator (DAX) for data that is frequently accessed. Export the data to an Amazon S3 bucket by using DynamoDB table export. Run one-time queries on the data in Amazon S3 by using Amazon Athena.**

---

### 📘 Explanation:

#### ✅ Why C is Correct:
- **DynamoDB with DAX** provides **sub-millisecond read performance**, ideal for real-time gaming applications.
- **DynamoDB table export to Amazon S3** is a **serverless, no-code** feature that allows you to export table data directly into S3 without affecting performance.
- **Amazon Athena** allows **serverless querying** of data stored in S3 using standard SQL, perfect for **one-time or ad-hoc historical queries**.
- This setup has **minimal operational overhead** because all components (DAX, table export, Athena) are managed by AWS.

#### 🚫 Why the other options are incorrect:

- **A.** RDS can introduce higher latency than DynamoDB+DAX and requires **custom scripting** for exporting data — more operational overhead.
- **B.** S3 alone does not provide **sub-millisecond** read latency. It's suitable for historical querying but not real-time game interactions.
- **D.** Using Kinesis Data Streams and Firehose adds **more moving parts** and **increases operational complexity**, not ideal for "least operational overhead."

---

### 🔗 References:
- [DynamoDB Accelerator (DAX)](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/DAX.html)  
- [DynamoDB Table Export to S3](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/DataExport.html)  
- [Amazon Athena Overview](https://docs.aws.amazon.com/athena/latest/ug/what-is.html)  

</details>

## Question #: 05

**Question:**  
A company uses a payment processing system that requires messages for a particular payment ID to be received in the same order that they were sent. Otherwise, the payments might be processed incorrectly.

**Which actions should a solutions architect take to meet this requirement? (Choose two.)**

**A.** Write the messages to an Amazon DynamoDB table with the payment ID as the partition key.  
**B.** Write the messages to an Amazon Kinesis data stream with the payment ID as the partition key.  
**C.** Write the messages to an Amazon ElastiCache for Memcached cluster with the payment ID as the key.  
**D.** Write the messages to an Amazon Simple Queue Service (Amazon SQS) queue. Set the message attribute to use the payment ID.  
**E.** Write the messages to an Amazon Simple Queue Service (Amazon SQS) FIFO queue. Set the message group to use the payment ID.

---

<details>
<summary><strong>✅ Check Answer</strong></summary>

---

### ✅ Correct Answers:  
**B.** Write the messages to an Amazon Kinesis data stream with the payment ID as the partition key.  
**E.** Write the messages to an Amazon Simple Queue Service (Amazon SQS) FIFO queue. Set the message group to use the payment ID.

---

### 📘 Explanation:

#### ✅ Why B is Correct:
- **Amazon Kinesis Data Streams** can guarantee **ordered message delivery** within a **shard**.
- Using the **payment ID as the partition key** ensures that all messages with the same key go to the same shard, preserving order.

#### ✅ Why E is Correct:
- **Amazon SQS FIFO (First-In-First-Out)** queues are specifically designed to **guarantee message order**.
- Using the **message group ID** set to the **payment ID** ensures that messages are processed in the exact order for that payment.

---

#### 🚫 Why the other options are incorrect:

- **A.** DynamoDB does not preserve the order in which items are written.
- **C.** ElastiCache (especially Memcached) is not a messaging or queuing system and does not maintain order.
- **D.** Standard SQS queues do **not guarantee ordering**. Message attributes alone do not enforce processing order.

---

### 🔗 References:
- [Amazon Kinesis Data Streams](https://docs.aws.amazon.com/streams/latest/dev/introduction.html)  
- [Amazon SQS FIFO Queues](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/FIFO-queues.html)  
- [ExamTopics Discussion](https://www.examtopics.com/discussions/amazon/view/102121-exam-aws-certified-solutions-architect-associate-saa-c03/)

</details>

## Question #: 06  

**Question:**  
A company is building a game system that needs to send unique events to separate leaderboard, matchmaking, and authentication services concurrently. The company needs an AWS event-driven system that guarantees the order of the events.

**Which solution will meet these requirements?**

**A.** Amazon EventBridge event bus  
**B.** Amazon Simple Notification Service (Amazon SNS) FIFO topics  
**C.** Amazon Simple Notification Service (Amazon SNS) standard topics  
**D.** Amazon Simple Queue Service (Amazon SQS) FIFO queues  

---

<details>
<summary><strong>✅ Check Answer</strong></summary>

---

### ✅ Correct Answer:  
**B.** Amazon Simple Notification Service (Amazon SNS) FIFO topics

---

### 📘 Explanation:

#### ✅ Why B is Correct:
- **Amazon SNS FIFO topics** are specifically designed to **support ordered message delivery** to multiple subscribers.
- They allow you to **fan out messages concurrently** to different services (like leaderboard, matchmaking, and authentication) **while preserving the order** of events.
- This makes them ideal for **event-driven architectures** that need **guaranteed ordering across multiple services**.

---

#### 🚫 Why the other options are incorrect:

- **A. Amazon EventBridge**: EventBridge does **not guarantee order** of events. It's useful for loosely coupled services but not for use cases requiring ordered delivery.
  
- **C. SNS standard topics**: Standard topics provide **best-effort ordering** but do **not guarantee message order**.

- **D. SQS FIFO queues**: FIFO queues **preserve order** but do **not support fan-out** (i.e., they send to one consumer group). They are more suitable for point-to-point messaging, not multi-subscriber systems.

---

### 🔗 References:
- [Amazon SNS FIFO Topics](https://docs.aws.amazon.com/sns/latest/dg/fifo-topics.html)  
- [EventBridge Event Bus](https://docs.aws.amazon.com/eventbridge/latest/userguide/what-is-amazon-eventbridge.html)
- [ExamTopics Discussion](https://www.examtopics.com/discussions/amazon/view/102124-exam-aws-certified-solutions-architect-associate-saa-c03/)

</details>

## Question #: 07

**Question:**  
A company runs a web application that is backed by Amazon RDS. A new database administrator caused data loss by accidentally editing information in a database table. To help recover from this type of incident, the company wants the ability to restore the database to its state from 5 minutes before any change within the last 30 days.

**Which feature should the solutions architect include in the design to meet this requirement?**

**A.** Read replicas  
**B.** Manual snapshots  
**C.** Automated backups  
**D.** Multi-AZ deployments  

---

<details>
<summary><strong>✅ Check Answer</strong></summary>

---

### ✅ Correct Answer:  
**C. Automated backups**

---

### 📘 Explanation:

#### ✅ Why C is Correct:
- **Automated backups** in Amazon RDS support **point-in-time recovery (PITR)**, allowing you to restore your database to **any second within the retention period (up to 35 days)**.
- This feature backs up the database and transaction logs automatically, enabling recovery to 5 minutes before an unintended change or data loss.
- It meets the requirement with minimal operational overhead.

#### 🚫 Why the other options are incorrect:

- **A.** Read replicas are designed for **horizontal read scaling**, not data recovery.
- **B.** Manual snapshots are static and must be initiated manually; they do **not allow point-in-time recovery** unless taken right before the incident.
- **D.** Multi-AZ deployments provide **high availability**, **not backup** or point-in-time recovery features.

---

### 🔗 References:
- [RDS Automated Backups](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_WorkingWithAutomatedBackups.html)  
- [Point-in-time Recovery](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_PIT.html)  
- [ExamTopics Discussion](https://www.examtopics.com/discussions/amazon/view/60048-exam-aws-certified-solutions-architect-associate-saa-c02/)

</details>

## Question #: 08

**Question:**  
A company is using Amazon Route 53 latency-based routing to route requests to its UDP-based application for users around the world. The application is hosted on redundant servers in the company’s on-premises data centers in the United States, Asia, and Europe. The company’s compliance requirements state that the application must be hosted on premises. The company wants to improve the performance and availability of the application.

**What should a solutions architect do to meet these requirements?**

**A.** Configure three Network Load Balancers (NLBs) in the three AWS Regions to address the on-premises endpoints. Create an accelerator by using AWS Global Accelerator, and register the NLBs as its endpoints. Provide access to the application by using a CNAME that points to the accelerator DNS.  
**B.** Configure three Application Load Balancers (ALBs) in the three AWS Regions to address the on-premises endpoints. Create an accelerator by using AWS Global Accelerator, and register the ALBs as its endpoints. Provide access to the application by using a CNAME that points to the accelerator DNS.  
**C.** Configure three Network Load Balancers (NLBs) in the three AWS Regions to address the on-premises endpoints. In Route 53, create a latency-based record that points to the three NLBs, and use it as an origin for an Amazon CloudFront distribution. Provide access to the application by using a CNAME that points to the CloudFront DNS.  
**D.** Configure three Application Load Balancers (ALBs) in the three AWS Regions to address the on-premises endpoints. In Route 53, create a latency-based record that points to the three ALBs, and use it as an origin for an Amazon CloudFront distribution. Provide access to the application by using a CNAME that points to the CloudFront DNS.

---

<details>
<summary><strong>✅ Check Answer</strong></summary>

---

### ✅ Correct Answer:  
**A. Configure three Network Load Balancers (NLBs) in the three AWS Regions to address the on-premises endpoints. Create an accelerator by using AWS Global Accelerator, and register the NLBs as its endpoints. Provide access to the application by using a CNAME that points to the accelerator DNS.**

---

### 📘 Explanation:

#### ✅ Why A is Correct:
- The application is **UDP-based**, and **Network Load Balancers (NLBs)** are the only AWS load balancers that support **UDP**.
- **AWS Global Accelerator** enhances **performance and availability** globally, while supporting **UDP traffic** and routing to **on-premises resources** via NLBs.
- This approach ensures the application remains **on-premises** (meeting compliance) while improving **global latency and fault tolerance**.
- Global Accelerator automatically routes user requests to the **nearest and healthiest endpoint**.

---

#### 🚫 Why the other options are incorrect:

- **B.** ALBs **do not support UDP**; they only work with **HTTP and HTTPS**, making this option invalid.
- **C.** CloudFront **does not support UDP** and is intended for **HTTP/HTTPS content delivery**.
- **D.** Same limitations as B and C — **ALBs and CloudFront** are not suitable for **UDP-based** workloads.

---

### 🔗 References:
- [Global Accelerator and On-premises Endpoints](https://docs.aws.amazon.com/global-accelerator/latest/dg/introduction-how-it-works-endpoints.html)  
- [Global Accelerator vs Route 53](https://docs.aws.amazon.com/global-accelerator/latest/dg/introduction-how-global-accelerator-differs.html)  
- [Network Load Balancer UDP Support](https://docs.aws.amazon.com/elasticloadbalancing/latest/network/introduction.html)
- [ExamTopics Discussion](https://www.examtopics.com/discussions/amazon/view/51508-exam-aws-certified-solutions-architect-associate-saa-c02/)

</details>

## Question #: 09

**Question:**  
A company has migrated an application to Amazon EC2 Linux instances. One of these EC2 instances runs several 1-hour tasks on a schedule. These tasks were written by different teams and have no common programming language. The company is concerned about performance and scalability while these tasks run on a single instance. A solutions architect needs to implement a solution to resolve these concerns.

**Which solution will meet these requirements with the LEAST operational overhead?**

**A.** Use AWS Batch to run the tasks as jobs. Schedule the jobs by using Amazon EventBridge (Amazon CloudWatch Events).  
**B.** Convert the EC2 instance to a container. Use AWS App Runner to create the container on demand to run the tasks as jobs.  
**C.** Copy the tasks into AWS Lambda functions. Schedule the Lambda functions by using Amazon EventBridge (Amazon CloudWatch Events).  
**D.** Create an Amazon Machine Image (AMI) of the EC2 instance that runs the tasks. Create an Auto Scaling group with the AMI to run multiple copies of the instance.

---

<details>
<summary><strong>✅ Check Answer</strong></summary>

---

### ✅ Correct Answer:  
**A. Use AWS Batch to run the tasks as jobs. Schedule the jobs by using Amazon EventBridge (Amazon CloudWatch Events).**

---

### 📘 Explanation:

#### ✅ Why A is Correct:
- **AWS Batch** enables running jobs with diverse language dependencies across managed compute environments.
- It’s ideal for **long-running** and **scheduled tasks** with **different runtimes or languages**.
- **EventBridge** can handle cron-like scheduling without needing any infrastructure management.
- **Minimal operational overhead**, highly scalable, and fully managed.

#### 🚫 Why the other options are incorrect:

- **B.** AWS App Runner is not designed for scheduled batch tasks—it's primarily for **web services and APIs**.
- **C.** Lambda is limited to **15 minutes per invocation**, so it cannot handle **1-hour tasks**.
- **D.** Launching EC2 instances using AMIs with Auto Scaling **adds complexity and overhead**, and doesn’t solve the task-specific scaling issue.

---

### 🔗 References:
- [AWS Batch Documentation](https://docs.aws.amazon.com/batch/latest/userguide/what-is-batch.html)  
- [EventBridge Scheduler](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-scheduler.html)  
- [AWS Compute Options](https://aws.amazon.com/products/compute/)
- [ExamTopics Discussion](https://www.examtopics.com/discussions/amazon/view/84704-exam-aws-certified-solutions-architect-associate-saa-c02/)

</details>

## Question #: 10

**Question:**   
A company is running several business applications in three separate VPCs within the us-east-1 Region. The applications must be able to communicate between VPCs. The applications also must be able to consistently send hundreds of gigabytes of data each day to a latency-sensitive application that runs in a single on-premises data center.

A solutions architect needs to design a network connectivity solution that maximizes cost-effectiveness.

**Which solution meets these requirements?**

**A.** Configure three AWS Site-to-Site VPN connections from the data center to AWS. Establish connectivity by configuring one VPN connection for each VPC.  
**B.** Launch a third-party virtual network appliance in each VPC. Establish an IPsec VPN tunnel between the data center and each virtual appliance.  
**C.** Set up three AWS Direct Connect connections from the data center to a Direct Connect gateway in us-east-1. Establish connectivity by configuring each VPC to use one of the Direct Connect connections.  
**D.** Set up one AWS Direct Connect connection from the data center to AWS. Create a transit gateway, and attach each VPC to the transit gateway. Establish connectivity between the Direct Connect connection and the transit gateway.  

---

<details>
<summary><strong>✅ Check Answer</strong></summary>

---

### ✅ Correct Answer:  
**D. Set up one AWS Direct Connect connection from the data center to AWS. Create a transit gateway, and attach each VPC to the transit gateway. Establish connectivity between the Direct Connect connection and the transit gateway.**

---

### 📘 Explanation:

#### ✅ Why D is Correct:
- **AWS Direct Connect** provides a **low-latency, high-bandwidth, and reliable** connection suitable for **sending large volumes of data consistently**.
- A **single Direct Connect connection** is **cost-effective** compared to multiple.
- **Transit Gateway** allows **centralized VPC-to-VPC and VPC-to-on-premises routing**, reducing management complexity and improving scalability.

#### 🚫 Why the other options are incorrect:
- **A.** Site-to-Site VPNs are cost-effective but **not ideal for high-throughput or latency-sensitive workloads** due to variability in internet routing.
- **B.** Launching third-party appliances introduces **more complexity and operational overhead** without added benefit in this case.
- **C.** Setting up three Direct Connect connections is **unnecessarily expensive** and does not improve performance significantly over a single connection with a Transit Gateway.

---

### 🔗 References:
- [AWS Direct Connect Overview](https://docs.aws.amazon.com/directconnect/latest/UserGuide/Welcome.html)  
- [Transit Gateway with Direct Connect](https://docs.aws.amazon.com/directconnect/latest/UserGuide/direct-connect-transit-gateways.html)  
- [VPC Connectivity Options](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-connectivity.html) 
- [ExamTopics Discussion](https://www.examtopics.com/discussions/amazon/view/67834-exam-aws-certified-solutions-architect-associate-saa-c02/) 

</details>

## Question #: 11

**Question:**  
An ecommerce company is building a distributed application that involves several serverless functions and AWS services to complete order-processing tasks. These tasks require manual approvals as part of the workflow. A solutions architect needs to design an architecture for the order-processing application. The solution must be able to combine multiple AWS Lambda functions into responsive serverless applications. The solution also must orchestrate data and services that run on Amazon EC2 instances, containers, or on-premises servers.

**Which solution will meet these requirements with the LEAST operational overhead?**

**A.** Use AWS Step Functions to build the application.  
**B.** Integrate all the application components in an AWS Glue job.  
**C.** Use Amazon Simple Queue Service (Amazon SQS) to build the application.  
**D.** Use AWS Lambda functions and Amazon EventBridge events to build the application.

---

<details>
<summary><strong>✅ Check Answer</strong></summary>

---

### ✅ Correct Answer:  
**A. Use AWS Step Functions to build the application.**

---

### 📘 Explanation:

#### ✅ Why A is Correct:
- **AWS Step Functions** provides **low-code visual workflows** that can coordinate multiple AWS services, including **Lambda, EC2, on-prem systems, and manual approval steps**.
- Supports **built-in support for human approval steps** using services like Amazon SNS or custom integrations.
- Reduces operational overhead by managing state, retries, error handling, and service orchestration **natively and reliably**.

#### 🚫 Why the other options are incorrect:

- **B.** AWS Glue is a data integration service mainly used for **ETL tasks**, not for orchestrating diverse application workflows.
- **C.** Amazon SQS handles messaging but does **not provide orchestration or human approval flow** capabilities.
- **D.** Lambda and EventBridge can coordinate some events, but building a full orchestrated workflow, especially with **manual approvals and integration with EC2 or on-prem**, would require **more custom logic and operational management**.

---

### 🔗 References:
- [AWS Step Functions](https://docs.aws.amazon.com/step-functions/latest/dg/welcome.html)  
- [Step Functions Use Cases](https://docs.aws.amazon.com/step-functions/latest/dg/use-cases.html)  
- [AWS Step Functions and Human Approval](https://aws.amazon.com/blogs/compute/implementing-human-approval-workflows-with-amazon-api-gateway-and-aws-step-functions/)
- [ExamTopics Discussion](https://www.examtopics.com/discussions/amazon/view/102139-exam-aws-certified-solutions-architect-associate-saa-c03/) 

</details>

## Question #: 12

**Question:** 
A company recently deployed a new auditing system to centralize information about operating system versions, patching, and installed software for Amazon EC2 instances. A solutions architect must ensure all instances provisioned through EC2 Auto Scaling groups successfully send reports to the auditing system as soon as they are launched and terminated.

**Which solution achieves these goals MOST efficiently?**

**A.** Use a scheduled AWS Lambda function and run a script remotely on all EC2 instances to send data to the audit system.  
**B.** Use EC2 Auto Scaling lifecycle hooks to run a custom script to send data to the audit system when instances are launched and terminated.  
**C.** Use an EC2 Auto Scaling launch configuration to run a custom script through user data to send data to the audit system when instances are launched and terminated.  
**D.** Run a custom script on the instance operating system to send data to the audit system. Configure the script to be invoked by the EC2 Auto Scaling group when the instance starts and is terminated.

---

<details>  
<summary><strong>✅ Check Answer</strong></summary>

---

### ✅ Correct Answer:  
**B. Use EC2 Auto Scaling lifecycle hooks to run a custom script to send data to the audit system when instances are launched and terminated.**

---

### 📘 Explanation:

#### ✅ Why B is Correct:
- **Lifecycle hooks** allow Auto Scaling groups to **pause instance launching or termination**, so custom actions (like reporting to an audit system) can occur reliably.
- Ensures that **both launch and termination events** are captured for auditing.
- Requires **low operational overhead** as it integrates directly with Auto Scaling workflows.

#### 🚫 Why the other options are incorrect:

- **A.** A scheduled Lambda would require continuous polling and manual management, making it less efficient and more error-prone.
- **C.** User data executes only at launch, not at termination — and may not capture all state info.
- **D.** The Auto Scaling group does not natively support calling scripts at both lifecycle stages without hooks, making this less robust.

---

### 🔗 References:
- [Amazon EC2 Auto Scaling lifecycle hooks](https://docs.aws.amazon.com/autoscaling/ec2/userguide/lifecycle-hooks.html)
- [Best Practices for EC2 Auto Scaling](https://docs.aws.amazon.com/autoscaling/ec2/userguide/best-practices.html)
- [AWS Documentation on EC2 Auto Scaling Lifecycle](https://docs.aws.amazon.com/autoscaling/ec2/userguide/lifecycle-overview.html)
- [ExamTopics Discussion](https://www.examtopics.com/discussions/amazon/view/27844-exam-aws-certified-solutions-architect-associate-saa-c02/) 

</details>

## Question #: 13

**Question:** 
A company is developing a real-time multiplayer game that uses UDP for communications between the client and servers in an Auto Scaling group. Spikes in demand are anticipated during the day, so the game server platform must adapt accordingly. Developers want to store gamer scores and other non-relational data in a database solution that will scale without intervention.

**Which solution should a solutions architect recommend?**

**A.** Use Amazon Route 53 for traffic distribution and Amazon Aurora Serverless for data storage.  
**B.** Use a Network Load Balancer for traffic distribution and Amazon DynamoDB on-demand for data storage.  
**C.** Use a Network Load Balancer for traffic distribution and Amazon Aurora Global Database for data storage.  
**D.** Use an Application Load Balancer for traffic distribution and Amazon DynamoDB global tables for data storage.

---

<details>  
<summary><strong>✅ Check Answer</strong></summary>

---

### ✅ Correct Answer:  
**B. Use a Network Load Balancer for traffic distribution and Amazon DynamoDB on-demand for data storage.**

---

### 📘 Explanation:

#### ✅ Why B is Correct:
- **Network Load Balancer (NLB)** is ideal for **UDP traffic**, which is required by the game server.
- **Amazon DynamoDB on-demand** is a **non-relational, fully managed NoSQL database** that can **scale automatically** without manual intervention, and is perfect for unpredictable workloads like gamer scores.

#### 🚫 Why the other options are incorrect:

- **A.** Route 53 is a DNS service, not suitable for handling real-time UDP traffic. Also, **Aurora Serverless** is a **relational DB**, not optimized for storing highly variable, non-relational gamer score data.
- **C.** Aurora Global Database is relational and not a good fit for the **non-relational workload**; also adds complexity and cost.
- **D.** **Application Load Balancer (ALB)** supports only HTTP/HTTPS and **not UDP**, so it cannot be used for the game servers.

---

### 🔗 References:
- [Amazon NLB and UDP Support](https://docs.aws.amazon.com/elasticloadbalancing/latest/network/introduction.html)
- [Amazon DynamoDB On-Demand Mode](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/HowItWorks.ReadWriteCapacityMode.html)
- [Choosing the Right Load Balancer](https://aws.amazon.com/elasticloadbalancing/features/)
- [ExamTopics Discussion](https://www.examtopics.com/discussions/amazon/view/102143-exam-aws-certified-solutions-architect-associate-saa-c03/) 


</details>