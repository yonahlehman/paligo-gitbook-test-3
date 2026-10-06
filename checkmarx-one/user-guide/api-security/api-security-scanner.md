# API Security Scanner

The **API Security Scanner** screen provides an overview of the last completed API security scan using API Security widgets.

<figure><img src="../../../assets/APISec_doc_12.png" alt="" width="576"><figcaption></figcaption></figure>

## API Security Widgets

### Detected APIs

The number of detected APIs in the code. This scan detected **10** APIs in the code.

<figure><img src="../../../assets/APISEC_Scanner_Dashboard__Detected_APIs.png" alt="" width="288"><figcaption></figcaption></figure>

### Sensitive Data APIs

The number of APIs with at least one sensitive data attribute. This scan detected sensitive data attributes in **9** out of the **10** detected APIs. Sensitive Data categories and parameters are listed in the table below.

<figure><img src="../../../assets/APISEC_Scanner_Dashboard__Sensitive_Data_APIs.png" alt="" width="288"><figcaption></figcaption></figure>

| Category | Parameters |
|---|---|
| **Name** | firstname, surname, familyname, fullname, name |
| **Personal Data** | birthday, dob, dateofbirth, phone, mobile, email, socialsecurity, ssn, driverslicense |
| **Address** | address, zipcode |
| **Bank** | credit, cardnumber, account |
| **Secrets** | credentials, secret, auth, apikey, pass, pwd, password |

### Undocumented APIs

Lists the number of undocumented API endpoints found in the code but not in the Swagger file after scanning both the code and the documentation.

In the illustrated example, API Security detected **Undocumented APIs** once.

![](../../../assets/UndocumentedAPIsOverview.png)

### Results by Vulnerabilities

A list of sensitive data attributes with an indicator on how often each of these sensitive data attributes was detected.

In the illustrated example, API Security detected **Parameter Tampering** twice and three more once each.

<figure><img src="../../../assets/6485115003.png" alt="" width="288"><figcaption></figcaption></figure>

### Results by Risk

The number of sensitive data attributes according to their risk.

In the illustrated example, API Security detected **5** vulnerabilities of which **2** were of high risk and **3** of medium risk.

<figure><img src="../../../assets/APISEC_Scanner_Dashboard__Results_by_Risk.png" alt="" width="432"><figcaption></figcaption></figure>

## Viewing Results

To view results, click **View Results**. The Risks table appears. It lists the risks and provides additional information detailed in the parameters below and described in [Viewing API Results](../viewing-scan-results-in-the-results-viewers/api-security-results-viewer.md).

<figure><img src="../../../assets/APISec_doc_04.png" alt="" width="576"><figcaption></figcaption></figure>

| Parameter | Description |
|---|---|
| **Severity**<img src="../../../assets/Severity.png" alt="" data-size="line"> | Indicates the risk severity as follows:<br>• <img src="../../../assets/Image_1339.png" alt="" data-size="line">**Critical**<br>• <img src="../../../assets/Image_1337.png" alt="" data-size="line">**High**<br>• <img src="../../../assets/Image_1335.png" alt="" data-size="line">**Medium**<br>• <img src="../../../assets/Image_1334.png" alt="" data-size="line">**Low**<br>• <img src="../../../assets/Image_1331.png" alt="" data-size="line">**Info** |
| **Risk Name** | The name of the risk. |
| **Status** | Indicates the status of the risk as follows:<br><img src="../../../assets/New.png" alt="" data-size="line">- A newly detected vulnerability.<br><img src="../../../assets/Recurrent_List.png" alt="" data-size="line">- The vulnerability has been detected at least once before. |
| **Endpoint Path** | The end path of the resource URL. |
| **Method** | The operation that the endpoint performs on resources. |
| **Data Origin** | Indicates where the risk was detected, for example inside the **code**. |
| **Risk Discovered** | The date when the risk was detected. |
| **Doc** | Undocumented APIs present a risk because attackers may use them as an undetectable surveillance and reconnaissance channel.<br>This column shows whether the endpoint is documented or not:<br>• "**-**" appears when no documentation file was not scanned<br>• **Yes**: The endpoint appears in the scanned document, and it is documented<br>• **No**: The endpoint appears in the scanned document, but it is not documented |
| **AuthN** | Unauthenticated APIs present a risk because they may allow easy access to confidential information.<br>This column shows whether the endpoint is authenticated or not.<br>• "**-**" appears when no documentation file was not scanned<br>• **Yes**: The endpoint appears in the scanned document, and it is authenticated<br>• **No**: The endpoint appears in the scanned document, but it is not authenticated |

You can view the parameters of a *code* risk by clicking its row.

- Under **Parameters**, click <img src="../../../assets/View_All_Parameters.png" alt="" data-size="line">. All sensitive data parameters in the code appear.

  <figure><img src="../../../assets/Parameters_Global.png" alt="" width="252"><figcaption></figcaption></figure>
- | Interface | Description |
  |---|---|
  | <img src="../../../assets/Global_Warnings.png" alt="" width="393"> | List of all sensitive parameters in the API with warnings. This section is identical to the list of sensitive data parameters. |
  | <img src="../../../assets/Global_Requests.png" alt="" width="381"> | List of all parameters in the request to the API. The sensitive parameters are labeled <img src="../../../assets/Sensitive.png" alt="" data-size="line">. |
  | <img src="../../../assets/Global_Responnse.png" alt="" width="397"> | List of all parameters in the response by the API. The sensitive parameters are labeled <img src="../../../assets/Sensitive.png" alt="" data-size="line">. |

To view the details of a *documentation* risk, click its row and the vulnerability in the Swagger file will appear with an embedded description box.

<figure><img src="../../../assets/SwaggerFileRiskView.png" alt="" width="576"><figcaption></figcaption></figure>
