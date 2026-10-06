# Checkmarx One Jenkins Plugin

The Checkmarx One Jenkins plugin enables you to integrate the full functionality of the Checkmarx One platform into your Jenkins pipelines. For your CI/CD integration, you can use this plugin to trigger scans running Checkmarx SAST, Checkmarx SCA, IaC Security, API Security, Container Security, and Software Supply Chain Security scanners.

This plugin provides a wrapper around the Checkmarx One CLI Tool, which creates a zip archive from your source code repository and uploads it to Checkmarx One for scanning. This allows for easy integration with Jenkins while enabling scan customization using the full functionality and flexibility of the CLI tool.

{% hint style="info" %}
The plugin code can be found [here](https://github.com/jenkinsci/checkmarx-ast-scanner-plugin/).
{% endhint %}

## Main Features

- Configure Jenkins pipelines to automatically trigger scans running Checkmarx SAST, Checkmarx SCA, IaC Security, API Security, Container Security and Software Supply Chain Security scanners
- Supports integrating Checkmarx One build steps into FreeStyle or Pipeline projects
- When a scan identifies a policy violation for a **break build** policy, the pipeline fails and aborts all subsequent steps.
- Supports the use of CLI arguments to customize scan configuration, enabling you to:

  - Customize filters to specify which folders and files are scanned
  - Apply preset query configurations
  - Customize SCA scans using Checkmarx SCA Resolver
  - Set thresholds to break the build
- Send requests via a proxy server
- View scan results summary and trends in the Jenkins environment
- Direct links from within Jenkins to detailed Checkmarx One scan results
- Generate customized scan reports in various formats (JSON, HTML, PDF, etc.)
- Generate SBOM reports (CycloneDX and SPDX)
- It can be configured to update to the latest CLI version automatically

## Prerequisites

- A Jenkins installation LTS 2.375 or above (Supported Operating systems: Windows and Linux)

  {% hint style="info" %}
  The plugin supports CloudBees.
  {% endhint %}
- You have a Checkmarx One account and an OAuth **Client ID** and **Client Secret** for that account. To create an OAuth client, see [Creating an OAuth Client for Checkmarx One Integrations](../../authentication-for-checkmarx-one-cli-and-plugins/creating-an-oauth-client-for-checkmarx-one-integrations.md).

  {% hint style="info" %}
  The minimum required roles for running an end-to-end flow of scanning a project and viewing results via the CLI or plugins are Checkmarx One `plugin-scanner` role and IAM `default-roles<tenant>` role.

  The permissions included in `plugin-scanner` are shown here. If you would like to create a custom role with more granular permissions, you should refer to this list of permissions in order to determine which permissions you will need to assign.
  {% endhint %}

## In this section

- [Quick Start Guide - Checkmarx One Jenkins Plugin](quick-start-guide---checkmarx-one-jenkins-plugin.md)
- [Checkmarx One Jenkins Plugin - Installation and Initial Setup](checkmarx-one-jenkins-plugin---installation-and-initial-setup/README.md)
- [Configuring Checkmarx One Build Steps in Jenkins](configuring-checkmarx-one-build-steps-in-jenkins/README.md)
- [Viewing Checkmarx One Results in Jenkins](viewing-checkmarx-one-results-in-jenkins.md)
- [Jenkins Plugin - Changelog](jenkins-plugin---changelog.md)
