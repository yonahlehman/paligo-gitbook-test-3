# Checkmarx One GitHub Actions

The **Checkmarx One** **GitHub Action** enables you to trigger SAST, SCA, IaC Security, API Security, Container Security and Software Supply Chain Security scans directly from the GitHub workflow. It provides a wrapper around the Checkmarx One CLI Tool which creates a zip archive from your source code repository and uploads it to Checkmarx One for scanning. The Github Action provides easy integration with GitHub while enabling scan customization using the full functionality and flexibility of the CLI tool.

The GitHub Action can be customized to trigger scans when particular actions (e.g., push, or pull request) occur on specific branches of your repo. You can also add pre and post scan steps to your workflow. For example, you can add a step to screen commits to verify if the changes made warrant running a new scan.

{% hint style="info" %}
The plugin code can be found [here](https://github.com/CheckmarxDev/ast-github-action).
{% endhint %}

{% hint style="info" %}
There is an alternative method for integrating GitHub with Checkmarx One which is done directly from Checkmarx One, see [GitHub Managed Setup](../../code-repository-integrations/github-managed-setup.md). That method is easier to implement but doesn’t enable full customization of the process.
{% endhint %}

## Main Features

- Automatically trigger CxSAST, CxSCA, IaC Security, API Security, Container Security and Software Supply Chain Security scans from the GitHub workflow
- Supports use of CLI arguments to customize scan configuration, enabling you to:

  - Customize filters to specify which folders and files are scanned
  - Apply preset query configurations
  - Customize SCA scans using [SCA Resolver](https://checkmarx.com/resource/documents/en/34965-19196-checkmarx-sca-resolver.html)
  - Set thresholds to break build
- Shows scan results summary in the GitHub build logs
- Supports generating reports that are integrated into the GitHub Security alerts
- Decorates pull requests with info about new vulnerabilities that were identified as well as vulnerabilities that were fixed by the code changes
- Supports scanning images in private registries

## Prerequisites

- The source code for your project is hosted on a GitHub repo (public or private)
- You have a Checkmarx One account and you have an OAuth **Client ID** and **Client Secret** for that account. To create an OAuth client, see [Creating an OAuth Client for Checkmarx One Integrations](../../authentication-for-checkmarx-one-cli-and-plugins/creating-an-oauth-client-for-checkmarx-one-integrations.md).

  {% hint style="info" %}
  The minimum required roles for running an end-to-end flow of scanning a project and viewing results via the CLI or plugins are Checkmarx One `plugin-scanner` role and IAM `default-roles<tenant>` role.

  The permissions included in `plugin-scanner` are shown here. If you would like to create a custom role with more granular permissions, you should refer to this list of permissions in order to determine which permissions you will need to assign.
  {% endhint %}

## In this section

- [Quick Start Guide - Checkmarx One GitHub Actions](quick-start-guide---checkmarx-one-github-actions.md)
- [Checkmarx One GitHub Actions Initial Setup](checkmarx-one-github-actions-initial-setup.md)
- [Configuring a GitHub Action with a Checkmarx One Workflow](configuring-a-github-action-with-a-checkmarx-one-workflow/README.md)
- [Viewing GitHub Action Checkmarx One Scan Results](viewing-github-action-checkmarx-one-scan-results.md)
- [GitHub Actions - Changelog](github-actions---changelog.md)
