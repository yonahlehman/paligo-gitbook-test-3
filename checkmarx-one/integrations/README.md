# Checkmarx One Integrations

## Overview

Checkmarx One is a robust platform that supports full integration into your SDLC. We support the following types of integrations:

- **Code Repository Integrations** - We support integration with most of the popular SCM platforms. You can set up SCM integrations using the web application by “Importing” a project from your SCM. You can activate automated scanning of your source code whenever the project is updated. Checkmarx One listens for commit events and uses a webhook to trigger Checkmarx scans when a push, or a pull request occurs. See [Checkmarx One SCM Integrations](code-repository-integrations/README.md)

  {% hint style="info" %}
  It is also possible to migrate an existing manual project and convert it to a Code Repository Integration project, see Project Migration.
  {% endhint %}
- **Feedback App Integrations** - Send scan results and new SCA vulnerability detection notifications directly to the relevant parties through your bug tracking and team collaboration tools. See [Feedback Apps](feedback-apps/README.md)
- **Cloud Connection Integrations** - Connect to your private registries in order to enable Checkmarx One to access images in your registries. This enables Checkmarx One to scan the images for risks and gather related to Cloud Insights.
- **CI/CD Integrations** - We provide specialized plugins to enable seamless integration of Checkmarx One with many popular CI/CD platforms. This enables you to trigger customized scans as part of your CI/CD pipeline. In addition, we support integration with other CI/CD platforms using our CLI Tool. See [Checkmarx One CI/CD Integrations](cicd-integrations/README.md)
- **IDE Integrations** - We provide specialized plugins that enable you to import Checkmarx One results into your favorite IDE tools. This makes it easy to identify the vulnerable code in your project and triage the scan results. See Checkmarx One IDE Plugins

## Plugins

Checkmarx One enables you to seamlessly integrate Checkmarx One with your favorite tools. We provide a robust CLI tool that enables you to access full Checkmarx One functionality via the CLI. We also provide dedicated plugins for integrating Checkmarx One into many of the most popular IDEs and CI/CD platforms. In addition, we support full integration with most code repositories.

### Checkmarx One Plugins - Quick Links

Checkmarx provides plugins that can be used to seamlessly integrate Checkmarx One into many of the most popular IDEs and CI/CD platforms.

{% hint style="info" %}
To benefit from the latest improvements and maintain compatibility with new features, we recommend keeping your CLI and plugin versions up to date.
{% endhint %}

#### Quick Links

##### CI/CD Plugins

| **Plugin** | **Marketplace** | **Code Repository** | **Documentation** |
|---|---|---|---|
| **Azure DevOps** | [Azure DevOps](https://marketplace.visualstudio.com/items?itemName=checkmarx.checkmarx-ast-azure-plugin) | [Azure DevOps](https://github.com/CheckmarxDev/checkmarx-ast-azure-plugin) | [Checkmarx One Azure DevOps Plugin](cicd-integrations/checkmarx-one-azure-devops-plugin/README.md) |
| **GitHub Actions** | [GitHub Actions](https://github.com/marketplace/actions/checkmarx-ast-github-action) | [GitHub Actions](https://github.com/Checkmarx/ast-github-action) | [Checkmarx One GitHub Actions](cicd-integrations/checkmarx-one-github-actions/README.md) |
| **TeamCity** | [TeamCity](https://plugins.jetbrains.com/plugin/17610-checkmarx-ast) | [TeamCity](https://github.com/CheckmarxDev/checkmarx-ast-teamcity-plugin) | [Checkmarx One TeamCity Plugin](cicd-integrations/checkmarx-one-teamcity-plugin/README.md) |
| **Jenkins** | [Jenkins](https://plugins.jenkins.io/checkmarx-ast-scanner/) | [Jenkins](https://github.com/jenkinsci/checkmarx-ast-scanner-plugin/) | [Checkmarx One Jenkins Plugin](cicd-integrations/checkmarx-one-jenkins-plugin/README.md) |
| **Maven** | [Maven](https://mvnrepository.com/artifact/com.checkmarx/ast-cli-maven-plugin) | [Maven](https://github.com/CheckmarxDev/ast-cli-maven-plugin) | [Checkmarx One Maven Plugin](cicd-integrations/checkmarx-one-maven-plugin.md) |

##### IDE Plugins

| **Plugin** | **Marketplace Link** | **Code Repository** | **Documentation Link** |
|---|---|---|---|
| **Visual Studio Code** | [Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=checkmarx.ast-results) | [Visual Studio Code](https://github.com/CheckmarxDev/ast-vscode-extension) | Checkmarx One Visual Studio Code Extension (Plugin) |
| **Visual Studio** | [Visual Studio](https://marketplace.visualstudio.com/items?itemName=checkmarx.astVisualStudioExtension) | [Visual Studio](https://github.com/Checkmarx/ast-visual-studio-extension) | Checkmarx One Visual Studio Extension (Plugin) |
| **JetBrains** | [JetBrains](https://plugins.jetbrains.com/plugin/17672-checkmarx-ast) | [JetBrains](https://github.com/CheckmarxDev/checkmarx-ast-jetbrains-plugin) | Checkmarx One JetBrains Plugin |
| **Eclipse** | [Eclipse](https://marketplace.eclipse.org/content/checkmarx-ast-plugin) | [Eclipse](https://github.com/Checkmarx/ast-eclipse-plugin/releases) | Checkmarx One Eclipse Plugin |

## In this section

- [Managing Checkmarx One Traffic and AWS S3 Access](managing-checkmarx-one-traffic-and-aws-s3-access.md)
- [Authentication for Checkmarx One CLI and Plugins](authentication-for-checkmarx-one-cli-and-plugins/README.md)
- [Code Repository Integrations](code-repository-integrations/README.md)
- [CI/CD Integrations](cicd-integrations/README.md)
- [Checkmarx One JFrog Plugin](checkmarx-one-jfrog-plugin.md)
- [Checkmarx One Vulnerability Integration with ServiceNow](checkmarx-one-vulnerability-integration-with-servicenow/README.md)
- [Feedback Apps](feedback-apps/README.md)
- [Cloud Connection Integrations](cloud-connection-integrations/README.md)
- [Migrating from SAST to Checkmarx One](migrating-from-sast-to-checkmarx-one/README.md)
- [Private Registry Integration for SCA Scanner](private-registry-integration-for-sca-scanner/README.md)
