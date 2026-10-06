# API Security

The growth in microservices and cloud-native applications is driving a broader industry migration to API-based architectures, while traditional tools often provide insufficient or no protection to APIs. This leaves applications partially or completely unprotected while the rate of application changes increases.

Each application includes hundreds or thousands of APIs, which causes the AppSec teams to lack visibility of the entire footprint of the fast-changing API inventory.

To address this issue, Checkmarx introduces API Security integrated with Checkmarx One. It lists the entire API inventory, exposes Shadow APIs and Zombie APIs, and identifies existing vulnerabilities and risks related to them with one single application. This eliminates the need for multiple API-specific tools and reduces the overhead on AppSec teams.

API Security capabilities and advantages are listed below:

- **Automatic API discovery**: Identifies API endpoints without requiring manual API definition or registration by AppSec teams or developers.
- **Complete API inventory**: Discovers newly created or updated APIs as developers check in or compile the source code as early as possible in the software development cycle.
- **Unknown API identification**: Compares the full API inventory of an application with its API documentation to identify unknown, Shadow, and Zombie APIs.
- **Prioritized remediation**: Helps developers and AppSec teams to solve the most critical issues by prioritizing API vulnerabilities based on their real impact and risks.
- **Whole application coverage**: Provides a single AST solution for the entire application, which may have API- and non-API-based components, for a holistic view of security risk and prioritization for vulnerability remediation.
- **True shift-left approach**: Discovers APIs in application source code to identify and fix problems early in the software development cycle.

{% hint style="info" %}
**API Security** supports **Python- Flask and Django, Java - Spring, Node.JS - Express** , and **C# - ASP.NET Web API** .
{% endhint %}

## In this section

- [Running a Scan](running-a-scan.md)
- [API Security Language and Framework Support](api-security-language-and-framework-support.md)
- [API Security Scanner](api-security-scanner.md)
- [Viewing the Scanners Tab (API Security)](viewing-the-scanners-tab-api-security.md)
- [API Inventory](api-inventory.md)
