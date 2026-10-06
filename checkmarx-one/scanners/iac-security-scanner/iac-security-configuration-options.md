# IaC Security Configuration Options

The following table shows the configuration options available for the IaC Security scanner. These configuration options can be applied on the **Account** > **Project** > **Scan** levels. The configurations can be set via the web application (UI), CLI or API, as shown in the table below.

In addition, the IaC Security scanner supports a **Configure as Code** file, which can be added directly to the repository or included in the ZIP file being scanned. For more information, see Configuring Projects Using Config as Code Files

{% hint style="info" %}
CLI flags are submitted on the scan level with the [scan create](../../cli-tool/checkmarx-one-cli-commands/scan/scan-create.md) command. API configs can be configured on the account or project level using the [Configuration](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/branches/main/cs61sszap44td-scan-configuration-service) API or on the scan level as part of the request body of the [POST /scans](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/branches/main/cs61sszap44td-scan-configuration-service) API. When using the POST /scans API the `scan.config.kics` prefix is left out.
{% endhint %}

| **Parameter** | **Values** | **Notes** | **CLI** | **API** | Config as Code |
|---|---|---|---|---|---|
| **Folder/file filter** | Allow users to select specific folders or files to include or exclude from the code-scanning process. | • Including a file type - \*.java<br>• Excluding a file type - !\*.java<br>• Use “,” sign to chain file types.<br>for example: \**.*java*,*\*.js<br>• The parameter also supports including/excluding folders.<br>• regex is not supported.<br>{% hint style="info" %}<br>For details on the filter application logic, see [here](#filter-application-logic).<br>{% endhint %} | `--iac-security-filter <string>` | scan.config.kics.filter<br>Example:<br>```<br>  {<br> "key": "scan.config.kics.filter",<br> "value": "*.java",<br> "allowOverride": true<br> }<br>``` | `filter` |
| **platforms** | • Ansible<br>• AzureResourceManager<br>• Buildah<br>• CICD<br>• CloudFormation<br>• Crossplane<br>• DockerCompose<br>• Dockerfile<br>• GoogleDeploymentManager<br>• GRPC<br>• Knative<br>• Kubernetes<br>• OpenAPI<br>• Pulumi<br>• ServerlessFW<br>• Terraform | {% hint style="info" %}<br>Configure one or more platforms, separated by a comma.<br><br>The parameter means that you only want to run scans (queries) for those platforms.<br><br>For example: Ansible, CloudFormation, Dockerfile<br>{% endhint %}<br>{% hint style="warning" %}<br>Any mistake in the platform characters will cause an error.<br>{% endhint %} | `--iac-security-platforms <string>, <string>` | scan.config.kics.platforms<br>Example:<br>```<br> {<br> "key": "scan.config.kics.platforms",<br> "value": "GRPC",<br> "allowOverride": true<br> }<br>``` | `filter` |
| **Preset Name** | All the available IaC Security Presets that exist in the system | There are no Checkmarx Default Presets now. For more information on IaC presets, see here.<br>{% hint style="warning" %}<br>The preset ID for IaC Security must be a valid UUID. Once you create one, you can copy the **PresetID** from the IaC Presets page.<br>{% endhint %} | | scan.config.kics.presetId<br>```<br> {<br> "key": "scan.config.kics.presetId",<br> "value": "047be3a8-c9d6-4c02-90d5-c243418c7d8a",<br> "allowOverride": true<br> }<br>``` | `presetId` |

## Filter Application Logic

- Filters are applied in the order they appear in the expression.
- When both *include* and *exclude* filters are used, *include* filters must come first.

### Why this order matters

If the *include* filters come first (**correct order**) the system starts with an empty selection set, then adds content from the original sources based on the include filters. The *exclude* filters are then applied to that populated set, successfully removing any unwanted items. The resulting, correctly filtered selection set is what gets sent for scanning.

If the *exclude* filters are applied first (**incorrect order**), the system begins with an empty selection set and attempts to remove content - which has no effect. Only afterward does it apply the *include* filters, adding content from the source set to the selection set. This results in the *exclude* rules being effectively ignored.
