# Code Repository Integrations

Checkmarx One supports integration with the most popular Code Repository platforms. You can import a project from your code repository directly to Checkmarx One, enabling automated scanning of your source code whenever the project is updated. Checkmarx One listens for commit events and uses a webhook to trigger Checkmarx scans when a push or pull request occurs. Once a scan is completed, the results can be viewed in Checkmarx One.

## Code Repository Integrations - Feature Parity

The following table shows support for Checkmarx One features for each code repository.

| | Create new integration | Convert manual project to integration | Monitor new repositories | Code repository coverage | Suggested repositories |
|---|---|---|---|---|---|
| Documentation Links | Code Repository Integration Projects | • [Project Migration](../../user-guide/managing-projects/project-migration.md)<br>• [API documentation](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/branches/main/nvgdi3222llie-code-repository-project-conversion-rest-api) | [Monitor New Repositories](monitor-new-repositories.md) | [Code Repository Coverage](code-repository-coverage.md) | [Suggested Repositories](suggested-repositories.md) |
| GitHub Managed Setup | UI/API | UI/API | UI/API | UI | UI |
| GitHub Custom Setup | UI/API | UI/API | UI/API | UI | UI |
| GitLab Managed Setup | UI | UI/API | ![](../../../assets/MicrosoftTeams-image__1_.png) | UI | ![](../../../assets/MicrosoftTeams-image__1_.png) |
| GitLab Custom Setup | UI | UI/API | ![](../../../assets/MicrosoftTeams-image__1_.png) | UI | ![](../../../assets/MicrosoftTeams-image__1_.png) |
| Bitbucket Managed Setup | UI | UI/API | ![](../../../assets/MicrosoftTeams-image__1_.png) | ![](../../../assets/MicrosoftTeams-image__1_.png) | ![](../../../assets/MicrosoftTeams-image__1_.png) |
| Bitbucket Custom Setup | UI | UI/API | ![](../../../assets/MicrosoftTeams-image__1_.png) | ![](../../../assets/MicrosoftTeams-image__1_.png) | ![](../../../assets/MicrosoftTeams-image__1_.png) |
| Azure DevOps Managed Setup | UI | UI/API | UI/API | UI | ![](../../../assets/MicrosoftTeams-image__1_.png) |
| Azure DevOps Custom Setup | UI | UI/API | UI/API | UI | ![](../../../assets/MicrosoftTeams-image__1_.png) |

## Code Repository Permissions

Only users with the required permissions in the code repository are able to set up integrations with Checkmarx One (create a “Code Repository Integration”).

{% hint style="info" %}
Checkmarx requires the permissions described below solely for the purpose of using the code repository APIs to create a webhook that triggers scans when relevant activity occurs in the repo (Push or Pull request). Checkmarx does not initiate any changes to the repo itself.
{% endhint %}

The following table explains the permissions needed to set up an integration with each of the supported code repositories.

| Code Repository | Code Repository Level | Code Repository Role | Allowed in Checkmarx One |
|---|---|---|---|
| **GitHub**<sup>1\]</sup> | Organization | Owner | • Set up an integration with any repository in the organization.<br>• Create a Webhook for the organization.<br>• See the code repository coverage widget statistics. |
| **GitHub**<sup>1\]</sup> | Repository | Admin | • Set up an integration with repositories that are assigned to the user.<br>• Create a Webhook for the repository. |
| **GitLab** | Group | Maintainer/Owner | • Set up an integration with any project in the group.<br>• See the code repository coverage widget statistics. |
| **GitLab** | Project | Maintainer/Owner | • Set up an integration with projects that are assigned to the user.<br>• Create a Webhook for the repository |
| **Bitbucket** | Workspace | **Administrator/Developer** who is configured as an Admin on the workspace level | Set up an integration with any project in the workspace |
| **Bitbucket** | Project | Owner/Admin | • Set up an integration with repositories that are assigned to the user.<br>• Create a Webhook for the repository. |
| **Bitbucket** | Project | Member/Contributor | Set up an integration with the repository that is assigned to the user |
| **Azure DevOps** | Group | **Owner/Users** that are assigned directly or indirectly to the **Project Collection Administrator** organizational group<br>{% hint style="info" %}<br>By default, the group **Project Collection Service Accounts** is a member of the **Project Collection Administrator** group, so that its members inherit the permissions needed to set up integrations from the parent group.<br>{% endhint %} | • Set up an integration with any project in the organization.<br>• See the code repository coverage widget statistics |
| **Azure DevOps** | Project | Member of a project group for which **Project Administrator** permissions exist. | • Set up an integration with the project that is assigned to the user.<br>• Create a Webhook for the repository. |

