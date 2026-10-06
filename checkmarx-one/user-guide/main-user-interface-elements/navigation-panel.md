# Navigation Panel

Checkmarx One has multiple screens, all accessible from the navigation panel on the left side of the workspace. Screens are divided into sections. For example, **Analytics & Dashboard** is under **ASPM**.

The following is a description of all screens plus helpful links.

<details>

<summary>ASPM</summary>

ASPM (Application Security Posture Management) provides an overview of all your data’s analytics, risks, and integrations. As the landing page in Checkmarx One, Application Risk Management features your top 10 risky applications.

| **Screen** | **Description** | **Links** |
|---|---|---|
| Analytics & Dashboard | The **Analytics and Dashboard** screen displays panels with charts, insights, and filtering to detail an organization’s data in Checkmarx One. | For details on leveraging analytics in Checkmarx One, see [Analytics](../analytics/README.md). |
| Risk Orchestration | The **Risk Orchestration** screen provides a unified view of scan results across security engines. View, filter, and triage risks for a selected project from a single consolidated table. | For details on reviewing and managing risks across security engines, see Risk Orchestration. |
| Application Risk Management | The **Application Risk Management** screen lists the top 10 risky applications. View risk scores, analyze 50 risks per application, and triage results. | For details on analyzing risky applications, see [Using Application Risk Management](../application-security-posture-management/application-risk-management/using-application-risk-management.md). |
| Cloud Insights | The **Cloud Insights** screen lets you manage the integration of runtime environments (Wiz, AWS, or other CNAPPs). You can analyze data between containers and their Checkmarx One projects. | To learn about managing vulnerabilities in runtime environments, see [Cloud Insights](../cloud-insights/README.md). |

</details>

<details>

<summary>Workspace</summary>

Workspace houses projects, applications, and environments together with all their scan results, plus any scan results imported from external tools.

| **Screen** | **Description** | **Links** |
|---|---|---|
| Projects | The **Projects** screen lets you manage projects and assign them to applications. You can also see detailed scan results for all projects. | For guidance on handling projects, see [Managing Projects](../managing-projects/README.md), [Creating Projects](../managing-projects/creating-projects.md), and [Scanning Projects](../scanning-projects/README.md).<br>To understand scan results, see [Viewing Scan Results in the Results Viewer](../viewing-scan-results-in-the-results-viewers/README.md). |
| Applications | The **Applications** screen lets you manage applications and view detailed scan results. | To manage applications within Checkmarx One, see [Managing Applications](../managing-applications/README.md) and its articles. |
| Environments | **Environments** are setups for DAST scans on web applications and APIs. You can manage and run environments on this screen. | For general information on DAST, see Checkmarx DAST.<br>For details on setting up a DAST environment, see DAST Environment Setup Wizard. |
| External Imports | The **External Imports** screen lets you import security test results from external tools to consolidate AppSec testing within Checkmarx One. You can attach imported results to projects. | For details on importing external test results into Checkmarx One, see [Bring Your Own Results](../application-security-posture-management/bring-your-own-results-byor.md). |

</details>

<details>

<summary>Resource Management</summary>

Resource Management is home to all scans, results, and configurations, including SAST and IaC presets, scan schedules, custom query editing, and policies.

| **Screen** | **Description** | **Links** |
|---|---|---|
| Scans | The **Scans** screen shows aggregate scan results for projects, with filters, tags, and search. | To learn how to read and filter scan results, see [Scans](../resource-management/scans.md). |
| SAST Presets | The **SAST Preset Management** screen is where you manage predefined and custom SAST presets. Presets enhance scan accuracy and are currently supported by SAST and IaC Security scanners only. | For details on managing SAST presets, see [SAST Presets Management](../resource-management/sast-presets-management.md). |
| IaC presets | The **IaC Preset Management** screen is where you manage custom IaC Security presets.<br>Currently, IaC offers custom presets only. It does not offer predefined presets. | For details on viewing and managing IaC presets, see [IaC Security Presets Management](../resource-management/iac-security-presets-management.md). |
| Schedules Management | The **Schedules Management** screen lets you automate schedules for scanning projects. | To schedule scans for your projects, see [Scheduling Scans](../resource-management/scheduling-scans.md). |
| Query Editor | The **Query Editor** screen lets you customize SAST queries or create new ones for QA, security, and application logic. | To learn how to create and edit SAST queries, see [SAST Query Editor](../resource-management/sast-query-editor/README.md). |
| Policies | The **Policies** screen lets you create and edit policies to evaluate project scan results and trigger automatic responses like breaking the software build. | To learn about policy management, including viewing policies and toggling a break build, see [Policy Management Overview](../policy-management-overview/README.md). |

</details>

<details>

<summary>Integrations</summary>

Manage your integrations. Checkmarx One supports integration with code repositories, feedback apps, cloud connection, CI/CD, and IDE. For an overview of all available integrations, see [Checkmarx One Integrations](../checkmarx-one-integrations.md).

