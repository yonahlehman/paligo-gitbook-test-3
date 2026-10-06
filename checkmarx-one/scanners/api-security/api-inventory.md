# API Inventory

To access the API Inventory from the main menu, select **Resources ![](../../../assets/Resources.png)> API Inventory**.

The **Global API Inventory** is divided into two tabs: **Inventory**, which lists all APIs detected across all projects on the platform, and **Risks**, which lists all API risks detected across all projects on the platform. In both tabs, you can filter the table by column and export the displayed results as a CSV file.

{% hint style="info" %}
In the exported CSV file, the **Total Risk** column is broken down into four separate columns: **Critical**, **High**, **Medium**, and **Low**.
{% endhint %}

## Inventory Tab

By default, the **Inventory** tab opens the **All APIs** subtab, which displays the **Global API Inventor**y table. Hovering over an API and clicking **view** at the end of the row opens its details in a new subtab next to All APIs. Multiple API detail subtabs can remain open simultaneously, allowing you to switch between the inventory table and previously opened APIs.

![](../../../assets/apirisk1.png)

The following table describes the information displayed for each API:

| Parameter | Description |
|---|---|
| **Application** | The application that contains the project to which this API belongs. If the project does not belong to any application, this field is marked **----**. |
| **Project** | The project in which the API was discovered. |
| **Endpoint Path** | The path portion of the API endpoint URL that identifies the resource (for example, `/users/{id}`). |
| **Method** | The HTTP method used by the endpoint, such as `GET`, `POST`, `PUT`, or `DELETE`, which indicates the type of operation requested. |
| **Total Risk** | The number of risks found in the API. |
| **Data Origins** | Indicates where the API was detected. Currently, three data origins are available: **Code**, **Documentation**, and **Testing**. |
| **Sensitive Data** | The number of sensitive data attributes for all scans in the listed project. |
| **API Discovered** | The date when the API was discovered. |
| **Last Updated** | The date when the API was updated last. |
| **Doc** | Undocumented APIs present a risk because attackers may use them as an undetectable surveillance and reconnaissance channel.<br>This column shows whether the endpoint is documented or not:<br>• "**-**" appears when no documentation file was scanned.<br>• **Yes**: The endpoint appears in the application and appears in the scanned API documentation.<br>• **No**: The endpoint appears in the application, but does not appear in the scanned API documentation |
| **AuthN** | Unauthenticated APIs present a risk because they may allow easy access to confidential information.<br>This column shows whether the endpoint is authenticated or not.<br>• "**-**" appears when no authentication data was detected.<br>• **Yes**: The endpoint appears in the application and it is authenticated.<br>• **No**: The endpoint appears in the application, but it is not authenticated. |

### API Detail Subtabs

Selecting an API in the **All APIs** subtab opens a new subtab displaying details for the selected API.

![](../../../assets/APISec_doc_10.png)

The API detail subtab contains the following widgets:

| Widget | Description |
|---|---|
| **Risk** | Displays the number and severity of risks detected in the selected API.<br>This pane may include any or all of the following sections:<br>• **Total**: The total number of risks found for the current endpoint by the API Security scanner (on the left) and by the SAST scanner (on the right).<br>• **Source Code**: The number of source code risks found by the API Security scanner (on the left) and the SAST scanner (on the right).<br>• **API Documentation**: The number of API documentation risks found by the API Security scanner (on the left) and by the SAST scanner (on the right).<br>If the scan did not include SAST queries, this section will show only the number of API documentation risks.<br>Select a severity bar to open the **Risks** tab. The **All Risks** subtab is automatically filtered to display the risks for the selected API.<br>![](../../../assets/RisksTable_for_API.png) |
| **Parameters** | Shows the number of occurrences of sensitive data in the code and documentation. To see a list of the sensitive data in the code, click inside the widget.<br>Sensitive data is a set of data that Checkmarx defines as sensitive. It is not related to the detected vulnerabilities. It simply provides you with an overview of what is potentially vulnerable to threats.<br>Sensitive parameters are divided into five categories like **Name**, **Personal Data**, etc. Each category has a set of parameters defined.<br>• **Name**: firstname, surname, familyname, fullname, name<br>• **Personal Data**: birthday, dob, dateofbirth, phone, mobile, email, socialsecurity, ssn, driverslicense<br>• **Address**: address, zipcode<br>• **Bank**: credit, cardnumber, account<br>• **Secrets**: dcredentials, secret, auth, apikey, pass, pwd, password<br>If the API was detected both in the API source code and the API documentation, this widget shows which warnings appear only in the code, only in the documentation, or in both. Code data origin is indicated by the ![](../../../assets/CodeIconParameter.png) icon, and documentation data origin is indicated by the ![](../../../assets/DocIconParameter.png) icon.<br>![](../../../assets/ParametersWidget.png) |
| **Data Origins** | Displays the details of the API data origins. It can be either the API source code, the Swagger file (documentation), both, or DAST tests. |
| **Latest Changes** | Lists the changes on this API since it was discovered. It can be one or several of the following:<br>**Structure**: Added or removed Response and Request parameters, for example:<br>• **Structure \| {Parameter} was removed**<br>• **Structure \| {Parameter} was added**<br>**Risk**: Detected one or more new risks. Risks are characterized by their risk level ( Critical, High, Medium, or Low) and grouped in categories, for example:<br>• **Risk \| {Number} new {Level} found**<br>**Sensitive Data**: Flagged parameters as sensitive, for example:<br>• **Sensitive Data \| {Parameter} was found in {Request or Response}**<br>If the API has not changed since its discovery, the corresponding message will appear. |

