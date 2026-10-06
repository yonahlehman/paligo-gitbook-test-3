# Application Reports

Application reports provide a concise and thorough summary of applications that are vulnerable and those that maintain a secure status. By tracking open vulnerabilities across applications, you can take proactive measures to tackle potential security vulnerabilities before they escalate, thereby reducing the risk of security flaws.

## Configuring and Generating Report

Before generating an Application report, you need to configure it in the **Generate Report** wizard.

Go to the **Workspace** <img src="../../../assets/Workspace.png" alt="" data-size="line">> **Applications** screen, and click on **Open Vulnerabilities Report**.

The **Generate Report** wizard includes four stages, each described in detail below.

### Step 1: Select Scanners

Select the scanners to be included in the report. You can select one or more of the options: SAST, SCA, IaC, Container Security, Secret Detection and Repository Health. By default, all are selected.

Click **Next** when done.

### Step 2: Select Filters

In this stage, you specify which applications will be included in the report.

- You can select applications either by tag or by application name. Click on the **By Tag** and/or **By Name** field and select the relevant entities from the drop-down list.
- **Include only last scanned branches** is selected by default. You can choose to deselect it.

Click **Next** when done.

### Step 3: Select Sections

In this step, you decide which sections will appear in the generated report. You can select **All Sections** or any combination of the following:

- **Vulnerable Applications:** This section offers specific information about applications that have vulnerabilities. It delves into the details of these vulnerabilities, their impact, and any other relevant information.
- **Vulnerable Projects:** This section provides an overview of projects in the specified applications with identified vulnerabilities.
- **Results Overview:** A summarized view of the overall scan results across the relevant applications.
- **Applications Overview:** Comprehensive information about the relevant applications. It goes beyond vulnerability details and offers a holistic view of each application, including its structure, components, and any other relevant information gathered during the scanning process.
- **Projects Overview:** A comprehensive view of all projects. It includes information about project structure, components, and any other relevant details collected during the scanning process.

### Step 4: Destination

In this stage, you choose the format for the generated report (PDF or JSON) and decide whether to send the report via email. If yes, enter email addresses of the recipients separated by a semi-colon.

{% hint style="warning" %}
Designating email recipients requires the permission `send-report-email`. Users without this permission won't see this field in the UI.
{% endhint %}

Click **Generate Report** when done.

## Key Performance Indicators (KPIs)

These metrics give a clear picture of the security posture of your application.

### Vulnerable Applications

This section is available only when the report is generated from **Applications** tab. It offers specific information about applications that have vulnerabilities. It delves into the details of these vulnerabilities, their impact, and any other relevant information.

#### Branch Inclusion Criteria

The vulnerability data shown here is based on selected branches from associated projects. The system determines which branches to analyze using the following logic:

1. **Primary Branch Configuration**: The branch designated as the primary branch on the project overview page is prioritized.
2. **Protected Branches**: Branches flagged as protected during the integration setup are included.
3. **Naming Convention**: Branches with the following names are included by default: `main`, `master`, `dev`, `develop`, `development`, or `merge`.

   {% hint style="info" %}
   Not case sensitive, but must be an exact match (no wildcards).
   {% endhint %}

#### By Results

The pie chart offers a visual breakdown comparing applications with unresolved vulnerabilities to those without any detected vulnerabilities. It provides a percentage-based representation for each category.

#### Top 10 Vulnerable Applications

The presented card highlights the ten most vulnerable applications, ranked in descending order of severity, from High to Information. If the report includes the **Vulnerable Applications** section, the names of these applications are interactive, allowing direct navigation to their corresponding entries in the **Vulnerable Applications** section. If this section is excluded, the application names remain non-clickable.

{% hint style="info" %}
You may see applications with zero results. This occurs when the KPI includes applications that were scanned but returned no vulnerabilities across any of their branches.
{% endhint %}

### Vulnerable Projects

