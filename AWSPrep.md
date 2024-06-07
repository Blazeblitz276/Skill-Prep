# AWS Cloud Computing

## Domains of AWS Services

- Compute
- Storage
- Database
- Networking

## Global Infrastructure

AWS has a global infrastructure that is divided into regions and availability zones. A region is a geographical area that consists of two or more availability zones. An availability zone is a data center that is isolated from other data centers in the same region. Each availability zone is connected to the other availability zones in the same region through a low-latency network. This allows you to build highly available and fault-tolerant applications.

Apart from regions and availability zones, AWS also has edge locations. Edge locations are used by the CloudFront service to cache content closer to the end-users. This reduces latency and improves the performance of web applications. CloudFront is a content delivery network (CDN) service that delivers content to users based on their geographical location.

## AWS Compute Services

AWS provides several compute services that allow you to run applications in the cloud. Some of the key compute services are:

- Amazon EC2 (Elastic Compute Cloud): A web service that provides resizable compute capacity in the cloud. You can launch virtual servers, known as instances, on EC2 and run applications on them.
- AWS Lambda: A serverless compute service that allows you to run code without provisioning or managing servers. You can upload your code to Lambda and it will automatically scale and run in response to events.
- Amazon ECS (Elastic Container Service): A container orchestration service that allows you to run and manage Docker containers on a cluster of EC2 instances.
- AWS Batch: A service that allows you to run batch computing workloads on the cloud. You can submit batch jobs to AWS Batch and it will automatically provision the necessary compute resources to run the jobs.
- Amazon Lightsail: A virtual private server (VPS) service that allows you to launch and manage virtual servers in the cloud. Lightsail is designed for developers who want a simple and cost-effective way to run applications in the cloud.

## AWS Storage Services

AWS provides several storage services that allow you to store and retrieve data in the cloud. Some of the key storage services are:

- Amazon S3 (Simple Storage Service): An object storage service that allows you to store and retrieve any amount of data at any time. You can use S3 to store files, images, videos, and other types of data.
- Amazon EBS (Elastic Block Store): A block storage service that allows you to create and attach storage volumes to EC2 instances. You can use EBS volumes as primary storage for your EC2 instances.
- Amazon EFS (Elastic File System): A file storage service that allows you to create and mount file systems on EC2 instances. You can use EFS to share files between multiple EC2 instances.
- Amazon Glacier: A low-cost storage service that is designed for data archiving and long-term backup. You can use Glacier to store data that is infrequently accessed and needs to be retained for a long period of time.

## AWS Database Services

AWS provides several database services that allow you to store and retrieve structured data in the cloud. Some of the key database services are:

- Amazon RDS (Relational Database Service): A managed database service that allows you to run relational databases in the cloud. You can use RDS to run MySQL, PostgreSQL, Oracle, SQL Server, and MariaDB databases.
- Amazon DynamoDB: A NoSQL database service that allows you to store and retrieve unstructured data in the cloud. You can use DynamoDB to build highly scalable and low-latency applications.
- Amazon Redshift: A data warehousing service that allows you to run analytics queries on large datasets. You can use Redshift to analyze data from multiple sources and generate insights for your business.
- Amazon ElastiCache: A caching service that allows you to store and retrieve data in memory. You can use ElastiCache to improve the performance of web applications by caching frequently accessed data.

## AWS Networking Services

AWS provides several networking services that allow you to connect resources in the cloud and build scalable and secure applications. Some of the key networking services are:

- Amazon VPC (Virtual Private Cloud): A virtual network that allows you to launch AWS resources in a logically isolated section of the cloud. You can create subnets, route tables, and security groups in a VPC to control the traffic flow between resources.
- Amazon Route 53: A domain name system (DNS) service that allows you to route traffic to AWS resources based on domain names. You can use Route 53 to register domain names, manage DNS records, and configure health checks for your applications.
- AWS Direct Connect: A dedicated network connection that allows you to connect your on-premises data center to AWS. You can use Direct Connect to establish a private and secure connection to AWS resources without going over the public internet.
- AWS CloudFront: A content delivery network (CDN) service that allows you to deliver content to users with low latency and high transfer speeds. You can use CloudFront to cache content at edge locations and improve the performance of web applications.

## AWS Security Services

AWS provides several security services that allow you to secure your applications and data in the cloud. Some of the key security services are:

- AWS Identity and Access Management (IAM): A service that allows you to manage access to AWS resources securely. You can create users, groups, and roles in IAM and assign permissions to them to control who can access your resources.
- AWS Key Management Service (KMS): A service that allows you to create and manage encryption keys to protect your data. You can use KMS to encrypt data at rest and in transit and control access to your encrypted data.
- AWS Shield: A managed Distributed Denial of Service (DDoS) protection service that helps protect your applications from DDoS attacks. You can use Shield to detect and mitigate DDoS attacks and ensure the availability of your applications.
- AWS WAF (Web Application Firewall): A web application firewall that allows you to protect your web applications from common web exploits. You can use WAF to monitor and filter HTTP and HTTPS requests to your applications and block malicious traffic.

## AWS Management Services

AWS provides several management services that allow you to monitor, automate, and optimize your cloud resources. Some of the key management services are:

- Amazon CloudWatch: A monitoring service that allows you to collect and track metrics, monitor logs, and set alarms for your AWS resources. You can use CloudWatch to monitor the performance of your applications and infrastructure.
- AWS CloudFormation: An infrastructure as code service that allows you to create and manage AWS resources using templates. You can use CloudFormation to automate the deployment of your applications and infrastructure.
- AWS Systems Manager: A management service that allows you to automate administrative tasks and manage your AWS resources. You can use Systems Manager to configure and maintain your EC2 instances, manage patching and compliance, and automate workflows.
- AWS Trusted Advisor: An optimization service that provides recommendations to help you optimize your AWS resources. You can use Trusted Advisor to reduce costs, improve performance, and increase security by following best practices.

