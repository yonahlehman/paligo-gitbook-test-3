# Checkmarx One CLI Config and Environment Variables

The CLI tool provides the ability to permanently store CLI options in configuration files.

The configuration files are kept in the users home directory under a subdirectory named ($HOME/.checkmarx).

## CLI Configuration Parameters

The following table contains all the values that can be stored in CLI configuration files:

### Authentication Parameters

- `cx_apikey` — An API Key to login to the Checkmarx One server.
- `cx_base_auth_uri` — The URL of the Checkmarx One User Management server.
- `cx_base_uri` — The URL of the Checkmarx One server.
- `cx_client_id` — The client ID that is used for client authentication.
- `cx_client_secret` — The client secret that is used for client authentication.
- `cx_tenant` — The customer's tenant name.

### Additional Configuration Parameters

- `cx_http_proxy` — An alternative method for specifying an optional proxy server. This enables users to designate a specialized proxy for use with Checkmarx One that doesn't affect the proxy used for other applications. When this is used it overrides the value of `http_proxy`.
- `cx_ignore_proxy` — Set this environment variable as `true` in order to ignore any proxies configured in your system, so that all Checkmarx One CLI commands run directly from your local machine. Alternatively, this can be done by using the global flag `--ignore-proxy`.
- `http_proxy` — An optional proxy server configuration.
- `sca-resolver` — The path to a correctly configured SCA resolver executable.
- `multipart_file_size` — Specifies the file chunk size (in gigabytes) used for multi-part uploads during CLI scans. This parameter is used when the source folder or ZIP file exceeds the Checkmarx One 5 GB upload limit. **Valid values**: 1–5 GB. Defaults to 2GB. Multi-part upload is only supported up to a total source size of 6 GB.

### Configuration Flags

The following flags are used with the `configure set` command.

{% hint style="info" %}
The `--prop-name` and `--prop-value` flags **must** be used with each `configure set` command.
{% endhint %}

- `---help, -h` — Help for the configure command.
- `--prop-name <string>` — Name of property set.
- `--prop-value <string>` — Value of property set.

Below are several examples for the CLI Configuration usage:

```
./cx configure set --prop-name cx_base_uri --prop-value "http://<AST-server>[:<port>]"
./cx configure set --prop-name cx_base_auth_uri --prop-value <AST User Management URI>
./cx configure set --prop-name cx_client_id --prop-value <Client ID>
./cx configure set --prop-name cx_client_secret --prop-value <Client Secret>
./cx configure set --prop-name http_proxy --prop-value <Proxy server>
./cx configure set --prop-name cx_apikey --prop-value <apikey>
./cx configure set --prop-name cx_tenant --prop-value <Tenant name>
```

## Environment Variables

The CLI tool supports several Environment Variables.

The below table includes all the Environment Variables that can be configured using the CLI tool.

{% hint style="info" %}
**The Environment Variables configuration is valid per shell session**.

This means that if Environment Variables were configured, but the CLI/CMD windows are closed, the configured Environment Variables will *not* be saved.

To use them again, you will need to configure them once again in a new shell session.
{% endhint %}

- `CX_APIKEY` — The API key to login to Checkmarx One with.
- CX_BASE_IAM_URI — The URL of the Checkmarx One User Management server. This is optional and only required when using a different instance than the Checkmarx One's built in one.
- `CX_BASE_URI` — The URL of the Checkmarx One server.
- `CX_CLIENT_ID` — The client ID that is used for client authentication.
- `CX_CLIENT_SECRET` — The client secret that is used for client authentication.
- CX_CONFIG_FILE_PATH — Specify the location where your config file is stored.

  By default, the config file is stored at ($HOME/.checkmarx). If this environment variable is set, all CLI commands will refer to the specified file location.
- `CX_HTTP_PROXY` — An alternative method for specifying an optional proxy server. This enables users to designate a specialized proxy for use with Checkmarx One that doesn't affect the proxy used for other applications. When this is used it overrides the value of `HTTP_PROXY`.
- `CX_LINK_SERVER_HOST` — Enter the CxLink to be used for connecting to your code repository. This enables sending PR decorations to the code repository without exposing it to the internet. Learn more about CxLink [here](../../user-guide/cxlink.md).
- `CX_TENANT` — The tenant that is used for client authentication.
- `CX_PROXY_AUTH_TYPE` — Proxy authentication type, (basic, ntlm, kerberos, or kerberos-native). `kerberos` for [MIT kereberos](https://web.mit.edu/kerberos/dist/) and `kerberos-native` for [SSPI](https://learn.microsoft.com/en-us/windows-server/security/windows-authentication/security-support-provider-interface-architecture).

  {% hint style="info" %}
  Required when using the `CX_HTTP_PROXY` variable.
  {% endhint %}
- `CX_PROXY_KERBEROS_CCACHE` *(Default - KRB5CCNAME env or OS default)* — Path to Kerberos credential cache.

  {% hint style="info" %}
  This optional variable is relevant only when `CX_PROXY_AUTH_TYPE` is set as `kerberos`, i.e., for MIT Kerberos authentication.
  {% endhint %}
- `CX_PROXY_KERBEROS_KRB5_CONF` *(Default - Linux - /etc/krb5.conf, Windows - C:\\Windows\\krb5.ini on windows)* — Path to Kerberos configuration file.

  {% hint style="info" %}
  This optional variable is relevant only when `CX_PROXY_AUTH_TYPE` is set as `kerberos`, i.e., for MIT Kerberos authentication.
  {% endhint %}
- `CX_PROXY_KERBEROS_SPN` — Service Principal Name (SPN) for Kerberos proxy authentication.

  {% hint style="info" %}
  Required when `CX_PROXY_AUTH_TYPE` is set as `kerberos` or `kerberos-native`.
  {% endhint %}
- `HTTP_PROXY` — Triggers the CLI to use a proxy server.
- `multipart_file_size` — Specifies the file chunk size (in gigabytes) used for multi-part uploads during CLI scans. This parameter is used when the source folder or ZIP file exceeds the Checkmarx One 5 GB upload limit. **Valid values**: 1–5 GB. Defaults to 2GB. Multi-part upload is only supported up to a total source size of 6 GB.

## Setting Environment Variables

### Linux/MAC

To set an Environment Variable on **Linux/MAC** operating systems, use the **export** command.

For example:

```
# Configure the CX_BASE_URI as an environment variable
export CX_BASE_URI=https://<URL of the Checkmarx One server>

# Configure the CX_APIKEY as an environment variable
export CX_APIKEY=<APIKEY>
```

### Windows

To set an Environment Variable on **Windows** operating systems, use the **setx** command.

For example:

```
# Configure the CX_BASE_URI as an environment variable
setx CX_BASE_URI https://<URL of the Checkmarx One server>

# Configure the CX_TOKEN as an environment variable
setx CX_APIKEY <APIKEY>
```
