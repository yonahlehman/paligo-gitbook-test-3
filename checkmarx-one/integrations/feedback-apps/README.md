# Feedback Apps

## Feedback Apps Overview

The Feedback Apps feature allows Checkmarx One users to integrate with external **Bug Tracking** and **Alerting** services.

**Bug Tracking** services include Jira, GitHub Issue, and Azure DevOps Bug Board. Integration with these supported services enables Checkmarx One users to automate the creation, modification, and closure of tickets.

**Alerting** services include Slack, Microsoft Teams, and Email notification services. The integration with these services serves as a way of alerting other team members about found vulnerabilities by sending a scan summary report to the respective channels. The report includes a results summary which presents the number of detected vulnerabilities in the scanned code. In addition, you can receive alerts when a newly discovered SCA vulnerability is detected in a package that is used in your projects.

{% hint style="info" %}
If you delete a Feedback App, then the tickets created by that app will automatically be closed. However, this behavior is not supported for GitHub Issues.
{% endhint %}

### Limitations

- Currently supported only for vulnerabilities identified by SAST, IaC Security, SCA and Container Security scanners. This may cause a discrepancy between the summary counters shown in Checkmarx One and the ones sent via Feedback App.
- Maximum bug tracking tickets created **per scanner** is 2,000. If a scanner identifies more than 2,000 results (that fit the trigger conditions) in a scan, then the excess results won't have tickets created for them. Priority is given to higher severity results, so that if a SAST scan has 1,000 critical + 1,000 high + 1,000 medium results, tickets will only be opened for the critical and high results.

## Feedback Profiles Overview

**Feedback Profiles** are entities in Checkmarx One where users can assign Feedback Apps and Projects. Users have the flexibility to assign either a single Feedback App or multiple Feedback Apps to a specific Feedback Profile. For example, by assigning multiple Feedback Apps to a Feedback Profile, a ticket can be opened in Jira while simultaneously triggering an alert in a Slack channel. Additionally, users can assign the same Feedback App to multiple Feedback Profiles.

The Projects assigned to a Feedback Profile can be either repository-based or ZIP-based Projects. A repository-based Project can be an automated Project (Code Repository integration Project) or a manually created one. If an automated repository-based Project is assigned to a Feedback Profile, tickets will be opened only for the **Protected Branches** configured during the code repository integration process.

On the other hand, assigning a manually created repository-based Project to a Feedback Profile follows a different process. For more information refer to [Assigning a Feedback Profile to a Checkmarx Project - Repository path scans](assigning-a-feedback-profile-to-a-checkmarx-project---repository-path-scans.md).

For *ZIP file* scans, Feedback Apps are triggered only for the branch that is **Set as Primary**. If the ZIP file doesn't contain a branch, Feedback Apps will be triggered for the entire file content. In pipeline scans, including plugins, Checkmarx One enables the Feedback App only for branches selected as **Primary**, which needs to be done manually from the UI. For more information about how to set a branch as Primary, refer to SAST Scanner.

## Permissions

To execute various actions in the Feedback Apps feature, a user needs to be assigned one of the following permissions:

- **create-feedbackapp** - Create feedback apps and feedback profiles.
- **manage-feedbackapp** - Update, delete, create and view feedback apps and feedback profiles.
- **update-feedbackapp** - Update feedback apps and feedback profiles.
- **view-feedbackapp** - View feedback apps and feedback profiles.
- **delete-feedbackapp** - Delete feedback apps and feedback profiles.

## Feedback Apps Flow

### Importing a Code Repository Project

The supported Code Repositories are:

- GitHub Cloud, [GitHub Custom Setup](../code-repository-integrations/github-custom-setup.md)
- GitLab Cloud, [GitLab Custom Setup](../code-repository-integrations/gitlab-custom-setup.md)
- Bitbucket Cloud, [Bitbucket Custom Setup](../code-repository-integrations/bitbucket-custom-setup.md)
- Azure DevOps Cloud, [Azure DevOps Custom Setup](../code-repository-integrations/azure-devops-custom-setup.md)

### Creating a new Feedback Profile

To create a profile, follow the steps below:

1. Create the Profile.
2. Configure the general settings.
3. Assign Feedback Apps.
4. Assign projects.

For full documentation, see [Creating a New Feedback Profile](creating-a-new-feedback-profile.md).

### Verification

Go to the relevant Feedback App and verify the following:

1. **Bug Tracking services** (Jira, GitHub Issues, Azure DevOps Bug Board) - Verify that tickets are opened/closed according to the discovered Checkmarx One scan vulnerabilities.
2. **Alerting services** (Slack, Microsoft Teams, Email notification service) - Verify that messages are received according to the discovered Checkmarx One scan vulnerabilities.

## In this section

- [Jira](jira.md)
- [Azure Boards](azure-boards.md)
- [GitHub Issues](github-issues.md)
- [Slack](slack.md)
- [Microsoft Teams](microsoft-teams.md)
- [Email Notification Service](email-notification-service.md)
- [Creating a New Feedback Profile](creating-a-new-feedback-profile.md)
- [Updating and Deleting Profiles](updating-and-deleting-profiles.md)
- [Assigning a Feedback Profile to a Checkmarx Project - Repository path scans](assigning-a-feedback-profile-to-a-checkmarx-project---repository-path-scans.md)
