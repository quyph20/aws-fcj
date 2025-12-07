---
title: "Blog 1"
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---


# Implementing Multi-party approval workflows for AWS Backup logically air-gapped vaults

Enterprises today face significant challenges securing backup data during incidents. When backup systems share authentication with production environments, compromised credentials can block access to both environments, leaving enterprises vulnerable during recovery. Enterprises with interconnected environments face heightened risk, where single-approval frameworks provide inadequate protection.

The integration of the Multi-party approval capability with AWS Backup provides a robust solution to this challenge by creating an secure independent access path to backups, making sure that backup data remains accessible even when traditional authentication methods fail and the vault owning account or AWS Organizations becomes compromised. Multi-party approval requires multiple approvers to authorize critical operations, preventing unilateral changes through a distributed decision-making process and ensuring this access path remains secure.

In our earlier post, we covered cyber threats to backup infrastructure, introduced the new Multi-party approval integration with logically air-gapped vaults, and explained the pillars of data protection. In this post, we’ll provide detailed implementation guidance for configuring Multi-party approval workflows, including best practices and practical examples. These guidelines will help you establish secure, resilient recovery mechanisms that maintain access to critical backup data during any scenario – from single-account incidents to enterprise-wide events.


---

## Recovery patterns

In Part 1, we introduced two critical recovery patterns designed to address different scales of security incidents.

The AWS account recovery pattern addresses scenarios where an account hosting a logically air-gapped vault becomes inaccessible. It uses Multi-party approval teams to create an independent access path needing multiple approvers. This enables recovery even when the vault-owning account is compromised and traditional authentication fails.

The AWS Organizations recovery pattern addresses scenarios where an entire Organizations structure is compromised. It establishes separate recovery Organizations with an independent Identity provider, maintaining access to backup data during Organization-wide incidents.

In this post, we’ll show you how to implement steps for both patterns and include best practices.


**Account recovery**

Implementation steps in this post establish Multi-party approval workflows for account recovery scenarios as referenced in the following architecture diagram.  

## Technology Choices and Communication Scope

Prerequisites
This implementation needs a minimum of two AWS accounts in a single Organization.

Workload account: Houses production environment with primary backup vault and plans protecting AWS resources. Copies recovery points to a logically air-gapped vault (preferably in same account or dedicated backup account).

Recovery account: Enables business continuity by requesting access through Multi-party approval to restore critical data when primary systems are compromised.

Before starting implementation, complete the following steps:

Enable AWS Backup and create a backup plan.
Create a logically air-gapped vault.
Have an active AWS Identity Center instance.
Note the Amazon Resource Name (ARN) of the logically air-gapped vault
Configure your Multi-party approval team
In this section we describe the steps to set up the AWS cross-account Multi-party approval workflow.

1. Enable Multi-party approval in the management account.

When you first set up Multi-party approval, it associates with your existing AWS Identity and Access Management (IAM) Identity Center and creates an Approval Portal for managing requests, team invites, and viewing historical decisions (available for up to 1 month).

a) In the Organizations management account, navigate to the Multi-party approval

b) Set-up Multi-party approval to enable the feature, then choose complete setup.

c) In the AWS Backup console, navigate to Settings > Cross-account Management and enable Multi-party approval integration. This is shown in the following figure.

Figure 2- Enable Multi-party approval integration

Figure 2: Enable Multi-party approval integration

2. Create a Multi-party approval team.

a) Navigate to Organizations from your AWS console and choose Multi-party approval from the menu.

b) Create team and provide details of the approval team, with the approval threshold set to a recommended minimum of at least two approvers.

> Best practice: The minimum threshold of trusted (identities) approvers is two, this prevents any single individual from unilaterally accessing backup data.

Figure 3- Multi-party approval creation form

Figure 3: Multi-party approval creation form

3. Accept team invitations.

Each designated approver receives an email notification to join the Multi-party approval team. Alternatively, they can visit the AWS access portal to access the Approval Portal application to view all requests.

a) Follow the invitation link in the email notification. Alternatively, visit the AWS access portal to access the Approval Portal application to view all requests.

