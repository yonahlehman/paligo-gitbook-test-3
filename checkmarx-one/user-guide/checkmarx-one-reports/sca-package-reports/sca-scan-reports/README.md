# SCA Scan Reports

You can export comprehensive Scan Reports for scans run using the Checkmarx One SCA scanner. The report shows an overview of the security of your project as well as specific vulnerabilities, legal risks, and outdated versions identified by the scan. Reports can be generated in pdf, xml, json, or csv format and downloaded locally.

{% hint style="info" %}
The info shown in the Scan Report is similar to the info shown in the web portal on the SCA [Results Viewer](../../../viewing-scan-results-in-the-results-viewers/sca-results-viewer.md) page.

We do not currently support the option to filter results included in a **Scan Report**. However, it is possible to filter the data exported as a CSV file from the **Global Inventory & Risks** page. So, on the **Global Inventory & Risks** page, you can filter for a specific Project and then apply additional filters as needed in order to generate a customized report for a particular Project.
{% endhint %}

Reports show data for the following subjects:

- **Packages** - shows info about the open source packages used by your project that contain risks, including: security vulnerabilities, license violations, and outdated versions. The info is separated into a direct packages table and a transitive packages table.
- **Vulnerabilities** - shows info about all of the security vulnerabilities that were identified in the open source packages used by your project, including: severity level, CVE references, remediation recommendations etc.
- **Licenses** - shows the licenses that you have for the packages in your project and the legal risks associated with those packages.
- **Policy Violations** - shows any security Policies which the Project violates.

When you generate a report, you can specify whether you want to include all sections or only specific sections.

## Generating an SCA Scan Report

1. Navigate to the **SCA Results Viewer**, and hover over the **Export** <img src="../../../../../assets/Image_021.png" alt="" data-size="line"> icon (top right of page).
2. Select the **Scan Report** option.
3. Click on the **Select Report Sections** field and choose which data tables to include in the report. Options are: **All data tables, Packages, Risks (Vulnerabilities and Suspected Malware), Licenses, Legal Risks** and **Risks by Package.** By default, **All data tables** is selected.
4. Select a file format. Options are **PDF, XML, JSON,** and **CSV**.
5. Select the **Hide Private Packages** checkbox if you want to exclude private packages from the report.
6. Select the **Exclude Dev and Test packages** checkbox to exclude Dev and Test packages from the report.

   {% hint style="success" %}
   To learn more about Dev and Test dependencies, see [here](https://docs.checkmarx.com/en/34965-322318-sca-scanner.html#UUID-2865b187-60e6-84f0-67c8-c5313ef205fc_UUID-ce0b5676-9ab8-dee1-1004-5c32410eaa0a).
   {% endhint %}
7. Select the **Include only effective licenses** checkbox if you want to exclude licenses that haven't been designated as effective from the report. By default, the checkbox is selected.
8. Click **Export**.

   The SCA Scan Report is generated and ready for download

## In this section

- [Viewing SCA Scan Reports](viewing-sca-scan-reports.md)
