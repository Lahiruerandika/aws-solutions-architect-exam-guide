## Question #: 01  

**Question:** 
A company is building a mobile app on AWS. The company wants to expand its reach to millions of users. The company needs to build a platform so that authorized users can watch the company’s content on their mobile devices.

**What should a solutions architect recommend to meet these requirements?**

**A.** Publish content to a public Amazon S3 bucket. Use AWS Key Management Service (AWS KMS) keys to stream content.  
**B.** Set up IPsec VPN between the mobile app and the AWS environment to stream content.  
**C.** Use Amazon CloudFront. Provide signed URLs to stream content.  
**D.** Set up AWS Client VPN between the mobile app and the AWS environment to stream content.  

<details>
<summary><strong>✅ Check Answer</strong></summary>

**Correct Answer: C. Use Amazon CloudFront. Provide signed URLs to stream content**

### 🧠 Explanation:
- **Amazon CloudFront** is a content delivery network (CDN) that securely delivers data, videos, and applications with low latency.
- **Signed URLs** allow the company to **restrict access** to authorized users only, making them ideal for serving **private content** such as video streams to mobile apps.
- This approach scales easily to millions of users and provides both **security** and **performance**.

> ❌ Option A exposes content publicly, even with encryption.
> ❌ Options B & D are VPN solutions, which are not scalable or suitable for content delivery to a global user base.

