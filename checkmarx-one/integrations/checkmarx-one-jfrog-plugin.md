# Checkmarx One JFrog Plugin

## Overview

The Checkmarx One JFrog plugin analyzes each of the open source packages in your JFrog artifactory, comparing them against our Software Composition Analysis (SCA) vulnerability database in order to identify security risks and license requirements. The findings are added as "cx" properties to each artifact, enriching the metadata displayed in the Artifactory UI. This provides seamless risk visibility within your DevOps workflow, helping you to identify and address vulnerabilities early in the development process.

The plugin allows you to configure compliance thresholds, so that artifacts exceeding these thresholds are automatically marked as non-compliant. Based on configuration, the plugin can enforce policies that block the download and use of such artifacts, helping prevent the consumption of insecure components.

When compliance enforcement is enabled, artifacts that exceed configured security or license thresholds are blocked at usage time. This means that when a developer’s build workflow, CLI, or UI request attempts to download a non-compliant artifact, the request is denied.

Artifacts are not blocked at upload time, and remain stored in Artifactory. Enforcement applies only when an artifact is requested for use.

{% hint style="info" %}
Risks identified by this plugin are shown **only** in the artifactory itself, they are not synced with the Checkmarx One platform and corresponding projects are not created in your Checkmarx One account.
{% endhint %}

![](../../assets/image__11_.png)

### Analyzing Artifacts

There are 3 ways in which artifacts are analyzed, causing the "cx" properties to be populated:

1. **Manual scan** - An administrator can manually trigger a scan of all artifacts in the system or of specific repositories. An initial manual scan should be run as part of the installation process.
2. **Adding repositories** - When a user tries to add an artifact from a remote repository, if it doesn't yet have "cx" properties in JFrog, then it is automatically analyzed and the "cx" properties are populated.
3. **Continuous evaluation** - The plugin has a scheduled cron job that runs in the background to update the "cx" properties of your artifacts based on the latest vulnerability data in the Checkmarx SCA database. By default, these evaluations run once an hour. You can adjust this by editing the properties file as described below.

{% hint style="info" %}
The plugin evaluates only the artifact being downloaded.

Transitive dependencies of that artifact are not scanned or enforced by the JFrog plugin. For full dependency-tree analysis, including transitive open-source components, a Checkmarx One platform scan should be used.
{% endhint %}

### Main Features

- Validates the compliance of open source packages by analyzing licenses, identifying vulnerabilities, and detecting malicious components.
- Evaluates artifacts against user-defined policies to ensure compliance with security standards related to malicious packages, vulnerabilities and licenses.
- You can whitelist licenses approved by the organization. Any artifact with a license not included in this list will be flagged as violating the license compliance threshold.
- Provides configurable policy enforcement to prevent the download and use of non-compliant artifacts, with actionable remediation feedback.
- The plugin supports artifact scanning for specific user-defined repositories. One or more JFrog repository keys can be configured via the properties file to limit the scope of the scan.
- The plugin includes a scheduled cron job that runs periodically in the background to coninuously evaluate risks related to your artifacts.
- You can also periodically trigger manual scans of all artifacts within the configured repositories.

### Prerequisites

- Self-hosted JFrog Artifactory, version 7.90.14+
- A Checkmarx One account

  {% hint style="warning" %}
  Anyone with a valid Checkmarx One user account can use this plugin. There are no specific account permissions required.
  {% endhint %}

  To set up the integration you will need to provide the following account info:

  - **Base URL** of your Checkmarx One environment

    **Checkmarx One Server Base URLs**

    - US Environment - https://ast.checkmarx.net
    - US2 Environment - https://us.ast.checkmarx.net
    - EU Environment - https://eu.ast.checkmarx.net
    - EU2 Environment - https://eu-2.ast.checkmarx.net
    - DEU Environment - https://deu.ast.checkmarx.net
    - Australia & New Zealand – https://anz.ast.checkmarx.net
    - India - https://ind.ast.checkmarx.net
    - India 2 - https://ind-2.ast.checkmarx.net/
    - Singapore - https://sng.ast.checkmarx.net
    - UAE - https://mea.ast.checkmarx.net
    - Israel - https://gov-il.ast.checkmarx.net
  - **Base Authentication URL** of your Checkmarx One authentication server

    **Checkmarx One Authentication URLs**

    - US Environment - https://iam.checkmarx.net
    - US2 Environment - https://us.iam.checkmarx.net
    - EU Environment - https://eu.iam.checkmarx.net
    - EU2 Environment - https://eu-2.iam.checkmarx.net
    - DEU Environment - https://deu.iam.checkmarx.net
    - Australia & New Zealand – https://anz.iam.checkmarx.net
    - India - https://ind.iam.checkmarx.net
    - Singapore - https://sng.iam.checkmarx.net
    - UAE - https://mea.iam.checkmarx.net
    - Israel - https://gov-il.iam.checkmarx.net
  - **Tenant name** of your Checkmarx One tenant account
  - **API Key** - See [Creating an API Key for Checkmarx One Integrations](authentication-for-checkmarx-one-cli-and-plugins/creating-an-api-key-for-checkmarx-one-integrations.md)

