# SAST to CxOne Export CLI Tool

Exporting the current SAST environment is performed by using a dedicated CLI tool.

{% hint style="warning" %}
The cxsast_exporter tool must have an internet connection.

For SAST on-prem instances, there is an option to avoid internet connection using the **--query-mapping** command. If there is no internet connection, users must download the latest version of mapping.json file & configure it accordingly.

Download mapping.json URL - https://raw.githubusercontent.com/Checkmarx/sast-to-ast-export/master/data/mapping.json
{% endhint %}

## Installation

1. Download the tool from the following link: [SAST CLI Exporter Tool](https://github.com/Checkmarx/sast-to-ast-export/releases/latest)
2. Place the tool in any location on the client that you are using.
3. Type **cxsast_exporter.exe** **→ Enter** and all the CLI tool commands will be prompt.

```
C:\Users>cxsast_exporter.exe
Error: required flag(s) "pass", "url", "user" not set
Usage:
  cxsast_exporter [flags]
  cxsast_exporter [command]

Available Commands:
  completion generate the autocompletion script for the specified shell
  help Help about any command
  version Print the version number of cxsast_exporter

Flags:
      --debug activate debug mode
      --export strings SAST export options (default [users,teams,triage,projects,queries,presets])
  -h, --help help for cxsast_exporter
      --nested-teams include original team structure without flattening
      --pass string SAST password
      --project-id string project ID filter
      --project-team string team name filter
      --projects-active-since int include only triaged results from projects active in the last N days (default 180)
      --query-mapping string path to file query mapping IDs from AST for triage (default "https://raw.githubusercontent.com/Checkmarx/sast-to-ast-export/master/data/mapping.json")
      --url string SAST url
      --user string SAST username
  -v, --verbose enable verbose logging to console

Use "cxsast_exporter [command] --help" for more information about a command.

Error: required flag(s) "pass", "url", "user" not set
```

## In this section

- [Using the SAST to CxOne Export CLI Tool](using-the-sast-to-cxone-export-cli-tool/README.md)
