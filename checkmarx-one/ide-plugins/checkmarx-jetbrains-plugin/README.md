# Checkmarx JetBrains Plugin

Checkmarx continues to spearhead the shift-left approach to AppSec by bringing our powerful AppSec tools into your IDE. This empowers developers to identify vulnerabilities and remediate them **as they code**. The Checkmarx JetBrains plugin integrates seamlessly into your IDE, enabling you to access the full functionality of your Checkmarx One account (SAST, SCA, IaC Security, and Secret Detection) directly from your IDE.

You can run new scans, or import results from scans run in your Checkmarx One account. Checkmarx provides detailed info about each vulnerability, including remediation recommendations and examples of effective remediation. The plugin enables you to navigate from a vulnerability to the relevant source code, so that you can easily zero-in on the problematic code and start working on remediation.

This extension also includes **Checkmarx Developer Assist**, an agentic AI tool that delivers real-time context-aware prevention, remediation, and guidance to developers inside the IDE.

These features require authentication, using an API key or credentials for your Checkmarx One account.

{% hint style="info" %}
This plugin provides easy integration with JetBrains IDEs. It is officially supported for **IntelliJ IDEA**. It may work effectively for other JetBrains IDEs such as Rider, WebStorm, RubyMine, PyCharm, MPS, etc. However, Checkmarx does not guarantee full functionality and stability for these IDEs.
{% endhint %}

## Key Features

- Access the full power of Checkmarx One (SAST, SCA, IaC Security, and Secret Detection) directly from your IDE.
- Run a new scan from your IDE even before committing the code, or import scan results from your Checkmarx One account.
- Rescan an existing branch from your IDE or create a new branch in Checkmarx One for the local branch in your workspace.
- Provides actionable results including remediation recommendations. Navigate from results panel directly to the highlighted vulnerable code in the editor and get right down to work on the remediation.
- Connect to Checkmarx via API Key or OAuth user login flow
- Group and filter results.
- Triage results - edit the result predicate (severity, state and comments) directly from the Jetbrains IntelliJ console (currently supported for SAST and IaC Security).
- Links to Codebashing lessons.
- Apply Auto Remediation to automatically remediate open source vulnerabilities, by updating to a non-vulnerable package version.
- ”AI Security Champion” harnesses the power of AI to help you understand the vulnerabilities in your code, and resolve them quickly and easily (currently supported for SAST and IaC Security vulnerabilities).

**Checkmarx Developer Assist** - AI guided remediation:

- An advanced security agent that delivers real-time context-aware prevention, remediation, and guidance to developers from the IDE.
- Realtime scanners identify risks as you code.

  - ASCA, a lightweight source code scanner, enables developers to identify secure coding best practice violations in the file that they are working on as they code.
  - Specialized realtime scanners identify vulnerable open source packages and container images, as well as exposed secrets and IaC risks.
- MCP-based agentic AI remediation.
- AI powered explanation of risk details.
- Reduce noise by marking false positives as ignored.

## Prerequisites

- You are running IntelliJ version 2022.2+

  {% hint style="info" %}
  Early versions of our plugin (2.0.16 and below) support JetBrains version 2021.1+ as well.
  {% endhint %}

  {% hint style="info" %}
  If you are using a JetBrains IDE other than IntelliJ (not officially supported), make sure that you are using a version based on IntelliJ version 2022.2+.
  {% endhint %}
- You have access to Checkmarx One via:

  - an **API Key** (see Generating an API Key), OR
  - login credentials (Base URL, Tenant name, Username and Password)

  {% hint style="warning" %}
  In order to use this integration for running an end-to-end flow of scanning a project and viewing results with the minimum required permissions, the API Key or user account should have the Checkmarx One `plugin-scanner` role and the IAM `default-roles<tenant>` role.

  The permissions included in `plugin-scanner` are shown here. If you would like to create a custom role with more granular permissions, you should refer to this list of permissions in order to determine which permissions you will need to assign.
  {% endhint %}
- In order to use Dev Assist, you need the following additional prerequisites:

  - You are running IntelliJ version 2024.3+
  - A Checkmarx One account with a **Checkmarx One Assist** license. Also, **Dev Assist** must be activated for your tenant account in the Checkmarx One UI under **Global Settings** > **Plugins** page. This must be done by an account admin.

    Users will need to provide:

    - an **API Key** (see Generating an API Key), OR
    - login credentials (Base URL, Tenant name, Username and Password)
  - You must have **GitHub Copilot Chat** (AI Agent) version 1.5.62-243+ installed

## In this section

- [Installing and Setting up the Checkmarx JetBrains Plugin](installing-and-setting-up-the-checkmarx-jetbrains-plugin.md)
- [Using the Checkmarx JetBrains Plugin](using-the-checkmarx-jetbrains-plugin.md)
- [Using Developer Assist in JetBrains](using-developer-assist-in-jetbrains.md)
- [JetBrains Plugin - Changelog](jetbrains-plugin---changelog.md)
