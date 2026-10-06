# Monitor New Repositories

**Monitor New Repositories** feature provides automation capabilities for Checkmarx One projects creation.

## Enabling the Feature

This feature is controlled by the **Automatically sync new projects created for this organization** toggle, shown when selecting the organization during the import process.

- If this is the first repository imported from the organization, you can enable or disable this toggle at this point.
- If the organization has already been connected, the toggle reflects its existing organization-level configuration, and may not be editable here.

Once enabled, Checkmarx One starts listening to the **repository creation** events inside your code repository platform.

To learn how to view or change this setting after import, see [Code Repository Settings](../../user-guide/configuring-account-settings/global-account-settings/code-repository-settings.md).

## How it Works

A project in Checkmarx One will be created for:

- Every new repository that is created in the monitored organization.
- Every existing repository that is transferred from a different organization to the monitored organization.

The new project follows the naming convention `<organization>/<repository>`.

After the project is created, its scan triggers and scan types settings are inherited from the parent organization's configuration - see [Code Repository Settings](../../user-guide/configuring-account-settings/global-account-settings/code-repository-settings.md) for details.

## Limitations

- The feature is supported for GitHub Cloud, [GitHub Custom Setup](github-custom-setup.md), [Azure DevOps Cloud](azure-managed-setup.md) and [Azure DevOps Self-hosted](azure-devops-custom-setup.md).
- The feature is *not* supported for the **User** organization. This is because it is not possible to create a new webhook under the User organization (although it is possible to create a new repository).
- Only users with **Admin** permissions for the organization can create new repositories under the organization. In case the user has a different permission level, an error message will be presented when selecting the organization.
- The feature doesn't support the repository **Update** or **Delete** events. This means that in case the repository was deleted, the project won't be deleted in Checkmarx One, and the user will need to manually delete it.
