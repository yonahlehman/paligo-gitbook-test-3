# Checkmarx One Calculation of Severity Level

Checkmarx One assigns a **Severity level** for each vulnerability discovered by any of the Checkmarx One scanners: **SAST**, **SCA**, **API Security**, **IaC Security**, and **Container Security**.

The severity level is helpful for prioritizing remediation of the most severe risks in your code. An initial severity level is assigned by Checkmarx One for each vulnerability, based on our expertise in assessing potential threats. Users, then have the ability to manually adjust the severity level of specific vulnerabilities based on their own assessment of the risk posed by the vulnerability, see Managing (Triaging) Vulnerabilities.

In addition, Checkmarx One assigns an overall Project and Application **Risk level** to each Project and Application based on the number of vulnerabilities discovered in the code and their severity. The risk level indicates the overall risk of the software being compromised by malicious attacks.

## Severity Level

The possible Severity Levels in Checkmarx One are:

- Critical
- High
- Medium
- Low
- Info

### Severity Levels for SCA and Container Security

For vulnerabilities identified by the SCA and Container Security scanners, the Severity Level is designated based on the NVD CVSS (Common Vulnerability Scoring System) for that vulnerability. We use the latest available scoring system for each vulnerability. When a CVSS v4.0 score is available, we use that. When no CVSS 4.0 score is available, we continue to use the most recent available score from previous scoring systems (3.1 or 2.0).

{% hint style="info" %}
Support for v4.0 is in the process of being rolled out in production environments for results identified by the SCA scanner. For Container Security, 3.1 remains the most recent supported version.
{% endhint %}

The score is mapped to Severity Level as follows:

- Critical - 9.0 to 10.0
- High - 7.0 to 8.9
- Medium - 4.0 to 6.9
- Low - 0.1 to 3.9
- Info - 0.0

#### CxScore

Checkmarx One provides an additional metric, CxScore, for each SCA vulnerability alongside the Risk Score. CxScore is a composite metric that reflects both vulnerability severity and likelihood of exploitation. It incorporates the EPSS score along with key exploitability indicators, including Exploitable Path, Known Exploited Vulnerabilities (KEV), and Proof of Concept (PoC) availability.

CxScore is assigned to vulnerabilities displayed in the Risks tab and is also shown for packages in the Packages tab. The Package CxScore reflects the highest CxScore among all vulnerabilities associated with that package.

For the complete documentation on CxScore, see [CxScore: Risk Prioritization for SCA Vulnerabilities](cxscore-risk-prioritization-for-sca-vulnerabilities.md)

### Severity Levels for SAST, IaC Security and API Security

For vulnerabilities identified by the SAST, IaC Security and API Security scanners, the Severity Level is designated by the Checkmarx One AppSec research team based on their evaluation of the risk posed by the vulnerarbility.

Checkmarx one does **not** show the NVD CVSS Score and the Severity Level is **not** directly related to the NVD designation, rather it is assigned by the Checkmarx One AppSec research team. The reason for this is that these scanners are static analysis tools for identifying weaknesses in code that cause vulnerabilities, while CVSS is a dynamic scoring system for known and tested vulnerabilities. Therefore, our AppSec research team takes into consideration the context and scope of the source code as well as a range of dynamic factors when determining the severity level for each vulnerability.

- Critical - Severe vulnerabilities that demand immediate attention due to their high risk to the security and functionality of the software. The exploitation of these vulnerabilities can result in devastating consequences, including complete system compromise, unauthorized access, or significant data breaches. They have the potential to completely compromise the confidentiality, integrity, and availability of the system, making them a top priority for remediation. These vulnerabilities often require urgent mitigation measures to prevent severe impact on the software and its users. Failure to address them promptly can lead to severe security breaches and substantial damage to the organization and its stakeholders.

  **Examples:** Remote code execution, command injection, SQL injection
- High - Vulnerabilities that pose a significant risk and require prompt attention due to their potential to cause serious security issues if exploited. Although they may not reach the same level of impact as critical vulnerabilities, high-severity issues enable malicious attackers to gain unauthorized access to application resources and sensitive data, thereby facilitating the theft of session information or valuable data from both the application and server. The key distinction between high and critical vulnerabilities lies in the potential consequences and severity of their impact, whereas a high-severity vulnerability does not cover the execution of code or a command on the application or server. On top of this, significant compromise and exploitability require factors beyond an attacker’s control such as an active privileged user being targeted and successfully exploited.Addressing high vulnerabilities on time is crucial to mitigate potential risks and protect the software.

  **Examples:** Cross-site scripting (XSS), XML external entity (XXE) injection, and cleartext submission of sensitive information
- Medium - Vulnerabilities that highlight potential security weaknesses such as misconfigurations that may result in limited unauthorized access or data exposure, which can have an adverse effect on the confidentiality, integrity, or availability of the system, although to a lesser extent. While the impact of these vulnerabilities is typically less severe compared to critical or high vulnerabilities, they still require attention to maintain the overall security posture of the software.

  **Examples:** Cross-site request forgery (CSRF), open redirections, ReDoS, and information exposure of some kinds (privacy violation, PCI exposure)
- Low - Vulnerabilities that are generally considered less pressing and have a minimal impact on the immediate security of the software. These vulnerabilities often involve specific coding weaknesses or potential areas for improvement rather than posing an immediate threat to the CIA triad. While low severity vulnerabilities may not directly compromise in a significant way the confidentiality, integrity, or availability of the system, addressing them is still important to maintain a robust security posture and minimize potential risks. By addressing low vulnerabilities, you can prevent their escalation into more significant security issues or potential routes for exploitation.

  Examples: Missing input validation (log forging), internal information exposure (logs, error messages), and misconfigurations
- Info - Lack of compliance with security best practices. The inadequacy of the security measures that are in place could possibly be exploited by a sophisticated attacker. This includes vulnerabilities that enable attackers to upload content to a website, access sensitive information, “clickjack” a website etc. To achieve the highest level of application security for critical apps, you may want to remediate these vulnerabilities after attending to all vulnerabilities of greater severity.

  **Examples:** X-XSS-Protection, Application Entry Point, and Debug Mode Enabled

## Project and Application Risk Level

The following is a description of the possible Project and Application **Risk levels** in Checkmarx One:

- Critical - The project/application contains one or more critical vulnerabilities that expose the code to imminent threat of being compromised by malicious attacks.
- High - The project/application contains one or more severe vulnerabilities that pose an imminent security risk.
- Medium - The project/application contains one or more moderately severe vulnerabilities that pose a security risk.
- Low - The project/application contains one or more security weaknesses that could possibly be exploited to compromise the code security.
- Info - The project/application contains one or more info level risks.

## In this section

- [Support for Critical Severity](support-for-critical-severity.md)
- [CxScore: Risk Prioritization for SCA Vulnerabilities](cxscore-risk-prioritization-for-sca-vulnerabilities.md)
