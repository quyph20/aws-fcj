---
title: "Week 7 Worklog"

weight: 1
chapter: false
pre: " <b> 1.7. </b> "
---



### Week 7 Objectives:

* Differentiate storage types (Object/S3, Block/EBS, NoSQL/DynamoDB, Relational/RDS) and S3 storage classes.
* Practice deploying a Multi-AZ RDS Instance and setting up the S3 lifecycle policy.

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                   | Start Date | Completion Date | Reference Material                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 2   | - Object Storage (S3): Clearly understood Amazon Simple Storage Service (S3) as a durable, highly available object storage service. Grasped the different S3 Storage Classes (Standard, IA, Glacier) and their respective use cases.                                                                                                   | 10/20/2025 | 10/20/2025      |
| 3   | - Block and File Storage: Differentiated between Amazon Elastic Block Store (EBS) (block storage) used for EC2 Instances and Amazon Elastic File System (EFS) (file storage) used for shared workloads.                                              | 10/21/2025 | 10/21/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Relational Database (RDS): Understood Amazon Relational Database Service (RDS) as a managed relational database service. Grasped the benefits of managed services (patching, backup, Multi-AZ) and supported Engines (PostgreSQL, MySQL, Aurora). | 10/22/2025 | 10/22/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - NoSQL Database (DynamoDB): Grasped Amazon DynamoDB as a scalable and high-performance Key-Value NoSQL database service. Understood the concepts of Partition Key and Sort Key.                            | 10/23/2025 | 10/23/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - Data Migration Strategies: Understood the tools and services used to migrate large volumes of data or extend storage from on-premises to AWS (e.g., AWS Snow Family, AWS Storage Gateway).                                                                                     | 10/24/2025 | 10/24/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Week 7 Achievements:

* S3 Data Lifecycle Management: Practiced creating an S3 Bucket, configuring a Bucket Policy to block public access. Set up a Lifecycle Rule to automatically transition older objects (e.g., after 30 days) from S3 Standard to S3 Standard-IA for cost optimization.

* Relational Database System Deployment: Launched an RDS Instance (using PostgreSQL engine) within a Private Subnet (from Week 6). Configured Multi-AZ for high availability and set up a Security Group to allow connections only from the application-tier EC2 Instance.

* High-Performance NoSQL Database Setup: Created a new DynamoDB Table. Defined appropriate Partition Key and Sort Key based on a simulated data access pattern. Performed basic PutItem, GetItem, and Query operations to test latency.

* Storage Cost & Performance Analysis: Compared the cost and I/O performance between EBS gp3 (General Purpose SSD) and EBS io2 (Provisioned IOPS SSD). Evaluated when to prioritize the 11 nines durability of S3 versus the strong consistency of RDS.

* Storage & Data Application Summary: Successfully completed the setup of critical storage and database services. Outcome: Gained the ability to make accurate architectural decisions when selecting storage services (Object, Block, File) and data services (Relational, NoSQL) based on application requirements for structure, performance, and cost.

