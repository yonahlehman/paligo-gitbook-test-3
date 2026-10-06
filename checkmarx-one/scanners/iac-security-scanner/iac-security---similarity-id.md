# IaC Security - Similarity ID

The Similarity ID uniquely identifies each IaC Security finding so you can see whether a result is **New** (first detected), **Recurring** (previously detected in an earlier scan of the same project), or **Fixed** (only found in the first scan) across scans. When the ID stays consistent, your triage choices - like marking a result as **Not Exploitable** or **Confirmed** - carry over automatically without needing to review them again.

## How the Similarity ID is Determined

| Parameter | Description |
|---|---|
| Project path | The root path(s) of the scanned project |
| File path | The relative path of the file containing the finding |
| Query ID | A hash uniquely identifying the IaC Security query (rule) that detected the finding |
| Search key | The key field from the query result metadata (e.g., the resource attribute or block identifier targeted by the rule) |
| Search value | The value field from the query result metadata |

As long as the same rule fires on the same attribute in the same file, the Similarity ID remains identical - regardless of surrounding code changes or line number shifts.

If the Similarity ID matches a result from a previous scan, you will see it classified as **Recurrent** and its existing triage state is kept. If there is no match, the result is classified as **New**. This ensures that any finding you previously triaged, such as marking it **Not Exploitable**, keeps that state in future scans as long as the finding has not changed in the scanned file.
