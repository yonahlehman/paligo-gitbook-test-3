# Viewing SCA Scan Reports

A Scan Report shows information about a specific scan that ran on one of your Checkmarx SCA Projects.

Reports are generated in the specified file type. A csv report is downloaded as a zip file, from which separate csv’s are extracted for each section.

Reports in xml, json and csv contain the raw data from the scan, divided into the following sections: *Summary*, *Packages*, *Vulnerabilities* and *Licenses*.

Pdf reports contain the following sections.

- **Title bar** - shows general info about the Report as well as a link to view the full results in the web application.
- **Overview section** - shows an overview pane with a graphic display of the overall results for each element that is included in the report (*Packages*, *Vulnerabilities*, *Licenses*, *Policies*).

{% hint style="info" %}
Only elements included in the report are represented in the overview pane, i.e if the report doesn’t include the Packages section then there won’t be a Packages overview pane.
{% endhint %}

- **Packages Data Table (Direct)** - shows a list of all packages called directly by your project. For each package, detailed info is shown about versions, licenses, vulnerabilities etc.
- **Packages Data Table (Transitive)** - shows a list of all packages called indirectly (via other packages). For each package, detailed info is shown about versions, licenses, vulnerabilities etc.
- **Vulnerabilities Data Table** - shows a list of all of the security vulnerabilities that were identified in the open source packages used by your Project. For each vulnerability, detailed info is shown about the severity, CVE ID, package where it is found etc.
- **Licenses Data Table** - shows a list of all of your licenses for the packages used by your project. For each license, detailed info is shown about the legal risks.

## Overview Section

The Title bar shows the following info about the report: *Project name*, *Date scanned*, *Date created*, *Printed Date*, and *Scan Origin*.

The Overview panes show a high level overview of the scan results for each of the sections that are included in the report (*Packages*, *Vulnerabilities*, and *Licenses)*.

There is also a Policies pane that shows any security Policies that are violated by this Project.

### Packages

<figure><img src="../../../../../assets/6426460348.png" alt="" width="648"><figcaption></figcaption></figure>

The *Packages Overview* shows the number of vulnerable packages over the total number of packages identified in the Project. It also shows a color coded graph indicating the number of vulnerable packages of each severity level. In addition, it shows the top five vulnerable packages along with the number of vulnerabilities in each of those packages.

### Vulnerabilities

<figure><img src="../../../../../assets/6426918991.png" alt="" width="648"><figcaption></figcaption></figure>

The *Vulnerabilities Overview* shows the number of high severity vulnerabilities over the total number of vulnerabilities in the Project. It also shows a color coded graph indicating the number of vulnerabilities of each severity level. In addition, it shows a breakdown of vulnerabilities based on other characteristics.

### Licenses

<figure><img src="../../../../../assets/Image_474.png" alt="" width="648"><figcaption></figcaption></figure>

The *Licenses Overview* shows the number of high severity legal risks over the total number of legal risks in the Project. It also shows a color coded graph indicating the severity of the legal risks with the licenses. In additions, it shows the seven licenses with the greatest legal risk.

### Policies

<figure><img src="../../../../../assets/Image_475.png" alt="" width="648"><figcaption></figcaption></figure>

The *Policies* section shows the number of violated Policies over the total number of Policies that apply to the Project. It also shows a breakdown of the number of Global and Specific policies as well as the number of packages that violate Policies and the number of Policies that cause builds to break.

## Packages Data Table

This table shows detailed info about each open source package used by your Project. Separate tables are shown for *Direct* and *Transitive* packages.

The header for each table shows how the table was filtered, the total number of filtered packages, and how the table is sorted.

<figure><img src="../../../../../assets/Image_607.png" alt="" width="648"><figcaption></figcaption></figure>

The following table describes the info shown for each package identified by this scan.

| **Item** | **Description** | **Possible Values** |
|---|---|---|
| **Package** | The name of the package. | e.g., dom4j:dom4j |
| **Version** | The version of the package that you are using. | e.g., 1.6.1 |
| **Outdated** | Indicates whether or not a more recent version of the package is available. | <img src="../../../../../assets/outdated.png" alt="" data-size="line">The package is outdated.<br><img src="../../../../../assets/Image_608-931603b8.png" alt="" data-size="line">The package is up to date. |
| **License** | Shows all licenses that you have that are associated with this package. | e.g., GPL 2.0, Apache2.1 |
| **Vulnerabilities** | A color coded bar graph indicating the number of vulnerabilities of each severity level. | e.g.,<br><img src="../../../../../assets/6426394805.png" alt="" width="547"> |
| **Usage** | Indicates whether or not the package is being called by the source code. | • **Used** - This package is used by your project’s source code.<br>• **Potentially Used** - This package is a dependency of a direct package that is used by your project’s source code.<br>• **Unused** - No usage of this package was found.<br>• **Unknown** - Checkmarx SCA could not determine whether the package is used. |
| **Dep. Type**<br>(Dependency Type) | Shows labels that Checkmarx applied to the package. There is a label indicating the package manager used for package resolution. In addition, the label “Dev” is applied to dev dependencies, and “Test” is applied to all packages that have the word “test” in their file path. | e.g., Maven, Pip, Nuget, Npm, Dev, Test |

