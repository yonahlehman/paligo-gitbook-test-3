# New Data Retention Policy

We will be changing our customer data retention policy in order to enhance data security, improve compliance and performance, and reduce risk across our platform.

The following data retention rules will be implemented:

- Results data (e.g., scan results, findings metadata, and analysis logs) will be retained for 3 months. For customers with Premium Support, the retention period will be extended to 12 months.
- Source code (e.g., uploaded or ingested code/packages used during scan analysis) will be retained for a period of 30 days.

This article explains how you can export your scan results using the Checkmarx One web application (UI) or the available APIs.

{% hint style="info" %}
This article relates to exporting data from Checkmarx One. A similar retention policy is also being impemented for SCA standalone, see SCA documentation.
{% endhint %}

## Exporting Data from Checkmarx One via Web Application

If you need to retain data (e.g., evidence packs, historical reports) beyond the scheduled time period, you should download reports that contain the relevant data.

For detailed information about various types of scan reports and how they can be exported, see [Scan Reports](../user-guide/checkmarx-one-reports/scan-reports.md).

The following procedure explains how you can easily download a "default" scan report.

1. In Checkmarx One, navigate to the left side panel and select **Projects**.
2. Select the project you want to export the scan results from and go to the overview page by selecting <img src="../../assets/pie_icon.png" alt="" data-size="line">.
3. Navigate to the **Scan History** tab.
4. At the end of the scan's row, click <img src="../../assets/Vertical_Ellipsis.png" alt="" data-size="line"> then **Generate Default Report** .
5. Once the report is ready, a notification will appear that it is available for downloading. Click **Download report** to download it.

## Exporting Data via API

You can use our APIs to export scan reports or to export lists of results (risks) identified by each scanner.

### Exporting Scan Reports via API

The following workflow explains how you can use our (REST) APIs to export scan reports.

1. Use the Scans API, GET **{Base_URL}**/[api/scans](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/branches/main/1wnhzwk5inwup-retrieve-list-of-scans)/ endpoint to obtain the list of scans and project IDs to generate the reports.

   {% hint style="info" %}
   This endpoint allows Checkmarx to pass different parameters as filters (e.g., branch, from-date, to-date, etc.). The full list of parameters can be found [here](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/branches/main/1wnhzwk5inwup-retrieve-list-of-scans). By default, the maximum number of results to return is 20; it’s possible to change this by altering the **limit** parameter.
   {% endhint %}
2. Once the scan and project IDs are returned, they can be used with the Reports API, Create a report POST **{Base_URL}**/[api/reports/v2](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/51flzmrawidq4-create-a-customized-report) endpoint to generate a report.
3. After the request for a new report is completed, the report may take a couple of seconds to become ready for download. The report status can be checked by using the Retrieve report status GET **{Base_URL}**[/api/reports/{reportId}](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/a1d7dc3fee9cc-retrieve-report-status) endpoint. The status of a report can be: **Requested**, **Started**, **Completed**, or **Failed**.
4. To download the report use the Download a report GET **{Base_URL}**[/api/reports/{reportId}/download](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/623847b6ec200-download-a-report) endpoint.

### Exporting Scanner Results via API

1. Use the Scans API, GET **{Base_URL}**/[api/scans](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/branches/main/1wnhzwk5inwup-retrieve-list-of-scans)/ endpoint to obtain the list of scans and project IDs to generate the reports.
2. After obtaining the scan IDs, the Scanners Results API, GET **{Base_URL}**[/api/results/](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/whqbw17zn6rg1-retrieve-scan-results-all-scanners) can be used to obtain the results for each scanner. By default, the maximum number of results to return is 20, it’s possible to change this by altering the **limit** parameter.

### Exporting Scanner Results for a Specific Scanner, via API

To retrieve more details on results from a specific scanner, use the following procedure:

