# Enrichment Workflow for Other CNAPP Vendors

The External 3rd Party Enrichment workflow enables a synergistic integration between Checkmarx One and 3rd Party CNAPP providers for the benefit of our mutual customers.

CNAPP vendors submit data from the runtime environments of our mutual customers into the corresponding Checkmarx One account. Checkmarx Cloud Insights then correlates the runtime data with Checkmarx One Projects and source code repositories, enriching Checkmarx One scanners results.

Then, the third-party CNAPP/Cloud Security vendors can query the Checkmarx One platform to obtain Checkmarx One scanner results data related to the container images ingested by the vendors, allowing them to enrich their systems accordingly.

This integration is done via Checkmarx One Rest APIs. Documentation of these APIs is available [here](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/branches/main/x9pzt8bcs5w36-cloud-insights-enrichment-service).

{% hint style="warning" %}
This process should be done by the CNAPP vendor, and not by individual Checkmarx customers.
{% endhint %}

## Prerequisites

- A valid Checkmarx One API Key (bearer token)
- A valid "External ID" - a unique ID for a specific vendor, provided by your Checkmarx support agent
- A valid JSON enrichment file - see below how to create this file

## Creating a JSON Enrichment File

Create a JSON file that provides detailed information about the clusters, pods and containers in your system, based on the following schema.

{% hint style="info" %}
The max. size limit is 20MB.
{% endhint %}

**Schema:**

```
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "title": "Versioned Asset Schema for Cloud Insights",
  "description": "A schema that handles two different versions of asset reporting. Defaults to v1 if version is not specified.",
  "type": "object",
  "properties": {
    "externalID": {
      "type": "string",
      "description": "A unique external identifier for the submission.",
      "maxLength": 255,
      "minLength": 1
    },
    "version": {
      "type": "string",
      "description": "The version of the schema. Can be 'v1' or 'v2'. Defaults to 'v1'.",
      "enum": ["v1", "v2"]
    },
    "clusters": {
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "name": {
            "type": "string",
            "maxLength": 200,
            "minLength": 1
          },
          "region": {
            "type": "string",
            "maxLength": 20
          },
          "pods": {
            "type": "array",
            "items": {
              "type": "object",
              "properties": {
                "name": {
                  "type": "string",
                  "maxLength": 200,
                  "minLength": 1
                },
                "ips": {
                  "type": "array",
                  "items": {
                    "type": "string",
                    "maxLength": 20
                  }
                },
                "containers": {
                  "type": "array",
                  "items": {
                    "type": "object",
                    "properties": {
                      "image": {
                        "type": "string",
                        "maxLength": 200,
                        "minLength": 1
                      },
                      "name": {
                        "type": "string",
                        "maxLength": 200,
                        "minLength": 1
                      },
                      "publicExposed": {
                        "type": "boolean"
                      },
                      "imageSha": {
                        "type": "string",
                        "maxLength": 71,
                        "minLength": 71,
                        "pattern": "^sha256:[a-fA-F0-9]{64}$"
                      },
                      "tags": {
                        "type": "object",
                        "patternProperties": {
                          "^.*$": {
                            "type": "string"
                          }
                        },
                        "additionalProperties": false
                      }
                    },
                    "required": [
                      "image",
                      "name"
                    ],
                    "additionalProperties": false
                  }
                }
              },
              "required": [
                "name",
                "containers"
              ],
              "additionalProperties": false
            }
          }
        },
        "required": [
          "name",
          "pods"
        ],
        "additionalProperties": false
      }
    },
    "resources": {
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "name": {
            "type": "string",
            "minLength": 1,
            "maxLength": 200
          },
          "type": {
            "type": "string",
            "maxLength": 100
          },
          "image": {
            "type": "string",
            "minLength": 1,
            "maxLength": 200
          },
          "imageSha": {
			"type": "string",
            "maxLength": 71,
            "minLength": 71,
            "pattern": "^sha256:[a-fA-F0-9]{64}$"
          },
          "metadata": {
            "type": "object",
            "patternProperties": {
              "^.*$": {
                "type": "string"
              }
            },
            "additionalProperties": false
          },
          "publicExposed": {
            "type": "boolean"
          },
          "clusterName": {
            "type": "string",
            "maxLength": 255
          },
          "clusterType": {
            "type": "string",
            "enum": ["Kubernetes", "ECS", "EKS", "GKE", "AKS", "HostedContainer", "UNKNOWN"]
          },
          "providerId": {
            "type": "string",
            "maxLength": 255
          },
          "region": {
            "type": "string",
            "maxLength": 100
          }
        },
        "required": [
          "name",
          "type",
          "image"
        ],
        "additionalProperties": false
      }
    }
  },
  "required": [
    "externalID"
  ],
  "if": {
    "required": [ "version" ],
    "properties": {
      "version": {
        "const": "v2"
      }
    }
  },
  "then": {
    "required": [
      "resources"
    ]
  },
  "else": {
    "required": [
      "clusters"
    ]
  },
  "additionalProperties": false
}
```

