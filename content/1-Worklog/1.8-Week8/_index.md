---
title: "Week 8 Worklog"

weight: 1
chapter: false
pre: " <b> 1.8. </b> "
---


### Week 8 Objectives:

* Understand Load Balancer types (ALB, NLB) and their role in traffic distribution.
* Practice configuring an Auto Scaling Group (ASG) based on CPU metrics to achieve high availability and elastic scalability.
### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                   | Start Date | Completion Date | Reference Material                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 2   | - Load Balancing Concept (ELB): Clearly understood Elastic Load Balancing (ELB) as a service that distributes incoming network traffic across multiple targets over multiple Availability Zones to increase availability and fault tolerance.                                                                                                   | 10/27/2025 | 10/27/2025      |
| 3   | - Differentiating Load Balancer Types: Distinguished the three main types of Load Balancers: Application Load Balancer (ALB) (Layer 7, HTTP/HTTPS), Network Load Balancer (NLB) (Layer 4, TCP/UDP), and Gateway Load Balancer (GLB).                                              | 10/28/2025 | 10/28/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Auto Scaling Concept (ASG): Grasped the Auto Scaling Group (ASG) as a logical grouping of EC2 Instances that automatically adjusts the number of Instances based on load demand. | 10/29/2025 | 10/29/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Scaling Strategies: Distinguished the scaling strategies in ASG: Target Tracking Scaling (maintaining a metric at a target value), Simple Scaling (threshold-based), and Step Scaling (scaling up or down in steps).                            | 10/30/2025 | 10/30/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | Health Checks and Sticky Sessions: Understood the role of Health Checks in verifying and automatically removing unhealthy Instances. Grasped the concept of Sticky Sessions and its impact on load distribution.                                                                                     | 10/31/2025 | 10/31/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Week 8 Achievements:

* Application Load Balancer (ALB) Configuration: Launched a Multi-AZ ALB and configured a Listener (port 80). Created a Target Group pointing to the application-tier EC2 Instances in the Private Subnet.

* Auto Scaling Group (ASG) Deployment: Set up a Launch Template for EC2 Instances, then created an ASG with Min/Max/Desired Capacity parameters. Placed the ASG to run across the Private Subnets.

* CPU-Based Scaling Policy Configuration: Configured a Target Tracking Scaling Policy for the ASG, setting the target to maintain an average CPU utilization of 60%. Outcome: Confirmed the ASG automatically scales out when CPU load increases and scales in when the load decreases.

* Fault Tolerance Testing: Simulated failure by manually terminating one of the running EC2 Instances. Outcome: The ASG automatically detected the failure via Health Check and launched a replacement Instance, confirming the architecture's self-healing capability.

* Availability Application Summary: Successfully completed the setup of the load balancing and auto-scaling system. Outcome: The application system now possesses High Availability (HA) and Elastic Scalability, capable of handling sudden load spikes and self-recovering from Instance failures.