1. Use the Scans API, GET **{Base_URL}**/[api/scans](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/branches/main/1wnhzwk5inwup-retrieve-list-of-scans)/ endpoint to obtain the list of scans and project IDs to generate the reports.
2. Depending on which specific scanner's results you are exporting, use one of the following:

   - **To export SAST results:**

     Use the SAST Results API GET, {Base_URL}[/api/sast-results](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/68dabfc984bc3-retrieve-sast-scan-results)/ endpoint with the previously obtained scan-id (required parameter) to obtain the scan results. By default, the maximum number of results to return is 20, it’s possible to change this by altering the **limit** parameter. The different parameters allowed with this endpoint can be found [here](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/68dabfc984bc3-retrieve-sast-scan-results).
   - **To export Container Security results:**

     Use the Container Security GraphQL API. The full guide on how to export these results using the Container Security GraphQL API can be found [here](https://docs.checkmarx.com/en/34965-397992-container-security-graphql-api-documentation.html#UUID-08a1718b-80cc-0e14-255d-0d547f046f51).
   - **To export IaC Security results:**

     Use the IaC Security Results API, GET {Base_URL}/[api/kics-results](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/dee80033baf07-retrieve-ia-c-security-scan-results)/ endpoint with the previously obtained scan-id (required parameter) to obtain the scan results. By default, the maximum number of results to return is 20, it’s possible to change this by altering the **limit** parameter. The different parameters allowed with this endpoint can be found [here](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/dee80033baf07-retrieve-ia-c-security-scan-results#query-parameters).

## Data Retention FAQ

| | |
|---|---|
| **Policy overview** | |
| Q: What are the retention periods? | A: Source code stored for a scan is retained for 30 days. Results data is retained for 3 months for Regular customers and 12 months for Premium Support customers. |
| Q: Does this policy delete projects? | A: No. Projects remain. What is removed is scan source packages (after 30 days) and scan history/results that exceed the results retention window. |
| **Source code visibility and remediation** | |
| Q: After 30 days, can we still view full source code in the CxOne UI for an older scan? | A: No. Full source browsing/view in the UI for that scan is not available after 30 days. |
| Q: If customers take longer than 30 days to consume results, is remediation/triage work lost? | A: No. The code won’t be visible in the UI for scans older than 30 days, but triage work is not lost. If customers need code context in the UI, enable Keep Code Snippets. |
| Q: Will code snippets live past the retention period if Keep Code Snippets is enabled? | A: Yes. When enabled, code snippets remain available to provide limited code context without retaining full source. |
| **Scan history, results, reporting, and analytics** | |
| Q: If a project is actively scanned at least once a month, is scan history still limited to 90 days (Regular)? | A: Yes. All results older than 90 days are removed for Regular retention, even if the project is actively scanned. |
| Q: Standard customer example: project last scanned ~100 days ago. What will they see when retention runs? | A: Projects remain visible. Only scans within the results window (3 months Regular / 12 months Premium) appear in scan history per branch. Scans older than 30 days won’t have source view in the UI, but results remain within the results window. Analytics data remains. |
| Q: After retention, will there be any evidence of scans beyond the retention windows (scan dates/IDs)? | A: No. There will be no evidence of scans beyond the results retention window (3 months Regular / 12 months Premium). |
| Q: If we can’t scan again within 3 months, does that mean everything is deleted? | A: Scan results older than the retention window are deleted and no longer available in the platform. If longer-term evidence is required, export the needed data on a cadence that stays within the retention window. |
| **Triage, statuses, Similarity ID behavior** | |
| Q: If a finding is marked Not Exploitable (or another status), does the status persist beyond 3 months? Will it be lost if we don’t scan again before retention expires? | A: Yes. Finding status persists based on Similarity ID. The question of whether alerts ‘trigger again’ depends on the specific alerting/policy mechanism in use. |
| Q: If a scan is deleted and the same vulnerability shows up in a future scan, will it be marked new or recurrent? | A: It should be treated as recurrent because status and history are associated with Similarity ID rather than an individual scan record. |
| Q: SimilarityID propagation scenario: if an older project ages out, will triage/status propagated to other active work be deleted or revert to To Verify? | A: No. Triage does not revert to To Verify due to retention. In CxOne, triage propagates across branches (Similarity ID), not across separate projects. |
| **Rules, filters, and UI behavior** | |
| Q: If a customer does not scan for the last 6 months, can they still use rule filtering? | A: No. If there is no scan for the last 6 months, the rule filtering capability is not available. |
| **Tenant-level flexibility and exceptions** | |
| Q: Can customers customize or shorten/extend retention periods per project/app/tenant? | A: No. Retention is standardized by tier (Regular vs Premium Support). |
| Q: EDPP exception: Do we always keep the latest scan per branch (including source + results) regardless of scan date? | A: This is under validation with R&D. Current expectation is that this is not accurate, but confirmation is pending. |
| **Definitions** | |
| Q: What is “triage work”? | A: Triage work includes actions such as changing a finding’s state/status (e.g., To Verify → Confirmed/Not Exploitable), adjusting severity, and adding notes/comments related to remediation decisions. |

{% hint style="info" %}
This FAQ will be updated as additional items are confirmed in writing by Product/R&D.
{% endhint %}
