---
title: "Week 9 Worklog"

weight: 1
chapter: false
pre: " <b> 1.9. </b> "
---


### Week 9 Objectives:

* The goal is to master monitoring (CloudWatch Metrics, Logs) and notification (SNS) services.
* Practice configuring CloudWatch Alarms, an SNS Topic, and using Systems Manager for remote operational management.

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                   | Start Date | Completion Date | Reference Material                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 2   | - Core Monitoring Service (CloudWatch): Clearly understood Amazon CloudWatch as the central service for resource monitoring and management, collecting Metrics, Logs, and Events from AWS and applications.                                                                                                   | 11/03/2025 | 11/03/2025      |
| 3   | - Differentiating Metrics and Logs: Clearly distinguished between Metrics (time-series numerical data, e.g., CPU Utilization) and Logs (detailed text data recording activity). Grasped how CloudWatch collects both types.                                              | 11/04/2025 | 11/04/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Configuring Alarms: Understood how to create CloudWatch Alarms based on Metric thresholds (e.g., CPU > 80% for 5 minutes). Grasped how Alarms can trigger automatic Actions via SNS or Auto Scaling. | 11/05/2025 | 11/05/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Notification Service (SNS): Grasped Amazon Simple Notification Service (SNS) as a managed messaging service used to send messages to various Subscriptions (email, SMS, Lambda, SQS) upon an event (e.g., an alarm).                            | 11/06/2025 | 11/06/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - Operational Management Tool: Introduced AWS Systems Manager (SSM) as a suite of tools to automate operational tasks such as OS patching, remote command execution (Run Command), and configuration management.                                                                                     | 11/07/2025 | 11/07/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Week 9 Achievements:

* CloudWatch Alarms Configuration: Created a CloudWatch Alarm for the EC2 Instance in the VPC (from Week 6), setting the alert threshold when CPU Utilization exceeds 75% consistently for 5 minutes.

* Notification Channel Setup (SNS Topic): Launched a new SNS Topic and configured an Email Subscription. Outcome: Confirmed receiving an email notification immediately when the Alarm transitioned to the ALARM state.

* Centralized Log Management: Configured the CloudWatch Agent on the EC2 Instance to collect custom application logs and stream them to CloudWatch Logs. Outcome: Gained the ability to monitor application logs from a centralized dashboard.

* Performing Operational Tasks with SSM: Used AWS Systems Manager Run Command to execute a simple shell command (e.g., checking kernel version) on an EC2 Instance without direct SSH access. Outcome: Confirmed the capability for secure and centralized resource management.

* Monitoring Application Summary: Successfully completed the setup of monitoring, alerting, and operational automation tools. Outcome: The system gained the ability to proactively track performance, react quickly to incidents, and maintain high resource health.

