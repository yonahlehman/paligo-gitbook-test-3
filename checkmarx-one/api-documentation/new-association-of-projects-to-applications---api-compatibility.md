# New Association of Projects to Applications - API Compatibility

{% hint style="warning" %}
This page describes upcoming changes that will affect how Projects are associated with Applications. These changes haven’t yet been implemented in production environments. However, we recommend preparing in advance to be ready when the changes occur.
{% endhint %}

This page describes the changes to the Checkmarx One REST APIs related to assignment of Projects to Applications.

Previously assignment of Projects to Applications was done based a system of “Rules”. Each Application had a series of rules that defined what characteristics a Project needed to have in order to be assigned to that Application (e.g., any Project with the tag Demo is included in the Application “DemoApp”).

The new functionality will be that Projects are assigned directly to Applications by specifying the Project ID of each Project that you want to assign. It will now be possible to assign Projects to Applications as part of the process of creating Applications, creating Projects, or as a separate action.

## Old Workflow

{% hint style="info" %}
In the old workflow the order of these two steps was irrelevant.
{% endhint %}

- Use `POST /applications` to create an Application and define rules for assigning Projects to that Application.
- Use `POST /projects` to create a Project with charechteristics that fit the rules of an Application.

  The Project is automatically assigned to that Application.

## New Workflow

1. Use `POST /applications` to create an Application.
2. Use `POST /projects` to create a Project, specifying the Application IDs of the Applications to which it is assigned.

OR

1. Use `POST /projects` to create a Project.
2. Use `POST /applications` to create an Application, specifying the Project IDs of each of the Projects that you would like to assign to it.

In addition, you can add existing Projects to existing Applications. To **add** to the existing assignments, use the new endpoints

`POST /applications/{application_id}/projects` OR

`POST /projects/{project_id}/applications`.

To **replace** the existing assignments, use the existing endpoints

`PUT /api/applications/{application_id}` OR

`PUT /api/projects{project_id}`.

### New Workflow for Assigning Projects According to Tags

It is still possible to assign Projects to Applications based on the Project tags, using the following workflow.

1. Create Projects and assign tags using `POST /projects`.
2. Obtain a list of Projects that have a specific tag using `GET /projects`, with a query parameter filtering for the specific tag.
3. Create an Application using `POST /applications`, specifying the list of Project IDs that you want to asssign to the Application.

## New Endpoints

- /api/applications

  - POST /{application_id}/projects - add Projects to an application
  - DELETE /{application_id}/Projects - remove projects from an application
- /api/projects

  - POST /{project_id}/applications - add applications to a Project
  - DELETE /{project_id}/applications - remove applications from a Project

| **Method** | **URL** | **Request** | **Success Response** | **Description** |
|---|---|---|---|---|
| POST | /api/applications/{application_id}/projects | Path parameter: application_id<br>Body:<br>`{`<br>`"projectIds": [`<br>` "string"`<br>` ],`<br>`}` | `{`<br>`"projectIds": [`<br>` "string"`<br>` ],`<br>`}` | Assign new projects to the Application specified in the path parameter. |
| DELETE | /api/applications/{application_id}/projects | Path parameter: application_id<br>Body:<br>`{`<br>`"projectIds": [`<br>` "string"`<br>` ],`<br>`}` | NO CONTENT | Remove projects from the Application specified in the path parameter. |
| POST | /api/projects/{project_id}/applications | Path parameter: project_id<br>Body:<br>`{`<br>`"applicationIds": [`<br>` "string"`<br>` ],`<br>`}` | `{`<br>`"applicationIds": [`<br>` "string"`<br>` ],`<br>`}` | Assign new Applications to the Project specified in the path parameter. |
| DELETE | /api/projects/{project_id}/applications | Path parameter: project_id<br>Body:<br>`{`<br>`"applicationIds": [`<br>` "string"`<br>` ],`<br>`}` | NO CONTENT | Remove Applications from the Project specified in the path parameter. |

### Deprecated Endpoints

All of the endpoints related specifically to "project rules" will be deprecated. This includes the following endpoints:

- POST /applications/{id}/project-rules
- GET /applications/{id}/project-rules
- GET /applications/{id}/project-rules/{rule-id}
- PUT /applications/{id}/project-rules/{rule-id}
- DELETE /applications/{id}/project-rules/{rule-id}
- POST /{id}/project-rules
- GET /{id}/project-rules
- GET /{id}/project-rules/{rule-id}
- PUT /{id}/project-rules/{rule-id}
- DELETE /{id}/project-rules/{rule-id}

### Changes to Existing APIs:

- /api/applications

  - POST - create application
  - GET - get applications
  - /{application_id} GET - get application by ID
  - /{application_id} PUT - update application
- /api/projects

  - POST - create project
  - GET - get projects
  - /{project_id} GET - get project by ID
  - /{project_id} PUT - update project

#### Changed Application APIs

