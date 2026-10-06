# Managing Projects

A Checkmarx One project defines the source to be scanned and uses scanners, scan tags, and group assignments. Normally, a Checkmarx One project should correspond to or be part of a software development project. Anytime a scan is run, the results remain associated with the project.

For Continuous Integration development methodology, if a new branch is created for each iteration, update the code location within the existing project (rather than creating a new project) so that all the results reside within a single project.

For every Project that exists in Checkmarx One, the following actions are available:

- [Modifying Project Settings](configuring-projects.md)
- [Deleting Projects](deleting-projects.md)

## Viewing the Projects Tab

The **Workspace** <img src="../../../assets/Workspace.png" alt="" data-size="line">**>** **Projects** screen enables you to manage and monitor your Checkmarx One Projects.

The expandable **Filters & Groups** section lets you group the projects list by Risk Level and display the applied table filters.

Below that, the **Projects** pane shows a list of the projects in your account. Click anywhere on a Project row to view its results on the **Risk Orchestration** page. Alternatively, click on a scanner icon in the **Scanner Results** column to view results for that scanner in its dedicated results viewer.

In addition, you can click on the Overview icon to open the Project's overview page.

The following table describes the information shown for each project and the actions that can be taken.

| **Item** | **Description** | **Possible Values** |
|---|---|---|
| **Selection Box** | Select multiple checkboxes to bulk delete the selected Projects. The Delete Projects button appears at the top of the table. | |
| **Name** | The name of the Project. | |
| **Risk Level** | The risk level of the Project is based on the vulnerabilities that were identified. | Critical, High, Medium, Low, No Risk |
| **Total Vulnerabilities** | The number of vulnerabilities identified for each severity level is shown. | |
| **Scanner Results** | Shows which engines ran on the project during the last scan. Color indicates severity: darker colors represent more critical findings. | SAST, SCS, SCA, CON, IaC, API, AISC |
| **Last Scan** | Shows how much time has passed since the Project was last scanned. | |
| **Applications** | Displays applications associated with a given project.<br>{% hint style="info" %}<br>The applications in the column are only visible if you have the **view application** permission enabled in Access Management. A project can be assigned to multiple applications, but you will only see the ones accessible to you. If you do not have this permission, the column will show **N/A** instead.<br>{% endhint %} | |
| **Internet Facing** | Shows if the project is internet-facing. | |
| **Tags** | Shows tags in **key** or **key:value** pairs applied to this Project. | |
| **Groups** | Shows the groups that are assigned to the project. | |
| **Scan Origin** | Shows how the most recent scan of the Project was triggered. | • `webapp` - manual project triggered from the UI<br>• `Push Webhook`/`PR Webhook` - code repository project triggered by a push or PR<br>• `Project Scan` - code repository project triggered manually from the UI<br>• `cli` - triggered from the Checkmarx One CLI tool<br>• `Jenkins`/ `Azure DevOps`/ `VS Code` etc. - triggered from the specified plugin (CI/CD or IDE) |
| **Source** | Shows how the source code was accessed for the most recent scan. | • `ZIP/TAR` - manual project scan from an uploaded file<br>• `GitHub`/ `GitLab`/ `Azure`/ `BitBucket` - the name of the code repository where the source code resides.<br>{% hint style="success" %}<br>This can be a code repository project or a manual project that scanned code from a code repository.<br>{% endhint %}<br>• `Confluence` - for Secret Detection scans of Confluence content. |
| **Quick Actions Buttons** - hover over the desired Project to reveal the quick action buttons. | | |
| **Scanner Results Icons** | Hovering over any of the **Scanner Results** icons will display the severity of that scanner for the last successfully completed scan. Clicking on the icon will open the last scan results in the Results Viewer.<br>If the icons do not all fit in your table view, a +{#} link is displayed at the right side of the column. Hover over the link to see the additional scanners. | SAST, SCS, SCA, CON, IaC, API, AISC |
| **Copy Project ID** | Click on the Copy ID <img src="../../../assets/Dulpicate.png" alt="" data-size="line"> icon at the end of a row to copy the ID of that Project to your clipboard. | |
| **Overview** | Click on the Overview icon that appears next to the Project's name. This opens the Project's Overview page, which shows detailed information about the Project. | |
| **Scan** | Click on the Scan icon at the end of a row to Initiate a new scan for the Project. | |
| **Action Menu** | | |
| **Associate to Applications** | Assign the Project to one or more Applications. See [Managing Applications](../managing-applications/README.md) | |
| **Project Settings** | Edit the Project settings. See [Configuring Projects](configuring-projects.md) | |
| **Query Editor** | Opens the default SAST, IaC, or Secret Detection Query Editor. If more than one option is available, a dropdown appears to select one. See [here](../resource-management/iac-security-query-editor.md) for more details on IaC Query Editor and [here](../resource-management/sast-query-editor/README.md) for SAST Query Editor. | |
| **Rescan Project** | Rescan a project directly from the latest source code already stored on the server, without requiring a new upload<br>Rescans are based on the last successful scan of the project, use the same engines, and automatically apply any updated project settings such as presets, exclusions, or scan mode changes.<br>{% hint style="info" %}<br>The rescan feature does not support Scorecard scans because they require credentials. Rescans use source data stored from the previous scan and do not have access to the credentials required to run a new Scorecard scan.<br>{% endhint %} | |
| **Optimization Service Order** | Order Optimization service from the Checkmarx AppSec experts for this Project. | |
| **Generate Project Report** | Generate a Project report. See [Project Reports](../checkmarx-one-reports/project-reports/README.md) | |
| **Delete Project** | Delete the Project and its associated scans. See [Deleting Projects](deleting-projects.md) | |

## In this section

- [Creating Projects](creating-projects.md)
- [Configuring Projects](configuring-projects.md)
- [Tenant-level Webhooks](tenant-level-webhooks.md)
- [Projects Page](projects-page.md)
- [Viewing the Project Details Page](viewing-the-project-details-page.md)
- [Project Migration](project-migration.md)
- [Configuring Projects Using Config as Code Files](configuring-projects-using-config-as-code-files/README.md)
- [Deleting Projects](deleting-projects.md)
