# Checkmarx One TeamCity Plugin

The Checkmarx One TeamCity plugin enables you to integrate the full functionality of the Checkmarx One platform into your TeamCity projects. You can use this plugin to trigger scans running Checkmarx SAST, Checkmarx SCA, IaC Security, API Security, Container Security and Software Supply Chain Security scanners as part of your CI/CD integration.

This plugin provides a wrapper around the Checkmarx One CLI Tool which creates a zip archive from your source code repository and uploads it to Checkmarx One for scanning. This provides easy integration with TeamCity while enabling scan customization using the full functionality and flexibility of the CLI tool.

{% hint style="info" %}
The plugin code can be found [here](https://github.com/Checkmarx/ast-teamcity-plugin).
{% endhint %}

## Main Features

- Configure TeamCity projects to automatically trigger scans running Checkmarx SAST, Checkmarx SCA, IaC Security, API Security, Container Security and Software Supply Chain Security
- Supports use of CLI arguments to customize scan configuration, enabling you to:

  - Customize filters to specify which folders and files are scanned
  - Apply preset query configurations
  - Customize SCA scans using Checkmarx SCA Resolver
  - Set thresholds to break build
- Send requests via a proxy server
- View scan results summary and trends in the TeamCity environment
- Direct links from within TeamCity to detailed Checkmarx One scan results
- Generate customized scan reports in various formats (JSON, HTML, PDF etc.)
- Generate SBOM reports (CycloneDX and SPDX)
- Automatically updates to the latest plugin version

## Prerequisites

- The source code for your project is hosted on a VCS that is supported by TeamCity (Subversion, Git, and Mercurial. TFS and Perforce are partially supported. See TeamCity documentation [here](https://www.jetbrains.com/help/teamcity/creating-and-editing-projects.html#Creating+Project).)
- Supported Java version - JDK 11
- You have a Checkmarx One account and you have an OAuth **Client ID** and **Client Secret** for that account. To create an OAuth client, see [Creating an OAuth Client for Checkmarx One Integrations](../../authentication-for-checkmarx-one-cli-and-plugins/creating-an-oauth-client-for-checkmarx-one-integrations.md).

  {% hint style="info" %}
  The minimum required roles for running an end-to-end flow of scanning a project and viewing results via the CLI or plugins are Checkmarx One `plugin-scanner` role and IAM `default-roles<tenant>` role.

  The permissions included in `plugin-scanner` are shown here. If you would like to create a custom role with more granular permissions, you should refer to this list of permissions in order to determine which permissions you will need to assign.
  {% endhint %}

## In this section

- [Installing the TeamCity Checkmarx One Plugin](installing-the-teamcity-checkmarx-one-plugin.md)
- [Configuring Global Integration Settings for Checkmarx One TeamCity Plugin](configuring-global-integration-settings-for-checkmarx-one-teamcity-plugin.md)
- [Adding a Checkmarx One Build Step in TeamCity](adding-a-checkmarx-one-build-step-in-teamcity.md)
- [Viewing Checkmarx One Results in TeamCity](viewing-checkmarx-one-results-in-teamcity.md)
- [TeamCity Plugin - Changelog](teamcity-plugin---changelog.md)
