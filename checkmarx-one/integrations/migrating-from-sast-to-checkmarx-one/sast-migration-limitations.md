# SAST Migration Limitations

The below list presents the SAST to Checkmarx One migration limitations:

{% hint style="info" %}
The migration flow is **partially manual,** some data can be migrated using the export/import tool and some data and integrations will require manual work.
{% endhint %}

| **Limitation** | **Comments** |
|---|---|
| **General** | |
| **ast-admin** and **iam-admin** permissions are required to execute the export / import procedures | |
| CLI export tool is supported only on Windows | |
| It is possible to export an existing SAST v9.3 (and up) environment | |
| **Projects / Scans / Results** | |
| Scan results are not migrated | Only results with triage are migrated<br>Custom states are migrated and the associated permissions are created in Checkmarx One. Migrated triage maintains custom states applied to specific vulnerabilities. The following limitations apply:<br>• Max. 200 characters, extra characters are truncated<br>• In case of duplicates (i.e., a custom state with that name already exists in Checkmarx One) a random string is added to the migrated custom state<br>• If migration fails for a custom state, triaged results revert to To Verify state |
| Results older then the configurable amount of days parameter to migrate won’t be migrated | If no value is used for the parameter, the default value is 180 days |
| Only one branch will be exported | |
| Sources won’t be migrated | |
| The ability to review findings in Code Viewer will be available *only* after the first real full scan via Checkmarx One | |
| First scan results in Checkmarx One might be different than the latest scan in SAST due to difference in SAST scanner version | |
| **Users / Groups / Roles and permissions** | |
| Groups from SAST are not migrated to Checkmarx One | • In this phase, groups from SAST are intentionally not migrated. As a result, the migration log shows `Skip groups importing` and `0 groups migrated` - this is expected behavior, not an error.<br>• In Checkmarx One, access is managed through direct user assignments at the tenant, application, or project level rather than through groups.<br>• If your SAST setup relies on a team or group hierarchy, you should plan to recreate this structure in Checkmarx One by organizing applications and projects accordingly, and assigning users directly to them. |
