# SAST vs. Checkmarx One Role Mapping

The table below presents the SAST vs. Checkmarx One Role Mapping:

| **SAST Role** | **SAST Description** | **Checkmarx One Role** |
|---|---|---|
| Access Control Manager | Manage users, authentication and system settings | iam-admin |
| Admin | Checkmarx products global administrator | ast-admin + iam-admin |
| SAST Admin | Grants full permissions | ast-admin |
| SAST Auditor | Grants permissions to manage vulnerability queries and use CxAudit | ast-risk-manager |
| SAST Data Cleaner | Grants permissions to delete projects and scans | manage-project |
| SAST Results Updater | Grants permissions to update the properties of scan results | ast-scanner |
| SAST Results Verifier | Grants permission to set the state of scan results to "Not Exploitable" | ast-scanner |
| SAST Reviewer | Grants "read only" permissions to view scan results and generate reports | ast-viewer |
| SAST Scanner | Grants permissions to create, manage projects, and run scans | ast-scanner, manage-application |
| User Manager | Manage the users in the system | Iam-admin |