| **Screen** | **Description** | **Links** |
|---|---|---|
| Feedback Apps | The **Feedback Apps** screen lets you create alerts in email or team collaboration apps. Alerts can be triggered by scan completion or vulnerability detection. | To connect and configure feedback apps, see [Feedback Apps](../checkmarx-one-integrations.md#feedback-apps). |
| Cloud Connections | The **Cloud Connections** screen lets you set up and configure private container repos to automatically pull images for scanning and runtime usage. | To set up an integration, read the guide for each repository under [Private Registry Integration for Container Security Scanner](../container-security/private-registry-integration-for-container-security-scanner/README.md).<br>To set up a Sysdig integration, see [Sysdig Integration - Runtime Usage](../container-security/sysdig-integration---runtime-usage.md). |
| External Plugins | The **External Plugins** screen lets you download and view the source code for CLI, CI/CD, IDE, and vulnerability management plugins. | To see all IDE plugins and their features, see [Checkmarx One IDE Plugins](../../ide-plugins/README.md). |
| Project Migration | The **Project Migration** screen lets you convert and export Checkmarx One projects to an external code repository. | To learn how to perform single-project and multi-project migrations to a cloud-hosted or self-hosted flow, see [Project Migrations](../managing-projects/project-migration.md). |

</details>

<details>

<summary>Resources</summary>

Resources extend Checkmarx One's core features by tracking AI components, SCA, and API risks to improve security posture.

Codebashing, a secure-coding boot camp, trains developers in secure coding practices.

| **Screen** | **Description** | **Links** |
|---|---|---|
| AI Supply Chain Global Inventory | The **AI Supply Chain Global Inventory** lists all detected AI components in an account, enhancing AI transparency and enforcement. | To learn about all possible AI components in an application, see AI Supply Chain Security.<br>To learn more about filtering projects out of AI scans, see Navigating AI Supply Chain. |
| SCA Inventory and Risks | The **SCA Inventory & Risks** screen lists policy violations, vulnerabilities, and outdated versions of software packages. | To learn about all the risks associated with packages, see [Global Inventory](../global-inventory.md). |
| SCA AppSec Knowledge Center | The **SCA AppSec Knowledge Center** lets you search vulnerabilities and affected packages by version and license. | To learn about the new version of the SCA AppSec Knowledge Center and see a sample workflow, see [AppSec Knowledge Center](../appsec-knowledge-center/README.md). |
| SCA Private Packages Catalog | The **SCA Private Packages Catalog** lists in-house libraries, indicating how many projects use outdated versions and the number of outdated versions in use. | To read the release notes and resolved issues for private packages, see [Private Packages](../cloud-insights/README.md#private-packages). |
| API Inventory | The **API Inventory** shows a comprehensive list of the APIs used in an account and associated risks. | For descriptions of API parameters, see [API Inventory](../global-inventory.md#api-inventory). |
| Codebashing | This is a link to **Codebashing,** the secure-code training platform for developers built by Checkmarx. | To learn about the assessments, challenges, tournaments in Codebashing, see What is Codebashing. |

</details>

<details>

<summary>Settings</summary>

In Settings, you can manage your license, identity and access, tenant settings, imports, CxLinks, and display language.

| **Screen** | **Description** | **Links** |
|---|---|---|
| License | The **License** screen presents license details, consumption, and upgrade options. | For available license information and details on upgrading, see Viewing License Info and Upgrading a License. |
| Global Settings | The **Global Settings** screen enables configuration of tenant-level parameters. These parameters apply to *all* applications, projects, and scans in the tenant account. | To learn how to control settings in most areas of your Checkmarx One account, including all scanner parameters, cloud insights, and code repositories, see [Global Account Settings](../configuring-account-settings/global-account-settings/README.md). |
| Identity and Access Management | In **Identity and Access Management** (IAM), admin managers can manage authorization and access settings for all Checkmarx One users, as follows:<br>• 0Auth Clients<br>• Users, user roles, groups<br>• Identity providers (SAML, Open ID)<br>• Groups<br>• Sessions<br>• API Keys | For complete information on IAM in Checkmarx One, see [User Management and Access Control](../user-management-and-access-control/README.md).<br>To learn how to open the IAM console, see [Accessing the IAM console](../user-management-and-access-control/accessing-the-identity-and-access-management-console.md). |
| Imports | Use the **Imports** screen to import external SAST environments into Checkmarx and see migration logs. | To learn how to export an outside environment and import it to Checkmarx One, see [Importing SAST to Checkmarx One](../../integrations/migrating-from-sast-to-checkmarx-one/importing-sast-to-checkmarx-one.md). |
| CxLink | As an alternative to a site-to-site VPN, use **CxLink** to generate and delete links to simplify your firewall and security when importing repositories into Checkmarx One. | To set up the CxLink Client and create CxLinks, see [CxLink](../cxlink.md). |
| Language | The **Language** popup lets you choose from three display languages: English, Korean, or Traditional Chinese. | |
| Access Control | The **Access Control** screen has basic access control resets of your authentication method and devices. | To learn more about when to use these access control options, see [Access Control](../logging-in-to-checkmarx-one/access-control.md). |

</details>

<details>

<summary>Support</summary>

Have a problem or suggestion? You can submit a ticket to the help desk or pitch an idea to the Idea Portal. Also, find the full guide to Checkmarx One.

| **Screen** | **Description** | **Links** |
|---|---|---|
| Contact Support | **Contact Support** opens a sliding pane to submit a ticket with attachments. | For details on submitting tickets, see [Contacting Support](../contacting-support.md). |
| Suggest a Feature | **Suggest a Feature** opens the Idea Portal, where you can suggest a feature directly to Checkmarx’s Product Management department. | For a guide on using the Idea Portal, see the Idea Portal Overview.<br>To register, click [here](https://checkmarx.com/ideas-portal-registration/).<br>Already a user? Log in to the Idea Portal [here](https://checkmarx.ideas.aha.io/). |
| Version | **Version** shows the current version of Checkmarx One. Clicking it opens the full guide to Checkmarx One. | You can also find the full guide to Checkmarx One here. |

</details>
