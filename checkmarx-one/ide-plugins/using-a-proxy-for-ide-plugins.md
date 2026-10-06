# Using a Proxy for IDE Plugins

You can direct your Checkmarx One calls through a proxy server. This can be done by using the additional parameters in the plugin configuration, as described below.

There are additional methods for setting up proxy servers that are supported for specific IDEs.

- JetBrains - [Environment Variable](checkmarx-jetbrains-plugin/installing-and-setting-up-the-checkmarx-jetbrains-plugin.md#setting-up-a-proxy-variable-using-your-os-system-environment-variables)
- VS Code - [Environment Variable or VS Code Proxy Settings](checkmarx-vs-code-extension-plugin/installing-and-setting-up-the-checkmarx-vs-code-extension.md#setting-up-a-proxy-optional)

## Setting up a Proxy Variable using Additional Parameters

1. Go to the Checkmarx One plugin **Settings** .
2. In the **Additional parameters** section, enter `--proxy <proxy_url>`, with the proxy_url using the following format `http://<proxy_ip>:<port_number>`. If authentication is required, then the format should be `http://<username>:<password>@<proxy_ip>:<port_number>`.

   {% hint style="info" %}
   Make sure to include the `http://` prefix.

   It is not recommended to pass the username and password in clear text.
   {% endhint %}
