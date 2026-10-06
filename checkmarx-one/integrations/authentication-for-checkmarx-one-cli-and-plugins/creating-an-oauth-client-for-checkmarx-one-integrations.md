# Creating an OAuth Client for Checkmarx One Integrations

You can create an OAuth Client by logging in to Checkmarx One and creating a new client.

{% hint style="info" %}
If the new access management is enabled, the OAuth client must be granted resource-level authorization (at the tenant, application, or project level) to function properly.
{% endhint %}

## Logging in to Checkmarx One

**To log in to Checkmarx One:**

1. Open the URL for your environment (see the full list above).
2. Log in to your Checkmarx One account by entering your *Tenant Account*, *Username* and *Password*.

   {% hint style="info" %}
   To create an OAuth Client, you need to be signed in as an admin user.
   {% endhint %}

## Creating an OAuth Client

To create an OAuth Client, you must have the following permissions:

- `assign-project-all-groups`: Allows assigning any existing group when creating or updating a project
- `view-access`: – Allows viewing endpoints.

{% embed url="https://vimeo.com/1083272869" %}

**To create an OAuth Client:**

1. Log in to Checkmarx One and click on **Settings <img src="../../../assets/Settings.png" alt="" data-size="line">> Identity and Access Management** in the Menu panel.

   <figure><img src="../../../assets/Settings_IAM.png" alt="" width="648"><figcaption></figcaption></figure>
2. In the **Identity and Access Management** console, click **OAuth Clients** and then click **Create Client**.

   <figure><img src="../../../assets/OAuth_Create.png" alt="" width="648"><figcaption></figcaption></figure>
3. In the **Client ID** field, enter a descriptive name for Client, and then click **Create**.

   {% hint style="info" %}
   The **Client ID** field accepts only letters, numbers, spaces, and these symbols: `. ( ) [ ] { } - _`.
   {% endhint %}

   ![](../../../assets/OAuth_Client_ID.png)

   The Client Settings screen is shown.

   <figure><img src="../../../assets/OAuth_Client_Settings.png" alt="" width="648"><figcaption></figcaption></figure>
4. Copy the **Client ID** for use in the plugin configuration.
5. Click on the **Regenerate** button to generate the Secret.
6. In the dialog that opens, copy the **Secret** for use in the plugin configuration, and then click **Ok** to close the dialog

   <figure><img src="../../../assets/OAuth_Client_Generate.png" alt="" width="432"><figcaption></figcaption></figure>
7. You can optionally adjust the **Settings** as follows:

   - **Name** - Specify the name that will be displayed for this Client.
   - **Other** - Enter additional information about this Client.
   - **Description** - Enter a description of this Client.
   - **Expiration period** - Specify the period of time until the key expires. The value can be from 30 to 365 days.

     {% hint style="info" %}
     If an administrator set the default expiration period to be "enforced", then this field will be locked.
     {% endhint %}
   - **Days before notification** - Specify the number of days before the Client will expire that notifications will start being sent. Notifications will be sent on a daily basis from the day on.
   - **Notification emails** - Enter emails of each recipient who you would like to receive notifications regarding expiration of the key. After entering each email, click **Add**. By default the email of the current user is included.
8. Under **Groups**, you can optionally assign groups to the Client.

   For more information, refer to Groups.
9. Under **Role Mapping** select the relevant roles, and click on **Add selected**.

   {% hint style="warning" %}
   The minimum required role for running an end-to-end flow of scanning a project and viewing results via the CLI or CI/CD plugins is `plugin-scanner`.

   Alternatively, you can use the combination of the following roles: CxOne composite role `ast-scanner`, CxOne role `view-policy-management` (not required for IDE plugins) and IAM role `default-roles`.
   {% endhint %}
10. Click **Save Client**.
