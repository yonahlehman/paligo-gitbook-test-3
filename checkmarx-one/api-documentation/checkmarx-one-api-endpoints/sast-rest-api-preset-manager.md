# SAST REST API Preset Manager

The previous **api/presets** endpoint was designed specifically for SAST. With the addition of other scanners, the new **api/preset-manager** provides a unified way to manage presets across scanners (SAST & IaC). This API requires specifying a scanner (SAST or IaC). The legacy endpoints will be deprecated in version 3.59. See [here](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/5913e9f3d4444-preset-management-generic-api) for more information on the APIs.

Below is a clear mapping between old and new endpoints to support the transition.

| Old Preset (/api/preset) | New Preset (/api/preset-manager) |
|---|---|
| **GET/** list presets | **GET/{scanner}/presets** |
| **POST/** create a new preset | **POST/{scanner}/presets** |
| **GET/{id}** get preset by ID<br>**GET/{id}/summary** get preset summary by ID | **GET/{scanner}/presets/{id}** |
| **PUT/{id}** updates a preset<br>**PUT/{id}/add-query** add query to preset | **PUT/{scanner}/presets/{id}** |
| **DELETE/{id}** delete a preset by ID | **DELETE/{scanner}/presets/{id}** |
| **POST/{id}/clone** | **POST/{scanner}/presets/{id}/clone** |
| **GET/queries** list queries executable | **GET/{scanner}/query-families**<br>**GET/{scanner}/query-families/{query-family}/queries** |
