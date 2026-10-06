# Using SCA Resolver in Checkmarx One CI/CD Integrations

You can run Checkmarx SCA Resolver with your Checkmarx One integrations, in order to resolve dependencies on-prem using pre-installed package managers. The Checkmarx One CLI Tool and plugins, run Resolver in Offline mode, which resolves the dependencies in the local build environment and outputs the results to a JSON file. Checkmarx One then bundles that data with additional Checkmarx One CLI data and sends it to the Checkmarx One Cloud for further processing.

## Prerequisites

- You have set up a CI/CD integration for Checkmarx One using a plugin or our CLI Tool, see [Checkmarx One CI/CD Integrations](README.md).
- When running a CLI scan that uses SCA Resolver, the source code must be in a local folder, not in a zip archive or a code repository.
- Make sure that all relevant package managers are installed on your local environment, see Installing Supported Package Managers for Resolver.

## Running Scans Using SCA Resolver

1. Use the following script to download and run SCA Resolver (for Linux64), as a step in the pipeline or as part of your script (depending on your platform).

   ```
   - wget https://sca-downloads.s3.amazonaws.com/cli/latest/ScaResolver-linux64.tar.gz
   - tar -xzvf ScaResolver-linux64.tar.gz
   - rm -rf ScaResolver-linux64.tar.gz
   ```

   {% hint style="warning" %}
   If you are using a different OS make sure to give the path to the appropriate installation file, as provided here.
   {% endhint %}
2. In the `scan create` command, add the following flag `--sca-resolver ./ScaResolver`.

   {% hint style="info" %}
   If you are using a plugin, then this flag is added in the **Additional parameters** section of the scan configuration.
   {% endhint %}

### Customizing Resolver Configuration

You can add additional arguments to the run command in order to customize the package resolution process. For a complete list of SCA Resolver configuration arguments, see Checkmarx SCA Resolver Configuration Arguments.

{% hint style="info" %}
Only arguments that can be used in **Offline** mode can be applied to scans run via the Checkmarx One CLI Tool and plugins.
{% endhint %}

**To customize the Resolver Configuration:**

1. Add the `--sca-resolver-params` flag to the `scan create` command followed by the additional arguments that you would like to add (surrounded by "").

**For Example:**

```
--sca-resolver ./ScaResolver --sca-resolver-params "--extract-archives zip,ear --extract-depth 3 --gradle-exclude-scopes api,testCompile"
```

{% hint style="warning" %}
Whenever a parameter value has a space or other special character in it, it needs to be escaped either by enclosing it in quotes or using an escape character. The specific syntax for escaping characters will vary depending on the command-line interface or programming language you are using.
{% endhint %}

### Integration Examples

#### Github Action

The following example shows how to create a GitHub Action for running a Checkmarx One scan with SCA Resolver.

```
# Documentation:
# https://checkmarx.atlassian.net/wiki/spaces/Checkmarx One/pages/6147408761/CI+CD+with+CxSCA+Resolver
#

name: SCA Resolver Example

on:
  push:
    branches:
      [main]
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v2

      - name: Download SCA Resolver
        run: |
          wget https://sca-downloads.s3.amazonaws.com/cli/latest/ScaResolver-linux64.tar.gz
          tar -xzvf ScaResolver-linux64.tar.gz
          rm -rf ScaResolver-linux64.tar.gz

      - name: Install Maven, NPM, ... # Add any necessary package management
        run: |
          sudo apt install maven npm

      - name: Run Checkmarx One CLI Scan
        run: |
          /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
          /home/linuxbrew/.linuxbrew/bin/brew install checkmarx/ast-cli/ast-cli
          /home/linuxbrew/.linuxbrew/Cellar/ast-cli/*/bin/cx \
            scan create \
            -s . \
            --agent GitHub \
            --project-name ${{ github.repository }} \
            --branch ${GITHUB_REF##*/} \
            --base-uri ${{ secrets.CX_BASE_URI }} \
            --tenant ${{ secrets.CX_TENANT }} \
            --client-id ${{ secrets.CX_CLIENT_ID }} \
            --client-secret ${{ secrets.CX_CLIENT_SECRET }} \
            --sca-resolver ./ScaResolver
```

{% hint style="info" %}
Check for updates to the code samples in [GitHub](https://github.com/CheckmarxDev/ast-cicd-templates/tree/master/CxScaResolver/github-action.yml).
{% endhint %}

#### Bitbucket Pipelines

The following example shows how to run a Checkmarx One scan with SCA Resolver in a Bitbucket pipeline.

```
image: checkmarx/ast-cli

pipelines:
  default:
    - step:
        script:
          - wget https://sca-downloads.s3.amazonaws.com/cli/latest/ScaResolver-linux64.tar.gz
          - tar -xzvf ScaResolver-linux64.tar.gz
          - rm -rf ScaResolver-linux64.tar.gz
          - >-
            /app/bin/cx
            scan create
            -s .
            --agent Bitbucket
            --project-name $BITBUCKET_REPO_SLUG
            --branch $BITBUCKET_BRANCH
            --base-uri $BASE_URI
            --tenant $TENANT
            --client-id $CLIENT_ID
            --client-secret $CLIENT_SECRET
            --sca-resolver ./ScaResolver
            $ADDITIONAL_PARAMS
```

{% hint style="info" %}
Check for updates to the code samples in [GitHub](https://github.com/CheckmarxDev/ast-cicd-templates/blob/main/CxScaResolver/bitbucket-pipelines.yml).
{% endhint %}
