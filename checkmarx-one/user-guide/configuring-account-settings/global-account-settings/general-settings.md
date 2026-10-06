# General Settings

The **General** settings screen contains the following configuration parameters:

- **Global SSH Key** - In case configured, this key will be used for authentication with 3rd party vendors.
- **Skip Submodules** - Enable this option to skip scanning repository submodules during project scans. By default, this option is set to `false`.

{% hint style="info" %}
- Clicking the <img src="../../../../assets/Trash.png" alt="" data-size="line">icon will clear the configuration field.
- Checking the <img src="../../../../assets/Allow_Override.png" alt="" data-size="line"> checkbox will allow overriding the same parameter in the Project configuration level.
- By default, **"Allow override"** is selected for all the parameters in the Tenant settings.
{% endhint %}

{% hint style="warning" %}
The item below describes a functionality that is being rolled out in waves. Contact your support agent to find out whether this functionality is currently available in your environment.
{% endhint %}

- The options in the **Enable Source Code Management** section allow you to determine whether to immediately delete the entire source code after a scan is completed or to retain code snippets (i.e., a few lines before and after the vulnerable line of code).

  - **Delete partial source code**: When this option is selected, the system retains only the relevant code snippets (a few lines before and after the vulnerable line of code) after the scan is completed. This allows for easy reference to the source code related to any identified vulnerabilities
  - **Delete all source code**: When this option is selected, the entire source code is deleted immediately after the scan is completed.

  Toggling on **Enable Source Code Management** and selecting one of the options will result in the following:

  - The **Incremental Scan** option will be disabled, meaning that all scans will always be full scans.
  - The **Query Editor** option in the Project page's three-dot menu will be grayed out, and Checkmarx Audit will not load.
  - When clicking on a vulnerability finding, you won't be able to see the full source code behind it. The results will be presented without displaying the actual code associated with the findings.