| **Method** | **url** | **Old** | **New** | **Description** |
|---|---|---|---|---|
| POST | /api/applications | Request body:<br>`{`<br>` "name": "string",`<br>` "description": "string",`<br>` "criticality": 3,`<br>` "rules": [`<br>` {`<br>` "type": "project.tag.key-value.exists",`<br>` "value": "key;value"`<br>` }`<br>` ],`<br>` "tags": {`<br>` "test": "",`<br>` "priority": "high"`<br>` }`<br>`}` | Request body:<br>`{`<br>` "name": "string",`<br>` "description": "string",`<br>` "criticality": 3,`<br>` "projectIds": [`<br>` "string"`<br>` ],`<br>` "tags": {`<br>` "test": "",`<br>` "priority": "high"`<br>` }`<br>`}` | Create an Application. Used to have rules key, but now replaced with “projectIds”.<br>“ProjectIds” is not mandatory. You can create the Application and then assign Projects later. |
| GET | /api/applications | Success Response:<br>`{`<br>` "totalCount": 0,`<br>` "filteredTotalCount": 0,`<br>` "applications": [`<br>` {`<br>` "id": "string",`<br>` "name": "string",`<br>` "description": "string",`<br>` "criticality": 3,`<br>` "rules": [`<br>` {`<br>` "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",`<br>` "type": "project.tag.key-value.exists",`<br>` "value": "key;value"`<br>` }`<br>` ],`<br>` "projectIds": [`<br>` "string"`<br>` ],`<br>` "createdAt": "2024-06-25T09:38:40.149Z",`<br>` "updatedAt": "2024-06-25T09:38:40.149Z",`<br>` "tags": {`<br>` "test": "",`<br>` "priority": "high"`<br>` }`<br>` }`<br>` ]`<br>`}` | Success Response:<br>`{`<br>` "totalCount": 0,`<br>` "filteredTotalCount": 0,`<br>` "applications": [`<br>` {`<br>` "id": "string",`<br>` "name": "string",`<br>` "description": "string",`<br>` "criticality": 3,`<br>` "projectIds": [`<br>` "string"`<br>` ],`<br>` "createdAt": "2023-09-14T09:46:13.071Z",`<br>` "updatedAt": "2023-09-14T09:46:13.071Z",`<br>` "tags": {`<br>` "test": "",`<br>` "priority": "high"`<br>` }`<br>` }`<br>` ]`<br>`}` | Get list of Applications. Removed the rules key. |
| GET | /api/applications/{application_id} | Path parameter: application_id<br>Success Response:<br>`{`<br>` "id": "string",`<br>` "name": "string",`<br>` "description": "string",`<br>` "criticality": 3,`<br>` "rules": [`<br>` {`<br>` "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",`<br>` "type": "project.tag.key-value.exists",`<br>` "value": "key;value"`<br>` }`<br>` ],`<br>` "projectIds": [`<br>` "string"`<br>` ],`<br>` "createdAt": "2024-06-25T09:43:47.435Z",`<br>` "updatedAt": "2024-06-25T09:43:47.435Z",`<br>` "tags": {`<br>` "test": "",`<br>` "priority": "high"`<br>` }`<br>`}` | Path parameter: application_id<br>Success Response:<br>`{`<br>` "id": "string",`<br>` "name": "string",`<br>` "description": "string",`<br>` "criticality": 3,`<br>` "projectIds": [`<br>` "string"`<br>` ],`<br>` "createdAt": "2023-09-14T09:48:58.328Z",`<br>` "updatedAt": "2023-09-14T09:48:58.328Z",`<br>` "tags": {`<br>` "test": "",`<br>` "priority": "high"`<br>` }`<br>`}` | Get Application by Application ID. Removed the rules key. |
| PUT | /api/applications/{application_id} | Path parameter: application_id<br>Request body:<br>`{`<br>` "name": "string",`<br>` "description": "string",`<br>` "criticality": 3,`<br>` "rules": [`<br>` {`<br>` "type": "project.tag.key-value.exists",`<br>` "value": "key;value"`<br>` }`<br>` ],`<br>` "tags": {`<br>` "test": "",`<br>` "priority": "high"`<br>` }`<br>`}` | Path parameter: application_id<br>Request body:<br>`{`<br>` "name": "string",`<br>` "description": "string",`<br>` "criticality": 3,`<br>` "tags": {`<br>` "test": "",`<br>` "priority": "high"`<br>` },`<br>` "projectIds": [`<br>` "string"`<br>` ],`<br>`}` | Update an Application. Removed the rules key and added “projectIds” parameter.<br>If the “projectIds” parameter is not set, then the Project assignment is not changed.<br>If “projectIds” is set, then the previously assigned Projects are overwritten by the submitted Project IDs.<br>{% hint style="info" %}<br>If you would like to **add** to the existing assigned Projects, use the new API, `POST /applications/{application_id}/projects`.<br>{% endhint %} |

#### Changed Project APIs

