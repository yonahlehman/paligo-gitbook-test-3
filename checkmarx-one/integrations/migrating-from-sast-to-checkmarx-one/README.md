# Migrating from SAST to Checkmarx One

Checkmarx One provides a mechanism to migrate a SAST on-prem environment to a Checkmarx One instance.

The migration flow is as follows:

1. Download the cxsast_exporter tool - See [SAST to CxOne Export CLI Tool](sast-to-cxone-export-cli-tool/README.md)
2. Export the SAST on-prem environment using the cxsast_exporter tool - See [Using the SAST to CxOne Export CLI Tool](sast-to-cxone-export-cli-tool/using-the-sast-to-cxone-export-cli-tool/README.md)
3. Import the SAST on-prem environment to Checkmarx One - See [Importing SAST to Checkmarx One](importing-sast-to-checkmarx-one.md)

{% hint style="info" %}
- SAST on-prem environments have different user roles than Checkmarx One roles - See [SAST vs. Checkmarx One Role Mapping](sast-vs-checkmarx-one-role-mapping.md)
- There are several limitations for the SAST export - See [SAST Migration Limitations](sast-migration-limitations.md)
{% endhint %}

## In this section

- [SAST to CxOne Export CLI Tool](sast-to-cxone-export-cli-tool/README.md)
- [Importing SAST to Checkmarx One](importing-sast-to-checkmarx-one.md)
- [CLI Tool Releases](cli-tool-releases/README.md)
- [SAST Migration Limitations](sast-migration-limitations.md)
- [SAST vs. Checkmarx One Role Mapping](sast-vs-checkmarx-one-role-mapping.md)
