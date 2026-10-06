# Checkmarx One Visual Studio Extension

Checkmarx continues to spearhead the shift-left approach to AppSec by bringing our powerful AppSec tools into your IDE. This empowers developers to identify vulnerabilities and remediate them **as they code**. The Checkmarx Visual Studio extension integrates seamlessly into your IDE, enabling you to access the full functionality of your Checkmarx One account (SAST, SCA, IaC Security and Secret Detection) directly from your IDE.

You can run new scans, or import results from scans run in your Checkmarx One account. Checkmarx provides detailed info about each vulnerability, including remediation recommendations and examples of effective remediation. The plugin enables you to navigate from a vulnerability to the relevant source code, so that you can easily zero-in on the problematic code and start working on remediation.

This extension also includes **Checkmarx Developer Assist**, an agentic AI tool that delivers real-time context-aware prevention, remediation, and guidance to developers inside the IDE.

These features require authentication using an API key from your Checkmarx One account.

## Key Features

- Access the full power of Checkmarx One (SAST, SCA, IaC Security and Secret Detection) directly from your IDE
- Run a new scan from your IDE even before committing the code, or import scan results from your Checkmarx One account
- Rescan an existing branch from your IDE or create a new branch in Checkmarx One for the local branch in your workspace.
- Provides actionable results. Navigate from results panel directly to the highlighted vulnerable code in the editor and get right down to work on the remediation.
- Group and filter results
- Triage results (by adjusting the severity and state and adding comments) directly from the Visual Studio console (currently supported for SAST and IaC Security)
- Links to Codebashing lessons

**Checkmarx Developer Assist** - AI guided remediation:

- An advanced security agent that delivers real-time context-aware prevention, remediation, and guidance to developers from the IDE.
- Realtime scanners identify risks as you code.

  - ASCA, a lightweight source code scanner, enables developers to identify secure coding best practice violations in the file that they are working on as they code.
  - Specialized realtime scanners identify vulnerable open source packages and container images, as well as exposed secrets and IaC risks.
- MCP-based agentic AI remediation.
- AI powered explanation of risk details.
- Reduce noise by marking false positives as ignored.

## Prerequisites

- Supported for **Visual Studio 2022** and **Visual Studio 2026** (tested and verified on **Community** and **Insider** editions)
- Officially supported only for .NET Framework version 4.7.2, 4.8 or 4.8.1.
- You have an **API key** for your Checkmarx One account. To create an API key, see Generating an API Key.

  {% hint style="info" %}
  In order to use this integration for running an end-to-end flow of scanning a project and viewing results with the minimum required permissions, the API Key or user account should have the role `plugin-scanner`. Alternatively, they can have at a minimum the out-of-the-box composite role `ast-scanner` as well as the IAM role `default-roles`.
  {% endhint %}
- In order to use Dev Assist, you need the following additional prerequisites:

  - A Checkmarx One account with a **Checkmarx One Assist** license
  - The **Checkmarx MCP** must be activated for your tenant account. This is done in the Checkmarx One web application (UI) on the **Settings** > **Plugins** page. This must be done by an account admin.
  - You must have **GitHub Copilot Chat** (AI Agent) version 1.5.62-243+ installed
  - You must have Node.js v22.22.0 or above installed in the OS specific PATH environment variable.

## In this section

- [Installing and Setting Up the Checkmarx One Visual Studio Extension](installing-and-setting-up-the-checkmarx-one-visual-studio-extension.md)
- [Using the Checkmarx One Visual Studio Extension](using-the-checkmarx-one-visual-studio-extension.md)
- [Using Developer Assist in Visual Studio](using-developer-assist-in-visual-studio.md)
- [Visual Studio Extension - Changelog](visual-studio-extension---changelog.md)
