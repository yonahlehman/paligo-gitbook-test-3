# Creating Checkmarx One Pipelines in Azure

You can add a Checkmarx One scan to an existing pipeline or you can create a new pipeline for the scan.

There are several ways to create a new pipeline in Azure DevOps. The following sections describe the two primary methods for creating a new pipeline with a Checkmarx One scan build step.

Additionally, you can set a pipeline variable to use a proxy server, as described [here](creating-a-checkmarx-one-pipeline-using-a-pre-configured-task.md#setting-up-a-proxy-pipeline-variable-optional).

## Output Variables

When a scan is completed, Checkmarx saves the scan ID as an environment variable, `CHECKMARXAST_CXONESCANID`. You can use this variable in the post-scan workflow of your pipeline. For example:

```
- displayName: 'Display Scan ID'
  script: |
       echo "The scan ID is $CHECKMARXAST_CXONESCANID"
```

## In this section

- [Creating a Checkmarx One Pipeline Using a Pre-configured Task](creating-a-checkmarx-one-pipeline-using-a-pre-configured-task.md)
- [Creating a Checkmarx One Pipeline Using a YAML](creating-a-checkmarx-one-pipeline-using-a-yaml.md)