### 📚 Reference (Official AWS Documentation):
- [Serving Private Content with Signed URLs and Cookies – Amazon CloudFront](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/private-content-signed-urls.html)
- [Using CloudFront for Video Streaming – AWS](https://docs.aws.amazon.com/whitepapers/latest/video-streaming-cloudfront/video-streaming-cloudfront.html)
- [ExamTopics Discussion – Question #100130 (SAA-C03)](https://www.examtopics.com/discussions/amazon/view/100130-exam-aws-certified-solutions-architect-associate-saa-c03/)

</details>


## Question #: 02

**Question:**  
A hospital needs to store patient records in an Amazon S3 bucket. The hospital’s compliance team must ensure that all protected health information (PHI) is encrypted in transit and at rest. The compliance team must administer the encryption key for data at rest.

**Which solution will meet these requirements?**

**A.** Create a public SSL/TLS certificate in AWS Certificate Manager (ACM). Associate the certificate with Amazon S3. Configure default encryption for each S3 bucket to use server-side encryption with AWS KMS keys (SSE-KMS). Assign the compliance team to manage the KMS keys.  
**B.** Use the aws:SecureTransport condition on S3 bucket policies to allow only encrypted connections over HTTPS (TLS). Configure default encryption for each S3 bucket to use server-side encryption with S3 managed encryption keys (SSE-S3). Assign the compliance team to manage the SSE-S3 keys.  
**C.** Use the aws:SecureTransport condition on S3 bucket policies to allow only encrypted connections over HTTPS (TLS). Configure default encryption for each S3 bucket to use server-side encryption with AWS KMS keys (SSE-KMS). Assign the compliance team to manage the KMS keys.  
**D.** Use the aws:SecureTransport condition on S3 bucket policies to allow only encrypted connections over HTTPS (TLS). Use Amazon Macie to protect the sensitive data that is stored in Amazon S3. Assign the compliance team to manage Macie.

---

<details>
<summary><strong>✅ Check Answer</strong></summary>

---

### ✅ Correct Answer:  
**C. Use the aws:SecureTransport condition on S3 bucket policies to allow only encrypted connections over HTTPS (TLS). Configure default encryption for each S3 bucket to use server-side encryption with AWS KMS keys (SSE-KMS). Assign the compliance team to manage the KMS keys.**

---

### 📘 Explanation:

#### ✅ Why C is Correct:
- The `aws:SecureTransport` condition ensures **encryption in transit** by only allowing HTTPS requests.
- **SSE-KMS** encrypts data at rest using **customer-managed AWS KMS keys**, allowing fine-grained access control and auditability.
- This setup meets **HIPAA compliance requirements** for protecting PHI.
- The **compliance team can control the KMS keys**, satisfying the requirement for key management.

#### 🚫 Why not the others?

- **A.** ACM public certificates cannot be directly associated with S3 buckets for upload/download access; S3 uses HTTPS natively.
- **B.** SSE-S3 does encrypt at rest but **does not allow customer-managed key administration**, which the compliance team requires.
- **D.** Amazon Macie helps **detect sensitive data** but does **not encrypt** it — and doesn’t replace KMS or bucket policies for encryption controls.

---

### 🔗 References:

- AWS Docs – [Protecting Data Using Server-Side Encryption with KMS keys (SSE-KMS)](https://docs.aws.amazon.com/AmazonS3/latest/userguide/UsingKMSEncryption.html)  
- AWS Docs – [Protecting Data In Transit](https://docs.aws.amazon.com/AmazonS3/latest/userguide/serv-side-encryption.html#encrypt-in-transit)  
- AWS Docs – [Bucket Policy Examples: Enforcing HTTPS](https://docs.aws.amazon.com/AmazonS3/latest/userguide/example-bucket-policies.html#example-bucket-policies-use-case-ssl)

</details>

## Question #: 03

**Question:**  
A company uses Amazon API Gateway to run a private gateway with two REST APIs in the same VPC. The BuyStock RESTful web service calls the CheckFunds RESTful web service to ensure that enough funds are available before a stock can be purchased. The company has noticed in the VPC flow logs that the BuyStock RESTful web service calls the CheckFunds RESTful web service over the internet instead of through the VPC. A solutions architect must implement a solution so that the APIs communicate through the VPC.

**Which solution will meet these requirements with the FEWEST changes to the code?**

**A.** Add an X-API-Key header in the HTTP header for authorization.  
**B.** Use an interface endpoint.  
**C.** Use a gateway endpoint.  
**D.** Add an Amazon Simple Queue Service (Amazon SQS) queue between the two REST APIs.

---

<details>
<summary><strong>✅ Check Answer</strong></summary>

---

### ✅ Correct Answer:  
**B. Use an interface endpoint.**

---

### 📘 Explanation:

#### ✅ Why B is Correct:
- **Private API Gateway** endpoints can be accessed via **interface VPC endpoints (powered by AWS PrivateLink)**.
- This ensures that communication between services **stays within the VPC**, avoiding traversal over the public internet.
- Using an interface endpoint enables **internal routing** between the REST APIs with **minimal code or architecture changes**.

#### 🚫 Why not the others?

- **A.** Adding an API key does not affect network routing. It is only for authorization.
- **C.** Gateway endpoints are used for **S3 and DynamoDB** only, not API Gateway.
- **D.** Introducing SQS adds unnecessary complexity and asynchronous communication, which is **not needed** and would **require major changes to the application logic**.

---

### 🔗 References:

- AWS Docs – [Accessing Private APIs](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-private-apis.html)  
- AWS Docs – [Interface VPC Endpoints (AWS PrivateLink)](https://docs.aws.amazon.com/vpc/latest/privatelink/endpoint-services-overview.html) 
- ExamTopics Discussion – Question (https://www.examtopics.com/discussions/amazon/view/100238-exam-aws-certified-solutions-architect-associate-saa-c03/)
</details>

## Question #: 04

**Question:**  
A company stores confidential data in an Amazon Aurora PostgreSQL database in the ap-southeast-3 Region. The database is encrypted with an AWS Key Management Service (AWS KMS) customer managed key. The company was recently acquired and must securely share a backup of the database with the acquiring company’s AWS account in ap-southeast-3.

**What should a solutions architect do to meet these requirements?**

**A.** Create a database snapshot. Copy the snapshot to a new unencrypted snapshot. Share the new snapshot with the acquiring company’s AWS account.  
**B.** Create a database snapshot. Add the acquiring company’s AWS account to the KMS key policy. Share the snapshot with the acquiring company’s AWS account.  
**C.** Create a database snapshot that uses a different AWS managed KMS key. Add the acquiring company’s AWS account to the KMS key alias. Share the snapshot with the acquiring company’s AWS account.  
**D.** Create a database snapshot. Download the database snapshot. Upload the database snapshot to an Amazon S3 bucket. Update the S3 bucket policy to allow access from the acquiring company’s AWS account.

---

<details>
<summary><strong>✅ Check Answer</strong></summary>

---

### ✅ Correct Answer:  
**B. Create a database snapshot. Add the acquiring company’s AWS account to the KMS key policy. Share the snapshot with the acquiring company’s AWS account.**

---

### 📘 Explanation:

#### ✅ Why B is Correct:
- Since the Aurora database is **encrypted with a customer managed KMS key**, sharing the snapshot with another AWS account **requires that account to have decrypt permissions** on the KMS key.
- You must **update the KMS key policy** to allow the acquiring company’s AWS account access.
- Once that’s done, you can **share the snapshot** using Amazon RDS's snapshot sharing feature.

#### 🚫 Why the others are incorrect:

- **A.** You **cannot copy an encrypted snapshot to an unencrypted one** for Aurora — it’s not supported for security reasons.
- **C.** Changing the KMS key or alias alone doesn't help. Sharing access requires **explicit permissions** on the key, not just the alias.
- **D.** You **cannot download RDS or Aurora snapshots** directly like regular files. There is **no mechanism to "download" a snapshot** and upload it to S3.

---

### 🔗 Reference:
- AWS Docs – [Sharing encrypted snapshots](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/USER_ShareSnapshot.html)
- AWS Docs – [Granting cross-account access to KMS keys](https://docs.aws.amazon.com/kms/latest/developerguide/key-policy-modifying.html)

</details>

## Question #: 05

**Question:**  
A company uses a 100 GB Amazon RDS for Microsoft SQL Server Single-AZ DB instance in the us-east-1 Region to store customer transactions. The company needs high availability and automatic recovery for the DB instance.

The company must also run reports on the RDS database several times a year. The report process causes transactions to take longer than usual to post to the customers’ accounts. The company needs a solution that will improve the performance of the report process.

**Which combination of steps will meet these requirements? (Choose two.)**

**A.** Modify the DB instance from a Single-AZ DB instance to a Multi-AZ deployment.  
**B.** Take a snapshot of the current DB instance. Restore the snapshot to a new RDS deployment in another Availability Zone.  
**C.** Create a read replica of the DB instance in a different Availability Zone. Point all requests for reports to the read replica.  
**D.** Migrate the database to RDS Custom.  
**E.** Use RDS Proxy to limit reporting requests to the maintenance window.

---

<details>
<summary><strong>✅ Check Answer</strong></summary>

---

### ✅ Correct Answers:  
**A. Modify the DB instance from a Single-AZ DB instance to a Multi-AZ deployment.**  
**C. Create a read replica of the DB instance in a different Availability Zone. Point all requests for reports to the read replica.**

---

### 📘 Explanation:

#### ✅ Why A is Correct:
- Converting from **Single-AZ to Multi-AZ** improves **high availability and automatic recovery**, ensuring failover to a standby in case of instance failure.

#### ✅ Why C is Correct:
- Creating a **read replica** offloads the **reporting workload** from the primary DB, improving **transaction performance** on the main database.

#### 🚫 Why the others are incorrect:

- **B.** Restoring a snapshot is a **manual, time-consuming** process and not intended for regular reporting or HA.
- **D.** RDS Custom is for **legacy or highly specialized** configurations and doesn’t provide a direct benefit for HA or performance in this use case.
- **E.** RDS Proxy improves **connection pooling** and application scaling, but it does not directly improve **reporting performance** or manage scheduling for reports.

---

### 🔗 Reference:
- [Amazon RDS Multi-AZ Deployments](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Concepts.MultiAZ.html)  
- [Amazon RDS Read Replicas](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_ReadRepl.html)
- [ExamTopics Discussion](https://www.examtopics.com/discussions/amazon/view/100300-exam-aws-certified-solutions-architect-associate-saa-c03/)

</details>

## Question #: 06

**Question:**  
A company wants to restrict access to the content of one of its main web applications and to protect the content by using authorization techniques available on AWS. The company wants to implement a serverless architecture and an authentication solution for fewer than 100 users. The solution needs to integrate with the main web application and serve web content globally. The solution must also scale as the company’s user base grows while providing the lowest login latency possible.

**Which solution will meet these requirements MOST cost-effectively?**

**A.** Use Amazon Cognito for authentication. Use Lambda@Edge for authorization. Use Amazon CloudFront to serve the web application globally.  
**B.** Use AWS Directory Service for Microsoft Active Directory for authentication. Use AWS Lambda for authorization. Use an Application Load Balancer to serve the web application globally.  
**C.** Use Amazon Cognito for authentication. Use AWS Lambda for authorization. Use Amazon S3 Transfer Acceleration to serve the web application globally.  
**D.** Use AWS Directory Service for Microsoft Active Directory for authentication. Use Lambda@Edge for authorization. Use AWS Elastic Beanstalk to serve the web application globally.

---

<details>
<summary><strong>✅ Check Answer</strong></summary>

---

### ✅ Correct Answer:  
**A. Use Amazon Cognito for authentication. Use Lambda@Edge for authorization. Use Amazon CloudFront to serve the web application globally.**

---

### 📘 Explanation:

#### ✅ Why A is Correct:
- **Amazon Cognito** provides a **cost-effective authentication** mechanism suitable for small user bases and easily scalable.
- **Lambda@Edge** enables **low-latency, geographically distributed authorization**, enforcing rules near the user.
- **Amazon CloudFront** provides **global content delivery**, enhancing speed and performance for users worldwide.
- This combination is **fully serverless**, **highly scalable**, and incurs **low operational costs**, especially for <100 users.

#### 🚫 Why the other options are incorrect:

- **B.** AWS Directory Service is **overkill and costly** for fewer than 100 users and isn't serverless.
- **C.** S3 Transfer Acceleration is for **upload performance**, not ideal for web app delivery. Lambda doesn't provide global low-latency like Lambda@Edge.
- **D.** AWS Directory Service and Elastic Beanstalk **add operational overhead** and cost, making it less suitable for a lightweight, serverless solution.

---

### 🔗 References:
- [Amazon Cognito Overview](https://docs.aws.amazon.com/cognito/latest/developerguide/what-is-amazon-cognito.html)  
- [Lambda@Edge](https://docs.aws.amazon.com/lambda/latest/dg/lambda-edge.html)  
- [CloudFront Global Delivery](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/Introduction.html)  
- [ExamTopics Discussion](https://www.examtopics.com/discussions/amazon/view/100341-exam-aws-certified-solutions-architect-associate-saa-c03/)

</details>


## Question #: 07

**Question:**  
A hospital is designing a new application that gathers symptoms from patients. The hospital has decided to use Amazon Simple Queue Service (Amazon SQS) and Amazon Simple Notification Service (Amazon SNS) in the architecture.

A solutions architect is reviewing the infrastructure design. Data must be encrypted at rest and in transit. Only authorized personnel of the hospital should be able to access the data.

**Which combination of steps should the solutions architect take to meet these requirements? (Choose two.)**

**A.** Turn on server-side encryption on the SQS components. Update the default key policy to restrict key usage to a set of authorized principals.  
**B.** Turn on server-side encryption on the SNS components by using an AWS Key Management Service (AWS KMS) customer managed key. Apply a key policy to restrict key usage to a set of authorized principals.  
**C.** Turn on encryption on the SNS components. Update the default key policy to restrict key usage to a set of authorized principals. Set a condition in the topic policy to allow only encrypted connections over TLS.  
**D.** Turn on server-side encryption on the SQS components by using an AWS Key Management Service (AWS KMS) customer managed key. Apply a key policy to restrict key usage to a set of authorized principals. Set a condition in the queue policy to allow only encrypted connections over TLS.  
**E.** Turn on server-side encryption on the SQS components by using an AWS Key Management Service (AWS KMS) customer managed key. Apply an IAM policy to restrict key usage to a set of authorized principals. Set a condition in the queue policy to allow only encrypted connections over TLS.

---

<details>
<summary><strong>✅ Check Answer</strong></summary>

---

### ✅ Correct Answer:  
**B.** Turn on server-side encryption on the SNS components by using an AWS Key Management Service (AWS KMS) customer managed key. Apply a key policy to restrict key usage to a set of authorized principals.  
**D.** Turn on server-side encryption on the SQS components by using an AWS Key Management Service (AWS KMS) customer managed key. Apply a key policy to restrict key usage to a set of authorized principals. Set a condition in the queue policy to allow only encrypted connections over TLS.

---

### 📘 Explanation:

#### ✅ Why B and D are Correct:
- **Server-side encryption using KMS** allows control of key usage and management, fulfilling compliance needs.
- **Applying key policies** restricts decryption access to only **authorized personnel**.
- **Setting TLS-only policies** ensures encryption **in transit**.
- This approach meets the requirements for **data encryption at rest and in transit** and restricts access based on hospital roles.

#### 🚫 Why the other options are incorrect:

- **A.** Uses the **default key policy**, which may not sufficiently restrict access to authorized personnel.
- **C.** Only updates **default key policy** and sets TLS condition but doesn’t enforce use of **customer managed KMS key**, which is required.
- **E.** IAM policies can help restrict actions, but **key policies** are the **preferred method** for fine-grained control over KMS keys.

---

### 🔗 References:
- [Amazon SQS Encryption](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-server-side-encryption.html)  
- [Amazon SNS Encryption](https://docs.aws.amazon.com/sns/latest/dg/sns-server-side-encryption.html)  
- [Using AWS KMS Key Policies](https://docs.aws.amazon.com/kms/latest/developerguide/key-policies.html)  

</details>


## Question #: 08

**Question:**  
A company’s web application consists of an Amazon API Gateway API in front of an AWS Lambda function and an Amazon DynamoDB database. The Lambda function handles the business logic, and the DynamoDB table hosts the data. The application uses Amazon Cognito user pools to identify the individual users of the application. A solutions architect needs to update the application so that only users who have a subscription can access premium content.

**Which solution will meet this requirement with the LEAST operational overhead?**

**A.** Enable API caching and throttling on the API Gateway API.  
**B.** Set up AWS WAF on the API Gateway API. Create a rule to filter users who have a subscription.  
**C.** Apply fine-grained IAM permissions to the premium content in the DynamoDB table.  
**D.** Implement API usage plans and API keys to limit the access of users who do not have a subscription.

---

<details>
<summary><strong>✅ Check Answer</strong></summary>

---

### ✅ Correct Answer:  
**D. Implement API usage plans and API keys to limit the access of users who do not have a subscription.**

---

### 📘 Explanation:

#### ✅ Why D is Correct:
- API Gateway **usage plans and API keys** allow control over API access by associating users with specific plans.
- Ideal for separating **subscription tiers** like free and premium users.
- It is **cost-effective** and **requires minimal operational overhead** to manage.
- API keys can be distributed to Cognito-authenticated users based on subscription status.

#### 🚫 Why the other options are incorrect:

- **A.** API caching and throttling enhance performance and limit traffic but **do not control access** based on subscription.
- **B.** AWS WAF is great for filtering **IP-based or pattern-based threats**, but not for **subscription-based user access control**.
- **C.** Fine-grained IAM is powerful but **adds complexity** and is not well-suited for **rapidly changing user subscription statuses**.

---

### 🔗 References:
- [API Gateway Usage Plans and API Keys](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-api-usage-plans.html)  
- [Amazon Cognito Overview](https://docs.aws.amazon.com/cognito/latest/developerguide/what-is-amazon-cognito.html)  
- [AWS Lambda + API Gateway Patterns](https://docs.aws.amazon.com/lambda/latest/dg/services-apigateway.html)  
- [ExamTopics Discussion](https://www.examtopics.com/discussions/amazon/view/102128-exam-aws-certified-solutions-architect-associate-saa-c03/)

</details>

## Question #: 09

**Question:**  
A solutions architect wants all new users to have specific complexity requirements and mandatory rotation periods for IAM user passwords.

**What should the solutions architect do to accomplish this?**

**A.** Set an overall password policy for the entire AWS account.  
**B.** Set a password policy for each IAM user in the AWS account.  
**C.** Use third-party vendor software to set password requirements.  
**D.** Attach an Amazon CloudWatch rule to the Create_newuser event to set the password with the appropriate requirements.

---

---

<details>
<summary><strong>✅ Check Answer</strong></summary>

---

### ✅ Correct Answer:  
**A. Set an overall password policy for the entire AWS account.**
### 📘 Explanation:

#### ✅ Why A is Correct:
- AWS IAM provides the ability to define a **global password policy** that applies to **all IAM users** in the AWS account.
- The policy supports settings such as:
  - Minimum password length
  - Required character types (uppercase, lowercase, numbers, symbols)
  - Password expiration (rotation)
  - Preventing password reuse
- This ensures **consistent and enforced security standards** across all users.

#### 🚫 Why the other options are incorrect:
- **B.** AWS IAM does not support **per-user password policies**. It can only be set at the account level.
- **C.** Using third-party software adds complexity and is unnecessary since IAM already supports this functionality.
- **D.** CloudWatch cannot automatically enforce or apply IAM password policies through events like `CreateUser`.

---

### 🔗 References:
- [IAM Password Policy Documentation](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_passwords_account-policy.html)  
- [AWS Best Practices for IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html)
- [ExamTopics Discussion](https://www.examtopics.com/discussions/amazon/view/46408-exam-aws-certified-solutions-architect-associate-saa-c02/)

</details>

## Question #: 10

**Question:**   
A company runs a public three-tier web application in a VPC. The application runs on Amazon EC2 instances across multiple Availability Zones. The EC2 instances that run in private subnets need to communicate with a license server over the internet. The company needs a managed solution that minimizes operational maintenance.

**Which solution meets these requirements?**

**A.** Provision a NAT instance in a public subnet. Modify each private subnet’s route table with a default route that points to the NAT instance.  
**B.** Provision a NAT instance in a private subnet. Modify each private subnet’s route table with a default route that points to the NAT instance.  
**C.** Provision a NAT gateway in a public subnet. Modify each private subnet’s route table with a default route that points to the NAT gateway.  
**D.** Provision a NAT gateway in a private subnet. Modify each private subnet’s route table with a default route that points to the NAT gateway.  

---

<details>  
<summary><strong>✅ Check Answer</strong></summary>  

---

### ✅ Correct Answer:  
**C. Provision a NAT gateway in a public subnet. Modify each private subnet’s route table with a default route that points to the NAT gateway.**

---

### 📘 Topic:  
**Designing Secure Applications and Architectures**

---

### 🧠 Explanation:

- **NAT Gateway** is the **managed solution** that allows **instances in a private subnet to access the internet**, without allowing inbound traffic from the internet. It requires minimal operational maintenance compared to NAT instances.
- **NAT Gateway must be in a public subnet** because it needs direct access to the internet through an internet gateway.
- **Private subnets** route internet-bound traffic to the NAT Gateway.

---

### 🚫 Why the other options are incorrect:

- **A.** NAT instances are not managed services and require patching and monitoring — higher operational overhead.
- **B & D.** NAT instances/gateways in **private subnets won't work** because they cannot reach the internet directly.

---

### 🔗 References:

- [AWS NAT Gateway Documentation](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.html)  
- [Amazon VPC Routing Basics](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Route_Tables.html)
- [ExamTopics Discussion](https://www.examtopics.com/discussions/amazon/view/102134-exam-aws-certified-solutions-architect-associate-saa-c03/)

</details>

## Question #: 11

**Question:**   
A company needs to create an Amazon Elastic Kubernetes Service (Amazon EKS) cluster to host a digital media streaming application. The EKS cluster will use a managed node group that is backed by Amazon Elastic Block Store (Amazon EBS) volumes for storage. The company must encrypt all data at rest by using a customer managed key that is stored in AWS Key Management Service (AWS KMS).

**Which combination of actions will meet this requirement with the LEAST operational overhead? (Choose two.)**

**A.** Use a Kubernetes plugin that uses the customer managed key to perform data encryption.  
**B.** After creation of the EKS cluster, locate the EBS volumes. Enable encryption by using the customer managed key.  
**C.** Enable EBS encryption by default in the AWS Region where the EKS cluster will be created. Select the customer managed key as the default key.  
**D.** Create the EKS cluster. Create an IAM role that has a policy that grants permission to the customer managed key. Associate the role with the EKS cluster.  
**E.** Store the customer managed key as a Kubernetes secret in the EKS cluster. Use the customer managed key to encrypt the EBS volumes.

---

<details>
<summary><strong>✅ Check Answer</strong></summary>

---

### ✅ Correct Answers:
**C. Enable EBS encryption by default in the AWS Region where the EKS cluster will be created. Select the customer managed key as the default key.**  
**D. Create the EKS cluster. Create an IAM role that has a policy that grants permission to the customer managed key. Associate the role with the EKS cluster.**

---

### 📘 Explanation:

#### ✅ Why C is Correct:
- AWS allows you to **set a default KMS key for EBS encryption** in a Region.
- Any EBS volume created after this setting—including those by EKS—will be **automatically encrypted** with the specified **customer managed key**.
- This removes the need to handle encryption manually, reducing operational overhead.

#### ✅ Why D is Correct:
- To allow EKS-managed nodes (EC2 instances) to use the customer managed KMS key, you must **grant them IAM permissions**.
- You do this by **attaching a policy** that includes `kms:Encrypt`, `kms:Decrypt`, etc., to the IAM role associated with the EKS node group.

---

#### 🚫 Why the other options are incorrect:

- **A.** Involves using a Kubernetes plugin for encryption, which adds **complexity** and increases operational overhead.
- **B.** You **cannot encrypt an existing unencrypted EBS volume**. You must copy it to a new volume, which increases effort.
- **E.** Storing KMS keys as Kubernetes secrets is insecure and **not recommended by AWS**.

---

### 🔗 References:
- [Amazon EBS Encryption by Default](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EBSEncryption.html)
- [EKS Worker Node IAM Role Permissions](https://docs.aws.amazon.com/eks/latest/userguide/create-node-role.html)
- [Using KMS with EBS](https://docs.aws.amazon.com/kms/latest/developerguide/services-ebs.html)
- [ExamTopics Discussion](https://www.examtopics.com/discussions/amazon/view/102135-exam-aws-certified-solutions-architect-associate-saa-c03/)


</details>

## Question #: 12

**Question:**   
A company has launched an Amazon RDS for MySQL DB instance. Most of the connections to the database come from serverless applications. Application traffic to the database changes significantly at random intervals. At times of high demand, users report that their applications experience database connection rejection errors.

**Which solution will resolve this issue with the LEAST operational overhead?**

**A.** Create a proxy in RDS Proxy. Configure the users’ applications to use the DB instance through RDS Proxy.  
**B.** Deploy Amazon ElastiCache for Memcached between the users’ applications and the DB instance.  
**C.** Migrate the DB instance to a different instance class that has higher I/O capacity. Configure the users’ applications to use the new DB instance.  
**D.** Configure Multi-AZ for the DB instance. Configure the users’ applications to switch between the DB instances.  

---

<details>
<summary><strong>✅ Check Answer</strong></summary>

---

### ✅ Correct Answer:  
**A. Create a proxy in RDS Proxy. Configure the users’ applications to use the DB instance through RDS Proxy.**

---

### 📘 Explanation:

#### ✅ Why A is Correct:
- **Amazon RDS Proxy** is designed to handle **large numbers of unpredictable and spiky database connections**, which is common in **serverless architectures**.
- It **pools and manages connections** efficiently, **reducing connection storms** and **minimizing database load**.
- RDS Proxy **improves application scalability and availability** without needing to manage additional infrastructure.
- It is the **least operational overhead** solution because it's a **fully managed service**.

---

#### 🚫 Why the other options are incorrect:

- **B.** ElastiCache is a caching layer and doesn’t solve **connection management** issues.
- **C.** Upgrading the instance class only temporarily increases capacity and **doesn’t solve connection pooling issues** for serverless apps.
- **D.** Multi-AZ provides **high availability**, but not **connection scaling** or **load management**. Also, apps don't typically switch between DBs manually.

---

### 🔗 References:
- [Amazon RDS Proxy](https://docs.aws.amazon.com/rds/proxy/)
- [Best practices for serverless apps with RDS](https://docs.aws.amazon.com/lambda/latest/dg/services-rds.html)
- [ExamTopics Discussion](https://www.examtopics.com/discussions/amazon/view/102140-exam-aws-certified-solutions-architect-associate-saa-c03/)

</details>

## Question #: 13

**Question:**  
A company has a three-tier application on AWS that ingests sensor data from its users’ devices. The traffic flows through a Network Load Balancer (NLB), then to Amazon EC2 instances for the web tier, and finally to EC2 instances for the application tier. The application tier makes calls to a database.

**What should a solutions architect do to improve the security of the data in transit?**

**A.** Configure a TLS listener. Deploy the server certificate on the NLB.  
**B.** Configure AWS Shield Advanced. Enable AWS WAF on the NLB.  
**C.** Change the load balancer to an Application Load Balancer (ALB). Enable AWS WAF on the ALB.  
**D.** Encrypt the Amazon Elastic Block Store (Amazon EBS) volume on the EC2 instances by using AWS Key Management Service (AWS KMS).

---

<details>
<summary><strong>✅ Check Answer</strong></summary>

---

### ✅ Correct Answer:  
**A. Configure a TLS listener. Deploy the server certificate on the NLB.**

---

### 📘 Explanation:

#### ✅ Why A is Correct:
- To protect **data in transit**, encryption using **TLS (Transport Layer Security)** is essential.
- A **Network Load Balancer** (NLB) supports **TLS listeners**, allowing TLS termination at the load balancer layer.
- You can associate an **SSL/TLS certificate** with the listener, ensuring encrypted traffic between users and the load balancer.

#### 🚫 Why the other options are incorrect:

- **B.** AWS Shield Advanced and AWS WAF protect against **DDoS and web-layer attacks**, but they do **not handle encryption** of data in transit.
- **C.** While an **ALB** supports TLS and WAF, switching to it isn't necessary. An **NLB already supports TLS**, and ALB is typically used for HTTP/HTTPS traffic (Layer 7), which may not apply here.
- **D.** EBS volume encryption protects **data at rest**, not data in transit.

---

### 🔗 References:
- [TLS Listeners for Network Load Balancer](https://docs.aws.amazon.com/elasticloadbalancing/latest/network/create-tls-listener.html)  
- [Data Protection Best Practices](https://docs.aws.amazon.com/whitepapers/latest/aws-overview/security-and-compliance.html#data-in-transit)
- [ExamTopics Discussion](https://www.examtopics.com/discussions/amazon/view/46507-exam-aws-certified-solutions-architect-associate-saa-c02/)

</details>


## Question #: 14

**Question:**  
A solutions architect is creating a new VPC design. There are two public subnets for the load balancer, two private subnets for web servers, and two private subnets for MySQL. The web servers use only HTTPS. The solutions architect has already created a security group for the load balancer allowing port 443 from 0.0.0.0/0. Company policy requires that each resource has the least access required to still be able to perform its tasks.

**Which additional configuration strategy should the solutions architect use to meet these requirements?**

**A.** Create a security group for the web servers and allow port 443 from 0.0.0.0/0. Create a security group for the MySQL servers and allow port 3306 from the web servers security group.  
**B.** Create a network ACL for the web servers and allow port 443 from 0.0.0.0/0. Create a network ACL for the MySQL servers and allow port 3306 from the web servers security group.  
**C.** Create a security group for the web servers and allow port 443 from the load balancer. Create a security group for the MySQL servers and allow port 3306 from the web servers security group.  
**D.** Create a network ACL for the web servers and allow port 443 from the load balancer. Create a network ACL for the MySQL servers and allow port 3306 from the web servers security group.

---

<details>
<summary><strong>✅ Check Answer</strong></summary>

---

### ✅ Correct Answer:  
**C. Create a security group for the web servers and allow port 443 from the load balancer. Create a security group for the MySQL servers and allow port 3306 from the web servers security group.**

---

### 📘 Explanation:

#### ✅ Why C is Correct:
- **Security Groups** are stateful and designed for least privilege access.
- The **web servers should only allow port 443 from the load balancer’s security group**, not from all IPs.
- The **MySQL servers should only allow port 3306 from the web server’s security group**, which enforces the principle of least privilege.
- This ensures **only specific, expected traffic paths are allowed**, minimizing exposure.

#### 🚫 Why the other options are incorrect:

- **A.** Opening port 443 on the web servers to 0.0.0.0/0 is too permissive and violates least privilege.
- **B & D.** Network ACLs are stateless and not ideal for complex, fine-grained security policies like limiting access by security group.

---

### 🔗 References:
- [Security Groups vs Network ACLs](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Security.html)
- [Security Group Best Practices](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html)
- [ExamTopics Discussion](https://www.examtopics.com/discussions/amazon/view/43796-exam-aws-certified-solutions-architect-associate-saa-c02/)

</details>

## Question #: 15

**Question:**  
A new employee has joined a company as a deployment engineer. The deployment engineer will be using AWS CloudFormation templates to create multiple AWS resources. A solutions architect wants the deployment engineer to perform job activities while following the principle of least privilege.

**Which combination of actions should the solutions architect take to accomplish this goal? (Choose two.)**

**A.** Have the deployment engineer use AWS account root user credentials for performing AWS CloudFormation stack operations.  
**B.** Create a new IAM user for the deployment engineer and add the IAM user to a group that has the PowerUsers IAM policy attached.  
**C.** Create a new IAM user for the deployment engineer and add the IAM user to a group that has the AdministratorAccess IAM policy attached.  
**D.** Create a new IAM user for the deployment engineer and add the IAM user to a group that has an IAM policy that allows AWS CloudFormation actions only.  
**E.** Create an IAM role for the deployment engineer to explicitly define the permissions specific to the AWS CloudFormation stack and launch stacks using that IAM role.

---

<details>
<summary><strong>✅ Check Answers</strong></summary>

---

### ✅ Correct Answers:
**D.** Create a new IAM user for the deployment engineer and add the IAM user to a group that has an IAM policy that allows AWS CloudFormation actions only.  
**E.** Create an IAM role for the deployment engineer to explicitly define the permissions specific to the AWS CloudFormation stack and launch stacks using that IAM role.

---

### 📘 Explanation:

#### ✅ Why D is Correct:
- Creating a **dedicated IAM user** and granting **only CloudFormation permissions** aligns with the **principle of least privilege**.
- This ensures the user can perform their job without access to unnecessary services.

#### ✅ Why E is Correct:
- Using an **IAM role** scoped to specific stack operations provides fine-grained control over **what resources and actions** the deployment engineer can access when launching stacks.
- This further enforces least privilege, especially when sensitive resource creation is involved.

---

#### 🚫 Why the other options are incorrect:

- **A.** Root user credentials should **never be used for daily tasks**. They are only for account setup and emergency purposes.
- **B.** PowerUsers have broad permissions and can perform almost all tasks **except IAM and billing**, which is **more access than required**.
- **C.** AdministratorAccess grants **full permissions**, violating the principle of least privilege.

---

### 🔗 References:
- [IAM Best Practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html)
- [AWS CloudFormation Access Control](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/using-iam-template.html)
- [ExamTopics Discussion](https://www.examtopics.com/discussions/amazon/view/102155-exam-aws-certified-solutions-architect-associate-saa-c03/)
</details>

## Question #: 16

A company is deploying a two-tier web application in a VPC. The web tier is using an Amazon EC2 Auto Scaling group with public subnets that span multiple Availability Zones. The database tier consists of an Amazon RDS for MySQL DB instance in separate private subnets. The web tier requires access to the database to retrieve product information.

The web application is not working as intended. The web application reports that it cannot connect to the database. The database is confirmed to be up and running. All configurations for the network ACLs, security groups, and route tables are still in their default states.

**What should a solutions architect recommend to fix the application?**

**A.** Add an explicit rule to the private subnet’s network ACL to allow traffic from the web tier’s EC2 instances.  
**B.** Add a route in the VPC route table to allow traffic between the web tier’s EC2 instances and the database tier.  
**C.** Deploy the web tier’s EC2 instances and the database tier’s RDS instance into two separate VPCs, and configure VPC peering.  
**D.** Add an inbound rule to the security group of the database tier’s RDS instance to allow traffic from the web tier’s security group.

---

<details>
<summary><strong>✅ Check Answer</strong></summary>

---

### ✅ Correct Answer:  
**D. Add an inbound rule to the security group of the database tier’s RDS instance to allow traffic from the web tier’s security group.**

---

### 📘 Explanation:

- By default, security groups are stateful and deny all inbound traffic unless explicitly allowed.
- The default security group allows all outbound traffic, so the web tier can send requests.
- However, the RDS instance’s security group will block inbound traffic if there is no rule allowing traffic from the web tier.
- Adding an inbound rule to the database security group to allow traffic on the MySQL port (usually TCP 3306) from the web tier’s security group allows the web tier to connect successfully.
- Network ACLs and route tables in default state already allow communication within the VPC, so no changes needed there.
- Option A is unnecessary because default NACLs allow all traffic.
- Option B is incorrect because routing between subnets in the same VPC is handled automatically.
- Option C adds unnecessary complexity.

---

### 🔗 References:
- [Security Groups for Your VPC](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html)  
- [Amazon RDS Security Groups](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Overview.RDSSecurityGroups.html)
- [ExamTopics Discussion](https://www.examtopics.com/discussions/amazon/view/102156-exam-aws-certified-solutions-architect-associate-saa-c03/)

</details>