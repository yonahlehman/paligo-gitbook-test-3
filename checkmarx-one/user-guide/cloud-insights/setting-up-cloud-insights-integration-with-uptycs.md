# Setting up Cloud Insights Integration with Uptycs

## Overview

Uptycs is a cloud security platform that is built to handle the scale and complexity of modern cloud environments, Uptycs provides unparalleled visibility into the entire infrastructure, continuously auditing for vulnerabilities, and delivering real-time, context-rich insights. The Uptycs platform captures and processes vast amounts of telemetry data in real-time, leveraging a unique ETL-free engine for low-latency, high-fidelity analytics. Uptycs cloud security platform can protect cloud workloads, orchestrators, and identities, ensuring robust security at every layer of the cloud ecosystem.

### Prerequisites

- A Checkmarx One account with **Essential**, **Professional** or **Enterprise** license
- A Uptycs account with **Uptycs Audit** or **Uptycs Secure** license
- The Uptycs eBPF sensor must be deployed on the environment that you would like to monitor

## Integration Procedure

1. Log in to the Uptycs platform, navigate to the **Configuration** section, and set up the **Checkmarx Integration**.
2. To verify that the integration was successful, log in to the Checkmarx One web console and go to **ASPM** <img src="../../../assets/Insights.png" alt="" data-size="line">> **Cloud Insights**. Check in the header bar for the status of the connection. Once it is **Connected**, you can start viewing Cloud Insights in Checkmarx One, as described in [Viewing Cloud Insights Results](README.md#viewing-cloud-insights-results).

   {% hint style="info" %}
   If you have several Cloud Insights accounts, click on **Manage Accounts** and search for Uptycs and then check if the status is Connected.
   {% endhint %}

   {% hint style="info" %}
   It may take a few hours for the data enrichment process to complete. If after 24 hr the status is still **Pending**, you should ensure that all prerequisites are in place. If the issue is not resolve, please contact Checkmarx Support for assistance.
   {% endhint %}
