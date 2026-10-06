# Managing Checkmarx One Traffic and AWS S3 Access

Checkmarx One supports integration with **on-prem** external tools and vendors. The supported tools include the following:

- **Code repositories** - [GitLab Self-Hosted](code-repository-integrations/gitlab-custom-setup.md), [GitHub Custom Setup](code-repository-integrations/github-custom-setup.md), [Bitbucket Custom Setup](code-repository-integrations/bitbucket-custom-setup.md), [Azure DevOps Custom Setup](code-repository-integrations/azure-devops-custom-setup.md)
- **Bug tracking tools** - [Jira](feedback-apps/jira.md)

If your organization generally restricts inbound and outbound traffic, and you want to allow it for Checkmarx One, you'll need to add the IP addresses for Checkmarx One outgoing and incoming traffic to your firewall allowlist to successfully integrate with the tools mentioned above.

- The IP addresses for Checkmarx One's outgoing traffic are listed by region in [Whitelisting IPs for Checkmarx One's outgoing traffic](#whitelisting-ips-for-checkmarx-ones-outgoing-traffic).
- The IP addresses for incoming traffic are dynamic. To manage these, we recommend implementing domain-based rules using application control and URL filtering, as described in [Implementing domain-based rules for Checkmarx One's incoming traffic](#implementing-domain-based-rules-for-checkmarx-ones-incoming-traffic).

To submit the necessary CLI commands for plugins, make sure to open access to AWS S3 endpoints if it is closed by default. Proceed as explained in Whitelisting IPs for Checkmarx One's outgoing traffic.

## Whitelisting IPs for Checkmarx One's outgoing traffic

The table below lists the relevant IP addresses per region.

{% hint style="info" %}
- For regions with multiple IP addresses, you need to add all the IPs.
- The IPs listed below apply to **Multi-Tenant** instances only.
- IPs for **Single Tenant** environments are specific for each Single Tenant setup.
{% endhint %}

| **Region** | **Outgoing traffic from Checkmarx** |
|---|---|
| EU (Europe) | • 52.51.139.20<br>• 52.208.211.217<br>• 54.228.84.29 |
| EU2 (Europe) | • 52.19.157.193<br>• 52.209.58.235<br>• 34.246.96.218 |
| [NA (North America)](http://ast.checkmarx.net) | • 35.172.44.54<br>• 35.175.89.213<br>• 44.209.47.135 |
| [US2](http://us.ast.checkmarx.net) | • 44.214.196.71<br>• 34.233.5.145<br>• 54.172.199.251 |
| IND (India) | • 43.205.65.230<br>• 3.7.6.185<br>• 3.6.109.180 |
| IND-2 (India) | • 3.109.189.62<br>• 13.235.249.74<br>• 65.0.141.73 |
| ANZ (Australia + New Zealand) | • 13.238.53.214<br>• 52.63.214.86<br>• 54.206.177.198 |
| SGP (Singapore) | • 54.251.227.202<br>• 54.251.231.165<br>• 52.76.18.234 |
| MEA (Middle East and Africa) | • 3.29.115.241<br>• 3.28.112.177<br>• 51.112.34.132 |
| Nimbus (TLV) | • 51.16.229.255<br>• 51.84.21.34<br>• 51.17.218.121 |
| CANARY-DEU | • 3.120.214.171<br>• 3.126.230.210<br>• 3.74.225.192 |

## Implementing domain-based rules for Checkmarx One's incoming traffic

IP addresses are dynamic and may change periodically. To avoid frequent updates to IP-based rules and ensure consistent access even when IPs change, implement domain-based rules using application control and URL filtering.

To do it, proceed as follows:

1. Open your network security management console.
2. Navigate to the section where security policies are defined.
3. Use the Application & URL Filtering feature to create a new application or site object.
4. Specify `*.checkmarx.net` as the **F**ully **Q**ualified **D**omain **N**ame (FQDN) .
5. Add a new rule to your security policy that allows traffic to the created application/site object.
6. Set the action to **Accept** or the appropriate permission level, and place the rule in the correct section of your firewall rules.
7. Ensure that your firewall or network device has DNS resolution enabled to dynamically resolve FQDNs to IP addresses.
8. Test the connectivity to confirm that traffic is being allowed correctly based on the FQDN.

## Providing access to AWS S3 endpoints

To submit the necessary CLI commands for plugins, ensure that access to AWS S3 endpoints is opened as described here: [https://docs.aws.amazon.com/general/latest/gr/s3.html](https://docs.aws.amazon.com/general/latest/gr/s3.html).

For instance, in the US-East region, the following endpoint should be added to your allowlist: `s3.dualstack.us-east-1.amazonaws.com`.
