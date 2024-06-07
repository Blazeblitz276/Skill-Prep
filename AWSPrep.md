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
