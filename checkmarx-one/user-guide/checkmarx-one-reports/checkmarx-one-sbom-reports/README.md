# Checkmarx One SBOM Reports

<details>

<summary>What is an SBOM Report?</summary>

Software Bill of Materials (SBOM), in simple words, is a list of all ingredients (i.e., components) of a software product. Just like you would check the ingredients of a food product before eating it, so too you should know what’s in your software before using it.

> *“On May 12, 2021, the President issued* [*Executive Order 14028,*](https://www.federalregister.gov/executive-order/14028) *“Improving the Nation's Cybersecurity.” \[**[1](https://www.federalregister.gov/documents/2021/06/02/2021-11592/software-bill-of-materials-elements-and-considerations#footnote-1-p29568)**\] An initial step towards the Executive Order's goal of “enhancing software supply chain security” is transparency.*
>
> (Quote: [federalregister.gov](http://federalregister.gov))

Generating an SBOM report may sound like a relatively simple task, but in most cases it’s not. Modern software projects make use of a long list of 3rd party software packages, each of which often calls on many other dependencies. This can create a very extensive tree of dependencies being used by your software.

SBOM reports follow a standard format that includes detailed information about each involved component. At a minimum, for each component, it must give the component’s name, supplier name, version, hashes and other unique identifiers, dependency relationship, author of SBOM data and timestamp.

It also needs to cover every software modification and update in order to reflect the current status of the project. This is best accomplished using an automated process that is integrated into your CI/CD pipeline.

</details>

## Overview

Checkmarx One uses the SCA and Container Security scanners to identify images and packages used in your project. Checkmarx also leverages our ability to identify vulnerabilities, suspected malware risks and licenses associated with your packages to supplement the standard SBOM info. This creates an SBOM that provides real insight into the risks associated with your 3rd party components.

SBOM reports can be generated in [CycloneDX v1.7](https://cyclonedx.org/docs/1.7/#SchemaProperties) or [SPDX v2.3](https://spdx.github.io/spdx-spec/v2.3/) formats, with additional “property” fields showing supplemental risk data. In CycloneDX format, you can also choose to include **VEX** documentation as part of the report. The reports can be exported in XML or JSON format. There are two types of SBOM reports that can be generated in Checkmarx One:

- **Project SBOM** - based on results from a specific project scan. Supported for SCA scanner.
- **Application SBOM** - based on the last successful scan of each project associated with application. Supported for SCA and Container Security scanners.

Project SBOMs can be generated from the web portal (UI) as well as via CLI or [SCA Scanner - Export Service REST API](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/branches/main/ngw39shhzpuwt-create-a-report).

Application SBOMs can be generated from the web portal (UI) or by the [Improved Reports Service REST API](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/branches/main/51flzmrawidq4-create-a-customized-report).

## In this section

- [Generating SBOM Report for a Project](generating-sbom-report-for-a-project.md)
- [Generating SBOM Report for an Application](generating-sbom-report-for-an-application.md)
- [Viewing CycloneDx SBOM Reports](viewing-cyclonedx-sbom-reports.md)
