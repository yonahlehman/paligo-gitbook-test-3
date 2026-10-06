# Configuring Projects Using Config as Code Files

**Config as Code** provides an additional level of scan configuration beyond **Global Account Settings** and **Project Rules** by enabling configuration through code-based files.

Before scanning, you can define scan behavior by placing a Config as Code file directly within the **repository** or **ZIP file** being scanned. These settings take precedence over the corresponding settings defined in Global Account Settings and Project Rules and apply only to the specific repository or ZIP scan that contains the configuration file.

## Configuration Rules

- The Config as Code `config.yml` file supports the same parameters available in Global Account Settings and Project Rules. For the full list of parameters, see [below](#scanners-parameters-configuration-options).
- By default, **Allow Override** is enabled for all supported parameters across all configuration levels.
- If **Allow Override** is disabled for a specific parameter in the Global Account Settings or the Project Rules, configuring that same parameter in the Config as Code `.yml` file will have no effect.
- A parameter cannot be assigned multiple values within the same configuration level.
- Parameters configured directly at scan runtime override the corresponding settings defined in the Config as Code file.

## Configuring Repository Scans

1. In the target repository, create a `.checkmarx` folder.
2. Inside the `.checkmarx` folder, create a `config.yml` file using the template below.
3. Configure the required scanner parameters according to the **Scanner Parameter Configuration Options** tables below.
4. Save the file before running the scan.

## Configuring ZIP File Scans

1. Create the ZIP file to be scanned.
2. Create a `.checkmarx` folder.
3. Inside the `.checkmarx` folder, create a `config.yml` file using the template below.
4. Configure the required scanner parameters according to the **Scanner Parameter Configuration Options** tables below.
5. Save the file.
6. Place the `.checkmarx` folder in the root directory of the ZIP file. If the folder is not located in the root directory, the Config as Code configuration will not be applied during the scan.

## Creating ZIP Files from Repositories

1. Download the repository as a ZIP file. The repository must not already contain a `.checkmarx` folder.
2. Follow the steps in **Configuring ZIP File Scans** above.

## config.yml Template

Use the following template as the basis for your `config.yml` file:

```
version: 1

# checkmarx-specific related configuration
# every value in this section is optional
checkmarx:
  scan:
    configs:
      sast:
        presetName: 'ASA Premium'
        fastScanMode: 'false'
        incremental: 'false'
        incrementalChangeThreshold: "10"
        lightQueries: "false"
        baseBranch: "main"
        languageMode: 'multi'
        filter: '!*.java,!*.cpp'
        engineVerbose: 'true'
        incrementalInBranch: "true"
        recommendedExclusions: "true"
        defaultConfigId: ""

      sca:
        filter: '!*.cpp'
        vulnerabilityComparisonMode: "Branch-Based"
        exploitablePath: 'true'
        javaLanguageVersion: "25"
        pythonLanguageVersion: "3.13"

      kics:
        filter: '*.java'
        platforms: 'Ansible,CloudFormation,Dockerfile'
        presetId: '047be3a8-c9d6-4c02-90d5-c243418c7abc'

      containers:
        imagesFilter: ""
        filesFilter: "!node_modules,!dist,!build"
        packagesFilter: ""
        nonFinalStagesFilter: "false"

      apisec:
        swaggerFilter: ''

      microengines:
        gitCommitHistory: "true"
```

## Scanners Parameters Configuration Options

### SAST Scanner Parameters

The table below presents all the optional parameters for the SAST scanner and their optional values.

{% hint style="info" %}
There is an additional configuration option for filtering, which compliance results to show. This can currently only be configured via REST API. See [API documentation](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/branches/main/cs61sszap44td-scan-configuration-service#compliance-filtering).
{% endhint %}

{% hint style="info" %}
CLI flags are submitted on the scan level with the [scan create](../../../cli-tool/checkmarx-one-cli-commands/scan/scan-create.md) command. API configs can be configured on the account or project level using the [Configuration](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/branches/main/cs61sszap44td-scan-configuration-service) API or on the scan level as part of the request body of the [POST /scans](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/branches/main/cs61sszap44td-scan-configuration-service) API. When using the POST /scans API the `scan.config.sast` prefix is left out.
{% endhint %}

| **Parameter** | **Values** | **Notes** | CLI | API | Config as Code |
|---|---|---|---|---|---|
| **PresetName** | All the available SAST Presets that exist in the system | • For the full Presets list (including descriptions) go to the following link:<br>Predefined Presets<br>• The default preset that is used is **ASA Premium** | `--sast-preset-name boolean` | `scan.config.sast.presetName`<br>` {`<br>` "key": "scan.config.sast.presetName",`<br>` "value": "ASA Premium",`<br>` "allowOverride": true`<br>` }` | `presetName` |
| **Fast scan mode** | true / false | By default, the Fast Scan mode is set to **true**.<br>For more information, refer to [Fast Scan Mode](#fast-scan-configuration). | `--sast-fast-scan boolean` | `scan.config.sast.fastScanMode`<br>` {`<br>` "key": "scan.config.sast.fastScanMode",`<br>` "value": "true",`<br>` "allowOverride": true`<br>` }` | `fastScanMode` |
| **Findings Analysis** | true/false | An optional capability that automatically classifies scan results and filters out results identified as unlikely to be relevant. When enabled, the results viewer shows only findings classified as relevant, helping analysts focus on actionable risks.<br>For more information, refer to SAST Findings Analysis. | | `{`<br>` "key": "scan.config.sast.findingsAnalysis",`<br>` "value": "true",`<br>` "allowOverride": true`<br>`}` | `findingsAnalysis` |
| **LLM-based scanning** | true/false | Configure to activate LLM-based scanning on SAST scans. | | `{"key": "scan.config.sast.extendedAnalysis","value": "true","allowOverride": true}` | `extendedAnalysis` |
| **Light queries** | true/false | Determines whether the scan should be performed using light queries or standard queries. Light Queries are simplified versions of standard queries focusing on the most urgent vulnerabilities, helping you spot threats faster.<br>For more information, refer to [Light Queries](#light-queries).<br>• When set to `true`, SAST will scan using light queries, quickly focusing on the most immediate and exploitable weaknesses.<br>• When set to `false`, SAST will not scan using light queries; it will scan using standard queries. | `--sast-light-queries` | `scan.config.sast.lightQueries`<br>` {`<br>` "key": "scan.config.sast.lightQueries",`<br>` "value": "true",`<br>` "allowOverride": true`<br>` }` | `lightQueries` |
| **incremental** | true / false | Determines whether the scan should be performed incrementally or as a full scan.<br>• When set to `true`, SAST will only scan the code changes made since the last scan, significantly reducing the scan time and resource usage.<br>• When set to `false`, SAST will perform a full scan. Full scans are more comprehensive but take longer to complete and use more resources. | `--sast-incremental boolean` | `scan.config.sast.incremental`<br>` {`<br>` "key": "scan.config.sast.incremental",`<br>` "value": "true",`<br>` "allowOverride": true`<br>` }` | `incremental` |
| **Recommended exclusions** | true / false | Determines whether the system should automatically exclude certain files and folders from the scan. Enabled by default.<br>By default, recommended exclusions is set to **true**.<br>• When set to `true`, SAST applies predefined exclusions, allowing developers to scan faster and focus on the most relevant code areas.<br>• SAST will include all files and directories in the scan when set to `false`. | --sast-recommended-exclusions | `scan.config.sast.recommendedExclusions`<br>` {`<br>` "key": "scan.config.sast.recomendedExclusions",`<br>` "value": "true",`<br>` "allowOverride": true`<br>` }` | `recommendedExclusions` |
| **LanguageMode** | primary / multi | For more information, see:<br>Specifying a Code Language for Scanning<br>Supported Code Languages and Frameworks:<br>• Click Engine Pack Versions and Delivery Model.<br>• Select the latest EP (Engine Pack) Supported Code Languages and Frameworks.<br>{% hint style="info" %}<br>By default, the languageMode is **Multi**.<br>{% endhint %} | | `scan.config.sast.languageMode`<br>` {`<br>` "key": "scan.config.sast.languageMode",`<br>` "value": "primary",`<br>` "allowOverride": true`<br>` }` | `languageMode` |
| **Folder/file filter** | Allow users to select specific folders or files to include or exclude from the code scanning process. | • Including a file type - \*.java<br>• Excluding a file type - !\*.java<br>• Use “,” sign to chain file types<br>for example: \**.*java*,*\*.js<br>• The parameter also supports including/excluding folders.<br>• regex is not supported. | `--sast-filter <string>` | `scan.config.sast.filter`<br>` {`<br>` "key": "scan.config.sast.filter",`<br>` "value": "*.java",`<br>` "allowOverride": true`<br>` }` | `filter` |
| **EngineVerbose** | true / false | • true = Enables PRINT_DEBUG mode.<br>• false = Enables PRINT_LOG mode. | | `scan.config.sast.engineVerbose`<br>` {`<br>` "key": "scan.config.sast.engineVerbose",`<br>` "value": "true",`<br>` "allowOverride": true`<br>` }` | `engineVerbose` |
| **Results scope level** | Project / Application | When you triage SAST results (change state, severity, comments), by default the adjustment applies only to identical results within that **Project**. You can adjust this setting to apply changes to all identical results in the entire **Application**. | | | |
| **Threshold for Incremental Scans (%)** | 0.5 - 10 (intervals of .5) | When running an incremental scan, if the changes from the previous scan exceed the threshold, a full scan is run. By default the threshold is 7%. Use this configuration to set a custom threshold. For more information, see [Adjusting the Incremental Scan Threshold](../../scanning-projects/README.md#adjusting-the-incremental-scan-threshold). | | `scan.config.sast.incrementalChangeThreshold`<br>` {`<br>` "key": "scan.config.sast.incrementalChangeThreshold",`<br>` "value": "1",`<br>` "allowOverride": true`<br>` }` | `incrementalChangeThreshold` |
| **Incremental in branch (API)** | true / false | When working with branches within Checkmarx GitHub Integration, if you open a pull request to merge into the master branch, you could run a faster incremental scan instead of a longer full scan. This capability is activated by configuring this setting to **true**. By default, it is **false**, so that only scans of the main branch are run as incremental. For more information, see [Incremental Scans of Branches](../../scanning-projects/README.md#incremental-scans-of-branches). | | `scan.config.sast.incrementalInBranch`<br>` {`<br>` "key": "scan.config.sast.incrementalInBranch",`<br>` "value": "true",`<br>` "allowOverride": true`<br>` }` | `incrementalInBranch` |
| **Mandatory Comment When Changing State** | true / false | When **true**, you are not able to save a state change until you add a comment explaining the rationale behind the change. | | | |
| **Grouping Similar Results** | Similarity ID / Attack Vector ID | Specify which identifier is used to define specific instance of a SAST result. Attack Vector ID is a more precise, flow-based grouping than Similarity ID. This determines which related results triage changes will be applied to.<br>For more info, see [Account Settings for Grouping Similar Results](../../managing-triaging-vulnerabilities/triaging-sast-results/account-settings-for-grouping-similar-results.md)<br>{% hint style="warning" %}<br>When you change this setting, previously run AI Triage is no longer applicable. Therefore, if you subsequently run AI Triage on the same result, AI Triage will run again and consume additional credits.<br>{% endhint %} | | | |

#### ASA Premium Preset

ASA Premium Preset is a part of the SAST collection of presets.

This Preset is available only for Checkmarx One. Its usage is described in the table below.

| **Preset** | **Usage** | **Includes vulnerability queries for....** |
|---|---|---|
| ASA Premium | The ASA Premium preset contains a subset of vulnerabilities that Checkmarx AppSec Accelerator team considers to be the starting point of the Checkmarx AppSec program.<br>The preset might change in future versions. The AppSec Accelerator team will remove old/deprecated queries or include new and improved queries in a continuously manner. | Apex, ASP, CPP, CSharp, Go, Groovy, Java, JavaScript, Kotlin (non-mobile only), Perl, PHP, PLSQL, Python, Ruby, Scala, VB6, VbNet, Cobol, RPG and VbScript coding languages. |
| ASA Mobile Premium | The ASA Mobile Premium preset is a dedicated preset designed for mobile apps.<br>The ASA Premium Mobile preset contains a subset of vulnerabilities that Checkmarx AppSec Accelerator team considers to be the starting point of the Checkmarx AppSec program.<br>The preset might change in future versions. The AppSec Accelerator team will remove old/deprecated queries or include new and improved queries in a continuously manner. | Apex, ASP, CPP, CSharp, Go, Groovy, Java, JavaScript, Kotlin (non-mobile only), Perl, PHP, PLSQL, Python, Ruby, Scala, VB6, VbNet, Cobol, RPG and VbScript coding languages. |

#### Fast Scan Configuration

Fast Scan configuration aims to find the perfect balance between thorough security tests and the need for quick and actionable results. There’s no need to choose between speed and security.

Fast Scan mode decreases the scanning time of projects up to 90%, making it faster to identify relevant vulnerabilities and enable continuous deployment while ensuring that security standards are followed. This will help developers tackle the most relevant vulnerabilities.

While the Fast Scan configuration identifies the most significant and relevant vulnerabilities, the In-Depth scan mode offers deeper coverage. For the most critical projects with a zero-vulnerability policy, it is advised also to use our In-Depth scan mode.

Fast Scan mode is activated by default. It can be deactivated manually on the **Tenant** (Account), **Project** or **Scan** level.

{% hint style="warning" %}
To expedite the results retrieval, the scanning process has been optimized to reduce the number of stages and flows involved in the scan. With this enhancement, the queries related to ASPM are not executed and results won’t be generated when utilizing this mode.

You may also notice impact on the API Security scanner results.
{% endhint %}

##### Fast Scan limitations

- Fast Scan is not advised for CPP, JS and Kotlin.
- Faster scans are achieved at the expense of comprehensive results.
- Differences in scan results are expected due to the methodology used by Fast Scan. It explores fewer flows compared to the "in-depth" mode, which may result in some vulnerabilities being missed or unique findings that differ from the standard scan.
- When fast scan mode is enabled, the language mode always runs as **Primary**, and any SAST rule that sets **languageMode** to multi is ignored until fast scan mode is turned off.

#### Light Queries

Light Queries are simplified versions of existing queries that focus on the most exploitable vulnerabilities. They help you prioritize threats while filtering out uncommon edge cases for clearer analysis. Light Queries are not intended to replace the more robust standard queries but offer an alternative form of analyzing code by focusing on the most immediate threats and readily exploitable weaknesses as quickly as possible. These queries offer a more straightforward way to analyze code, giving you key findings without the complexity. The Light Queries have a more restrictive subset of results regarding inputs and sinks and a broader one regarding sanitizers.

{% hint style="warning" %}
Consider the following when Light Queries are enabled:

- The Similarity ID, source, and sync remain unchanged whether or not Light Queries are enabled.
- When Light Queries are enabled, the scan results are a subset of those from a standard query (i.e., when Light Queries are disabled).
- When scanning with Light Queries enabled, the scan will likely get fewer results.
{% endhint %}

##### Supported Languages and Detected Vulnerabilities

Light Queries support the following languages:

- Java
- JavaScript

  - Client_DOM_XSS
  - Client_DOM_Stored_XSS
  - Client_DOM_Code_Injection
  - Client_DOM_Stored_Code_Injection
  - Client_DOM_Code_Injection_from_AJAX
  - Client_DOM_XSS_from_Ajax
- C#

The following vulnerabilities are detected in all the above languages when Light Queries are enabled:

- SQL Injection
- Reflected XSS

##### Enabling Light Queries

Enable Light Queries under the Account Settings page by setting its value to true. By default, Light Queries are set to false (disabled), and the **Allow Override** option is enabled.

<figure><img src="../../../../assets/acctsett_lq.png" alt="" width="576"><figcaption></figcaption></figure>

When creating a new project, on the project settings page, you must enable Light Queries as a rule. To add Light Queries as a rule, perform the following:

1. Click **+ Add Rule**. The scanner, mode, and value dropdown options appear.
2. Select **SAST**, **light queries**, and **true** for the scanner, mode, and value dropdowns.
3. Select **Create Project** when finished.

<figure><img src="../../../../assets/newprj_lq.png" alt="" width="432"><figcaption></figcaption></figure>

To delete a rule, click <img src="../../../../assets/Trash.png" alt="" data-size="line"> at the end of the rule's row.

### IaC Security Scanner Parameters

When configured globally, these parameters will apply to IaC Security scans across all projects. When configured at the project level, they will apply only to IaC Security scans for that project.

The table below presents all the optional parameters and their values.

{% hint style="info" %}
CLI flags are submitted on the scan level with the [scan create](../../../cli-tool/checkmarx-one-cli-commands/scan/scan-create.md) command. API configs can be configured on the account or project level using the [Configuration](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/branches/main/cs61sszap44td-scan-configuration-service) API or on the scan level as part of the request body of the [POST /scans](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/branches/main/cs61sszap44td-scan-configuration-service) API. When using the POST /scans API the `scan.config.kics` prefix is left out.
{% endhint %}

| **Parameter** | **Values** | **Notes** | CLI | API | Config as Code |
|---|---|---|---|---|---|
| **Folder/file filter** | Allow users to select specific folders or files to include or exclude from the code-scanning process. | • Including a file type - \*.java; .tf<br>• Excluding a file type - !\*.java; !.yaml<br>• Use “,” sign to chain file types, for example: .tf,.json<br>for example: \**.*java*,*\*.js<br>• The parameter also supports including/excluding folders.<br>• regex is not supported. | `--iac-security-filter <string>` | scan.config.kics.filter<br>`  {`<br>` "key": "scan.config.kics.filter",`<br>` "value": "*.java",`<br>` "allowOverride": true`<br>` }` | `filter` |
| **Platforms** | • Ansible<br>• Azure Blueprints<br>• AzureResourceManager<br>• Buildah<br>• CICD<br>• CloudFormation<br>• CDK<br>• Crossplane<br>• Docker<br>• Docker Compose<br>• Dockerfile<br>• Google Deployment Manager<br>• gRPC<br>• Helm<br>• Knative<br>• Kubernetes<br>• OpenAPI<br>• Pulumi<br>• SAM<br>• ServerlessFW<br>• Terraform | {% hint style="info" %}<br>Configure one or more platforms, separated by a comma.<br><br>The parameter means you only want to run scans (queries) for those platforms.<br><br>For example, Ansible, CloudFormation, Dockerfile<br>{% endhint %}<br>{% hint style="warning" %}<br>Any mistake in the platform characters will cause an error.<br>{% endhint %} | `--iac-security-platforms <string>, <string>` | scan.config.kics.platforms<br>` {`<br>` "key": "scan.config.kics.platforms",`<br>` "value": "GRPC",`<br>` "allowOverride": true`<br>` }` | `platforms` |
| **Preset Name** | All the available IaC Security Presets that exist in the system | There are no Checkmarx Default Presets now. For more information on IaC presets, see [here](../../resource-management/iac-security-presets-management.md).<br>{% hint style="warning" %}<br>The preset ID for IaC Security must be a valid UUID. Once you create one, you can copy the **PresetID** from the IaC Presets page.<br>{% endhint %} | | scan.config.kics.presetId<br>` {`<br>` "key": "scan.config.kics.presetId",`<br>` "value": "047be3a8-c9d6-4c02-90d5-c243418c7d8a",`<br>` "allowOverride": true`<br>` }` | `presetId` |

### SCA Scanner Parameters

When configured globally, these parameters will apply to SCA scans across all projects. When configured at the project level, they will apply only to SCA scans for that project.

The table below presents all the optional parameters, and their values.

{% hint style="info" %}
CLI flags are submitted on the scan level with the [scan create](../../../cli-tool/checkmarx-one-cli-commands/scan/scan-create.md) command. API configs can be configured on the account or project level using the [Configuration](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/branches/main/cs61sszap44td-scan-configuration-service) API or on the scan level as part of the request body of the [POST /scans](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/branches/main/cs61sszap44td-scan-configuration-service) API. When using the POST /scans API the `scan.config.sca` prefix is left out.
{% endhint %}

| **Parameter** | **Values** | **Notes** | CLI | API | Config as Code |
|---|---|---|---|---|---|
| **Folder/file filter** | Allow users to select specific folders or files that they want to include or exclude from the code scanning process. | • Including a file type - \*.java<br>• Excluding a file type - !\*.java<br>• Use “,” sign to chain file types.<br>for example: \**.*java*,*\*.js<br>• The parameter also supports including/excluding folders.<br>• regex is not supported. | `--sca-filter <string>` | `scan.config.sca.filter`<br>` {`<br>` "key": "scan.config.sca.filter",`<br>` "value": "*.java,*.js",`<br>` "allowOverride": true`<br>` }` | `filter` |
| **Exploitable Path** | Toggle On/Off | When Exploitable Path is activated, scans that use the SCA scanner will identify whether or not there is an exploitable path from your source code to the vulnerable 3rd party package.<br>Learn more about Exploitable Path. | `--sca-exploitable-path <string>` | `scan.config.sca.ExploitablePath`<br>` {`<br>` "key": "scan.config.sca.ExploitablePath",`<br>` "value": "true",`<br>` "allowOverride": true`<br>` }` | `ExploitablePath` |
| **New Vulnerability Comparison Mode** | Project-Wide (default) or Branch-Based | Determines what is used as the base-line for determining whether or not a vulnerability is a New finding in the current scan.<br>• Project-wide - compares to the most recent scan of any branch of the project.<br>• Branch-based - compares to the most recent scan of the specific branch that was scanned. | | `scan.config.sca.vulnerabilityComparisonMode`<br>` {`<br>` "key": "scan.config.sca.vulnerabilityComparisonMode",`<br>` "value": "Branch-Based",`<br>` "allowOverride": true`<br>` }` | `vulnerabilityComparisonMode` |
| **Java Language Version** | 8, 11, 17, 21 (default) or 25 | Specify the Java version used for dependency resolution for gradle package manager. This version does not affect Java version used for maven resolution. If not defined, gradle scans will run with Java version 21 by default. | | `scan.config.sca.javaLanguageVersion`<br>` {`<br>` "key": "scan.config.sca.javaLanguageVersion",`<br>` "value": "17",`<br>` "allowOverride": true`<br>` }` | `javaLanguageVersion` |
| **UV Resolution** | true/false | Uses the UV package manager instead of pip for Python dependency resolution. | | `scan.config.sca.useUvResolution`<br>` {`<br>` "key": "scan.config.sca.useUvResolution",`<br>` "value": "true",`<br>` "allowOverride": true`<br>` }` | `useUvResolution` |
| **Python Language Version** | 2.7, 3.11, 3.12, 3.13 (default) or 3.14 | Specify the Python version used for dependency resolution for pip and poetry package managers. Poetry does not support Python prior to version 3, if version 2.7 is supplied, the default version is used instead. If not defined, scans will run with Python version 3.13 by default. | | `scan.config.sca.pythonLanguageVersion`<br>` {`<br>` "key": "scan.config.sca.pythonLanguageVersion",`<br>` "value": "3.12",`<br>` "allowOverride": true`<br>` }` | `pythonLanguageVersion` |

### API Security Scanner Parameters

When configured globally, these parameters will apply to API Security scans across all projects. When configured at the project level, they will apply only to API Security scans for that project.

The table below presents the optional parameters, and their optional values.

{% hint style="info" %}
API configs can be configured on the account or project level using the [Configuration](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/branches/main/cs61sszap44td-scan-configuration-service) API or on the scan level as part of the request body of the [POST /scans](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/branches/main/cs61sszap44td-scan-configuration-service) API. When using the POST /scans API the `scan.config.apisec` prefix is left out.
{% endhint %}

| Parameter | Values | Notes | CLI | API | Config as Code |
|---|---|---|---|---|---|
| Swagger folder/file filter | Swagger folder path or any folder/file type.<br>Allow users to select specific folders or files that they want to include or exclude from the code scanning process. | • Including a file type - \*.java<br>• Excluding a file type - !\*.java<br>• Use “,” sign to chain file types.<br>For example: \*.java,\*.js<br>• The parameter also supports including/excluding folders.<br>• regex is not supported. | | `scan.config.apisec.swaggerFilter` | `swaggerFilter` |

### Container Security Scanner Parameters

Checkmarx One offers robust filter settings to enhance container security by enabling users to configure their scans for precision and relevance. Below is an overview of the four available filter settings, designed to reduce noise and focus on critical vulnerabilities in your scans.

The following table provides an overview of the functionality of each filter. Additional details about the usage and syntax for these filters is available in [Filter Usage Details](../../container-security/container-security-filter-usage.md#filter-usage-details).

{% hint style="info" %}
CLI flags are submitted on the scan level with the [scan create](../../../cli-tool/checkmarx-one-cli-commands/scan/scan-create.md) command. API configs can be configured on the account or project level using the [Scan Configuration](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/branches/main/cs61sszap44td-scan-configuration-service) APIs or on the scan level as part of the request body of the [POST /scans](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/branches/main/cs61sszap44td-scan-configuration-service) API. When using the POST /scans API the `scan.config.containers` prefix is left out.
{% endhint %}

| Filter name | Description | Syntax | Examples | CLI | API | Config as Code |
|---|---|---|---|---|---|---|
| Folder/file filter | Specify **files and folders** to be included (allow list) or excluded from (block list) scans. You can create complex filters that combine include and exclude patterns. | `*.abc` - include specific file types<br>`!*.abc` - exclude specific file types<br>`!/folder-name/` - exclude a specific folder<br>{% hint style="success" %}<br>You can submit multiple items separated by a comma.<br>{% endhint %} | `!Dockerfile*` - exclude all Dockerfiles in the root folder<br>`*.yaml,*.yml` - include all yaml and yml files | `--containers-file-folder-filter <string>` | scan.config.containers.filesFilter<br>` {`<br>` "key": "scan.config.containers.filesFilter",`<br>` "value": "*.yaml,*.yml",`<br>` "allowOverride": true`<br>` }` | `filesFilter` |
| Image/tag filter | Include or exclude **images** by image name and/or tag. | `image-name:image-tag` - include by image name and tag<br>`image-name` - include by image name<br>`!:image-tag` - exclude by image tag<br>{% hint style="success" %}<br>You can use wildcard (\*) at the beginning, end or both.<br>{% endhint %} | `!*test-image*` - to exclude all images that contain "test-image" in their name<br>`!:*latest` - to exclude all image tags that end with "latest" | `--containers-image-tag-filter <string>` | scan.config.containers.imagesFilter<br>` {`<br>` "key": "scan.config.containers.imagesFilter",`<br>` "value": "!*test-image*",`<br>` "allowOverride": true`<br>` }` | `imagesFilter` |
| Package regex Filter | Prevent sensitive **packages** from being sent to the cloud for analysis. Exclude packages by package name or file path using regex.<br>{% hint style="success" %}<br>Excluded packages will nonetheless appear in the scan results. However, no vulnerabilities will be identified in those packages since their info wasn't sent to the cloud for analysis.<br>{% endhint %} | Regex | `^internal-.*` - filters out any package names starting with "internal-" | `--containers-package-filter <string>` | scan.config.containers.packagesFilter<br>` {`<br>` "key": "scan.config.containers.packagesFilter",`<br>` "value": "^internal-.*",`<br>` "allowOverride": true`<br>` }` | `packagesFilter` |
| Exclude non-final stages filter | Exclude all images that are not from the final stage of the build process, so that only the final deployable image is scanned.<br>{% hint style="success" %}<br>Only supported for Dockerfile images.<br>{% endhint %} | True - apply filter<br>False - don't apply filter | | `--containers-exclude-non-final-stages` | scan.config.containers.nonFinalStagesFilter<br>` {`<br>` "key": "scan.config.containers.nonFinalStagesFilter",`<br>` "value": "true",`<br>` "allowOverride": true`<br>` }` | `nonFinalStageFilter` |

### Secret Detection Configuration Options

The following table shows the configuration options available for the **Secret Detection** scanner. These configuration options can be applied on the **Account** > **Project** > **Scan** levels. These configurations can be set via the web application (UI), CLI or API, as shown in the table below.

In addition, the Secret Detection scanner supports a **Configure as Code** file, which can be added directly to the repository or included in the ZIP file being scanned. For more information, see Configuring Projects Using Config as Code Files

{% hint style="info" %}
CLI flags are submitted on the scan level with the [scan create](../../../cli-tool/checkmarx-one-cli-commands/scan/scan-create.md) command. API configs can be configured on the account or project level using the [Scan Configuration](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/branches/main/cs61sszap44td-scan-configuration-service) APIs or on the scan level as part of the request body of the [POST /scans](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/i20w1fceb1l15-run-a-scan) API. When using the POST /scans API the `scan.config.microengines` prefix is left out.
{% endhint %}

| Parameter | Values | Notes | CLI | API | Config as Code |
|---|---|---|---|---|---|
| **GIT commit history** | true / false | When set to **`true`** Secret Detection scans both the source code and Git commit history, providing full historical coverage for compliance and deeper analysis.<br>When set to **`false`** (default), Secret Detection scans the source code only.<br>For more information on scanning GIT commit history, see [Git commit history](../../configuring-account-settings/global-account-settings/secret-detection-settings.md#git-commit-history) | `--git-commit-history` | `scan.config.microengines.gitCommitHistory`<br>Example:<br>` {`<br>` "key": "scan.config.microengines.gitCommitHistory",`<br>` "value": "true",`<br>` "allowOverride": true`<br>` }` | `gitCommitHistory` |

## In this section

- [Secret Detection Configuration Options](secret-detection-configuration-options.md)