b) In the Approval Portal, navigate to the Approval teams tab to locate the pending invitation and Accept.

> Best practice: Make sure that approvers understand their responsibilities and respond promptly. Share the portal link through out-of-band channels for faster access when emails are delayed.

Pending approval team invite for the user to ‘accept’ or ‘decline’

Figure 4: Pending approval team invite for the user to ‘accept’ or ‘decline’

When all of the necessary approvers have accepted, as shown in the preceding figure, the team status changes to Active, as shown in the following figure.

Figure 5- Approval team now in Active state

Figure 5: Approval team now in Active state

4. Share the approval team with target accounts.

Target accounts include all logically air-gapped vault owning accounts and recovery accounts. These accounts need the Multi-party approval team to be shared with them so they can request access to the vaults.

a) Navigate to AWS Resource Access Manager (AWS RAM) in the AWS management account where the team was created, as shown in the following figure. The share currently has to be created within the us-east-1 AWS Region.

Figure 6- AWS RAM form for sharing approval teams

Figure 6: AWS RAM form for sharing approval teams

b) Choose Create resource share.

c) Configure the team details with Multi-party approval team as the resource type, and choose recovery accounts or organizational units (OUs) under Principals in Step 3 of the wizard.

d) Review and Create resource share.

Important: This sharing must be prepared in advance for critical recovery accounts. If not done proactively, this step can only be performed during an incident if the team-owning account is still accessible.

5. Configure Service Control Policies (SCPs) to govern team usage (optional).

You can use SCPs to restrict which approval teams can be associated with your logically air-gapped vaults. This enhances security by preventing unauthorized teams from accessing critical backup vaults.

Example SCP:

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Deny",
      "Action": "backup:AssociateMultiPartyApprovalTeam",
      "Resource": "*",
      "Condition": {
        "ArnNotLike": {
          "backup:MultiPartyApprovalTeamArn": "arn:aws:mpa:region:account-id:approval-team/team-id"
        }
      }
    }
  ]
}
JSON
6. Accept the resource shares in target accounts.

a) In each target account, navigate to AWS Resource Access Manager.

b) Choose Shared with me > Resource shares.

c) Locate the pending invitation and Accept resource share.

Figure 7- Invite for the user to accept or reject the resource share from primary account

Figure 7: Invite for the user to accept or reject the resource share from primary account

7. Associate the approval team with the logically air-gapped vault.

As per the prerequisites, make sure that AWS Backup is enabled in the vault owning account and that you’ve created a logically air-gapped vault with appropriate backup plans.

a) Navigate to the AWS Backup console in the vault owning account.

b) Choose Vaults and choose your existing logically air-gapped vault.

c) Assign approval team by choosing the shared approval team from the dropdown, then choose Submit, as shown in the following figure

Figure 8- Assign approval team to logically air-gapped vault form

Figure 8: Assign approval team to logically air-gapped vault form

For the first time assignment, no approval is needed. Any subsequent changes to the team need the approval of the original team.

> Best practice: Store the vault ARN in multiple secure locations, including offline storage, to make sure of accessibility during recovery scenarios.

> Important: After establishing the vault and approval team association, any changes need a two-step process: either the backup administrator must initiate vault reassignment requests, or team facilitators must initiate team deletion. This needs explicit approval from the existing approval team. Team deletion triggers AWS Backup to remove the team association and any created shares (Restore access backup vault). This enforced workflow makes sure that changes cannot occur unilaterally, thus enhancing security.

Recovery process during accessibility compromise
Next, we cover the recovery steps for when your primary AWS account containing logically air-gapped backup vaults becomes inaccessible due to a security incident or credential compromise.

8. Initiate recovery though vault sharing request from one or many recovery accounts.

a) From the recovery account, navigate to the AWS Backup console.

b) Choose Vaults > Vaults accessible through Multi-party approval.

c) Request vault access and enter the ARN of the logically air-gapped vault in the request form, as shown in the following figure.

Figure 9- Form to request access to logically air-gapped vault

Figure 9: Form to request access to logically air-gapped vault

