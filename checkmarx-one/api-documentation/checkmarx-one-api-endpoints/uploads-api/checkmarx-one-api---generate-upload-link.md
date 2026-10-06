# Checkmarx One API - Generate Upload Link

## Endpoint

`POST /api/uploads`

## Description

This API is used when the source code for your Project is in a zip archive. This API generates an upload link for uploading the zip archive to be scanned. The upload link generated in this step will then be used in the `PUT Upload Source` and `POST Scan` calls.

## Workflow

1. Use `POST /api/uploads` to generate an upload link.
2. Use `PUT /{uploadLink}` , specifying the path to your zip archive, to upload your file.
3. Use `POST /api/scans` , specifying the Project ID and upload link, to scan the zip archive.
4. Use `GET /api/scans/{scanId}` to check the status of the scan.
5. View the results using `GET /api/results`, specifying the Scan ID. Alternatively, you can view the results in the Checkmarx One web portal (UI), see Scan Results.

## URL

The URL for Uploads endpoints is \<base_url>/api/uploads

<details>

<summary>Checkmarx One Server Base URLs</summary>

- US Environment - https://ast.checkmarx.net
- US2 Environment - https://us.ast.checkmarx.net
- EU Environment - https://eu.ast.checkmarx.net
- EU2 Environment - https://eu-2.ast.checkmarx.net
- DEU Environment - https://deu.ast.checkmarx.net
- Australia & New Zealand – https://anz.ast.checkmarx.net
- India - https://ind.ast.checkmarx.net
- India 2 - https://ind-2.ast.checkmarx.net/
- Singapore - https://sng.ast.checkmarx.net
- UAE - https://mea.ast.checkmarx.net
- Israel - https://gov-il.ast.checkmarx.net

</details>

## Curl Sample

```
curl -X POST "https://ast.checkmarx.net/api/uploads/" -H "accept: application/json" -d ““
```

## Media Type (header)

Authorization: `Bearer <access_token>`

Accept: `application/json`

## Parameters

There are no parameters.

## Success Response

Code: 200 OK

Attributes:

| **Attribute** | **Type** | **Enums** | **Description** |
|---|---|---|---|
| url | string | **-** | The url that will be needed for scanning a zip archive. This URL is used in the `PUT Upload Source` and `POST Scan` APIs. |

### Sample Success Response

```
{
    "url": "https://ast.checkmarx.net/storage/uploads.ast.checkmarx.net-eu-west-1-941355383184/2021_06_08_06_28_24.853?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=ast%2F20210608%2Feu-west-1%2Fs3%2Faws4_request&X-Amz-Date=20210608T062824Z&X-Amz-Expires=86400&X-Amz-Signature=1e61cae58f1ac273e7f251e13ee6755599&X-Amz-SignedHeaders=host"
}
```

## Error Response

| |
|---|
| <details><br><br><summary>Status code: 400</summary><br><br>Message: `Bad Request`<br><br></details><br><details><br><br><summary>Status code: 401</summary><br><br>Message: `Access token is missing or invalid`<br><br></details> |
