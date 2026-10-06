# V1.2.0 Overview

SAST Migration to Checkmarx One feature is created in order to provide existing SAST customers the ability to perform the following:

- Export the existing SAST v9.3 (and up) environment including:

  - **Users** - Application users, Users Roles.
  - **Teams & teams assignments**.
  - **Project team assignments**.
  - **Triage for the last scans** - Including history, labels & comments.
  - **Queries** - Custom queries
  - **Presets** - Custom presets

    {% hint style="info" %}
    - In case using a filter with project ID's only the presets that are associated with those project ID's will be exported.
    - When exporting all presets, the default presets will be included.
    {% endhint %}
- Using the installation.json file to export bundle that includes SAST version information.

{% hint style="info" %}
Any combination of the above is valid for the SAST export.

For more information see [V1.2.0 SAST Export Matrix](v120-sast-export-matrix.md)
{% endhint %}

- Import the the exported SAST environment to an existing Checkmarx One tenant.