d) Provide a descriptive restore access backup vault name that is created (optional but recommended for easier identification).

e) Submit the request.

> Best practice: Include comprehensive information in your justification to help approvers understand the context and urgency of the request.

9. Approve the recovery request using Multi-party approval workflow.

Approvers receive email notifications about the pending request.

a) Approvers can follow the link in the email or access the Approval Portal through AWS Identity Center, as shown in the following figure.

b) Review the Requested operations tab, and Approve or Reject based on your assessment.

Figure 10- Recovery request approval invite

Figure 10: Recovery request approval invite

When the approval threshold is met, the status changes to Approved and the logically air-gapped vault becomes accessible in the recovery account as a read-only restore access backup vault, as shown in the following figure.

 Figure 11- Logically air-gapped vault now available for recovery operations

Figure 11: Logically air-gapped vault now available for recovery operations

> Best practice: While access requests can only come from AWS Accounts with an established RAM share, approvers should still verify the legitimacy and urgency of the request through out-of-band communication channels before approving.

10. Perform recovery operations.

a) In the recovery account, navigate to the AWS Backup console and choose Vaults.

b) Under the Vaults accessible through Multi-party approval, the newly accessible vault appears under Restore access backup vaults.

c) Browse recovery points from the source logically air-gapped vault.

d) Choose a Recovery point, choose Restore operation, and complete the recovery, as shown in the following figure.

> Best practice: Consider copying select recovery points to alternate accounts/Regions. Document the recovery process and challenges to improve future procedures.

 Figure 12- Recovery points to restore or copy from the logically air-gapped vault

Figure 12: Recovery points to restore or copy from the logically air-gapped vault

More Multi-party approval management workflows
Beyond recovery scenarios, Multi-party approval also supports ongoing vault management through two more key workflows:

Changing Team Assignment: From the vault-owning account (AWS Backup > Vaults), choose the vault, and Request approval team change. Choose the new team and Send request. The current approval team must approve this request.

Revoking Access: In the vault-owning account (AWS Backup > Vaults), choose the vault, and navigate to the Access through multi-party approval section. Find the Restore access backup vault, choose Request to remove vault access, and choose Send request. The current approval team must approve this request.

Organization recovery
In this section we cover the implementation steps needed to establish Multi-party approval workflows for cross-Organization recovery scenarios as referenced in the following architecture diagram.

Figure 13- Cross-Organization Multi-party approval workflow

Figure 13: Cross-Organization Multi-party approval workflow

Prerequisites
This implementation needs a minimum of two AWS accounts in two different Organizations.

Before we dive into the implementation, make sure that you already have the following:

Enabled AWS Backups and created a backup plan
Created a logically air-gapped vault 
Noted the ARN of the logically air-gapped vault, because this is needed during the recovery steps
Established a recovery Organization
Set up an independent IdP
> Best practice: Use a different IdP vendor than primary to avoid shared dependencies. This IdP only needs to maintain Multi-party approvers, not a full implementation.

Configure your Multi-party approval team
In this section we describe the steps to set up the cross-Organization Multi-party approval workflow.

In your recovery Organization, complete Steps 1-3 from the Account recovery section, adding approvers from your external IdP when creating the team, then continue to Step 4. You can also apply the principle of least privilege using SCPs to restrict which teams can be associated with logically air-gapped vaults.

4. Share the approval team with the primary Organization.

a) In the recovery Organization, navigate to AWS RAM.

b) Choose Create resource share.

c) Configure the resource share and choose Multi-party approval team as the resource type, as shown in the following figure.

Figure 14- Resource share of the Multi-party approval team form

Figure 14: Resource share of the Multi-party approval team form

d) Under Grant access to principals, choose Allow sharing with anyone and enter account ID of the AWS account hosting your logically air-gapped vault in the primary Organization.

e) Review and Create resource share.

> Best practice: Test cross-Organization sharing during regular recovery drills, as shown in the following figure.

Figure 15- Resource share to grant access to resources cross-Organization

Figure 15: Resource share to grant access to resources cross-Organization

5. Accept the resource share in the primary Organization.

