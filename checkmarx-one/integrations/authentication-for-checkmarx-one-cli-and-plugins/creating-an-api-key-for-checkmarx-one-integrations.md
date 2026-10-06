# Creating an API Key for Checkmarx One Integrations

You can generate an API Key by logging in to Checkmarx One and generating a new API Key, as described below. Alternatively, an API Key can be generated using the Authentication API.

The roles (permissions) assigned to an API Key are inherited from the user who is logged in when the API key is generated. Therefore, make sure that you are logged in to an account with the appropriate permissions.

{% hint style="info" %}
The minimum required roles for running an end-to-end flow of scanning a project and viewing results via the CLI or plugins are Checkmarx One `plugin-scanner` role and IAM `default-roles<tenant>` role.

The permissions included in `plugin-scanner` are shown here. If you would like to create a custom role with more granular permissions, you should refer to this list of permissions in order to determine which permissions you will need to assign.
{% endhint %}

{% hint style="warning" %}
Whenever you update your Checkmarx One license (e.g., adding a new scanner) all existing API Keys become invalid. You will need to generate new API Keys to replace those that are used in your integrations and plugins.
{% endhint %}

**To log in to Checkmarx One:**

1. Open the URL for your environment.

   **Checkmarx One Server Base URLs**

   - US Environment - https://ast.checkmarx.net
   - US2 Environment - https://us.ast.checkmarx.net
   - EU Environment - https://eu.ast.checkmarx.net
   - EU2 Environment - https://eu-2.ast.checkmarx.net
   - DEU Environment - https://deu.ast.checkmarx.net
   - Australia & New Zealand – https://anz.ast.checkmarx.net
   - India - https://ind.ast.checkmarx.net
   - India 2 - https://ind-2.ast.checkmarx.net/
   - Singapore - https://sng.ast.checkmarx.net
   - UAE - https://mea.ast.checkmarx.net
   - Israel - https://gov-il.ast.checkmarx.net
2. Log in to your Checkmarx One account by entering your *Tenant Account*, *Username* and *Password*.

## Generating an API Key

{% embed url="https://vimeo.com/1083267558" %}

**To generate an API Key:**

1. Log in to the Checkmarx One web portal and select **Settings <img src="../../../assets/Settings.png" alt="" data-size="line">> Identity and Access Management** in the main navigation.

   The IAM portal opens.
2. In the main navigation, click **API Keys**, then click on the **Create Key** button.

   <figure><img src="../../../assets/API_Keys.png" alt="" width="648"><figcaption></figcaption></figure>

   The API Key configuration window opens.

   <figure><img src="../../../assets/API_Keys_Create.png" alt="" width="360"><figcaption></figcaption></figure>
3. You can optionally adjust the configuration as follows:

   - **Note** - Add a descriptive note to the API Key.
   - **Expiration period** - Adjust the period of time until the key expires. The value can be from 30 to 365 days.

     {% hint style="info" %}
     If an administrator set the default expiration period to be "enforced", then this field will be locked.
     {% endhint %}
   - **Notification emails** - Enter emails of each recipient who you would like to receive notifications regarding expiration of the key. After entering each email, click **Add**. By default the email of the current user is included.
4. Click **Create**.

   The API Key is created and a window opens showing the key.

   <figure><img src="../../../assets/API_Keys_Created.png" alt="" width="360"><figcaption></figcaption></figure>
5. Copy the key and save it in a place where you will be able to retrieve it for future use.

{% hint style="info" %}
Once you close the window, you will no longer be able to access this API Key.
{% endhint %}

{% hint style="info" %}
You can obtain a curl for submitting the request for an access token, by clicking on **Show details** and copying the content.
{% endhint %}
