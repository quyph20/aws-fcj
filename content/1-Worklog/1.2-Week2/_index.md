---
title: "Week 2 Worklog"
date: "2025-09-19"
weight: 1
chapter: false
pre: " <b> 1.2. </b> "
---



### Week 2 Objectives:

* The goal is to master the Shared Responsibility model and the core components of IAM.
* Implement setting up Groups/Users under the Least Privilege principle and enable MFA.

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                   | Start Date | Completion Date | Reference Material                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 2   | - Shared Responsibility Model: Clearly differentiated the responsibilities of AWS (Security of the Cloud: physical infrastructure) and User responsibilities (Security in the Cloud: configuration, data). Understood this as the foundational security principle on AWS.                                                                                                   | 	09/15/2025 | 	09/15/2025      |
| 3   | - LBasic IAM Components (Users & Groups): Mastered how to create and manage IAM Users (human identities) and assign them to IAM Groups for centralized, time-saving access management.                                             | 09/16/2025 | 09/16/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Authorization Mechanism (Roles & Policies): Gained a clear understanding of how IAM Policies (JSON documents defining permissions) are created and attached to Roles or Users to precisely define allowed/denied actions on AWS resources. | 09/17/2025 | 08/17/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Principle of Least Privilege: Adopted the Least Privilege principle as a guideline to only grant the minimum necessary permissions to an identity, preventing privilege abuse or leakage.                            | 09/18/2025	 | 09/18/2025	      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - Identity Security with MFA: Understood the importance of Multi-Factor Authentication (MFA) in account protection. Establishing MFA is a mandatory step for enhancing security for critical accounts (Root User and privileged IAM Users).                                                                                     | 09/19/2025 | 09/19/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Week 2 Achievements:

* Configuring IAM Users and Groups: Created an IAM Group named DevTeam and a new IAM User. Assigned the User to the DevTeam Group. Outcome: Confirmed the User automatically inherits the permissions assigned to the Group, simplifying group-based access management.

* Practicing with IAM Policies: Constructed an IAM Policy allowing the User read-only access to specific S3 buckets. Conversely, tested a Policy that denies access to the EC2 service. Outcome: Gained a clear understanding of how Policies function under Implicit Deny and achieved granular access control.

* Security Application Summary: Successfully completed the setup of MFA for critical Users and successfully applied the Least Privilege principle through custom Policies. Outcome: Established a solid security foundation for subsequent deployment weeks.
