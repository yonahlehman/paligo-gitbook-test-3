# Setting up Cloud Insights Integration with Sysdig

## Overview

Sysdig Secure is part of Sysdig’s container intelligence platform which provides container, Kubernetes, and cloud security for the entire enterprise.

Sysdig integration with Checkmarx One enables submission of data from the runtime environments of joint-customers into Checkmarx Cloud Insights which then correlates the runtime data with Checkmarx One Projects and source code repositories, enriching Checkmarx One scanners results.

After the initial setup, Sysdig will push up-to-date data to Checkmarx every 24 hours.

Sysdig connector to Checkmarx One is built as a Lambda function which leverages the Sysdig Inventory API and Checkmarx One Cloud Insights API. Please contact us if you are interested in the deployment and configuration instructions.

### Prerequisites

- A Checkmarx One account with **Essential**, **Professional** or **Enterprise** license.
- A Sysdig account with **Sysdig Secure** license

## Integration Procedure

1. Set up the integration using the Lambda function provided by Sysdig. For more information, contact us.
2. To verify that the integration was successful, log in to the Checkmarx One web console and go to **ASPM** <img src="../../../assets/Insights.png" alt="" data-size="line">> **Cloud Insights**. Check in the header bar for the status of the connection. Once it is **Connected**, you can start viewing Cloud Insights in Checkmarx One, as described in [Viewing Cloud Insights Results](README.md#viewing-cloud-insights-results).

   {% hint style="info" %}
   If you have several Cloud Insights accounts, click on **Manage Accounts** and search for Sysdig and then check if the status is Connected.
   {% endhint %}

   {% hint style="info" %}
   It may take a few hours for the data enrichment process to complete. If after 24 hr the status is still **Pending**, you should ensure that all prerequisites are in place. If the issue is not resolve, please contact Checkmarx Support for assistance.
   {% endhint %}