## Vulnerabilities Data Table

This table shows detailed info about each vulnerability that was identified in the open source packages used by your Project.

The header for the table shows how the table was filtered, the total number of filtered vulnerabilities, and how the table is sorted.

<figure><img src="../../../../../assets/Image_610.png" alt="" width="648"><figcaption></figcaption></figure>

The following table describes the info shown for each vulnerability identified by this scan.

| **Item** | **Description** | **Possible Values** |
|---|---|---|
| **Risk Level** | The severity level of the vulnerability, based on its CVSS score in the NVD. | • **HIGH** - 7.0-10.0<br>• **MEDIUM** - 4.0-6.9<br>• **LOW** - 0.0-3.9<br>For more info see Severity Levels. |
| **ID** | The ID of the CVE listing. The ID consists of the CVE prefix followed by the year that the CVE was discovered and the serial counter for that year's CVE listings.<br>**Note:** Vulnerabilities discovered by the Checkmarx Vulnerability Research Team which are not yet cataloged as CVEs, are indicated by the “Cx” prefix. | e.g., CVE-2020-9488 |
| **Package** | The name of the package in which the vulnerability was identified. | e.g., mysql:mysql-connector-java |
| **Version** | The version of the package where the vulnerability was identified. | e.g., 5.1.26 |
| **Ignored** | Indicates whether or not the vulnerability has been marked to be Ignored for this Project. Ignored vulnerabilities aren’t included in the count of vulnerabilities for the Project. | *Yes*, *No* |
| **Exploitable Path** | Indicates whether an exploitable path was detected by which the vulnerable package is called by your Project. | • **Yes** - an exploitable path was detected<br>• **No** - no exploitable path was detected<br>• **Unknown** - the Exploitable Path feature wasn’t activated for the scan |
| **Publication Date** | The date the vulnerability was published in the NVD. | e.g., Nov 16, 2020 |

## Licenses Data Table

This table shows detailed info about all of the licenses that were identified in the open source packages used by your Project.

The header for the table shows how the table was filtered, the total number of filtered licenses, and how the table is sorted.

<figure><img src="../../../../../assets/Image_614.png" alt="" width="648"><figcaption></figcaption></figure>

| **Item** | **Description** | **Possible Values** |
|---|---|---|
| **Legal Risk Level** | The Legal Risk calculation is based on the copyright risk score (below), where Level 1-3 is considered as a low risk, Level 4-5 as a medium risk, and Level 6-7 as a high risk. | • **High (Red)** – (6 to 7)<br>• **Medium (Orange)** – (4 to 5)<br>• **Low (Grey)** – (1 to 3)<br>• **Unknown (Light Grey)** |
| **Royalty** | Indicates whether or not a patent license is granted for free. | • **Free** – patent license is granted<br>• **NotFree** – patent license is not granted<br>• **Conditional** – patent license granted under some condition (e.g., if sued by user license is revoked) – this may change according to each license and requires consultation.<br>• **Empty** – status not known |
| **Name** | The name of the license. | e.g., GPL 2.0, Apache2.1 |
| **Copy Risk Score** | The score is defined as follows:<br>• **1** – Licensee may use code without restriction.<br>• **2** – Anyone who distributes the code must retain any attributions included in original distribution.<br>• **3** – Anyone who distributes the code must provide certain notices, attributions and/or licensing terms in documentation with the software.<br>• **4** – Anyone who distributes a modification of the code may be required to make the source code for the modification publicly available at no charge.<br>• **5** – Anyone who distributes a modification of the code or a product that is based on or contains part of the code may be required to make publicly available the source code for the product or modification, subject to an exception for software that dynamically links to the original code.<br>• **6** – Anyone who distributes a modification of the code or a product that is based on or contains part of the code may be required to make publicly available the source code for the product or modification.<br>• **7** – Anyone who develops a product that is based on or contains part of the code, or who modifies the code, may be required to make publicly available the source code for that product or modification if s/he (a) distributes the software or (b) enables others to use the software via hosted or web services. | A number between 1 and 7 |
| **Patent Risk Score** | Ranks the license based on:<br>• **1** – Royalty free and no identified patent risks<br>• **2** – Royalty free unless litigated<br>• **3** – No patents granted<br>• **4** – Specific identified patent risks | A number between 1 and 4 |
| **Affected Packages** | The number of packages in the Project in which the license was identified. | e.g., 3 |

## Policies Data Table

This table shows detailed info about each security Policy that was violated by your Project.

The header for the table shows the number of violated Policies, as well as how the table is filtered and sorted.

<figure><img src="../../../../../assets/Image_611.png" alt="" width="648"><figcaption></figcaption></figure>

The following table describes the info shown for each Policy violation identified by this scan.

| **Item** | **Description** | **Possible Values** |
|---|---|---|
| **Policy's set of conditions** | The name of the Policy and set of conditions that was violated. | e.g., Sample Policy 02 / Rule 1 / set #1 |
| **Violated Conditions** | A description of the specific rule that was violated. | e.g., Single Vulnerability Package vulnerability has severity level of { "valuekind": 2 } |
| **Violating Packages** | A list of all of the packages that violated this Policy. | e.g., Maven-com.thoughtworks.xstream:xstream- 1.4.5 |
