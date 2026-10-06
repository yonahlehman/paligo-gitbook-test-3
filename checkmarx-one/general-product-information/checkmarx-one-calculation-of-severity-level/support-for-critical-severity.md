# Support for Critical Severity

Checkmarx One will soon add a new CRITICAL Severity to its list of severity options. This severity affects almost all of the platforms. Some of the SAST, SCA, and IaC Security vulnerabilities labeled as HIGH will be classified as CRITICAL.

This landing page will provide information on delivery dates, areas of impact, and actions that users might need to take in response to these changes.

{% hint style="info" %}
Please note that this rollout will be gradual, and we'll notify you about a month in advance. Contact your Account Manager or Customer Success Manager for more details about the planned date.
{% endhint %}

## Impact areas

| Area | Impact (What is changing) |
|---|---|
| SAST Engine Results | • For the comprehensive list of SAST query updates in PDF format, click [here](https://download.checkmarx.com/cxcustomersdocuments/SAST Query Updates.pdf).<br>- Only new scans are affected<br>- 9.6: High to Critical<br>- Result Viewer will display “Critical”<br>- Result Viewer will have filters on “Critical”<br>- Project page will be updated with total number of “Critical” findings per project<br>- Overview page will be updated with “Critical” trends |
| SCA Engine | • Based on scoring (CVSS standard)<br>- Only new scans are affected |
| IaC Engine | • For the comprehensive list of IaC query updates in PDF format, click [here](https://download.checkmarx.com/cxcustomersdocuments/IaC Security Query Updates.pdf).<br>- Only new scans are affected |
| DAST Engine | • The Engine does not provide Critical results<br>• The customer can change the severity of a scan to Critical<br>• DAST tab in the app will show Critical in the Risk bar |
| Reporting | • Scan reports will support “Critical” findings |
| Analytics Module | Insights will be updated with “Critical” vulnerabilities in the corresponding dashboards. |
| APIs | All relevant APIs have been given Critical Severity. The change does not affect existing customers who consume the APIs. |
| Feedback Apps | • “Critical” state is added to the Wizard<br>• Customers need to edit existing Trigger conditions to create Feedback issues with “Critical” findings |
| Policy Management | • Important Action item: Customers to edit existing policies<br>• All scanners support Critical severities in their respective policies |
| CI/CD Reports | Reports to have a summary that includes “Critical” |
| CLI Filtering | • CLI will support all “Critical” filtering<br>• Thresholds updated to handle “Critical” |

## FAQ

| Question | Answer |
|---|---|
| Can I opt out of having the Critical severity? | No, this is a mandatory change for all customers. |
| Will this change be gradual or all at once? | Yes, this change will be gradual. Please contact your CSM for more details or to join the early adopters. |
| I have policies set up that report on High vulnerabilities. Will I need to do anything? | **Important!**: Yes, you must manually go into the policy and add Critical as a criteria in your already existing policy. |
| I have feedback apps that create bugs or notifications on High vulnerabilities. Will I need to do anything? | Yes, you must manually go into the feedback app and add “Critical” as a filter. |
| I have thresholds set up in the CLI. Will I need to do anything? | Yes, you must update the CLI additional arguments and the filter options on the thresholds. |
| Do we expect the vulnerabilities to be set to Critical when the Critical Severity is released? | No, the vulnerabilities will change on a new scan.<br>This change will only impact new scans. Previous scans will not be impacted. |
| What are the dates for the “preview scan” and can this be somehow combines (preview of the new priority)? | It’s in a pre-release environment but is not expected to be released until Q3 2024. |
| How are severity labels for individual results calculated? | For SCA it is based on CVSS score. For SAST, our AppSec team identified vulnerability types that should be considered Critical. |
| How are severity labels for projects and applications calculated? | If one Critical vulnerability is found, the project or application is considered Critical. |
| How are historic results migrated? | They will be migrated with the same severity but can change after the first scan. |
| What impact will there be to my current dashboard/reports? | It’s possible that the HIGHs will go down and the CRITICAL will go up. |
| Why did it take so long for Checkmarx to adopt CVSS v3 severity labels? | It’s been a Work In Progress for over a year. It affects all aspects of not only our current CxOne Platform, but will affect the CxSAST 9.7 version in the future, too. |
| How will this change impact the Checkmarx plugins I am using? | The plugins will support showing the Critical results but won’t affect the initiation of scans. |
| If a vulnerability was manually changed from HIGH to LOW before the upgrade, will it be re-evaluated and updated to CRITICAL after the upgrade when the next scan is performed? | If the user manually changes the severity of a result before the upgrade, the severity will remain as defined by the user after the upgrade and will not change to Critical. |
| If a vulnerability was detected as HIGH before the upgrade and changed to CRITICAL after the upgrade and next scan, will it still be considered a "recurrent" vulnerability and not "new"? | The severity may change, but the vulnerability is still considered Recurrent after a new scan. For example before the upgrade, all vulnerability results were new; after the upgrade and a new scan, the results appear as Recurrent. |
| Will the queryID and similarityId of a vulnerability detected as HIGH before the upgrade, and now as CRITICAL after the upgrade and next scan, will remain unchanged due to the upgrade (assuming the code has not changed)? | Changes in severity do not impact the SimilarityID algorithm. |
