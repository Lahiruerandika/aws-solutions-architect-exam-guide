## Question #01  

A company hosts a web application on multiple Amazon EC2 instances. The EC2 instances are in an Auto Scaling group that scales in response to user demand. The company wants to optimize cost savings without making a long-term commitment.

**Which EC2 instance purchasing option should a solutions architect recommend to meet these requirements?**

**A.** Dedicated Instances only  
**B.** On-Demand Instances only  
**C.** A mix of On-Demand Instances and Spot Instances  
**D.** A mix of On-Demand Instances and Reserved Instances  

<details>
<summary><strong>✅ Check Answer</strong></summary>

**Correct Answer: C. A mix of On-Demand Instances and Spot Instances**

**Explanation:**  
- **Spot Instances** offer significant cost savings (up to 90%) and are ideal for stateless, flexible, or fault-tolerant workloads.  
- **On-Demand Instances** provide reliability and are used for the baseline needs.  
- This mix allows the application to remain cost-efficient and scalable without committing to long-term contracts like Reserved Instances.

### 📚 Reference (Official AWS Documentation):
- [Auto Scaling Groups with Multiple Instance Types and Purchase Options – AWS Docs](https://docs.aws.amazon.com/autoscaling/ec2/userguide/ec2-auto-scaling-mixed-instances-groups.html)
- [Amazon EC2 Instance Purchasing Options – AWS Docs](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/instance-purchasing-options.html)

</details>

## Question #02  

**Question:** 
 A company has an application that is running on Amazon EC2 instances. A solutions architect has standardized the company on a particular instance family and various instance sizes based on the current needs of the company.

The company wants to maximize cost savings for the application over the next 3 years. The company needs to be able to change the instance family and sizes in the next 6 months based on application popularity and usage.

**Which solution will meet these requirements MOST cost-effectively?**

**A.** Compute Savings Plan
**B.** EC2 Instance Savings Plan
**C.** Zonal Reserved Instances
**D.** Standard Reserved Instances

<details>
<summary><strong>✅ Check Answer</strong></summary>

**✅ Correct Answer: A. Compute Savings Plan**

### ✔ Why Compute Savings Plan?

| Requirement                              | Benefit with Compute Savings Plan |
|------------------------------------------|-----------------------------------|
| Maximize cost savings                    | Up to **66% discount** vs On-Demand pricing |
| Flexibility across instance families     | Applies to **any instance family**, size, OS, or region |
| Anticipating usage pattern changes       | Ideal for unpredictable workloads |
| Lower management overhead                | No manual reservations or tracking needed |

## ❌ Why not the other options?

- **B. EC2 Instance Savings Plan**
  - Locked to a specific **instance family** within a region.
  - Less flexible than Compute Savings Plan.

- **C. Zonal Reserved Instances**
  - Tied to a specific **Availability Zone**.
  - No flexibility to change instance types or zones.

- **D. Standard Reserved Instances**
  - Locked to specific **instance types and configurations**.
  - Most cost-effective only when workloads are very stable and predictable.

---

Let me know if you'd like this saved as a file or want to add a table of contents, diagrams, or more examples!

### 🔗 References:

- AWS Docs – [Amazon S3 File Gateway](https://docs.aws.amazon.com/filegateway/latest/filefsxw/what-is-file-gateway.html)  

</details>

## Question #: 03

**Question:**  
A company collects data from a large number of participants who use wearable devices. The company stores the data in an Amazon DynamoDB table and uses applications to analyze the data. The data workload is constant and predictable. The company wants to stay at or below its forecasted budget for DynamoDB.

**Which solution will meet these requirements MOST cost-effectively?**

**A.** Use provisioned mode and DynamoDB Standard-Infrequent Access (DynamoDB Standard-IA). Reserve capacity for the forecasted workload.  
**B.** Use provisioned mode. Specify the read capacity units (RCUs) and write capacity units (WCUs).  
**C.** Use on-demand mode. Set the read capacity units (RCUs) and write capacity units (WCUs) high enough to accommodate changes in the workload.  
**D.** Use on-demand mode. Specify the read capacity units (RCUs) and write capacity units (WCUs) with reserved capacity.

---

<details>
<summary><strong>✅ Check Answer</strong></summary>

---

### ✅ Correct Answer: **B. Use provisioned mode. Specify the read capacity units (RCUs) and write capacity units (WCUs).**

---

### 📘 Explanation:

Since the company’s workload is **constant and predictable**, the most **cost-effective** approach is to use **provisioned mode**. In this mode, you can manually define the required RCUs and WCUs to match the expected usage. This allows tighter control over costs and avoids overprovisioning.

#### ✅ Why Option B is Correct:
- **Provisioned mode** fits **predictable workloads**, offering the ability to reserve just enough capacity.
- Avoids the overhead of on-demand costs.
- Allows the company to **stay within budget** by avoiding unnecessary scaling or unpredictable usage charges.

#### 🚫 Why not the others?

- **A.** Incorrect: DynamoDB Standard-IA is meant for **infrequently accessed** data, but the data here is **frequently accessed**, so this storage class is not appropriate.
- **C.** Incorrect: On-demand mode auto-scales, which is better for unpredictable workloads, and may be **more costly** for consistent workloads.
- **D.** Incorrect: On-demand mode does **not** allow manual specification of RCUs/WCUs or use reserved capacity, so the suggestion is technically invalid.

---

### 🔗 References:

- AWS Docs – [DynamoDB Read/Write Capacity Modes](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/HowItWorks.ReadWriteCapacityMode.html)  
- AWS Docs – [DynamoDB Table Classes](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/table-class.html)  
</details>

## Question #: 04

**Question:**  
A company stores its data objects in Amazon S3 Standard storage. A solutions architect has found that 75% of the data is rarely accessed after 30 days. The company needs all the data to remain immediately accessible with the same high availability and resiliency, but the company wants to minimize storage costs.

**Which storage solution will meet these requirements?**

**A.** Move the data objects to S3 Glacier Deep Archive after 30 days.  
**B.** Move the data objects to S3 Standard-Infrequent Access (S3 Standard-IA) after 30 days.  
**C.** Move the data objects to S3 One Zone-Infrequent Access (S3 One Zone-IA) after 30 days.  
**D.** Move the data objects to S3 One Zone-Infrequent Access (S3 One Zone-IA) immediately.

---
<details>
<summary><strong>✅ Check Answer</strong></summary>
---
### ✅ Correct Answer: **B. Move the data objects to S3 Standard-Infrequent Access (S3 Standard-IA) after 30 days.**

---

### 📘 Explanation:

#### ✅ Why Option B is Correct:
- **S3 Standard-IA** is designed for data that is **accessed less frequently but must be immediately accessible** when needed.
- It offers the **same high durability and availability** as S3 Standard, but at a **lower cost** for storage and a slightly higher cost for retrieval.
- Perfect for **rarely accessed data** that still needs **high resiliency and immediate access** — exactly matching the use case described.
- You can automate this using **S3 Lifecycle policies** to transition data to Standard-IA after 30 days.

#### 🚫 Why not the others?

- **A.** S3 Glacier Deep Archive is for **archival** storage. Data is **not immediately accessible** — retrieval takes hours.
- **C. & D.** S3 One Zone-IA is cheaper but stores data in **only one Availability Zone**, which does **not meet high availability or resiliency** requirements.

---

### 🔗 References:

- AWS Documentation – [S3 Storage Classes](https://aws.amazon.com/s3/storage-classes/)
- AWS Docs – [S3 Lifecycle Configuration](https://docs.aws.amazon.com/AmazonS3/latest/userguide/lifecycle-configuration-examples.html)
- ExamTopics Discussion - (https://www.examtopics.com/discussions/amazon/view/100229-exam-aws-certified-solutions-architect-associate-saa-c03/)

</details>

## Question #05
 
A company has an application that collects data from IoT sensors on automobiles. The data is streamed and stored in Amazon S3 through Amazon Kinesis Data Firehose. The data produces trillions of S3 objects each year. Each morning, the company uses the data from the previous 30 days to retrain a suite of machine learning (ML) models.

Four times each year, the company uses the data from the previous 12 months to perform analysis and train other ML models. The data must be available with minimal delay for up to 1 year. After 1 year, the data must be retained for archival purposes.

**Which storage solution meets these requirements MOST cost-effectively?**

**A.** Use the S3 Intelligent-Tiering storage class. Create an S3 Lifecycle policy to transition objects to S3 Glacier Deep Archive after 1 year.  
**B.** Use the S3 Intelligent-Tiering storage class. Configure S3 Intelligent-Tiering to automatically move objects to S3 Glacier Deep Archive after 1 year.  
**C.** Use the S3 Standard-Infrequent Access (S3 Standard-IA) storage class. Create an S3 Lifecycle policy to transition objects to S3 Glacier Deep Archive after 1 year.  
**D.** Use the S3 Standard storage class. Create an S3 Lifecycle policy to transition objects to S3 Standard-Infrequent Access (S3 Standard-IA) after 30 days, and then to S3 Glacier Deep Archive after 1 year.

---

<details>
<summary><strong>✅ Check Answer</strong></summary>

---

### ✅ Correct Answer:  
**D. Use the S3 Standard storage class. Create an S3 Lifecycle policy to transition objects to S3 Standard-Infrequent Access (S3 Standard-IA) after 30 days, and then to S3 Glacier Deep Archive after 1 year.**

---

### 📘 Explanation:

#### ✅ Why D is Correct:
- **S3 Standard** supports frequent access in the first 30 days (daily ML training).
- **S3 Standard-IA** is ideal after 30 days (quarterly model training).
- **S3 Glacier Deep Archive** provides the **lowest-cost** long-term archival storage.
- Lifecycle policies **automate transitions** with minimal operational overhead.

#### 🚫 Why the other options are incorrect:

- **A & B:** S3 Intelligent-Tiering incurs **monitoring charges**, which is unnecessary here since the access pattern is **predictable**.
- **C:** Using S3 Standard-IA from the start doesn't make sense because the data is actively used in the first 30 days.

---

### 🔗 References:
- [Amazon S3 Storage Classes](https://docs.aws.amazon.com/AmazonS3/latest/userguide/storage-class-intro.html)  
- [S3 Lifecycle Configuration](https://docs.aws.amazon.com/AmazonS3/latest/userguide/lifecycle-configuration-examples.html)
- [ExamTopics Discussion](https://www.examtopics.com/discussions/amazon/view/102137-exam-aws-certified-solutions-architect-associate-saa-c03/)

</details>

## Question #06

A company is migrating its on-premises workload to the AWS Cloud. The company already uses several Amazon EC2 instances and Amazon RDS DB instances. The company wants a solution that automatically starts and stops the EC2 instances and DB instances outside of business hours. The solution must minimize cost and infrastructure maintenance.

**Which solution will meet these requirements?**

**A.** Scale the EC2 instances by using elastic resize. Scale the DB instances to zero outside of business hours.  
**B.** Explore AWS Marketplace for partner solutions that will automatically start and stop the EC2 instances and DB instances on a schedule.  
**C.** Launch another EC2 instance. Configure a crontab schedule to run shell scripts that will start and stop the existing EC2 instances and DB instances on a schedule.  
**D.** Create an AWS Lambda function that will start and stop the EC2 instances and DB instances. Configure Amazon EventBridge to invoke the Lambda function on a schedule.

---

<details>
<summary><strong>✅ Check Answer</strong></summary>

---

### ✅ Correct Answer:  
**D. Create an AWS Lambda function that will start and stop the EC2 instances and DB instances. Configure Amazon EventBridge to invoke the Lambda function on a schedule.**

---

### 📘 Explanation:

#### ✅ Why D is Correct:
- **AWS Lambda** combined with **Amazon EventBridge (formerly CloudWatch Events)** allows for serverless automation with low maintenance.
- It **minimizes cost** by shutting down resources when not needed.
- No need to maintain a scheduler server (as in option C).
- It is **scalable**, **automated**, and aligns with AWS best practices for serverless operations.

#### 🚫 Why the other options are incorrect:

- **A.** EC2 and RDS do not support “scaling to zero.” You must **stop the instance** to avoid costs, not “scale.”
- **B.** AWS Marketplace solutions may work but introduce **additional cost** and **complexity** for a task that can be done with native services.
- **C.** Using a separate EC2 instance with cron introduces **unnecessary infrastructure and maintenance overhead**.

---

### 🔗 References:
- [Stop and Start EC2 Instances at Scheduled Times](https://aws.amazon.com/premiumsupport/knowledge-center/start-stop-lambda-eventbridge/)
- [RDS Stop and Start](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_StopInstance.html)
- [Amazon EventBridge Scheduling](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-scheduler.html)
- [ExamTopics Discussion](https://www.examtopics.com/discussions/amazon/view/102145-exam-aws-certified-solutions-architect-associate-saa-c03/)

</details>

## Question #07

**Question:**  
A company is planning to migrate a commercial off-the-shelf application from its on-premises data center to AWS. The software has a software licensing model using sockets and cores with predictable capacity and uptime requirements. The company wants to use its existing licenses, which were purchased earlier this year.

**Which Amazon EC2 pricing option is the MOST cost-effective?**

**A.** Dedicated Reserved Hosts  
**B.** Dedicated On-Demand Hosts  
**C.** Dedicated Reserved Instances  
**D.** Dedicated On-Demand Instances  

---

<details>
<summary><strong>✅ Check Answer</strong></summary>

---

### ✅ Correct Answer:  
**A. Dedicated Reserved Hosts**

---

### 📘 Explanation:

#### ✅ Why A is Correct:
- **Dedicated Hosts** allow you to bring your own licenses (BYOL) for software that is bound to physical sockets, cores, or VMs.
- **Reserved** pricing on Dedicated Hosts provides significant cost savings over time when workloads are predictable and always-on.
- Since the application has **predictable capacity and uptime**, **Dedicated Reserved Hosts** are **the most cost-effective** option that complies with licensing restrictions.

#### 🚫 Why the other options are incorrect:

- **B.** Dedicated On-Demand Hosts offer the same licensing benefits but are **not cost-effective** for predictable, long-term workloads due to higher pricing.
- **C.** Reserved Instances are not tied to physical hosts and do not allow BYOL based on **socket/core licensing**, so they do **not satisfy licensing terms**.
- **D.** Dedicated On-Demand Instances also do not provide the cost savings needed for long-term, predictable workloads and may not support socket/core licensing.

---

### 🔗 References:
- [AWS EC2 Dedicated Hosts](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/dedicated-hosts-overview.html)  
- [Bring Your Own License (BYOL) to AWS](https://aws.amazon.com/license-manager/)
- [ExamTopics Discussion](https://www.examtopics.com/discussions/amazon/view/102150-exam-aws-certified-solutions-architect-associate-saa-c03/)

</details>

---

## Question #:08

**Question:**  
A company runs an application on Amazon EC2 Linux instances across multiple Availability Zones. The application needs a storage layer that is highly available and Portable Operating System Interface (POSIX)-compliant. The storage layer must provide maximum data durability and must be shareable across the EC2 instances. The data in the storage layer will be accessed frequently for the first 30 days and will be accessed infrequently after that time.

**Which solution will meet these requirements MOST cost-effectively?**

**A.** Use the Amazon S3 Standard storage class. Create an S3 Lifecycle policy to move infrequently accessed data to S3 Glacier.  
**B.** Use the Amazon S3 Standard storage class. Create an S3 Lifecycle policy to move infrequently accessed data to S3 Standard-Infrequent Access (S3 Standard-IA).  
**C.** Use the Amazon Elastic File System (Amazon EFS) Standard storage class. Create a lifecycle management policy to move infrequently accessed data to EFS Standard-Infrequent Access (EFS Standard-IA).  
**D.** Use the Amazon Elastic File System (Amazon EFS) One Zone storage class. Create a lifecycle management policy to move infrequently accessed data to EFS One Zone-Infrequent Access (EFS One Zone-IA).

---

<details>
<summary><strong>✅ Check Answer</strong></summary>

---

### ✅ Correct Answer:  
**C. Use the Amazon Elastic File System (Amazon EFS) Standard storage class. Create a lifecycle management policy to move infrequently accessed data to EFS Standard-Infrequent Access (EFS Standard-IA).**

---

### 📘 Explanation:

#### ✅ Why C is Correct:
- Amazon **EFS** provides a **highly available, durable, POSIX-compliant shared file system** accessible across multiple EC2 instances and Availability Zones.
- **EFS Standard** is the default storage class optimized for frequent access.
- **EFS Standard-IA** provides cost savings for infrequently accessed data.
- Lifecycle policies in EFS automatically transition files to IA after a period of inactivity (e.g., 30 days).
- This makes it **cost-effective**, **durable**, and **highly available** while meeting POSIX requirements.

#### 🚫 Why the other options are incorrect:

- **A & B.** Amazon S3 is not POSIX-compliant and does not support shared file system semantics needed by applications using local file system calls.
- **D.** EFS One Zone is less expensive but is not **highly available across AZs** — which violates the requirement for multi-AZ high availability.

---

### 🔗 References:
- [Amazon EFS Overview](https://docs.aws.amazon.com/efs/latest/ug/whatisefs.html)  
- [EFS Lifecycle Management](https://docs.aws.amazon.com/efs/latest/ug/lifecycle-management.html)  
- [EFS Storage Classes](https://aws.amazon.com/efs/features/)
- [ExamTopics Discussion](https://www.examtopics.com/discussions/amazon/view/102152-exam-aws-certified-solutions-architect-associate-saa-c03/)

</details>