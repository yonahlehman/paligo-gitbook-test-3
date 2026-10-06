# SCA Configuration Options

The following table shows the configuration options available for the SCA scanner. These configuration options can be applied on the **Account** > **Project** > **Scan** levels. The configurations can be set via the web application (UI), CLI or API, as shown in the table below.

In addition, the SCA scanner supports a **Configure as Code** file, which can be added directly to the repository or included in the ZIP file being scanned. For more information, see Configuring Projects Using Config as Code Files

{% hint style="info" %}
CLI flags are submitted on the scan level with the [scan create](../../cli-tool/checkmarx-one-cli-commands/scan/scan-create.md) command. API configs can be configured on the account or project level using the [Configuration](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/branches/main/cs61sszap44td-scan-configuration-service) API or on the scan level as part of the request body of the [POST /scans](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/i20w1fceb1l15-run-a-scan) API. When using the POST /scans API the `scan.config.sca` prefix is left out.
{% endhint %}

| **Parameter** | **Values** | **Notes** | CLI | API | Config as Code |
|---|---|---|---|---|---|
| **Folder/file filter** | Allow users to select specific folders or files that they want to include or exclude from the code scanning process. | • Including a file type - \*.java<br>• Excluding a file type - !\*.java<br>• Use “,” sign to chain file types.<br>for example: \**.*java*,*\*.js<br>• The parameter also supports including/excluding folders.<br>• regex is not supported.<br>{% hint style="info" %}<br>For details on the filter application logic, see [here](#filter-application-logic).<br>{% endhint %} | `--sca-filter <string>` | `scan.config.sca.filter`<br>Example:<br>```<br> {<br> "key": "scan.config.sca.filter",<br> "value": "*.java,*.js",<br> "allowOverride": true<br> }<br>``` | `filter` |
| **Exploitable Path** | Toggle On/Off | When Exploitable Path is activated, scans that use the SCA scanner will identify whether or not there is an exploitable path from your source code to the vulnerable 3rd party package.<br>Learn more about Exploitable Path. | `--sca-exploitable-path <string>` | `scan.config.sca.ExploitablePath`<br>Example:<br>```<br> {<br> "key": "scan.config.sca.ExploitablePath",<br> "value": "true",<br> "allowOverride": true<br> }<br>``` | `ExploitablePath` |
| **Vulnerability Comparison Mode** <sup>1\]</sup> | Project-Wide (default) or Branch-Based | Determines what is used as the base-line for determining whether or not a vulnerability is a New finding in the current scan.<br>• Project-wide - compares to the most recent scan of any branch of the project.<br>• Branch-based - compares to the most recent scan of the specific branch that was scanned. | | `scan.config.sca.vulnerabilityComparisonMode`<br>Example:<br>```<br> {<br> "key": "scan.config.sca.vulnerabilityComparisonMode",<br> "value": "Branch-Based",<br> "allowOverride": true<br> }<br>``` | `vulnerabilityComparisonMode` |
| **Java Language Version** <sup>1\]</sup> | 8,11,17, 21 (default) or 25 | Specify the Java version used for dependency resolution for gradle package manager. This version does not affect Java version used for maven resolution. If not defined, gradle scans will run with Java version 21 by default. | | `scan.config.sca.javaLanguageVersion`<br>Example:<br>```<br> {<br> "key": "scan.config.sca.javaLanguageVersion",<br> "value": "17",<br> "allowOverride": true<br> }<br>``` | `javaLanguageVersion` |
| **UV Resolution**<sup>1\]</sup> | true/false | Uses the UV package manager instead of pip for Python dependency resolution. | | `scan.config.sca.useUvResolution`<br>```<br> {<br> "key": "scan.config.sca.useUvResolution",<br> "value": "true",<br> "allowOverride": true<br> }<br>``` | `useUvResolution` |
| **Python Language Version** <sup>1\]</sup> | 2.7,3.11,3.12, 3.13 (default) or 3.14 | Specify the Python version used for dependency resolution for pip and poetry package managers. Poetry does not support Python prior to version 3, if version 2.7 is supplied, the default version is used instead. If not defined, scans will run with Python version 3.13 by default. | | `scan.config.sca.pythonLanguageVersion`<br>Example:<br>```<br> {<br> "key": "scan.config.sca.pythonLanguageVersion",<br> "value": "3.12",<br> "allowOverride": true<br> }<br>``` | `pythonLanguageVersion` |
| **Scan SBOM**<sup>2\]</sup> | | Run an SCA scan on a specific SBOM file. Learn more about scanning SBOM files [here](README.md#scanning-sboms). | `--sbom-only` | `sbom`<br>For exact syntax, see [Scanning from an SBOM](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/branches/main/07jx5a2de1zlu-scans-service-rest-api#scanning-from-an-sbom-for-sca) in our API documentation portal. | `sbom` |

1\] These configurations are only available on the tenant or project level. They can't be set on the scan level.

2\] This configuration is only available on the scan level.

## Filter Application Logic

- Filters are applied in the order they appear in the expression.
- When both *include* and *exclude* filters are used, *include* filters must come first.

### Why this order matters

If the *include* filters come first (**correct order**) the system starts with an empty selection set, then adds content from the original sources based on the include filters. The *exclude* filters are then applied to that populated set, successfully removing any unwanted items. The resulting, correctly filtered selection set is what gets sent for scanning.

If the *exclude* filters are applied first (**incorrect order**), the system begins with an empty selection set and attempts to remove content - which has no effect. Only afterward does it apply the *include* filters, adding content from the source set to the selection set. This results in the *exclude* rules being effectively ignored.
