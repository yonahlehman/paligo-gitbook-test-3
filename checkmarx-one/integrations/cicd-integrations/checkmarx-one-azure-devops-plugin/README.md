# Checkmarx One Azure DevOps Plugin

The Checkmarx One Azure DevOps (ADO) plugin enables you to integrate the full functionality of the Checkmarx One platform into your ADO pipelines. You can use this plugin to trigger scans running Checkmarx SAST, Checkmarx SCA, IaC Security, API Security, Container Security and Software Supply Chain Security scanners as part of your CI/CD integration.

This plugin provides a wrapper around the Checkmarx One CLI Tool which creates a zip archive from your source code repository and uploads it to Checkmarx One for scanning. This provides easy integration with ADO while enabling scan customization using the full functionality and flexibility of the CLI tool.

{% hint style="info" %}
The plugin code can be found [here](https://github.com/Checkmarx/ast-azure-plugin).
{% endhint %}

## Main Features

- Configure ADO pipelines to automatically trigger scans running Checkmarx SAST, Checkmarx SCA, IaC Security, API Security, Container Security and Software Supply Chain Security scanners
- Supports adding a Checkmarx One scan as a pre-configured task or as a YAML
- Supports use of CLI arguments to customize scan configuration, enabling you to:

  - Customize filters to specify which folders and files are scanned
  - Apply preset query configurations
  - Customize SCA scans using Checkmarx SCA Resolver

    {% hint style="info" %}
    The plugin does not bundle or automatically download the SCA Resolver.

    Before running a pipeline that uses SCA Resolver functionality, ensure the SCA Resolver binary is installed on the build agent. Pass its path to the plugin using the `--sca-resolver` command line flag.
    {% endhint %}
  - Set thresholds to break build
- Send requests via a proxy server
- View scan results summary and trends in the ADO environment
- Direct links from within ADO to detailed Checkmarx One scan results
- Generate customized scan reports in various formats (JSON, HTML, PDF etc.)
- Generate SBOM reports (CycloneDX and SPDX)
- Supports Team Foundation Version Control (TFVC) based repos.

## Prerequisites

- You have a Microsoft account with:

  - **Azure DevOps Services**, or
  - **Azure DevOps Server version 2020 or 2022**
- Azure DevOps Build Environment:

  - Build agent must be version **3.232.1 or later** and the agent must be using Node version 20 (which is the default configuration).
- You have a Checkmarx One account and you have an OAuth **Client ID** and **Client Secret** for that account (see [Creating an OAuth Client for Checkmarx One Integrations](../../authentication-for-checkmarx-one-cli-and-plugins/creating-an-oauth-client-for-checkmarx-one-integrations.md)) or you have a Checkmarx One **API Key** (see Generating an API Key).

  {% hint style="info" %}
  The minimum required roles for running an end-to-end flow of scanning a project and viewing results via the CLI or plugins are Checkmarx One `plugin-scanner` role and IAM `default-roles<tenant>` role.

  The permissions included in `plugin-scanner` are shown here. If you would like to create a custom role with more granular permissions, you should refer to this list of permissions in order to determine which permissions you will need to assign.
  {% endhint %}

## In this section

- [Quick Start Guide - Checkmarx One Azure DevOps Plugin](quick-start-guide---checkmarx-one-azure-devops-plugin.md)
- [Installing the Azure Checkmarx One Plugin](installing-the-azure-checkmarx-one-plugin.md)
- [Checkmarx One Azure DevOps Plugin Initial Setup](checkmarx-one-azure-devops-plugin-initial-setup.md)
- [Creating Checkmarx One Pipelines in Azure](creating-checkmarx-one-pipelines-in-azure/README.md)
- [Viewing Checkmarx One Results in Azure](viewing-checkmarx-one-results-in-azure.md)
- [Checkmarx One Azure DevOps Plugin - Changelog](checkmarx-one-azure-devops-plugin---changelog.md)