## AWS Developer Tools

AWS provides several developer tools that allow you to build, test, and deploy applications in the cloud. Some of the key developer tools are:

- AWS CodeCommit: A source control service that allows you to store and manage code repositories in the cloud. You can use CodeCommit to collaborate with other developers and manage your source code.
- AWS CodeBuild: A build service that allows you to compile and test code in the cloud. You can use CodeBuild to automate the build process and generate artifacts for your applications.
- AWS CodeDeploy: A deployment service that allows you to automate the deployment of applications to EC2 instances, Lambda functions, and on-premises servers. You can use CodeDeploy to deploy code changes with minimal downtime and monitor the deployment process.
- AWS CodePipeline: A continuous integration and continuous deployment (CI/CD) service that allows you to automate the release process for your applications. You can use CodePipeline to build, test, and deploy code changes across multiple environments.
- AWS X-Ray: A debugging and tracing service that allows you to analyze and debug distributed applications. You can use X-Ray to trace requests as they travel through your application and identify performance bottlenecks.
- AWS SDKs: Software development kits (SDKs) that allow you to interact with AWS services from your applications. You can use SDKs to access AWS services programmatically and build applications that integrate with AWS services.

## AWS AI and Machine Learning Services

AWS provides several AI and machine learning services that allow you to build intelligent applications in the cloud. Some of the key AI and machine learning services are:

- Amazon SageMaker: A fully managed machine learning service that allows you to build, train, and deploy machine learning models. You can use SageMaker to build predictive models, analyze data, and generate insights for your business.
- Amazon Rekognition: A deep learning-based image and video analysis service that allows you to analyze and recognize objects, scenes, and faces in images and videos. You can use Rekognition to build applications that can automatically tag and search images and videos.
- Amazon Polly: A text-to-speech service that allows you to convert text into lifelike speech. You can use Polly to build applications that can read text aloud and provide voice-enabled interfaces.
- Amazon Lex: A conversational interface service that allows you to build chatbots and voice-enabled applications. You can use Lex to create natural language understanding models and integrate them with your applications.
- Amazon Comprehend: A natural language processing service that allows you to analyze text and extract insights from it. You can use Comprehend to identify key phrases, entities, and sentiment in text data.
- Amazon Translate: A neural machine translation service that allows you to translate text between languages. You can use Translate to build applications that can translate text in real-time and support multilingual communication.

## Compute using Server and Serverless Services

- **Server-based computing**: In server-based computing, you provision virtual servers, known as instances, on AWS EC2 and run applications on them. You have full control over the servers and can customize them based on your requirements. You pay for the compute capacity that you provision, regardless of whether the servers are running or not.

- **Serverless computing**: In serverless computing, you run code without provisioning or managing servers. You upload your code to AWS Lambda and it automatically scales and runs in response to events. You pay only for the compute time that your code consumes, without worrying about the underlying infrastructure. Eg. AWS Lambda which will trigger the code based on the events.

![AWS Compute Scenario](ReferImgs/AWSComputes.png)

## Storage Services using Direct and Archival Storage

The storage types provided by AWS are:
Direct Storage: Amazon S3, Amazon EBS, Amazon EFS
Archival Storage: Amazon Glacier

- **Amazon S3 (Simple Storage Service)**: An object storage service that allows you to store and retrieve any amount of data at any time. You can use S3 to store files, images, videos, and other types of data. S3 is highly durable, scalable, and secure. You can control access to your S3 buckets using bucket policies and access control lists (ACLs).

- **Amazon EBS (Elastic Block Store)**: A block storage service that allows you to create and attach storage volumes to EC2 instances. You can use EBS volumes as primary storage for your EC2 instances. EBS volumes are persistent and can be detached from one EC2 instance and attached to another EC2 instance. You can take snapshots of your EBS volumes to back up your data and create new volumes from the snapshots.

- **Amazon EFS (Elastic File System)**: A file storage service that allows you to create and mount file systems on EC2 instances. You can use EFS to share files between multiple EC2 instances. EFS file systems are highly available and scalable. You can mount an EFS file system on multiple EC2 instances and access the same files from all the instances.

- **Amazon Glacier**: A low-cost storage service that is designed for data archiving and long-term backup. You can use Glacier to store data that is infrequently accessed and needs to be retained for a long period of time. Glacier provides three retrieval options: Expedited, Standard, and Bulk. You can choose the retrieval option based on your requirements.

![AWS Storage Scenario](ReferImgs/Storage.png)!

## Database Services using Relational and NoSQL Databases

The database services provided by AWS are:

- **Relational Databases**: Amazon RDS - The relational database service allows you to run relational databases in the cloud. You can use RDS to run MySQL, PostgreSQL, Oracle, SQL Server, and MariaDB databases. RDS manages routine database tasks such as provisioning, patching, backup, recovery, and scaling. You can use RDS to build scalable and highly available database applications.

- **NoSQL Databases**: Amazon DynamoDB - The NoSQL database service allows you to store and retrieve unstructured data in the cloud. You can use DynamoDB to build highly scalable and low-latency applications. DynamoDB is a fully managed service that provides seamless scalability, high availability, and low latency. You can use DynamoDB to build real-time applications that require high performance and low latency.
