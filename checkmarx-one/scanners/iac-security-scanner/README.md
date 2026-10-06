# IaC Security Scanner

## Overview

{% hint style="info" %}
Infrastructure as Code (IaC) is the creation, provisioning and configuration of software-defined compute (SDC), network and storage infrastructure through machine-readable definition files, rather than physical hardware configuration or interactive configuration tools. IaC automates the manual tasks usually associated with computing infrastructure configuration and implementation.
{% endhint %}

Checkmarx's IaC Security scanner (based on [KICS](https://docs.kics.io/latest/about/) opens source project powered by Checkmarx) examines configuration definitions and scripts used to instantiate infrastructure to ensure the resulting resources are secure. This scanner consumes configuration files and scripts in relevant formats and then applies tests to ensure conformance with common configuration hardening standards (i.e., Center for Internet Security Benchmarks and many others), identifies security issues associated with specific operational environments, identifies embedded secrets, and performs other tests supporting organization-specific standards and compliance requirements.

### Query Editor

Checkmarx Audit complements Checkmarx IaC Security by enabling you to quickly and intuitively customize Iac Security's analysis queries or configure additional queries for purposes of:

- Security
- Application logic

Audit can be used to adapt IaC Security's basic security functionality to non-standard code. This helps eliminate false positives and ensure that all real vulnerabilities are identified. Audit can also expand IaC Security's functionality to include queries supporting specific QA or application logic needs.

For more information about Query Editor, see [IaC Security Query Editor](../../user-guide/resource-management/iac-security-query-editor.md).

### IaC Security Presets

Improve the accuracy of IaC Security scan results by creating IaC Security Presets - sets of queries that allow you to triage findings based on the core capabilities of the IaC Security scanner.

With preset management, you can easily create and manage custom or predefined presets, tailoring security scans to their specific needs.

For more information about IaC Security Presets, see here.

## In this section

- [IaC Security Scanner - Supported Platforms/Technologies](iac-security-scanner---supported-platformstechnologies.md)
- [IaC Security Results Viewer](iac-security-results-viewer.md)
- [Triaging IaC Security Results](triaging-iac-security-results.md)
- [IaC Security - Similarity ID](iac-security---similarity-id.md)
- [IaC Security Configuration Options](iac-security-configuration-options.md)
