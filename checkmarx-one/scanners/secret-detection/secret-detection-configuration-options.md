# Secret Detection Configuration Options

The following table shows the configuration options available for the **Secret Detection** scanner. These configuration options can be applied on the **Account** > **Project** > **Scan** levels. These configurations can be set via the web application (UI), CLI or API, as shown in the table below.

In addition, the Secret Detection scanner supports a **Configure as Code** file, which can be added directly to the repository or included in the ZIP file being scanned. For more information, see Configuring Projects Using Config as Code Files

{% hint style="info" %}
CLI flags are submitted on the scan level with the [scan create](../../cli-tool/checkmarx-one-cli-commands/scan/scan-create.md) command. API configs can be configured on the account or project level using the [Scan Configuration](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/branches/main/cs61sszap44td-scan-configuration-service) APIs or on the scan level as part of the request body of the [POST /scans](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/i20w1fceb1l15-run-a-scan) API. When using the POST /scans API the `scan.config.microengines` prefix is left out.
{% endhint %}

| Parameter | Values | Notes | CLI | API | Config as Code |
|---|---|---|---|---|---|
| **GIT commit history** | true / false | When set to **`true`** Secret Detection scans both the source code and Git commit history, providing full historical coverage for compliance and deeper analysis.<br>When set to **`false`** (default), Secret Detection scans the source code only.<br>For more information on scanning GIT commit history, see Secret Detection Settings | `--git-commit-history` | `scan.config.microengines.gitCommitHistory`<br>Example:<br>` {`<br>` "key": "scan.config.microengines.gitCommitHistory",`<br>` "value": "true",`<br>` "allowOverride": true`<br>` }` | `gitCommitHistory` |
