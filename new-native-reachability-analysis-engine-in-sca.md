# New Native Reachability Analysis Engine in SCA

## Planned General Availability: September 20, 2026

Checkmarx One SCA is introducing a native reachability engine for Package Usage and Exploitable Path analysis. Previously, this analysis depended on a separate SAST scan; the new engine runs the analysis directly within the SCA scan itself, removing the SAST-specific prerequisites, connectivity requirements, and scan-method restrictions that applied before.

No additional configuration is required, and results continue to appear in the same views used today.

{% hint style="warning" %}
**Scope note**: This change applies to Checkmarx One SCA only. SCA Standalone is not affected.
{% endhint %}

<a id="UUID-673b7fd4-f24d-841f-87c5-1984d9921c2e_section-id235774025466638"></a>
## What's Changing?

| Previous Behavior | New Behavior |
| --- | --- |
| Exploitable Path relied on a separate SAST scan | Reachability analysis runs natively as part of the SCA scan. |
| SAST-specific prerequisites, connectivity requirements, and scan-method restrictions applied | None of these restrictions apply |
| A separate SAST scan was required to get full open source usage and exploitability insights | Reachability analysis runs independently of the SAST engine.No separate SAST scan is required |

<a id="UUID-673b7fd4-f24d-841f-87c5-1984d9921c2e_section-id235774037157105"></a>
## How Exploitable Path Analysis Works

The reachability engine analyzes the application's source code to determine whether an open source package is used and whether the application code can reach a known vulnerable method within the package.

Package Usage and Exploitable Path are two distinct signals, evaluated independently. Package Usage tells you whether — and how — a package is called by your code. Exploitable Path tells you whether a code path reaches the specific vulnerable method inside that package. A package can be in active use while its Exploitable Path status shows no reachable vulnerability, if your code calls the package but never touches the vulnerable method.

When an exploitable path is found, results show the specific lines of code that reach the vulnerable method and the full path to the vulnerability — helping you prioritize fixes for vulnerabilities that are actually reachable over those that aren't.

<a id="UUID-673b7fd4-f24d-841f-87c5-1984d9921c2e_section-id23577403829018"></a>
## Feature Scope

The new reachability engine supports:

- **Languages**: Python, Java, JavaScript, and C#.
- **Dependency scope**: Direct dependencies only (packages called directly by the application)
- **Vulnerability scope**: Vulnerabilities where the vulnerable method is contained in the directly called package.
- **New package coverage**: Packages not yet in Checkmarx's analyzed database are queued automatically and are typically analyzed within 48 hours; from then on, they're included in every future scan.

<a id="UUID-673b7fd4-f24d-841f-87c5-1984d9921c2e_section-id235774068229454"></a>
## Enabling the Engine

Exploitable Path runs only on Projects where it's been activated — during Project creation, via Project Settings, or as an account-wide default for new Projects. Activating it as an account default does not retroactively enable it for Projects created earlier; those need to be activated individually.

<a id="UUID-673b7fd4-f24d-841f-87c5-1984d9921c2e_section-id235774039971889"></a>
## Key Benefits

- Runs as part of the regular SCA scan — no separate SAST scan needed
- No SAST prerequisites, connectivity requirements, or scan-method restrictions
- No additional configuration required
- Faster time to reachability results
- Lower operational overhead for maintaining exploitability insights