### Limitations

- Properties are applied only to the **cached artifact entry** created by Artifactory for each remote package, and not to any internal or sub-artifacts.
- The plugin supports self-hosted JFrog Artifactory installations only, regardless of whether they are deployed on cloud infrastructure or on-premises servers. **JFrog Cloud** (SaaS) is not supported.
- While the Checkmarx One platform supports container image scanning, the JFrog plugin currently supports package artifacts only. **Container images and AI models are not scanned** by the plugin in its current version.

### Supported Package Managers

The plugin supports only projects that use the following package managers:

Bower, CocoaPods, Composer, Go, Gradle, Ivy, Maven, Npm, Nuget, Pypi, Sbt

Package ecosystems not listed (for example, CPAN) are **not supported** by the plugin

### Download Links

Download the latest version of the plugin [here](https://download.checkmarx.com/CxOneJFrogPlugin/latest/cxone_jfrog_plugin.zip).

## Installing and Configuring the Plugin

**To install and configure the plugin:**

1. Download the plugin using the above link.
2. Extract the archive.

   The extracted folder contains a "plugins" folder with the following items:

   - `checkmarxSecurityPlugin.groovy`
   - `cxsupplychainsecurity-plugin.properties`
   - lib > `artifactory-checkmarx-security-core.jar`
   - lib > `checkmarxSecurityPlugin.version`
3. Open the `cxsupplychainsecurity-plugin.properties` file.
4. Configure access to your Checkmarx One account by entering your account info (see [Prerequesites](#prerequisites) above) in the relevant properties as follows:

   - `cxsca.api-key` - **API Key**
   - `cxsca.cxurl` - **Base URL**
   - `cxsca.base-auth-url` - **Base Authentication URL**
   - `cxsca.tenant` - **Tenant name**
5. The plugin is configured to run as-is, using default settings. You can edit the settings to adjust the following configurations, as described in [Adjusting Property Configurations](#adjusting-property-configurations) below:

   - Adjust thresholds for non-compliance (Default: Only malicious packages are non-compliant)
   - Block usage of non-compliant artifacts (Default: Not blocked)
   - Add or remove allowed licenses (Default: Allow only MIT,Apache 2.0,BSD 3,ISC,Zlib)
   - Specify repos for scanning (Default: All repos are scanned)
   - Adjust the analysis schedule (Default: every hour)
6. Once the configuration is completed, save the changes to apply them.
7. Copy the files from the plugin folder to your installed Artifactory directory at `${ARTIFACTORY_HOME}/var/etc/artifactory/plugins`.
8. If your JFrog instance is not configured to reload plugins automatically (this is the default configuration), then you will need to manually reload the plugins using the following command:

   ```
   curl -u username:password -X POST " https://<JFrogURL>/artifactory/api/plugins/execute/checkmarxSecurityReload
   ```
9. To verify that the plugin has been installed successfully, log in to your JFrog Artifactory instance and navigate to **Administrator** > **Platform Monitoring** > **Artifactory Logs** (i.e., https://\<JFrogURL>/ui/admin/artifactory/advanced/system_logs).

   The logs should show:

   <figure><img src="../../assets/Image_2099.png" alt="" width="272"><figcaption></figcaption></figure>
10. After completing the installation, run an initial analysis of your artifacts using the following command:

    {% hint style="info" %}
    By default, all artifacts are scanned. If you configured specific repositories in the properties file, then only the specified repos are scanned.
    {% endhint %}

    {% hint style="warning" %}
    If you didn't configure `cxsca.repositories`, the scan will run on all artifacts in all of your repositories. This may take a long time and consume significant system resources. It may be preferable to scan a few remote repositories at a time using the configuration property `cxsca.repositories`. Repeat scans for the remaining remote repositories by updating this property. Once you have run an initial scan on all repos, for continuous evaluation you can set the `cxsca.repositories` property as empty to scan all repositories, or list all remote repositories that you want to scan on a regular basis.
    {% endhint %}

    ```
    curl -u username:password -X POST "<JFrogURL>/artifactory/api/plugins/execute/scanArtifacts"
    ```

### Adjusting Property Configurations

After installing the plugin, you can customize your plugin by adjusting the following properties in the `cxsupplychainsecurity-plugin.properties` file.

Whenever you change a property you must run the following command to update the configuration:

```
curl -u username:password -X POST "<JFrogURL>/artifactory/api/plugins/execute/checkmarxSecurityReload"
```

{% hint style="warning" %}
When you change the `cxsca.update-period` property, you need to restart the system in order for the change to take effect.
{% endhint %}

#### Compliance Thresholds

Compliance thresholds define the **maximum number of vulnerabilities allowed** for an artifact to be considered compliant. If the number of vulnerabilities for a given severity **exceeds** the configured threshold, the artifact is marked non-compliant. Setting a threshold value to `none` means that severity level is **ignored** during compliance evaluation.

For example:

- Setting `cxsca.security.risk.critical.threshold` to `0` means no critical vulnerabilities are allowed
- Setting it to `1` allows up to one critical vulnerability
- Setting it to `none` disables critical vulnerability evaluation entirely

| **Property Name** | Possible Values | Default | **Description** |
|---|---|---|---|
| cxsca.security.risk.critical.threshold | none, Integer >=0 | none | Sets the maximum number of Critical vulnerabilities allowed; if the count exceeds this value the artifact is non-compliant.<br>`none` means this severity level is not evaluated at all. |
| cxsca.security.risk.high.threshold | none, Integer >=0 | none | Sets the maximum number of High vulnerabilities allowed; if the count exceeds this value the artifact is non-compliant.<br>`none` means this severity level is not evaluated at all. |
| cxsca.security.risk.medium.threshold | none, Integer >=0 | none | Sets the maximum number of Medium vulnerabilities allowed; if the count exceeds this value the artifact is non-compliant.<br>`none` means this severity level is not evaluated at all. |
| cxsca.security.risk.low.threshold | none, Integer >=0 | none | Sets the maximum number of Low vulnerabilities allowed; if the count exceeds this value the artifact is non-compliant.<br>`none` means this severity level is not evaluated at all. |
| cxsca.security.allow-malicious | yes/no | no | `no` indicates that malicious packages are considered non-compliant |

#### Block Usage

| **Property Name** | Possible Values | Default | **Description** |
|---|---|---|---|
| cxsca.security.block-by-default | yes/no | no | `yes` indicates that non-compliant artifacts will be blocked from being downloaded or used.<br>This setting does not prevent artifacts from being uploaded to or stored in Artifactory. |

#### Allowed Licenses

| **Property Name** | Possible Values | Default | **Description** |
|---|---|---|---|
| cxsca.security.allowed-licenses | \[License names\] | MIT,Apache 2.0,BSD 3,ISC,Zlib | A comma separated list of licenses that are allowed. All other licenses will be considered non-compliant. |

#### Remote Repositories to be Analyzed

| **Property Name** | Possible Values | Default | **Description** |
|---|---|---|---|
| cxsca.repositories | JFrog repository key | All repositories | If this property is defined, then only the specified repos are analyzed by Checkmarx. Enter a comma separated list of JFrog repository keys for the repos that will be analyzed. |

#### Continuous Evaluation Frequency

| **Property Name** | Possible Values | Default | **Description** |
|---|---|---|---|
| cxsca.update-period | 1-168 | 1 hour | Specify the number of hours of the interval between evaluations. |

## Using the Plugin

Once the plugin is installed and an initial scan has been run, the results are displayed for each scanned artifact as part of the artifact's properties. The data is automatically updated periodically by our continuous evaluation process.

### Checkmarx Artifact Properties

For each artifact that has been analyzed by Checkmarx One, the following properties are added to the properties tab of the artifact.

| **Property Name** | Possible Values | **Description** |
|---|---|---|
| CxSCA.TotalVulnerabilities | Integer >=0 | The total number of vulnerabilities identified for the artifact |
| CxSCA.Vulnerabilities.Critical | Integer >=0 | The total number of Critical vulnerabilities identified for the artifact |
| CxSCA.Vulnerabilities.High | Integer >=0 | The total number of High vulnerabilities identified for the artifact |
| CxSCA.Vulnerabilities.Medium | Integer >=0 | The total number of Medium vulnerabilities identified for the artifact |
| CxSCA.Vulnerabilities.Low | Integer >=0 | The total number of Low vulnerabilities identified for the artifact |
| CxSCA.IsMalicious | yes/no | `yes` indicates that the package is malicious |
| CxSCA.Licenses | \[string\] | A list of licenses associated with the artifact |
| Cx.LastScanned | Date | The date and time that the artifact was last scanned |
| Cx.IsCompliant | yes/no | `yes` indicates the the artifact complies with the security and licensing thresholds that you have configured in the Checkmarx JFrog plugin.<br>`no` indicates that the artifact has security risks and/or disallowed licenses that make it non-compliant with the thresholds that you have configured in the Checkmarx JFrog plugin. |
| Cx.ForceAllow | yes/no | You can set this as `yes` if you would like to override non-compliance of the artifact and always allow usage of the artifact. |
| Cx.NonCompliantReason | \[string\] | For non-compliant artifacts, this shows a list of reasons why this artifact is categorized as non-compliant. |

### Exempting Artifacts from Compliance

If you have set thresholds for blocking usage, you can override these thresholds for specific artifacts.

{% hint style="warning" %}
Once an artifact is exempted, the exemption applies globally to all developers and applications. Because Artifactory does not track which developers or applications consume an artifact, and the plugin does not support granular override rules, all users will be able to download the artifact despite it containing risks of any severity level.
{% endhint %}

**To override the threshold:**

1. Open the properties tab for the desired artifact.
2. Set the property `Cx.ForceAllow` to `yes`.

### Running Scans Manually

In addition to the analysis that is done in the background according to the plugin configuration, you can also trigger a manual scan from time to time using the following command:

```
curl -u username:password -X POST "<JFrogUrl>/artifactory/api/plugins/execute/scanArtifacts"
```

### Getting Info About Blocked Artifacts

If a developer tries using an artifact that is blocked from usage due to non-compliance with the plugin thresholds, they will receive an **HTTP 403** error. If the developer would like to understand the reason for the blocked usage, they can follow the artifact link displayed in the build console output. They can then view the content of the json response. They can also check the artifact properties to see the value for `Cx.NonCompliantReason`.

### Event Logs

By default, the INFO level event logs from the plugin are written to the artifactory logs. You can access those logs using following URL:

```
https://<JFrogURL>/ui/admin/artifactory/advanced/system_logs
```

The following are some common examples of event logs:

- **Manual Scan Logs**

  - Starting scan of artifacts
  - Success Log: “Scanning completed for artifacts of all repositories. Total artifacts: {}, Successfully processed: {}, Processing failed: {}.”;
- **Background Scan Logs**

  - Number of packages to re-scan :{}
  - Success Log: “Correlation-Statistics: Total artifacts successfully processed: {}, total artifacts failed: {}";
- **Processing Chunk**

  - Success Log: “Chunk {} statistics: Successfully processed: {}, Failed: {}“
- **Each Repository**

  - Processing repository: {}
  - Success Log: Processed: {}, Successful: {}, Failed: {} artifacts in repository: {}
- **Specific repository configuration not found in artifactory**

  - Repo config not found for key: {}, repoPath={}

#### Troubleshooting

For troubleshooting purposes, you can change the log level to DEBUG, so that all debug logs are sent to the JFrog logs.

1. insert the following snippet in `$ ${ARTIFACTORY_HOME}/var/etc/artifactory/logback.xml:`

   ```

   <logger name="io.checkmarx" level="debug"/>
   <logger name="com.checkmarx.plugin" level="debug"/>
   ```
2. View the generated logs in the `artifactory-service.log` file in the `$ {ARTIFACTORY_HOME}/var/log` folder, or access them using the system logs URL:

   ```
   https://<JFrogURL>/ui/admin/artifactory/advanced/system_logs
   ```

### FAQ

**Can the CxOne JFrog plugin replace JFrog Curation?**

The CxOne JFrog plugin is not a replacement for the JFrog Curation product. JFrog Curation prevents non-compliant artifacts from being added to Artifactory, while the CxOne JFrog plugin operates between the developer workflow and Artifactory, enforcing policy at artifact usage time.

**Does the plugin analyze artifact reputation or malicious behavior?**

Yes. In addition to vulnerability and license analysis, the plugin evaluates whether a package is flagged as malicious by the Checkmarx One.

**How does the plugin block artifact usage?**

If an artifact is marked non-compliant, JFrog is instructed to block access to the artifact during build workflows, UI downloads, or CLI usage.