This section of the Open Vulnerabilities report examines the contrast between the projects with unresolved vulnerabilities and those that remain free from detected issues. It also shows the top 10 vulnerable projects and their associated applications, offering insights into their severity levels.

#### By Results

The provided pie chart offers a visual breakdown, highlighting the comparison between projects with unresolved vulnerabilities and those with no vulnerabilities detected. The distribution of each category is illustrated in percentage terms.

#### Top 10 Vulnerable Projects

This card spotlights the ten projects most vulnerable due to their elevated count of open vulnerabilities. Projects are arranged in descending order of severity, ranging from High to Information. Each project entry also includes a list of associated applications with their respective project names.

If the report includes the **Vulnerable Projects** section, project names featured in the top 10 are interactive, allowing for navigation to their corresponding entries in the **Vulnerable Projects** section. If the **Vulnerable Projects** section is not included, the project names remain non-clickable.

{% hint style="info" %}
You might come across projects displaying zero results. This can happen because the KPI considers a project as vulnerable if it has undergone scans, even if the last scan yielded zero results.
{% endhint %}

### Results Overview

This section offers a comprehensive overview through visual aids and informative cards, providing insights into the overall results derived from scans. We break down the results by severity, state, status, scanner, and further explore findings across different languages, technologies, and packages.

#### By Severity

The pie chart visually represents the overall results categorized by severity levels, presenting the respective percentage for each severity. This helps to gauge the distribution of issues based on their criticality.

#### By State

Another pie chart breaks down the results by state, showing the percentage distribution for each state. This offers insights into the current status of identified issues.

#### By Status

This pie chart categorizes the overall results by status, providing the respective percentage for each status. This helps in understanding the progress of issue resolution.

#### By Scanner

A pie chart breaks down the results by scanner, offering the respective percentage for each scanning tool used. This sheds light on the efficacy of different scanning methods.

#### By Language, Technology & Package

A stacked chart provides a detailed breakdown of findings by severity level for each scanned language, technology, and package. This in-depth analysis helps identify areas that may require specific attention.

#### Top 10 Vulnerabilities

A card highlights the ten vulnerabilities identified in scans, ranked by severity levels from High to Informational, irrespective of the scanned language. Each vulnerability listed includes details about the scanner that flagged it.

#### Top 10 Oldest Vulnerabilities

Another card presents the ten oldest vulnerabilities, regardless of language. Each vulnerability listed includes details about the scanner that flagged it, as well as its age measured in days. This insight helps prioritize the resolution of longstanding issues.

### Applications Overview

This section is available only when the report originates from the **Applications** tab. It provides detailed information about the applications and associated projects. Each application entry includes an overview of overall results, results categorized by severity level, and the total number of associated projects.

The interactive application name allows for direct navigation to the corresponding **Application Overview** page. For each associated project, you'll find interactive details such as:

- **Project name:** Click to navigate directly to the corresponding Project Overview page.
- **Branch name:** The name of the corresponding branch. If the project has no branches, **N/A** is displayed.
- **Open vulnerabilities:** Overall results and results categorized by severity level, based on the vulnerabilities from the last scan of each engine in the project for the selected branch.
- **Last scan details:** Scan ID, scanned date, scan type (full or incremental), scanned scanners.
- **Oldest vulnerability name:** The age of the oldest vulnerability and details about the scanner that flagged it.

### Project Overview

This section provides information about the projects included in the report. Each project presents data on the overall results, results categorized by severity level, and the associated applications. If a project is not linked to any application, **N/A** is displayed. The project name is interactive and can be clicked to navigate directly to the corresponding **Project Overview** page.

Each project includes the following details:

- **Branch name:** The name of the corresponding branch. If the project has no branches, **N/A** is displayed.
- **Open vulnerabilities:** Overall results and results categorized by severity level.
- **Last scan details:** Scan ID, scanned date, scan type (full or incremental), scanned scanners.
- **Oldest vulnerability name:** The age of the oldest vulnerability and details about the scanner that flagged it.
