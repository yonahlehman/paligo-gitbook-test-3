# Checkmarx One GitHub Action Configuration Variables

When you set up a Checkmarx One GitHub Action in a GitHub workflow you need to configure the following variables.

| **Variable** | **Required** | **Description** | **Possible Values** |
|---|---|---|---|
| base_uri | <img src="../../../../../assets/_tick_.png" alt="" width="16"> | The base URL of your Checkmarx One environment. | <details><br><br><summary>Checkmarx One Server Base URLs</summary><br><br>- US Environment - https://ast.checkmarx.net<br>- US2 Environment - https://us.ast.checkmarx.net<br>- EU Environment - https://eu.ast.checkmarx.net<br>- EU2 Environment - https://eu-2.ast.checkmarx.net<br>- DEU Environment - https://deu.ast.checkmarx.net<br>- Australia & New Zealand – https://anz.ast.checkmarx.net<br>- India - https://ind.ast.checkmarx.net<br>- India 2 - https://ind-2.ast.checkmarx.net/<br>- Singapore - https://sng.ast.checkmarx.net<br>- UAE - https://mea.ast.checkmarx.net<br>- Israel - https://gov-il.ast.checkmarx.net<br><br></details> |
| cx_tenant | <img src="../../../../../assets/_tick_.png" alt="" width="16"> | The name of your Checkmarx One Tenant Account. | e.g., MyOrganization |
| cx_client_id | <img src="../../../../../assets/_tick_.png" alt="" width="16"> | The Checkmarx One client ID.<br>Recommended to create a GitHub Secret. | e.g., `${{ secrets.CX_CLIENT_ID }}` |
| cx_client_secret | <img src="../../../../../assets/_tick_.png" alt="" width="16"> | The Checkmarx One Client Secret.<br>Recommended to create a GitHub Secret. | e.g., `${{ secrets.CX_CLIENT_SECRET }}` |
| project_name | <img src="../../../../../assets/_blue_star_-eff4a4c6.png" alt="" width="16"> | The name that will be assigned to this Project in Checkmarx One. | e.g DemoProject<br>Default: If no project name is specified, then the name of the GitHub repo is assigned to the project in Checkmarx One. |
| branch | <img src="../../../../../assets/_blue_star_-eff4a4c6.png" alt="" width="16"> | The branch name that will be designated for this Project in Checkmarx One. | e.g., main<br>Default: `${{ github.ref#refs/heads/}}` |
| global_params | <img src="../../../../../assets/_blue_star_-eff4a4c6.png" alt="" width="16"> | Submit CLI `global flags` | |
| scan_params | <img src="../../../../../assets/_blue_star_-eff4a4c6.png" alt="" width="16"> | Submit `scan create` flags | |
| utils_params | <img src="../../../../../assets/_blue_star_-eff4a4c6.png" alt="" width="16"> | Submit `utils pr` flags | |
| results_params | <img src="../../../../../assets/_blue_star_-eff4a4c6.png" alt="" width="16"> | Submit`results show` flags | |
| additional_params | <img src="../../../../../assets/_blue_star_-eff4a4c6.png" alt="" width="16"> | You can specify any CLI arguments that you would like to apply to scans of this project. See documentation here.<br>{% hint style="success" %}<br>This variable has been replaced by the dedicated parameter groups `global_params`, `scan_params`, `utils_params` or `results_params`.<br><br>It remains supported for backward compatibility, but must not be used in combination with any of these newer parameters.<br>{% endhint %} | e.g., `--sast-incremental`, `--sast-preset-name "Checkmarx Default"`, `--scan-types sast` |
