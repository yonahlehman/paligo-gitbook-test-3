# Private Registry Integration for SCA Scanner

Checkmarx One provides integration with **JFrog Artifactory** and **GitHub Packages**, enabling you to run SCA scans on packages in your private registries. We provide a convenient wizard on the Checkmarx One **Integrations** page that enables you to submit your access credentials and create the integration. Then, you need to add the relevant info to the configuration files in each of the relevant projects.

## Prerequisites

- A Personal API key or **Identity Token** for the repository where the packages are located, with read access to the relevant repos.

  {% hint style="info" %}
  In JFrog go to **Admin** > **Identity & Access** > **Users** then select your user and go to the **Authentication** tab and generate the API key/Identity Token.
  {% endhint %}
- If your Artifactory instance cannot be reached over the public internet by the Checkmarx SCA service (for example, it is on-premises), you must configure a CxLink to enable access.

## Supported Package Managers

Supported for projects that use Nuget, Maven, Npm, Gradle and Pip package managers.

## In this section

- [JFrog Artifactory Integration for SCA Scanner](jfrog-artifactory-integration-for-sca-scanner.md)
- [GitHub Container Registry Integration for SCA Scanner](github-container-registry-integration-for-sca-scanner.md)
