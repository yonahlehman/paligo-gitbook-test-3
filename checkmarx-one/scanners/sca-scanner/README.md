# SCA Scanner

## Overview

Software developers are relying more and more on open source components to expedite the software development process. Projects often use numerous open source libraries, each of which calls on numerous direct and transitive dependencies. No matter how secure your proprietary code is, these open source dependencies can expose you to a broad range of security and legal risks.

The SCA scanner is Checkmarx's proprietary Software Composition Analysis (SCA) solution for detecting risks associated with your open source dependencies. Checkmarx SCA enables you to easily identify, prioritize, and remediate the risks posed by your open source packages. These risks may include security vulnerabilities, license requirements and outdated open source packages. SCA addresses all of these issues, providing highly accurate, relevant, and actionable insights.

### Understanding the Scan Process

The following are the main processes that Checkmarx One SCA scans run to identify the 3rd party packages in your project:

1. **File Analysis** – SCA identifies all files in your project that may be part of a 3<sup>rd</sup> party package, and analyzes them in order to determine which packages are being used. This is done by comparing the hashes and metadata of the relevant files (e.g., .jar files for Java, .js files for JS) in the scanned project with the hashes and metadata of packages that are cataloged in our database.

   {% hint style="info" %}
   For non-scripting files (e.g., .dll, .jar .zip .egg) there is a one to one relationship between files and packages. For scripting files (e.g., .js, .php, .c .cpp) we identify the package that best matches the group of related files in your project.
   {% endhint %}

   As part of this process, compressed files of supported types (.jar, .war, .ear, .zip) are extracted so that the files can be analyzed. This is applied recursively up to four levels of depth.
2. **Dependency Resolution** - SCA uses package managers to resolve the dependencies against customer-defined or public repositories and extract the dependency trees.
3. **Evidence Analysis** - SCA takes the output of the previous steps and uses it to identify the specific risks that affect the packages in your project. This is done by checking the packages that were identified against our extensive database of vulnerabilities as well as checking for legal and suspected malware risks.

## Key Features

### Exploitable Path

Prioritizing remediation of the many open source vulnerabilities identified by Checkmarx SCA can be a challenging task. It isn't always apparent whether the vulnerable packages are actually being called by your project, or whether the vulnerable methods inside them are actually being used by your code. The key question is: is there a path from your project code into the vulnerable package code, through which the vulnerability could be exploited? If not, remediation is a much lower priority

This is where **Exploitable Path** is essential. Checkmarx SCA analyzes your actual project source code, in parallel with your manifest file, to determine whether the vulnerable open source packages are called from your proprietary code and whether the vulnerable methods are actually used. This lets you focus remediation effort on vulnerabilities that are genuinely exploitable, rather than on every CVE reported in your dependency tree.

Exploitable Path also identifies which lines in your project code actually reach the vulnerable method in the vulnerable package, and shows you the full path to the vulnerability.

{% hint style="info" %}
Because Exploitable Path analyzes your entire codebase, it also shows the actual usage of packages in your project. You may find that some packages listed in your manifest file are no longer used, letting you streamline your manifest file and reduce your dependency footprint.
{% endhint %}

#### How Exploitable Path Works

Exploitable Path combines what Checkmarx already knows about a vulnerability with what it finds in your code:

1. For every supported CVE, the Checkmarx AppSec research team identifies the exact function, or functions, that must be called for the vulnerability to be triggered, and documents its signature. In parallel, Checkmarx indexes the public methods of the open source package itself.
2. When you run a Checkmarx One SCA scan, that same engine analyzes your source code to identify what it imports and calls. It confirms the package is genuinely used, resolves your calls to concrete methods inside it, and searches for a code path from your code to the documented vulnerable method.

If that path exists, the finding is flagged as an Exploitable Path: a real, traceable route from your application code to the vulnerable behavior.

#### Key Benefits

