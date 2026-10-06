# AI Assist Settings

## Configuring AI Triage in Global Account Settings

In the global account settings you can define the default rules that determine when AI Triage is automatically run across your organization.

**To configure the global account settings:**

1. In the Checkmarx One web application, navigate to **Global Settings > AI Assist**.
2. Activate the **Auto-triage** toggle.

   The Auto-triage configuration options are shown:

   <figure><img src="../../../../assets/Image_1304-9d1c9cba.png" alt="" width="432"><figcaption></figcaption></figure>
3. Specify values for the following parameters:

   - **Projects** – The projects to which the following rules for running AI Triage apply.
   - **Branches** – The branches which trigger automatic AI Triage.
   - **Scanners** – The scanners whose results trigger AI Triage.
   - **Risk Status** – The vulnerability status values that trigger AI Triage.
   - **Risk Severity** – The vulnerability severity levels to include.
4. For each parameter, select the **Allow Override** checkbox to permit individual projects to customize their own Auto-triage settings.
5. Click **Save**.
