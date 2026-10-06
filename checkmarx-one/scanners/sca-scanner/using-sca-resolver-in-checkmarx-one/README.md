# Using SCA Resolver in Checkmarx One

## Checkmarx SCA Resolver

Checkmarx SCA Resolver is an on-prem utility that enables you to resolve and extract dependencies and fingerprints from your source code and send them to the Checkmarx One SCA scanner for risk analysis. This enables you to run a comprehensive SCA scan without the need to send your actual source code to the cloud. It also enables you to scan private (local) dependencies that aren’t accessible to the Checkmarx SCA cloud platform. For Checkmarx One users, Resolver is used in Offline mode for dependency resolution and the results file is then sent for analysis via your Checkmarx One account.

In order to use the SCA Resolver with the Checkmarx One CLI, you need to download the Checkmarx SCA Resolver separately in a location that the Checkmarx One CLI can access. Download links are available [below](#checkmarx-sca-resolver-download-and-installation).

To use the SCA Resolver, you need to add the **--sca-resolver** flag to your command line with an argument with the path to your local installation of the Resolver executable. For example:

```
./cx scan create --project-name <Project Name> -s <path> --branch <branch name> --sca-resolver <path-to-resolver> --sca-resolver-params <additional-resolver-arguments>
```

Sample command:

```
user@laptop:/AST$ ./cx scan create --project-name demo --scan-types sast,sca -s . --sca-resolver /sca/scaResolver --sca-resolver-params "-q -e my_file" --async
```

{% hint style="warning" %}
When running a CLI scan that uses SCA Resolver, the source code must be in a local folder, not in a zip archive or a code repository.
{% endhint %}

The Delta Scan feature will run by default on the CxOne CLI (since version 2.3.44) scans using SCAResolver (since version 2.13.3). To disable this feature, use the **--sca-resolver-params** flag with the argument **--disable-delta-scan**. For more information on this feature, see [Delta Scans](../README.md#delta-scans).

To add additional arguments to Checkmarx SCA Resolver, use the flag **--sca-resolver-params** with any additional arguments that you need. If necessary to use spaces and/or quotes, wrap the arguments in double quotes and use single quotes inside the value. For a complete list of SCA Resolver configuration arguments, see Checkmarx SCA Resolver Configuration Arguments.

{% hint style="info" %}
Only arguments that can be used in **Offline** mode can be applied to scans run via the Checkmarx One CLI Tool and plugins.
{% endhint %}

<details>

<summary>Alternative Method</summary>

There is an alternative method that offers maximum control over the files being sent to the cloud for analysis. This is done by first running a scan using Resolver in offline mode on-prem. You can then run the scan create command in Checkmarx One and provide only the results file for upload. The following procedure describes this method.

1. Run SCA Resolver in offline mode and save the results to a file named `.cxsca-results.json` (precise name required) in the root path of your Checkmarx One CLI.

   ```
   ./ScaResolver offline -r "./cx-results/.cxsca-results.json" -s "%LOCATION_PATH%"
   ```
2. Run the `scan create` command in Checkmarx One, with the `-s` argument pointing to the folder where the Resolver results file was saved. For `--scan-types`, specify only `sca`.

   ```
   ./cx scan create -s "./cx-results/" --project-name "DemoProject" --branch "DemoBranch" --scan-types "sca"
   ```

</details>

For more information about using SCA Resolver in Checkmarx One CI/CD integrations, see Using SCA Resolver in Checkmarx One CI/CD Integrations.

## Checkmarx SCA Resolver Download and Installation

{% hint style="warning" %}
Versions of SCA Resolver **prior to 2.5.15** are no longer supported. Older versions will no longer be able to run Container scans. Download links for newer versions are available here.

We recommend always keeping up to date with the latest version of SCA Resolver, in order to benefit from the latest features as well as ongoing performance improvements and bug fixes.
{% endhint %}

### Download Latest Version of Resolver

Use the relevant link to download the latest version of SCA Resolver.

{% hint style="info" %}
The latest version of SCA Resolver is currently **2.16.2**.
{% endhint %}

- [Windows](https://sca-downloads.s3.amazonaws.com/cli/latest/ScaResolver-win64.zip)
- [Debian](https://sca-downloads.s3.amazonaws.com/cli/latest/ScaResolver-linux64.tar.gz)
- [Alpine Linux](https://sca-downloads.s3.amazonaws.com/cli/latest/ScaResolver-musl64.tar.gz)
- [MacOS](https://sca-downloads.s3.amazonaws.com/cli/latest/ScaResolver-macos64.tar.gz)
- [MacOS Installer](https://sca-downloads.s3.amazonaws.com/cli/latest/ScaResolver-macos64.pkg)

Use the relevant link to download the checksum for the latest version of Resolver.

- [Windows sha256sum](https://sca-downloads.s3.amazonaws.com/cli/latest/ScaResolver-win64.zip.sha256sum)
- [Debian sha256sum](https://sca-downloads.s3.amazonaws.com/cli/latest/ScaResolver-linux64.tar.gz.sha256sum)
- [Alpine Linux sha256sum](https://sca-downloads.s3.amazonaws.com/cli/latest/ScaResolver-musl64.tar.gz.sha256sum)
- [MacOS sha256sum](https://sca-downloads.s3.amazonaws.com/cli/latest/ScaResolver-macos64.tar.gz.sha256sum)
- [MacOS Installer sha256sum](https://sca-downloads.s3.amazonaws.com/cli/latest/ScaResolver-macos64.pkg.sha256sum)

{% hint style="info" %}
Links to download older versions of Resolver are available at Checkmarx SCA Resolver Changelog.
{% endhint %}

### Installation

{% hint style="info" %}
The following procedure is relevant when you download Resolver as a zip archive. When you run the MacOS Installer you just need to follow the prompts to run the installer. The installer saves the Configuration.yml file to `/Library/ScaResolver/{version}/Configuration.yml`.
{% endhint %}

**To download and Install Checkmarx SCA Resolver:**

1. Use the appropriate link (shown above) to download the correct version of Checkmarx SCA Resolver for your OS.
2. Extract the compressed archive file.
3. Install all required resolution utilities, see [Installing Supported Package Managers for Resolver](installing-supported-package-managers-for-resolver.md)

**Installation Notes:**

- On **Ubuntu**, run the command as root before running, or if you encounter any startup issues.

```
apt update
apt install ca-certificates libgssapi-krb5-2
```

- On **Alpine Linux**, run the command as root before running, or if you encounter any startup issues.

```
apk add libstdc++
apk add glib
apk add krb5 pcre
apk add bash
```

## In this section

- [Installing Supported Package Managers for Resolver](installing-supported-package-managers-for-resolver.md)
