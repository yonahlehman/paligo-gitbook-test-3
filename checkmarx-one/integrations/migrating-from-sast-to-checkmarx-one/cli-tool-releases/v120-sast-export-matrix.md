# V1.2.0 SAST Export Matrix

The table below presents the SAST export matrix.

{% hint style="info" %}
When projects are migrated to Checkmarx One, the custom fields of each project are migrated as tags in the following form:

**name:value** (as you can see in the image below)

<figure><img src="../../../../assets/img-137485_hpr.png" alt="" width="576"><figcaption></figcaption></figure>
{% endhint %}

| **Users** | **Teams** | **Results (Projects)** | **Queries** | **Presets** | **Outcome** |
|---|---|---|---|---|---|
| ![](../../../../assets/Check-Small.png) | | | | | Users are migrated into a single root/default group in Checkmarx One |
| ![](../../../../assets/Check-Small.png) | ![](../../../../assets/Check-Small.png) | | | | • Users are migrated.<br>• Users are assigned to the same teams as in SAST.<br>• Teams are migrated to groups in the same organizational structure. |
| ![](../../../../assets/Check-Small.png) | ![](../../../../assets/Check-Small.png) | ![](../../../../assets/Check-Small.png) | | | • Users are migrated.<br>• Users are assigned to the same teams as in SAST.<br>• Teams are migrated to groups in the same organizational structure.<br>• Projects are created and assigned to the same groups as in SAST.<br>• Triaged vulnerabilities are migrated into the projects. |
| | ![](../../../../assets/Check-Small.png) | ![](../../../../assets/Check-Small.png) | | | • Teams are migrated to groups in the same organizational structure.<br>• Projects are created and assigned to the same groups as in SAST.<br>• Triaged vulnerabilities are migrated into the projects. |
| | | ![](../../../../assets/Check-Small.png) | | | • Projects are created and assigned to the same groups as in SAST. |
| ![](../../../../assets/Check-Small.png) | | ![](../../../../assets/Check-Small.png) | | | • Users are migrated into a single root/default group in Checkmarx One.<br>• Projects are created and assigned to a single root/default group in Checkmarx One.<br>• Triaged vulnerabilities are migrated into the projects. |
| | | | <img src="../../../../assets/Check-Small.png" alt="" data-size="line"> | | • Queries have no dependencies<br>• Only custom queries are exported |
| | | | | <img src="../../../../assets/Check-Small.png" alt="" data-size="line"> | • Presets have no dependencies<br>• Only custom presets are exported |
