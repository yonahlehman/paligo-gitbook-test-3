# Authentication for Checkmarx One CLI and Plugins

You need to be authenticated for your Checkmarx One account in order to submit CLI commands. The required authentication parameters can be submitted as part of the CLI command or via Config or Environment variables, as described [above](../../cli-tool/configuring-the-checkmarx-one-cli/README.md). Authentication can be done either via **OAuth Clients** or an **API Key**.

{% hint style="info" %}
OAuth Clients let you specify only the permissions the integration needs. API Keys, by contrast, automatically inherit all permissions of the user who generated them, which may be broader than intended.
{% endhint %}

The Checkmarx One CLI tool supports both methods, but some Checkmarx One plugins support only one or the other.

The articles in this section explain how to generate the required credentials in Checkmarx One.

## In this section

- [Creating an API Key for Checkmarx One Integrations](creating-an-api-key-for-checkmarx-one-integrations.md)
- [Creating an OAuth Client for Checkmarx One Integrations](creating-an-oauth-client-for-checkmarx-one-integrations.md)
