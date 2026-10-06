# Using the SAST to CxOne Export CLI Tool

The `cxsast_exporter` command provides the ability to perform the following actions:

- **Export an existing SAST v9.3 (and up) environment**.
- **Generate** **autocompletion** script for the specified shell.
- **Print** the **version number** of cxsast_exporter tool.
- Provide a **help menu** for the command,

## Usage

```
cxsast_exporter [flags]
cxsast_exporter [command]
```

## Flags

The SAST Exporter CLI Tool supports the following flags:

| **Name** | **Default** | **Description** | **Version** |
|---|---|---|---|
| --debug | | Activates debug mode | V1.2.0 |
| --export \<strings> | users, teams, triage, projects, queries, presets | SAST export options:<br>• users<br>• teams<br>• projects - export project including presetid<br>• queries - export only custom queries<br>• presets - export only custom presets<br>{% hint style="info" %}<br>- Scans can't be exported.<br>- Scan results that are **triaged** can be exported.<br><br> For more information about triaging results in Checkmarx SAST, see the table in SAST [Results Tab](https://checkmarx.com/resource/documents/en/34965-152263-navigating-scan-results.html#UUID-63dc4af2-ead5-0713-8c94-1487ef87b8bc_id_NavigatingScanResults-Results) section.<br>{% endhint %} | V1.2.0 |
| --help, -h | | help for cxsast_exporter | V1.2.0 |
| --nested-teams | | include original team structure without flattening | V1.2.0 |
| --pass \<string> | | SAST password | V1.2.0 |
| --project-id \<string> | | Filter according to project ID | V1.2.0 |
| --project-team \<string> | | Filter according to team name | V1.2.0 |
| --projects-active-since \<int> | 180 | Include only results from projects active in the last N days | V1.2.0 |
| --query-mapping \<string> | https://raw.githubusercontent.com/Checkmarx/sast-to-ast-export/master/data/mapping.json | Path to file query mapping IDs from Checkmarx One for triage<br>For additional information see the note at the beginning of the [SAST to CxOne Export CLI Tool](../README.md) topic. | V1.2.0 |
| --query-renaming \<string> | https://raw.githubusercontent.com/Checkmarx/sast-to-ast-export/refs/heads/master/data/renames.json | path to file query renaming IDs from AST for overrides | |
| --simIDVersion \<int> | 0 - standard | Specify the version of SimilarityID to use.<br>• 0 - Standard<br>• 1 - Ignore leading spaces<br>• 2 - Ignore all spaces | V1.6.0 |
| --url \<string> | | SAST URL | V1.2.0 |
| --user \<string> | | SAST username | V1.2.0 |
| --verbose, -v<br>{% hint style="warning" %}<br>For debugging, place this argument before others so that if the command fails at any other argument, **Verbose** mode remains active.<br>{% endhint %} | | To enable logs for external libraries, configure the appropriate logger levels in the external **log4j2.xml** file. The updated log levels are applied at runtime.<br>{% hint style="info" %}<br>Optional: Turn on **Verbose** mode. All messages and events are sent to the console or log file when turned on.<br>{% endhint %} | V1.2.0 |

## Export Examples

### Exporting all Files & Options

To export all the possible options, run the cxsast_exporter command without flags:

```
C:\User>cxsast_exporter --user <SAST user> --pass <SAST Password> --url <SAST URL>
```

### Exporting Users & Teams

To export several options, run the cxsast_exporter command with the relevant parameters:

```
C:\User>cxsast_exporter --user <SAST user> --pass <SAST Password> --url <SAST URL> --export users,teams
```

{% hint style="info" %}
Any combination is valid for the SAST export.

For more information see [V1.2.0 SAST Export Matrix](../../cli-tool-releases/v120-sast-export-matrix.md)
{% endhint %}

### Exporting Users, Teams & Results Including Results from Projects Active more then the Default (180 days)

```
C:\User>cxsast_exporter --user <SAST user> --pass <SAST Password> --url <SAST URL> --projects-active-since 360
```

## In this section

- [Available Commands](available-commands.md)