a) In the primary Organization’s account hosting the logically air-gapped vault, navigate to AWS RAM.

b) Choose Shared with me > Resource shares.

c) Locate the pending invitation from the recovery Organization and Accept resource share. When it is accepted, the approval team from the recovery Organization is available for use, as shown in the following figure.

> Best practice: Verify the resource share details carefully before accepting to make sure that it’s from your legitimate recovery Organization.

Figure 16- Request to approve Multi-party approval team share cross-Organization

Figure 16: Request to approve Multi-party approval team share cross-Organization

6. Associate the approval team with the logically air-gapped vault.

a) Navigate to the AWS Backup console in the vault owning account.

b) Choose the existing logically air-gapped vault and choose Assign approval team, as shown in the following figure.

Figure 17- Form to assign approval team to logically air-gapped vault that you want to recover

Figure 17: Form to assign approval team to logically air-gapped vault that you want to recover

c) Choose the shared approval team from the recovery Organization and choose Submit.

> Best practice: Verify the association is successful and test the approval workflow before an actual incident occurs.

Recovery process during accessibility compromise
Next, we cover the recovery steps for when your primary Organization containing logically air-gapped backup vaults becomes inaccessible due to a security incident or credential compromise.

7. Initiate vault sharing request.

a) From a recovery account in the recovery Organization, navigate to AWS Backup.

b) Choose Vaults > Vaults Accessible Through Multi-party approval.

c) Choose Request vault access and enter the ARN of the logically air-gapped vault in the request form, as shown in the following figure.

Figure 18- Form to request access to the logically air-gapped vault that you want to recover

Figure 18: Form to request access to the logically air-gapped vault that you want to recover

d) Provide a descriptive Restore Access Backup Vault name that is created (optional but recommended for easier identification).

e) Submit the request.

> Best practice: Include comprehensive information in your justification to help approvers understand the context and urgency of the Organization-wide recovery scenario.

8. Execute Multi-party approval workflow.

Approvers in the recovery Organization receive email notifications about the pending request.

a) Approvers can follow the link in the email or alternatively access the Multi-party Approval Portal through the external IdP and review the details in the Operations tab.

b) Approvers can Approve or Reject based on their assessment.

> Best practice: Establish clear criteria for what constitutes a valid Organization-wide recovery scenario to help approvers make informed decisions quickly.

9. Perform recovery operations.

When the minimum threshold of approvals is reached, the logically air-gapped vault from the primary Organization becomes accessible in the recovery account.

a) In the recovery account within the recovery Organization, navigate to AWS Backup > Backup vaults.

b) The newly accessible Restore access backup vault appears in your vault list under Vaults accessible through Multi-party approval.

c) Browse recovery points from the source logically air-gapped vault in the primary Organization and choose a recovery point to Restore, as shown in the following figure.

> Best practice: Document the recovery process and lessons learned to improve future Organization-wide recovery procedures.

Figure 19- Recovery points to restore or copy from the logically air-gapped vault

Figure 19: Recovery points to restore or copy from the logically air-gapped vault

Conclusion
Using Multi-party approval with AWS Backup and implementing it across cross-account or cross-Organization setups provides you with a highly resilient, layered recovery posture. The steps outlined in this guide allow you to establish a resilient recovery mechanism that operates independently of your primary authentication infrastructure.

This implementation addresses the fundamental challenge of maintaining access to your backups when your primary environment is compromised. The distributed approval process makes sure that no single individual can unilaterally access backup data, while the separate identity infrastructure for Organization recovery provides the highest level of resilience.

Your recovery strategy must be regularly exercised to remain effective. Incorporate these workflows into your disaster recovery testing, document the procedures clearly, and train your teams on both the technical implementation and approval processes. Baseline your teams regularly so that the teams remain functional with minimum approvers being available, making sure that they’re not impacted by staff departures or role changes.

As cyber threats continue to evolve, the ability to recover quickly and completely becomes increasingly critical. Multi-party approval for AWS Backup logically air-gapped vaults provides the tools needed to protect your enterprise’s most valuable asset—its data.