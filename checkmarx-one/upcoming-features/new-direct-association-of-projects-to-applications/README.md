# New Direct Association of Projects to Applications

In order to make the association of Projects to Applications more transparent and easier to manage, we are changing the method by which the association is made. The new functionality will be that Projects are associated explicitly to Applications by selecting the specific Projects that you want to associate with that Application. This can be done via the web application or (REST) APIs.

## Required Permissions

We are introducing a new permission on the project level to allow assigning the project to applications: ***assign-to-application***.

This permission is automatically added to the **manage-application** role.

- **Associating Projects to Applications via API**:

  - API Endpoint: POST /api/applications/{id}/projects
  - Permissions:

    - `update-application` on the application level
    - projects with `assign-to-application`
- **Associating Applications to Projects via API**:

  - API Endpoint: POST /api/projects/{id}/applications
  - Permissions:

    - `update-project` on the project level
    - applications with `update-application`
- **Creating an Application and Adding a Project**:

  - Permissions:

    - `create-application` at global level
    - projects with `assign-to-application`
- **Updating an Application and Adding a Project**:

  - Permissions:

    - `update-application` at application level
    - projects with `assign-to-application`
- **Creating a Project and Adding an Application**:

  - Permissions:

    - applications with `create-project` permission.
- **Updating a Project and Adding an Application**:

  - Permissions:

    - applications with `update-project`

## In this section

- [New Association of Projects to Applications via the Web Application](new-association-of-projects-to-applications-via-the-web-application.md)
- [New Association of Projects to Applications - API Compatibility](new-association-of-projects-to-applications---api-compatibility.md)
