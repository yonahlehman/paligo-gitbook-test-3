# Checkmarx One Eclipse Plugin

Checkmarx continues to spearhead the shift-left approach to AppSec by bringing our powerful AppSec tools into your IDE. This empowers developers to identify vulnerabilities and remediate them **as they code**. The Checkmarx Eclipse plugin integrates seamlessly into your IDE, enabling you to access the full functionality of your Checkmarx One account (SAST, SCA, IaC Security) directly from your IDE.

You can run new scans, or import results from scans run in your Checkmarx One account. Checkmarx provides detailed info about each vulnerability, including remediation recommendations and examples of effective remediation. The plugin enables you to navigate from a vulnerability to the relevant source code, so that you can easily zero-in on the problematic code and start working on remediation.

## Key Features

- **Checkmarx One Platform** - scanning projects and viewing results:
- **Checkmarx Developer Assist** - AI guided remediation:

  - An advanced security agent that delivers real-time context-aware prevention, remediation, and guidance to developers from the IDE.
  - Realtime scanners identify risks as you code.

    - ASCA, a lightweight source code scanner, enables developers to identify secure coding best practice violations in the file that they are working on as they code.
    - Specialized realtime scanners identify vulnerable open source packages and container images, as well as exposed secrets and IaC risks.
  - MCP based agentic AI remediation.
  - AI powered explanation of risk details
  - Reduce noise by marking false positives as ignored

## Prerequisites

- An eclipse installation, version 2020-09 or above.

  {% hint style="info" %}
  Supported platforms: Windows, Mac, Linux/GTK
  {% endhint %}

- You have an **API key** for your Checkmarx One account. To create an API key, see Generating an API Key

  {% hint style="info" %}
  In order to use this integration for running an end-to-end flow of scanning a project and viewing results with the minimum required permissions, the API Key or user account should have the role `plugin-scanner`. Alternatively, they can have at a minimum the out-of-the-box composite role `ast-scanner` as well as the IAM role `default-roles`.
  {% endhint %}
- To use **Dev Assist**, you need the following additional prerequisites:

  - Eclipse installation, version 2025-06 and above with GitHub Copilot
  - A Checkmarx One account with a **Checkmarx One Assist** license. Also, **Dev Assist** must be activated for your tenant account in the Checkmarx One UI under **Global Settings** > **Plugins** page. This must be done by an account admin.

## In this section

- [Installing and Setting up the Checkmarx One Eclipse Plugin](installing-and-setting-up-the-checkmarx-one-eclipse-plugin.md)
- [Using the Checkmarx One Eclipse Plugin](using-the-checkmarx-one-eclipse-plugin.md)
- [Using the Eclipse Plugin - Dev Assist](using-the-eclipse-plugin---dev-assist.md)
- [Eclipse Plugin - Changelog](eclipse-plugin---changelog.md)
