# Secret Detection Settings

The **Secret Detection Defaults** page contains global default settings that determine how Secret Detection scans are executed unless overridden at the project level.

## Git commit history

Scanning Git commit history helps you uncover secrets that were introduced in the past and may still pose a security or compliance risk today. It provides deeper visibility and stronger assurance that no exposed secrets are overlooked.

When set to **true** Secret Detection scans both the source code and Git commit history, providing full historical coverage for compliance and deeper analysis.

When set to **false** (default), Secret Detection scans the source code only.

Select **Allow Override** to let individual projects enable or disable commit history scanning as needed.

### Limitations

- The repository’s .git folder size must not exceed **1.5 GB**.
- Only the most recent **50,000 commits** are scanned.
- Commit history scanning requires a **primary branch** to be defined for the project. The scan itself may run on a different branch, but the primary branch must be configured so that commit history can be analyzed for the scan.

{% hint style="info" %}
You can also implement this configuration in the following ways:

- via **CLI** using the [scan create](../../../cli-tool/checkmarx-one-cli-commands/scan/scan-create.md) command with `--git-commit-history` flag
- via **API** on the account or project level, using the [Scan Configuration](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/branches/main/cs61sszap44td-scan-configuration-service) API with the `scan.config.microengines.gitCommitHistory` configuration parameter, or on an individual scan using the [POST /scans](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/branches/main/cs61sszap44td-scan-configuration-service) API with the `microengines` config param.

  **Account/Project** level example:

  ```
    {
      "key": "scan.config.microengines.gitCommitHistory",
      "value": "true",
      "allowOverride": true
    }
  ```
{% endhint %}
