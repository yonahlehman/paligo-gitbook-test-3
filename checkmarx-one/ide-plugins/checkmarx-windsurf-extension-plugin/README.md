# Checkmarx Windsurf Extension (Plugin)

Checkmarx continues to spearhead the shift-left approach to AppSec by bringing our powerful AppSec tools into your IDE. This empowers developers to identify vulnerabilities and remediate them **as they code**. The Checkmarx VS Code plugin in Windsurf integrates seamlessly into your IDE, identifying vulnerabilities in your proprietary code, open source dependencies, and IaC files. The plugin offers actionable remediation insights in real-time.

{% hint style="info" %}
Although there is no dedicated Checkmarx plugin for Windsurf, the plugin for VS Code has been tested and found to be effective for use in Windsurf.
{% endhint %}

The Checkmarx Windsurf extension contains three separate tools:

- [Checkmarx One Platform](#checkmarx-one-platform) (includes Checkmarx Developer Assist)
- [KICS Realtime Scanner](#kics-realtime-scanner)
- [Checkmarx SCA Realtime Scanner](#checkmarx-sca-realtime-scanner)

{% hint style="info" %}
Download the extension from the [Open VSX Registry](https://open-vsx.org/extension/checkmarx/ast-results).
{% endhint %}

## Checkmarx One Platform

This tool enables Checkmarx One users to access the full functionality of your Checkmarx One account (SAST, SCA, IaC, and Secret Detection) directly from your IDE. You can run new scans or import results from scans run in your Checkmarx One account. Checkmarx provides detailed info about each vulnerability, including remediation recommendations and examples of effective remediation. The plugin enables you to navigate from a vulnerability to the relevant source code, so that you can easily zero-in on the problematic code and start working on remediation.

This extension also includes **Checkmarx Developer Assist**, an agentic AI tool that delivers real-time context-aware prevention, remediation, and guidance to developers inside the IDE.

These features require authentication, using an API key or credentials for your Checkmarx One account.

### Key Features

- **Checkmarx One Platform** - scanning projects and viewing results:

  - Access the Checkmarx One platform directly from your IDE.
  - Run a new scan from your IDE even before committing the code, or import scan results from your Checkmarx One account.
  - Rescan an existing branch from your IDE or create a new branch in Checkmarx One for the local branch in your workspace.
  - Provides actionable results including remediation recommendations. Navigate from results panel directly to the highlighted vulnerable code in the editor and get right down to work on the remediation.
  - Connect to Checkmarx via API Key or OAuth user login flow.
  - View info about how to remediate SAST vulnerabilities, including code samples.
  - Group and filter results.
  - Triage results - edit the result predicate (severity, state and comments) directly from the Visual Studio Code console (currently supported for SAST and IaC Security).
  - Links to Codebashing lessons.
  - Apply Auto Remediation to automatically remediate open source vulnerabilities, by updating to a non-vulnerable package version.
  - ”AI Security Champion” harnesses the power of AI to help you understand the vulnerabilities in your code and resolve them quickly and easily. (currently supported for SAST and IaC Security vulnerabilities).
  - Shows [Application Security Posture Management (ASPM)](../../user-guide/application-security-posture-management/README.md) results in the IDE.
- **Checkmarx Developer Assist** - AI guided remediation:

  - An advanced security agent that delivers real-time context-aware prevention, remediation, and guidance to developers from the IDE.
  - Realtime scanners identify risks as you code.

    - AI Secure Coding Assistant (ASCA), a lightweight source code scanner, enables developers to identify secure coding best practice violations in the file that they are working on as they code.
    - Specialized realtime scanners identify vulnerable open source packages and container images, as well as exposed secrets and IaC risks.
  - MCP based agentic AI remediation.
  - AI powered explanation of risk details.
  - Reduce noise by marking false positives as ignored.

### Prerequisites

- An installation of Windsurf.
- You have access to Checkmarx One via:

  - an **API Key** (see Generating an API Key), OR
  - login credentials (Base URL, Tenant name, Username and Password)

  {% hint style="warning" %}
  In order to use this integration for running an end-to-end flow of scanning a project and viewing results with the minimum required permissions, the API Key or user account should have the Checkmarx One `plugin-scanner` role and the IAM `default-roles<tenant>` role.

  The permissions included in `plugin-scanner` are shown here. If you would like to create a custom role with more granular permissions, you should refer to this list of permissions in order to determine which permissions you will need to assign.
  {% endhint %}
- "git" is installed on your local machine. For installation instructions, see [here](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).
- To use **AI Generated Remediation**, you need to have an API Key for your GPT account (unless your account is configured to use Azure AI, see [Plugins Settings](../../user-guide/configuring-account-settings/global-account-settings/plugins-settings.md)).
- To use **Dev Assist**, you need the following additional prerequisites:

  - A Checkmarx One account with a **Checkmarx One Assist** license
  - The **Checkmarx MCP** must be activated for your tenant account in the Checkmarx One UI under **Settings** > **Plugins**. This must be done by an account admin.

### Checkmarx Developer Assist

Checkmarx Developer Assist is an advanced security agent that delivers real-time context-aware prevention, remediation, and guidance to developers from the IDE. It empowers developers to identify risks in their code in realtime and harness the power of AI to remediate the risks on the spot.

Checkmarx Developer Assist comprises two main elements:

- **Realtime Scanning -** Identify vulnerabilities in realtime during IDE development of both human-generated and AI-generated code. Our super-fast scanners run in the background whenever you edit a relevant file. Our scanners identify vulnerabilities and unmasked secrets in your code. We also identify vulnerable or malicious container images and open source packages used in your project. Results are marked as Problems which are highlighted in the code and annotated with identifying icons.
- **Agentic-AI Remediation** – Initiate an Agentic-AI session to receive remediation suggestions. Checkmarx feeds all relevant info to the AI agent which accesses our MCP server to gather data from our proprietary databases and customized AI models. The AI assistant then uses this data to generate remediated code for your project. You can accept the suggested changes or you can chat with the AI agent to learn more about the vulnerability and fine-tune the remediation suggestion.

See complete documentation here.

## KICS Realtime Scanner

This tool initiates KICS scans directly from their Windsurf console. The scan runs automatically whenever an infrastructure file of a [*supported type*](https://docs.kics.io/latest/platforms/) is saved, either manually or by auto-save. The scan runs only on the file that is open in the editor. The results are shown in the Windsurf console, making it easy to remediate the vulnerabilities that are detected. This is a **free tool** provided by Checkmarx for all Windsurf users, and does not require the user to submit credentials for a Checkmarx One account.

See complete documentation [here](../checkmarx-vs-code-extension-plugin/using-the-checkmarx-vs-code-extension---kics-auto-scanning.md).

### Key Features

- Free tool, no Checkmarx account required
- Run scans directly from your IDE
- Scans are triggered automatically whenever a file is saved
- Apply Auto Remediation to automatically fix IaC vulnerabilities
- ”AI Security Champion” harnesses the power of AI to help you to understand the vulnerabilities in your code, and resolve them quickly and easily.

### Prerequisites

- You must have a supported container engine (e.g., Docker, Podman etc.) installed and running in your environment.
- In order to use **AI Generated Remediation**, you need to have an API Key for your GPT account.

## Checkmarx SCA Realtime Scanner

This tool enables Windsurf users to initiate SCA scans directly from their Windsurf console, and shows detailed results as soon as the scan is completed. The scan identifies the open-source dependencies used in your code and indicates the security risks associated with those packages. The identified packages are shown in a tree structure with an indication of the risk level for each package. You can drill down to show the specific vulnerabilities associated with a package. This is a **free tool** provided by Checkmarx for all Windsurf users, and does not require the user to submit credentials for a Checkmarx One account.

See complete documentation [here](../checkmarx-vs-code-extension-plugin/using-the-vs-code-checkmarx-extension---sca-realtime-scanning.md).

### Key Features

- Free tool, no Checkmarx account required
- Run scans directly from your IDE
- View actionable results in your IDE, indicating which of your open-source packages are at risk
- Provides links to detailed info about the vulnerabilities on the Checkmarx Developer Hub

### Prerequisites

- In order to get comprehensive results, you need to install all relevant package managers on your local environment, see Installing Supported Package Managers for Resolver.

## In this section

- [Installing and Setting up the Checkmarx Windsurf Extension](installing-and-setting-up-the-checkmarx-windsurf-extension.md)
- [Using the Checkmarx Windsurf Extension](using-the-checkmarx-windsurf-extension.md)
