# Settings for Specific Scanners

Each Checkmarx One scanner has its own unique set of configurable parameters.

{% hint style="info" %}
Only scanners included in your license will appear in the Settings UI.
{% endhint %}

By default, Allow Override is enabled for all parameters, which means the same parameter can be overridden at a lower configuration level. Uncheck it to enforce a value tenant-wide. For more information see [Configuring Project Rules](../../managing-projects/configuring-projects.md#project-rules).

Use the <img src="../../../../assets/Trash.png" alt="" data-size="line">icon to reset a configuration field.

## Configuration Hierarchy

Scanner parameters use a two-phase hierarchy that works differently depending on whether you are configuring or running a scan:

- **When configuring**: Tenant is the top of the hierarchy. Parameters flow downward: Tenant > Project > Config as Code > Scan. Lower levels inherit from higher ones.
- **When running a scan**: The order reverses. The most specific (lowest-level) setting wins: Scan > Config as Code > Project > Tenant.

This means a parameter set at the Tenant level is the default, but a developer can override it at scan time if **Allow Override** is enabled.

Parameters are inherited from one level to the other, starting from Tenant level.

Removing parameters from a lower configuration level can be performed *only* by deleting the parameter configuration from the higher configuration level. In this case the parameter won't be presented in the lower configuration level.

In case users edit a parameter in a lower configuration level, a <img src="../../../../assets/Trash.png" alt="" data-size="line">icon will appear at the right. Deleting the parameter can't be performed, as the parameter is inherited from the higher configuration level. This behavior is designed to emphasize that the configuration exist at the Tenant level and it is set with "X" value.

In case using the icon, it might appear that the parameter is deleted, but it is not. In case exiting the page and returning, the parameter will be presented again.

## Filtering Options

Some scanner parameters, such as file and folder exclusions for SAST and IaC Security, use Glob syntax to define which paths to include or exclude from scanning.

For instance:

- **Exclude all java files:** !\*\*/\*.java
- **Exclude all files inside a folder Test:** !\*\*/Test/\*\*
- **Exclude all files under root folder Test:** !Test/\*\*
- **Exclude just the files inside a folder leaving all subfolders content:** !\*\*/Test/\*
- **Exclude all JavaScript minified files:** !\*\*/\*.min.js

{% hint style="info" %}
The rules follow the same logic at **tenant** and **project** level.
{% endhint %}

For more information see [Glob Tool](https://www.digitalocean.com/community/tools/glob).
