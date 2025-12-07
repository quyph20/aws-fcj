---
title: "Week 6 Worklog"

weight: 1
chapter: false
pre: " <b> 1.6. </b> "
---



### Week 6 Objectives:

* The goal is to understand and self-configure a layered Virtual Private Cloud (VPC).
* Practice creating Public/Private Subnets, and configuring the Internet Gateway and NAT Gateway for a secure network.

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                   | Start Date | Completion Date | Reference Material                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 2   | - VPC Concept: Clearly understood Amazon Virtual Private Cloud (VPC) as the core networking platform of AWS, allowing the creation of a logically isolated, customizable virtual network within the public cloud.                                                                                                   | 10/13/2025 | 10/13/2025      |
| 3   | - Subnet Partitioning: Grasped the concept of Subnets and their role in network partitioning. Differentiated between Public Subnets (for public-facing resources) and Private Subnets (for internal, secured resources).                                              | 10/14/2025 | 10/14/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Routing and Internet Gateway: Understood the role of the Internet Gateway (IGW). Grasped how the Route Table directs traffic between Subnets and the IGW. | 10/15/2025 | 10/15/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Network-Level Security (Security Groups & NACLs): Differentiated between Security Groups (SG) (instance-level firewall) and Network Access Control Lists (NACLs) (subnet-level firewall).                            | 10/16/2025 | 10/16/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - N.A.T Gateway: Understood the role of the NAT Gateway in allowing Instances in a Private Subnet to access the Internet without exposing their private IP addresses externally.                                                                                     | 10/17/2025 | 10/17/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Week 6 Achievements:

* Multi-AZ VPC and Subnet Setup: Launched a new VPC with a custom CIDR block. Created Public and Private Subnets spanning at least two Availability Zones to ensure High Availability.

* Internet Routing Configuration: Configured the Internet Gateway and the Main Route Table to ensure traffic from the Public Subnet is routed correctly to the Internet.

* Internal Network NAT Setup: Launched a NAT Gateway and placed it within the Public Subnet. Created a dedicated Route Table for the Private Subnet, routing outbound traffic through the NAT Gateway instead of the IGW.

* Dual Security Layer Deployment: Set up Network ACLs to control inbound/outbound traffic at the Subnet level and configured a restrictive Security Group to allow only necessary ports for EC2 Instances within the Private Subnet.

* Networking Application Summary and Testing: Launched test Instances in both Subnets and verified: Public Instances are accessible from the Internet; Private Instances can ping the Internet (via NAT) but are not directly accessible from outside. Outcome: Successfully created a secured, layered network architecture.

