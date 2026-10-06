# Viewing and Triaging BYOR Results

After the import is completed, you can assess the results inside the Application Risk Management feature.

Go to the **Workspace** > **Applications** page for the application to which the results were imported, and open the **Risk Management** tab. This tab shows up to 50 of the most severe risks in the application. Filter the **Vulnerability Type** column for **Imported Results** to show the vulnerabilities imported via BYOR.

<figure><img src="../../../assets/Image_1933.png" alt="" width="576"><figcaption></figcaption></figure>

Clicking on a row will open that result in a new tab, displaying detailed information about the vulnerability that was retrieved from the imported SARIF file.

<figure><img src="../../../assets/Image_1935.png" alt="" width="576"><figcaption></figcaption></figure>

This page shows sections for **Remediation**, **Resolution** and **Result Info**. If some of the optional fields were not included in the SARIF file then data may be missing for some of these sections. There is also a summary section at the bottom of the page.

## Triaging BYOR Results

The state of the result is shown in the top left top corner. By default, all new results are designated as To Verify. Based on your assessment of the risk posed to your application, you can change the state. Possible states are: To Verify (default), Not Exploitable, Proposed Not Exploitable, Confirmed, and Urgent.

To change the state, click on the state and select the desired state from the drop-down list.

<figure><img src="../../../assets/Image_1936.png" alt="" width="576"><figcaption></figcaption></figure>

### Identifying Unique Results for BYOR

When you triage a vulnerability (i.e., change the state), the new state will be applied to that unique result each time that it is identified in a subsequent file upload. For results that are imported using the BYOR feature, we identify unique results for multiple imported files based on the following criterion.

- **Guid Field in SARIF file**: If the results section of the SARIF file contains a `Guid` field, we will use this as the `resultID` to identify the result uniquely.
- **Hash Calculation:** In the absence of the `Guid` field, we calculate a hash by combining the following 5 fields to create a unique identifier:

  - **toolName:** The name of the tool that generated the result.
  - **ruleID:** The identifier for the rule that triggered the result.
  - **snippetText:** The code snippet associated with the result.
  - **locationURI:** The URI of the file or resource where the result was found.
  - **lineStart:** The starting line number where the issue was detected.
