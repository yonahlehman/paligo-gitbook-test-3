# API Security Configuration Options

The following table shows the configuration options available for the **API Security** scanner. These configuration options can be applied on the **Account** > **Project** > **Scan** levels. These configurations can be set via the web application (UI), CLI or API, as shown in the table below.

In addition, the API Security scanner supports a **Configure as Code** file, which can be added directly to the repository or included in the ZIP file being scanned. For more information, see Configuring Projects Using Config as Code Files

{% hint style="info" %}
API configs can be configured on the account or project level using the [Configuration](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/branches/main/cs61sszap44td-scan-configuration-service) API or on the scan level as part of the request body of the [POST /scans](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/branches/main/cs61sszap44td-scan-configuration-service) API. When using the POST /scans API the `scan.config.apisec` prefix is left out.
{% endhint %}

| Parameter | Values | Notes | CLI | API | Config as Code |
|---|---|---|---|---|---|
| Swagger folder/file filter | Swagger folder path or any folder/file type.<br>Allows users to select specific folders or files that they want to include or exclude from the code scanning process. | • Including a file type - \*.java<br>• Excluding a file type - !\*.java<br>• Use “,” sign to chain file types.<br>For example: \*.java,\*.js<br>• The parameter also supports including/excluding folders.<br>• regex is not supported.<br>{% hint style="info" %}<br>For details on the filter application logic, see [here](#filter-application-logic).<br>{% endhint %} | | `scan.config.apisec.swaggerFilter`<br>**Tenant/Project** example:<br>```<br> {<br> "key": "scan.config.apisec.swaggerFilter",<br> "value": "*.java,*.js",<br> "allowOverride": true<br> }<br>```<br>**Scan** example:<br>```<br>"config" [<br> {<br> "type": "apisec",<br> "value": {<br> "swaggerFilter": "*.java,*.js"<br> }<br> }<br>]<br>``` | `swaggerFilter` |
| uuid<sup>1\]</sup> | The upload link to your Swagger file. | See [Workflow for API Scanner](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/branches/main/07jx5a2de1zlu-scans-service-rest-api#workflow-for-api-security-scanner) for the complete process of uploading a Swagger file and generating this upload link | | `uuid`<br>Example:<br>```<br>"config" [<br> {<br> "type": "apisec",<br> "value": {<br> "uuid": "<link_to_your_swagger>"<br> }<br> }<br>]<br>``` | |

1\] This configuration is only available **via API** and only on the scan level.

## Filter Application Logic

- Filters are applied in the order they appear in the expression.
- When both *include* and *exclude* filters are used, *include* filters must come first.

### Why this order matters

If the *include* filters come first (**correct order**) the system starts with an empty selection set, then adds content from the original sources based on the include filters. The *exclude* filters are then applied to that populated set, successfully removing any unwanted items. The resulting, correctly filtered selection set is what gets sent for scanning.

If the *exclude* filters are applied first (**incorrect order**), the system begins with an empty selection set and attempts to remove content - which has no effect. Only afterward does it apply the *include* filters, adding content from the source set to the selection set. This results in the *exclude* rules being effectively ignored.