## Risks Tab

The **Risks** tab displays the **Global Risks Table**. By default, the **All Risks** subtab displays all API risks detected across all projects on the platform. Selecting a risk opens its details in a new subtab next to All Risks. Multiple risk detail subtabs can remain open simultaneously, allowing you to switch between the risks table and previously opened risks.

![](../../../assets/APISec_doc_08.png)

The following table describes the information displayed for each risk:

| Parameter | Description |
|---|---|
| **Severity**![](../../../assets/Severity.png) | Indicates the risk severity. Possible severity levels are:Critical, High, Medium, or Low. |
| **Applications** | The application to which this project belongs. If the project does not belong to any application, this field is marked **----**. |
| **Project** | The project for which the risk was detected. |
| **Risk Name** | The name of the risk. |
| **Status** | Indicates the status of the risk as follows:<br>![](../../../assets/New.png)- A newly detected vulnerability.<br>![](../../../assets/Recurrent_List.png)- The vulnerability has been detected at least once before. |
| **Endpoint Path** | The end path of the resource URL. |
| **Method** | The operation that the endpoint performs on resources. |
| **Risk Origin** | Indicates where the risk was detected. Currently, three risk origins are available: **Code**, **Documentation**, and **Testing**. To filter the risks by their origin, click on the column header to display a drop-down list, check the required option, and click OK: |
| **Risk Discovered** | The date when the risk was detected. |
| **Doc** | Undocumented APIs present a risk because attackers may use them as an undetectable surveillance and reconnaissance channel.<br>This column shows whether the endpoint is documented or not:<br>• "**-**" appears when no documentation file was scanned.<br>• **Yes**: The endpoint appears in the application and appears in the scanned API documentation.<br>• **No**: The endpoint appears in the application, but does not appear in the scanned API documentation |
| **AuthN** | Unauthenticated APIs present a risk because they may allow easy access to confidential information.<br>This column shows whether the endpoint is authenticated or not.<br>• "**-**" appears when no authentication data was detected.<br>• **Yes**: The endpoint appears in the application and it is authenticated.<br>• **No**: The endpoint appears in the application, but it is not authenticated. |

### Risk Detail Subtabs

Select a risk in the **All Risks** subtab to open its details in a new subtab.

![](../../../assets/Risk_for_API_Detailed.png)

In the subtab, two widgets are displayed: **Details** and **Parameters**. Click on a widget to show more information.

![](../../../assets/Risk_for_API_detailed_in_detail.png)

#### Details Widget

The **Details** widget shows the following information:

| Parameter | Description | Values |
|---|---|---|
| **Vulnerability Name** | The name of the vulnerability | Example:<br>Unsafe Object Binding |
| **Source File** | The path and file name of the file with the vulnerability | Example:<br>**/iast-manager-times-6-total-589252-locjava-354324-loc/manager-servicescopy5/src/main/java/com/checkmarx/iast/manager/rest/ScansResource.java**(line:250) |
| **Status** | The status of the vulnerability | **New**<br>**Recurrent**. The vulnerability has been detected at least once before |
| **Source Node** | The beginning of the attack vector | The first node (input) of the vulnerable sequence. |

In addition, the **Details** widget provides a link ![](../../../assets/View_SAST_Results.png) to view the highlighted vulnerability in the **SAST Results Viewer**. Clicking on a specific instance of the vulnerability opens a subtab with the vulnerability details

![](../../../assets/SAST_Vulnerabilities_1234_Java_Stored_XSS_1st_instance.png)

{% hint style="info" %}
For a detailed explanation of the **SAST Results Viewer**, see [SAST Results Viewer](../sast-scanner/sast-results-viewer.md).
{% endhint %}

{% hint style="info" %}
For a detailed explanation of triaging SAST results, see [Triaging SAST Results](../sast-scanner/triaging-sast-results.md)
{% endhint %}

#### Parameters Widget

In the **Parameters**, clicking on ![](../../../assets/View_All_Parameters.png) opens a side-panel that displays all sensitive data parameters in the code.

The following table describes the available information:

| Interface | Description |
|---|---|
| ![](../../../assets/Global_Warnings.png) | List of all sensitive parameters in the API with warnings. This section is identical to the list of sensitive data parameters. |
| ![](../../../assets/Global_Requests.png) | List of all parameters in the request to the API. The sensitive parameters are labeled ![](../../../assets/Sensitive.png). |
| ![](../../../assets/Global_Responnse.png) | List of all parameters in the response by the API. The sensitive parameters are labeled ![](../../../assets/Sensitive.png). |

<details>

<summary>Filtering the Table View</summary>

To filter the lists or to display them in ascending or descending order, do the following:

- To view list entries in ascending or descending order, point to the relevant header and select **Click to sort ascending** or **Click to sort descending** respectively.
- To only show specific parameters, for example, a specific status, point to the relevant header, click ![](../../../assets/Filter.png)and then select the desired parameter(s) from the filter options.

</details>
