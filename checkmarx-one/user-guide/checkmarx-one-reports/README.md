# Checkmarx One Reports

You can generate various types of reports containing data from your Checkmarx One account to share with relevant stakeholders.

{% hint style="warning" %}
To access and generate Scan Reports and Project Reports, users must have the `manage-reports` permission assigned.
{% endhint %}

{% hint style="info" %}
All timestamps returned in Checkmarx One reports are standardized to UTC-0, regardless of the user’s geographic location.
{% endhint %}

The following types of reports are available:

- **Scan Reports** - Scan reports provide comprehensive information on scans that have been run in Checkmarx One.

  {% hint style="info" %}
  This report shows info from all scanners run in the scan, including SCA. However, you can obtain more comprehensive SCA info by generating SCA (Package) Reports.
  {% endhint %}
- **Project Reports** - Project reports provide information on a specific project using the selections made by the user when generating the report.
- **Global CSV Result Reports** - These reports consolidate all security findings across the tenant into a single digestible CSV format.
- **SCA (Package) Reports** - SCA reports provide detailed information about the open source packages in your project and the risks associated with those packages. There are two types of SCA reports:

  - **SCA Scan Reports** - shows an overview of the open source packages in your project as well as specific vulnerabilities, legal risks, and outdated versions identified by the scan.
  - **Software Bill of Materials (SBOM)** - shows detailed info about each of the open source packages used by your program and the associated risks. You can choose between [CycloneDX v1.7](https://cyclonedx.org/docs/1.7/#SchemaProperties) format or SPDX [SPDX v2.3](https://spdx.github.io/spdx-spec/v2.3/) format.

## In this section

- [Scan Reports](scan-reports.md)
- [Project Reports](project-reports/README.md)
- [Application Reports](application-reports.md)
- [Global CSV Result Reports](global-csv-result-reports.md)
- [Checkmarx One SBOM Reports](checkmarx-one-sbom-reports/README.md)
- [SCA (Package) Reports](sca-package-reports/README.md)
