# API Security Scanner Parameters

When configured globally, these parameters will apply to API Security scans across all projects. When configured at the project level, they will apply only to API Security scans for that project.

The table below presents the optional parameters, and their optional values.

{% hint style="info" %}
API configs can be configured on the account or project level using the [Configuration](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/branches/main/cs61sszap44td-scan-configuration-service) API or on the scan level as part of the request body of the [POST /scans](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/branches/main/cs61sszap44td-scan-configuration-service) API. When using the POST /scans API the `scan.config.apisec` prefix is left out.
{% endhint %}

| Parameter | Values | Notes | CLI | API | Config as Code |
|---|---|---|---|---|---|
| Swagger folder/file filter | Swagger folder path or any folder/file type.<br>Allow users to select specific folders or files that they want to include or exclude from the code scanning process. | • Including a file type - \*.java<br>• Excluding a file type - !\*.java<br>• Use “,” sign to chain file types.<br>For example: \*.java,\*.js<br>• The parameter also supports including/excluding folders.<br>• regex is not supported. | | `scan.config.apisec.swaggerFilter` | `swaggerFilter` |