- Verify whether the vulnerable methods in open source packages are actually being called by your proprietary code.
- Prioritize remediation of exploitable vulnerabilities.
- See the full path from your project code to the vulnerable method.
- Runs natively as part of your regular Checkmarx One SCA scan: no separate scan, no additional engine, and no extra configuration required.

#### Enabling Exploitable Path

Exploitable Path only runs on Projects for which it has been activated. You can activate it during Project Creation or by editing Project Settings. You can also set it as your account's default for all new Projects, via Account Settings.

{% hint style="info" %}
Activating the feature globally does not retroactively activate Exploitable Path for Projects that were created before the activation.
{% endhint %}

Once activated for a Project, Exploitable Path runs automatically as part of every Checkmarx One SCA scan of that Project, whether triggered from the web portal, a CI/CD integration, or the CLI. No separate scan or additional setup is required.

#### Viewing the Exploitable Path Results

On the **[SCA Results > Packages](https://docs.checkmarx.com/en/34965-253661-sca-results.html#UUID-a5fb3fa5-578e-3f6a-bcd8-54357376fda1_UUID-fcbdaec2-8dac-b017-0414-1d0de94f414a)** tab, next to each package in the list, the **Usage** column shows the package's usage status.

Opening a package's details takes you to the **Package Usage** section, where you can see how many times, and in which files and lines, the package is called by your project code.

On the **[SCA Results > Risks](https://docs.checkmarx.com/en/34965-253661-sca-results.html#UUID-a5fb3fa5-578e-3f6a-bcd8-54357376fda1_UUID-ca525db6-548a-250d-fda4-4cb102387a9a)** tab, the **Reachability** column shows each vulnerability's Exploitable Path status.

Opening a vulnerability's details shows the full **Exploitable Path**: the visual call chain from your code, through the open source package, to the vulnerable method. You can clearly see which lines in your project code reach the vulnerable method, giving you a clear basis for remediation.

The following tables list the different values and their meanings.

**Package Usage status**

| Status | What it means |
|---|---|
| Used | The package is used by your source code. |
| Potentially | The package is a transitive dependency of a direct package that your source code uses. |
| Unused | No usage of this package was found in your source code. |
| Package to be analayzed soon | The package is newly seen and has been added to the analysis queue. Usage information will be available in an upcoming scan. |
| Package source code not available | The package's source code isn't publicly available, so usage can't be determined. |
| Failed to analyse source code | An error occurred while analyzing the package or your source code. |
| Unsupported language | Package Usage analysis isn't available yet for this programming language. |

**Exploitable Path status**

| Status | What it means |
|---|---|
| Exp. Path Found | A code path was found from your source code to the vulnerable method in the package. The vulnerability is reachable and can potentially be triggered. |
| Not Detected | Exploitable Path was evaluated for this finding, but no code path to the vulnerable method was found in your project. |
| Pending Analysis | The package is newly seen and has been added to the analysis queue. This finding will be evaluated for Exploitable Path in an upcoming scan. |
| Not Supported | Exploitable Path can't be evaluated for this finding. This covers a few underlying cases: the package's source code isn't available, the package is only used as a transitive dependency, or the language or package manager isn't yet supported for Exploitable Path. |
| Calculation Failed | An error occurred while analyzing the source code for this finding. |

{% hint style="info" %}
Package Usage and Exploitable Path are evaluated independently. A package can show as **Used** while its Exploitable Path status is **Not Detected**, if your code calls the package but never reaches the specific vulnerable method.
{% endhint %}

#### Current Support

1. Supported languages: Python, Java, JavaScript and C#.
2. **Scope:** Exploitable Path evaluates packages that your code calls directly, where the vulnerable method lives in that same package. This direct-call analysis gives you a fast, high-confidence answer for the dependencies your code actually touches.
3. **Package Coverage:** Checkmarx continuously grows its database of analyzed open source packages. If a package in your scan hasn't been analyzed yet, scanning a project that uses it moves that package to the front of the queue, and it's typically analyzed within the next 48 hours. From then on, it's included in Exploitable Path evaluation for every future scan.

### SCA Global Inventory

The **SCA Global Inventory and Risks** page displays a comprehensive list of all packages identified in your account, along with their associated risks and license information. This includes details such as vulnerabilities, outdated versions, and policy violations. By aggregating information across all Projects, the Global Inventory helps you prioritize remediation by showing which risks and vulnerable packages impact multiple Projects, making it easier to coordinate efforts across development teams.

With the addition of **bulk triage actions** in the Global Inventory, managing these risks at scale has become even more efficient. You can now select multiple items and triage them all at once across the **Packages**, **Vulnerabilities and Malware**, and **Licenses** tabs. For example, if you determine that a particular package is not a concern, you can search for all its instances in the Packages tab and mark them all as *Muted* with a single action. This capability streamlines large-scale triage workflows and saves time by enabling consistent decisions to be applied across the entire tenant.

For instructions on how to view the SCA Global Inventory, see Global Inventory.

### SCA Resolver

Checkmarx SCA Resolver is an on-prem utility that enables you to resolve and extract dependencies and fingerprints from your source code and send them to the Checkmarx One platform for risk analysis. The Resolver uses command line interface (CLI) commands to configure and scan your Projects.

Checkmarx SCA Resolver enables you to run a comprehensive SCA scan without the need to send your actual source code to the cloud. It also enables you to scan private (local) dependencies that aren’t accessible to the Checkmarx One platform.

For Checkmarx One accounts, Resolver is run via the Checkmarx One CLI, by adding the relevant flags to the `scan create` command. Resolver runs in Offline mode and the results are automatically sent to the Checkmarx One cloud for analysis.

- Learn more about downloading and installing SCA Resolver [here](using-sca-resolver-in-checkmarx-one/README.md#checkmarx-sca-resolver-download-and-installation).
- Learn about running scans via Checkmarx One CLI using SCA Resolver [here](using-sca-resolver-in-checkmarx-one/README.md).

<details>

<summary>What data is sent to the Checkmarx One Cloud?</summary>

After the File Analysis and Dependency Resolution are completed on-prem, the output of the analysis, the “evidence files”, are sent to the cloud for the final process of Evidence Analysis.

- The project name
- List of all file names and relative paths (except the ones that were excluded from the scan)
- Various checksums of the files (SHA-1, SHA-1 on content without spaces, etc.)
- Manifest files (except for scans run via Resolver with the `--no-upload-manifest` flag)

{% hint style="info" %}
The complete list of files that are sent to the cloud can be seen in Files Used for Manifest Resolution.
{% endhint %}

- Names of dependencies extracted from manifest files
- Scan errors and warnings such as “Failed resolving dependencies”. Each warning message may contain a file path as an argument.
- SAST Exploitable Path Query result (for Exploitable Path scans)

</details>

### Delta Scans

The Delta scan feature dramatically cuts the time of SCA scans when rescanning an existing project., if the manifest files haven’t been changed since the last scan, then we skip the dependency resolution process. This can cut scan times by up to 95% without detracting from the accuracy of the scan.

Once a week a full scan is enforced even if no changes were detected in the manifest files. This is intended to identify version changes caused by use of ranged versions.

{% hint style="info" %}
A failed scan won't be used as the basis for a subsequent Delta scan. However, if a partially successful scan identified the manifest files and they did not change, this will be used as the basis for a Delta scan.
{% endhint %}

When a scan runs as a Delta scan, an indication is shown in the Resolving Info dialog in the SCA scan results viewer.

#### Current Limitations

- Supported for all languages and package managers for which dependency resolution is done using manifest files except for C and C++.
- Does not apply to languages for which dependency resolution is done by file analysis (fingerprint method).
- For Single-Tenant, this is not available for scans run in the cloud. However, it is available for Single-Tenant accounts v3.56+ running scans locally using SCA Resolver.

### Export Remediated Manifest File

You can generate remediated manifest file/s that contain the recommended versions of your packages. These files can be download and used to update your project.

Remediated manifest files can be exported directly from the SCA scan results viewer. They are provided as a ZIP archive that preserves your project’s original file structure.

{% hint style="info" %}
- Currently supported for the following manifest files:

  - npm `package.json`
  - Python `requirement.txt`
  - NuGet `*.csproj` and `packages.config`
- Remediates only direct dependencies (not transitive)
- Because this method updates all vulnerable packages (sometimes changing a major version) it may break methods used in your code. You may need to refactor your code to avoid changes in functionality.
{% endhint %}

For a guided procedure of exporting remediated manifest files, see [Remediation using a Manifest File](sca-results-viewer.md#remediation-using-a-manifest-file).

### SCA Auto Pull Request

For Code Repository Integration projects, **SCA Auto Pull Request** automatically submits pull requests with suggested remediation for SCA vulnerabilities. When code is pushed to a protected branch, triggering an SCA scan, Checkmarx identifies vulnerable packages for which a remediated version is available and sends an automatic PR to adjust your manifest files to use the remediated versions. The PR is created with branch name `branch_auto_pr`, and once approved, it is merged into your protected branch.

This is supported for all supported SCMs (GitHub, GitLab, Bitbucket and Azure DevOps).

This feature can be activated on the project level by turning on the **SCA Auto Pull Request** toggle in the project settings.

#### Limitations

- Currently supported for the following manifest files:

  - npm `package.json`
  - Python `requirement.txt`
  - NuGet `*.csproj` and `packages.config`
- A single PR is sent with all of the suggested changes (i.e., no separate PR for each package).
- A PR is sent whenever a remediated package is available. It is not possible to set thresholds or filter conditions.
- For Bitbucket integrations, the user who sets up the integration must have an email associated with their Bitbucket user account in order for this feature to work.

### Recalculating SCA Scan Results

Checkmarx enables scan **Recalculation** for the SCA scanner. This feature utilizes the dependencies identified in a previous scan and re-assesses the risks affecting your project based on the current data. There is no need to resubmit the source code in order to run scan recalculation since it uses the dependency resolution output from the previous scan. This method is useful for “static” projects, where no significant changes have been made to the source code since the previous scan.

Results from scan recalculation are shown in Checkmarx One as a separate scan.

The following factors will affect the recalculated scan results:

- If you changed the state of risks since the last scan of the project, those changes will be applied to the recalculated scan.

  {% hint style="info" %}
  If you have made state changes since the last scan, a warning icon is shown next to the project name in the list of projects, indicating the need for a scan recalculation.
  {% endhint %}
- Checkmarx has identified new vulnerabilities associated with the dependencies in your project since the previous scan.
- If you have changed the Policies that apply to your project since the last scan, the policy violations for the project will be updated.

To view the procedure for recalculating SCA scans, see Running Scan Recalculation.

### Scan Reports and SBOM Reports

Results from the SCA scanner are returned together with results from other scanners in Checkmarx One Scan Reports and Projects Reports. See Checkmarx One Reports

In addition, you can generate specialized SCA scan reports as well as Software Bill of Materials (SBOM) reports based on the packages identified by SCA.

### Scanning SBOMs

You can run an SCA scan on an SBOM file. The scan is run as a Checkmarx One project, with the source specified as an SBOM file. The SCA scanner returns comprehensive results of all risks associated with your open source packages. This enables customers who don’t want to submit their actual code, to obtain comprehensive SCA results for their project and manage the remediation via Checkmarx One.

SBOM scans can be run from the UI as well as via CLI or [REST API](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/branches/main/3zac73jdvh6e8-scans-service-rest-api#scanning-from-an-sbom-for-sca).

{% hint style="info" %}
This capability is distinct from the capability to analyze an SBOM using the POST /analysis/requests API. The new method shows SCA results in the context of an actual Checkmarx One project, as opposed to just returning a report with the enriched SBOM data.
{% endhint %}

Requirements:

- Supported file formats: json or xml following CycloneDX (v1.0-1.6) or SPDX (v2.2 or v2.3)
- It is mandatory to include the Package URL (purl) for each package in the SBOM. For more information about purl syntax, see [here](https://spdx.github.io/spdx-spec/v3.0/model/Software/Properties/packageUrl/).
- Only the SCA scanner can run on an SBOM
- Can only run on a “manual” project (not a code repository integration)

The procedure for running a scan on an SBOM is described here.

### AI Guided Package Remediation

When the SCA scanner identifies a vulnerable package in your project and there is no remediated version available, a button is shown that enables you to get AI generated suggestions for non-vulnerable replacement packages.

<details>

<summary>Hiding Dev & Test Dependencies</summary>

Checkmarx SCA is able to distinguish between development dependencies and production dependencies for several package managers. On the **Scan Results** page, the number in parenthesis next to the **Hide Dev & Test Dependencies** toggle indicates the number of dev & test dependencies in the Project. Toggle the **Hide Dev & Test Dependencies** switch ON if you would like to hide vulnerable packages that were identified as dev and test dependencies.

{% hint style="info" %}
This filter can also be applied to the following REST APIs: [Results Summary](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/branches/main/510ldapufb6ns-retrieve-summary-of-scan-results) and [All Scanners Results](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/branches/main/bf7eab3023aac-retrieve-scan-results-all-scanners).
{% endhint %}

#### Identifying Dev Dependencies

The following table shows how dev dependencies are identified for specific package managers.

| **Package Manager** | **Dev Dependency Specification** |
|---|---|
| NPM | In the manifest file (package.json or bower.json), using the devDependencies attribute. For example,<br>```<br>"devDependencies" : {<br> "my_test_framework": "^3.1.0".<br> "another_dev_dep": "1.0.0 - 1.2.0"<br>}<br>``` |
| Yarn | In the manifest file (package.json or bower.json), using the devDependencies attribute. For example,<br>```<br>"devDependencies" : {<br> "my_test_framework": "^3.1.0".<br> "another_dev_dep": "1.0.0 - 1.2.0"<br>}<br>``` |
| Bower | In the manifest file (package.json or bower.json), using the devDependencies attribute. For example,<br>```<br>"devDependencies" : {<br> "my_test_framework": "^3.1.0".<br> "another_dev_dep": "1.0.0 - 1.2.0"<br>}<br>``` |
| Composer | Packages under the require-dev section in the composer.json file. |

#### Identifying Test Dependencies

Any package with the word "test" in the file path is identified as a test dependency.

</details>

### Policy Management

Create customized policies with conditions relating to results from the SCA scanner. Conditions can relate to packages, vulnerabilities, malicious packages, and licenses.

For more information, see SCA Policy Conditions.

### CxScore

In addition to Risk Score (which focuses on severity of the risk based on CVSS), Checkmarx One provides an additional metric, CxScore, for each vulnerability. CxScore is a composite metric that reflects both vulnerability severity and likelihood of exploitation. It incorporates the EPSS score along with key exploitability indicators, including Exploitable Path, Known Exploited Vulnerabilities (KEV), and Proof of Concept (PoC) availability.

CxScore is assigned to vulnerabilities displayed in the Risks tab and is also shown for packages in the Packages tab. The Package CxScore reflects the highest CxScore among all vulnerabilities associated with that package.

For the complete documentation on CxScore, see CxScore: Risk Prioritization for SCA Vulnerabilities

## In this section

- [SCA Scanner - Supported Languages and Package Managers](sca-scanner---supported-languages-and-package-managers.md)
- [SCA Results Viewer](sca-results-viewer.md)
- [Triaging SCA Results](triaging-sca-results.md)
- [SCA Configuration Options](sca-configuration-options.md)
- [Preventing Malicious Software Attacks](preventing-malicious-software-attacks.md)
- [Using SCA Resolver in Checkmarx One](using-sca-resolver-in-checkmarx-one/README.md)
- [Scanning SBOMs](scanning-sboms.md)
- [SCA Scanner FAQ](sca-scanner-faq.md)
