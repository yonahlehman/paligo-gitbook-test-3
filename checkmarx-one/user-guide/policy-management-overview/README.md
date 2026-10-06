# Policy Management Overview

## Overview

Policy Management is a mechanism for identifying security risks across projects and scans.

Organizations often handle hundreds or even thousands of projects that undergo daily scans, with each project generating distinct scan results. To pinpoint projects with specific types of results, security engineers must manually review and prioritize findings.

Organizations can easily detect projects that violate their established security rules by using policies. For example, an organization may want to understand whether specific projects contain high-severity findings from static code analysis or feature particular types of open-source packages, such as the recent log4j concerns.

Policy rules can be created for identifying risks across scanners. There are also specialized conditions that can be used to create policy rules for specific scanners. Currently, the scanners supported for Policy management are, SAST, SCA, IaC Security and Container Security.

Policy Management does not stop at identification alone; it enables organizations to develop automated responses for project violations, such as blocking a software build if it violates a policy. In addition, for scans initiated by a pull request, the PR decoration includes a summary of the Policy violations. For SAST policy violations, details are shown about the violated conditions and the vulnerabilities that caused the violations.

Once a scan is completed, the policies associated with the respective projects are assessed. These policies are then matched against the findings from the scan results.

Checkmarx One generates and maintains an incident report containing details of projects that violated policies during the scan.

## Permissions

To execute various actions in the Policy Management feature, a user needs to be assigned one of the following permissions:

- **create-policy-management** - Create policies.
- **delete-policy-management** - Delete policies.
- **manage-policy-management** - Update, delete, create and view policies.
- **update-policy-management** - Update policies.
- **view-policy-management** - View policies.

## In this section

- [Creating a Policy](creating-a-policy/README.md)
- [Viewing Policies and Incidents](viewing-policies-and-incidents.md)