You can validate your file using our [Online Validator](https://www.jsonschemavalidator.net/s/WUgql69b) tool.

Example:

```
{
  "version":"v2",
  "externalID":"1223-123-123123",
  "resources": [
    {
      "name": "ECS Container",
      "type": "CONTAINER",
      "image": "ghrc.io/Your_Org/my-ecs-container-source-code:1255db389feb1027626f8d3d255fc6d5b7d7ad34",
      "imageSha": "sha256:8ec140f12b1ec77041606ae0435baa3cb5f31c80e21680d0a52d1af297e5e9f8",
      "metadata": {
        "test.source":"https://github.com/Your_Org/my-ecs-container-source-cod",
        "test.commithash":"1255db389feb1027626f8d3d255fc6d5b7d7ad34"
      },
      "publicExposed": true,
      "clusterName": "ecs test cluster",
      "clusterType": "ECS",
      "providerId": "",
      "region": "us-east-1"
    },
    {
      "name": "My EKS Container",
      "type": "CONTAINER",
      "image": "ghrc.io/Your_Org/My-EKS-Container",
      "imageSha": "sha256:8ec140f12b1ec77041606ae0435baa3cb5f31c80e21680d0a52d1af297e5e9f8",
      "metadata": {
        "test.source":"https://github.com/Your_Org/My-EKS-Container"
      },
      "publicExposed": false,
      "clusterName": "EKS Cluster test",
      "clusterType": "EKS",
      "providerId": "",
      "region": "us-east-1"
    },
}
```

## Third-Party Enrichment Workflow

### Step 1 - Create account and run enrichment

1. Create a JSON enrichment file, following the specifications described above.
2. Use [POST /cnas/accounts/enrich](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/branches/main/46emqu55hdfs2-create-a-cloud-insights-enrichment-account) to create a new Cloud Insights enrichment account using the ExternalID that was provided by Checkmarx. Take note of the Account ID that is returned.
3. Use [POST /api/uploads](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/branches/main/992ed893f5a38-generate-upload-link) to generate an upload link.
4. Use [PUT /{uploadLink}](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/branches/main/lwvmj7m3k5ei6-uploads-service-rest-api#upload-file), to upload the JSON enrichment file to the pre-signed URL.
5. Use [POST /cnas/v2/accounts/{id}/enrich](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/e58b691h86nj6-run-cloud-insights-enrichment-async), specifying the Account ID and upload link, to trigger the enrichment process as an asynchronous process. Take note of the Sync ID that is returned.
6. Use [GET /accounts/{id}/logs](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/8tjgxjgrulnit-get-account-logs), specifying the Account ID, and submitting the `syncId` as a query parameter to check the status of the enrichment. If the 'data' object is returned, this indicates that the process has completed and you can check the status and details of the process.

### Step 2 - Obtain results

{% hint style="info" %}
These APIs can be used to import results from Checkmarx One into the 3rd party platform.
{% endhint %}

1. Use [GET /cnas/accounts/{accountID}/resources](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/ma3kbuchb9si8-retrieve-list-of-resources) to obtain the Project ID of a Checkmarx One project associated with a specific image.
2. Use [GET /scans](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/1wnhzwk5inwup-retrieve-list-of-scans), specifying the Project ID in the query params, in order to obtain the Scan ID of the most recent scan of that project.
3. Use [GET /results](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/whqbw17zn6rg1-retrieve-scan-results-all-scanners) or [GET /sast-results](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/branches/main/68dabfc984bc3-retrieve-sast-scan-results), specifying the Scan ID in the query parameters, in order to obtain results for all risks identified in that scan of that project.

Alternatively, you can view the results on the Cloud Insights screen of the Checkmarx One web application (UI).