| **Method** | **url** | **Old** | **New** | **Description** |
|---|---|---|---|---|
| POST | /api/projects | Request body:<br>`{`<br>` "name": "string",`<br>` "groups": [`<br>` "string"`<br>` ],`<br>` "repoUrl": "string",`<br>` "mainBranch": "string",`<br>` "origin": "string",`<br>` "tags": {`<br>` "test": "",`<br>` "priority": "high"`<br>` },`<br>` "criticality": 3`<br>`}` | Request body:<br>`{`<br>` "name": "string",`<br>` "groups": [`<br>` "string"`<br>` ],`<br>` "repoUrl": "string",`<br>` "mainBranch": "string",`<br>` "origin": "string",`<br>` "tags": {`<br>` "test": "",`<br>` "priority": "high"`<br>` },`<br>` "applicationIds": [`<br>` "string"`<br>` ],`<br>` "criticality": 3`<br>`}` | Create a Project. You can now specify Application IDs to assign the Project to Applications.<br>“applicationIds” is not mandatory. |
| GET | /api/projects | Success response:<br>`{`<br>` "totalCount": 0,`<br>` "filteredTotalCount": 0,`<br>` "projects": [`<br>` {`<br>` "id": "string",`<br>` "name": "string",`<br>` "groups": [`<br>` "string"`<br>` ],`<br>` "repoUrl": "string",`<br>` "mainBranch": "string",`<br>` "origin": "string",`<br>` "createdAt": "2024-06-26T07:22:21.955Z",`<br>` "updatedAt": "2024-06-26T07:22:21.955Z",`<br>` "tags": {`<br>` "test": "",`<br>` "priority": "high"`<br>` },`<br>` "criticality": 3`<br>` }`<br>` ]`<br>`}` | Success response:<br>`{`<br>` "totalCount": 0,`<br>` "filteredTotalCount": 0,`<br>` "projects": [`<br>` {`<br>` "id": "string",`<br>` "name": "string",`<br>` "groups": [`<br>` "string"`<br>` ],`<br>` "repoUrl": "string",`<br>` "mainBranch": "string",`<br>` "origin": "string",`<br>` "createdAt": "2023-09-19T13:31:06.431Z",`<br>` "updatedAt": "2023-09-19T13:31:06.431Z",`<br>` "tags": {`<br>` "test": "",`<br>` "priority": "high"`<br>` },`<br>` "applicationIds": [`<br>` "string"`<br>` ],`<br>` "criticality": 3`<br>` }`<br>` ]`<br>`}` | Get list of Projects with associated Application IDs |
| GET | /api/projects{project_id} | Path parameter: project_id<br>Success response:<br>`{`<br>` "id": "string",`<br>` "name": "string",`<br>` "applicationIds": [`<br>` "string"`<br>` ],`<br>` "groups": [`<br>` "string"`<br>` ],`<br>` "repoUrl": "string",`<br>` "mainBranch": "string",`<br>` "origin": "string",`<br>` "createdAt": "2024-06-26T07:44:17.640Z",`<br>` "updatedAt": "2024-06-26T07:44:17.640Z",`<br>` "tags": {`<br>` "test": "",`<br>` "priority": "high"`<br>` },`<br>` "criticality": 3`<br>`}` | Path parameter: project_id<br>Success response:<br>`{`<br>` "id": "string",`<br>` "name": "string",`<br>` "applicationIds": [`<br>` "string"`<br>` ],`<br>` "groups": [`<br>` "string"`<br>` ],`<br>` "repoUrl": "string",`<br>` "mainBranch": "string",`<br>` "origin": "string",`<br>` "createdAt": "2023-09-19T13:31:52.875Z",`<br>` "updatedAt": "2023-09-19T13:31:52.875Z",`<br>` "tags": {`<br>` "test": "",`<br>` "priority": "high"`<br>` },`<br>` "applicationIds": [`<br>` "string"`<br>` ],`<br>` "criticality": 3`<br>`}` | Get Project info with associated Application IDs |
| PUT | /api/projects{project_id} | Path paremeter: project_id<br>Request body:<br>`{`<br>` "name": "string",`<br>` "groups": [`<br>` "string"`<br>` ],`<br>` "repoUrl": "string",`<br>` "mainBranch": "string",`<br>` "origin": "string",`<br>` "tags": {`<br>` "test": "",`<br>` "priority": "high"`<br>` },`<br>` "criticality": 3`<br>`}` | Path parameter: project_id<br>Request body:<br>`{`<br>` "name": "string",`<br>` "groups": [`<br>` "string"`<br>` ],`<br>` "repoUrl": "string",`<br>` "mainBranch": "string",`<br>` "origin": "string",`<br>` "tags": {`<br>` "test": "",`<br>` "priority": "high"`<br>` },`<br>` "applicationIds": [`<br>` "string"`<br>` ],`<br>` "criticality": 3`<br>`}` | Update a Project. Added the “applicationIds” parameter.<br>If the “applicationIds” parameter is not set, then the assignment to Applications is not changed.<br>If “applicationIds” is set, then the previous assignment to Applications is overwritten by the submitted Application IDs.<br>{% hint style="info" %}<br>If you would like to **add** to the existing Application assignments, use the new API, `POST /projects/{project_id}/applications`.<br>{% endhint %} |