1\] When a GitHub repository is forked from a private repository, it remains linked to the original repository. Therefore, in order to access the repo, GitHub requires the user or integration to have the required level of permissions in **both the fork and the source repository**. A similar limitation applies to internal repositories used by Enterprise customers.

## Code Repository Integration without Admin Permissions

Checkmarx One also supports integration with most of the popular code repository platforms for users without Admin permissions for the relevant organization/repository.

You can import a project from your code repository directly to Checkmarx One, scan the code manually, and once a scan is completed the results can be viewed in Checkmarx One.

However, the feature comes with some limitations.

It is not possible to perform the following via Checkmarx One:

- Create a Webhook for the organization level (organization level Webhooks are supported only for GitHub).
- Create a Webhook for the repository level.
- See the code repository coverage widget statistics.
- Push & pull requests events via code repository won’t trigger automatic scan in Checkmarx One.

The following table explains the permissions needed to set up an integration with each of the supported code repositories for users without Admin permissions.

| Code Repository | Code Repository Level | Code Repository Role | Allowed in Checkmarx One |
|---|---|---|---|
| **GitHub** | Organization | Member | Set up an integration with permitted repositories in the organization |
| **GitHub** | Repository | Member | Set up an integration with the repository that is assigned to the user |
| **GitLab** | Group | Developer/Reporter/Guest | Set up an integration with permitted projects in the group |
| **GitLab** | Project | Developer/Reporter | Set up an integration with the repository that is assigned to the user |
| **Bitbucket** | Workspace | Users which are not configured as workspace Admins | Set up an integration with permitted projects in the group |
| **Bitbucket** | Project | Designated as Admin for a specific repo | • Set up an integration with repository that is assigned to the user.<br>• Create a Webhook for the repository. |
| **Azure DevOps** | Group | Users who are not assigned to the **Group Project Collection Administrator** organization | Set up an integration with permitted projects in the group |
| **Azure DevOps** | Project | Member of a project group for which the following permissions exist:<br>• Build Administrator<br>• Contributors<br>• Project Valid Users<br>• Readers | Set up an integration with the repository that is assigned to the user |

## In this section

- [GitHub Apps Code Repository Integrations](github-apps-code-repository-integrations.md)
- [GitHub Managed Setup](github-managed-setup.md)
- [GitHub Custom Setup](github-custom-setup.md)
- [GitLab Managed Setup](gitlab-managed-setup.md)
- [GitLab Custom Setup](gitlab-custom-setup.md)
- [Bitbucket Managed Setup](bitbucket-managed-setup.md)
- [Bitbucket Custom Setup](bitbucket-custom-setup.md)
- [Azure Managed Setup](azure-managed-setup.md)
- [Azure DevOps Custom Setup](azure-devops-custom-setup.md)
- [Single Tenant Flow](single-tenant-flow.md)
- [Organization-Level Configuration for Code Repository Integrations](organization-level-configuration-for-code-repository-integrations.md)
- [Monitor New Repositories](monitor-new-repositories.md)
- [Code Repository Integration Usage & Results](code-repository-integration-usage-results/README.md)
- [Code Repository Coverage](code-repository-coverage.md)
- [Suggested Repositories](suggested-repositories.md)
- [Policy Management - Break Build](policy-management---break-build.md)
