# Container Security GraphQL API Documentation

## Overview

The Container Security GraphQL API provides comprehensive access to container security scan data, allowing clients to query information about scans, images, layers, packages, and vulnerabilities. The API implements a hybrid approach, offering both hierarchical access and flat access patterns to provide maximum flexibility for data retrieval.

## API Endpoint

The GraphQL API is available at:

```
https://{BASE_URL}/api/containers/buffet/graphql-v2
```

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

## Authentication and Authorization

All API requests require authentication.

Authentication is done by submitting a JWT (JSON Web Token) access token. This is the same token used for authentication for Checkmarx One REST APIs. For information about generating a JWT, see [here](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/branches/main/fm1ma9xg73dx9-authentication-api).

All queries via this API require the permission `ContainerPermissions.ViewResults`.

## Headers

- A header of **Cx-Project-Id** must be included in every request.

## Schema Components

### Core Types

The API exposes the following primary data types:

1. **Scan**: Contains information about a security scan, including metadata and references to images
2. **Image**: Represents a container image that was analyzed during a scan
3. **Layer**: Represents a layer within a container image
4. **Package**: Represents a software package found within an image
5. **Vulnerability**: Represents a security vulnerability found in a package

### Relationships

The data model follows a hierarchical structure:

- A **Scan** contains multiple **Images**
- An **Image** contains multiple **Layers**, **Packages**, and **Vulnerabilities**
- A **Layer** is associated with **Packages**
- A **Package** may have multiple **Vulnerabilities**
- A **Vulnerability** can affect multiple **Packages** and **Images**

### Access Patterns

The API supports two primary access patterns:

1. **Hierarchical Access**: Navigate the data structure following the natural relationships (e.g., scan → images → packages → vulnerabilities)
2. **Flat Access**: Directly query specific entities across a scan (e.g., get all vulnerabilities in a scan regardless of which image or package they belong to)

## Detailed Type Descriptions

### Scan

Root query entity representing a container security scan.

**Fields:**

| Field Name | Type | Description |
|---|---|---|
| id | String! | Unique identifier for the scan |
| createdAt | DateTime | Timestamp when the scan was created |
| imagesCount | Int | Number of images included in this scan |
| fixableCount | Int | Number of fixable issues found in the scan |
| vulnerabilityCounters | VulnerabilityCounters | Aggregated vulnerability statistics |
| images | \[Image\] | List of images analyzed in this scan |
| hasCriticalVulnerabilities | Boolean | Indicates whether critical vulnerabilities were found |
| hasMaliciousPackages | Boolean | Indicates whether malicious packages were found |

**Filtering:** Supports filtering via `ApiClientScanFilterType`

**Sorting:** Supports sorting via `ApiClientScanSortType`

**Pagination:** Supports offset-based pagination on the images field

### Image

Represents a container image analyzed during a scan.

**Fields:**

| Field Name | Type | Description |
|---|---|---|
| id | String! | Unique identifier for the image |
| imageId | String | Alternative image identifier |
| imageName | String | Name of the image |
| imageTag | String | Tag of the image |
| baseImage | String | Base image identifier |
| runtime | Boolean | Indicates if the image is a runtime image |
| fixable | Boolean | Indicates if vulnerabilities in this image are fixable |
| isImageMalicious | Boolean | Indicates if the image is flagged as malicious |
| maliciousDescription | String | Description of malicious findings (if applicable) |
| packagesCount | Int | Number of packages in the image |
| maliciousPackagesCount | Int | Number of malicious packages in the image |
| vulnerabilityCounters | VulnerabilityCounters | Aggregated vulnerability statistics |
| imageLocations | \[ImageLocation\] | Locations where this image was found |
| triage | TriageInfo | Information about triage status and history |
| recommendations | ImageRecommendationsResult | Recommendations for fixing vulnerabilities |
| layers | \[Layer\] | Layers that make up this image |
| packages | \[Package\] | Packages found in this image |
| vulnerabilities | \[Vulnerability\] | Vulnerabilities found in this image |

**Filtering:** Supports filtering via `ApiClientImageFilterType`

**Sorting:** Supported

**Pagination:** Supports offset-based pagination on packages and vulnerabilities fields

### Layer

Represents a layer within a container image.

**Fields:**

| Field Name | Type | Description |
|---|---|---|
| id | String | Unique identifier for the layer |
| command | String | Command used to create this layer |
| index | Int | Position of this layer in the image |
| size | Int | Size of this layer in bytes |
| packagesCount | Int | Number of packages in this layer |
| packages | \[Package\] | Packages found in this layer |
| images | \[Image\] | Images that contain this layer |
| imageIds | \[String\] | IDs of images that contain this layer |

**Filtering:** Supports filtering via `ApiClientLayerFilterType`

**Sorting:** Supports sorting via `ApiClientLayerSortType`

**Pagination:** No pagination on packages and images (returns all items)

### Package

Represents a software package found within an image.

**Fields:**

| Field Name | Type | Description |
|---|---|---|
| id | String! | Unique identifier for the package |
| packageName | String | Name of the package |
| packageVersion | String | Version of the package |
| distribution | String | Distribution the package belongs to |
| type | String | Type of package (e.g., npm, pip, apt) |
| packageId | String | Alternative package identifier |
| vulnerabilitiesCount | Int | Number of vulnerabilities in this package |
| maxRiskSeverity | SeverityLevel | Maximum severity level of vulnerabilities |
| isMalicious | Boolean | Indicates if the package is flagged as malicious |
| maliciousDescription | String | Description of malicious findings (if applicable) |
| runtimeUsage | RuntimeUsage | Indicates if the package is used at runtime |
| licenses | \[String\] | Licenses associated with this package |
| isSource | Boolean | Indicates if this is a source package |
| triage | TriageInfo | Information about triage status and history |
| vulnerabilities | \[Vulnerability\] | Vulnerabilities found in this package |
| layers | \[Layer\] | Layers that contain this package |
| images | \[Image\] | Images that contain this package |

**Filtering:** Supports filtering via `ApiClientPackageFilterType`

**Sorting:** Supports sorting via `ApiClientPackageSortType`

**Pagination:** No pagination on vulnerabilities (returns all items)

### Vulnerability

Represents a security vulnerability found in a package.

**Fields:**

| Field Name | Type | Description |
|---|---|---|
| cve | String! | Common Vulnerabilities and Exposures identifier |
| cwe | String | Common Weakness Enumeration identifier |
| vulnerabilityLevel | SeverityLevel | Current severity level after triage |
| vulnerabilityScore | Float | CVSS score for this vulnerability after triage |
| originalSeverityLevel | SeverityLevel | Original severity level before triage |
| originalScore | Float | Original CVSS score before triage |
| description | String | Description of the vulnerability |
| publicationDate | DateTime | Date when the vulnerability was published |
| status | Status | Current status of the vulnerability |
| firstScanId | String | ID of the first scan that detected this vulnerability |
| firstFoundDate | DateTime | Date when this vulnerability was first found |
| triage | VulnerabilityTriage | Triage information for this vulnerability |
| affectedPackages | \[Package\] | Packages affected by this vulnerability |
| affectedImages | \[Image\] | Images affected by this vulnerability |

**Filtering:** Supports filtering via `ApiClientVulnerabilityFilterType`

**Sorting:** Supports sorting via `ApiClientVulnerabilitySortType`

**Pagination:** No pagination on affectedPackages and affectedImages (returns all items)

### Supporting Types

#### VulnerabilityCounters

Provides counts of vulnerabilities by severity level.

**Fields:**

| Field Name | Type | Description |
|---|---|---|
| totalVulnerabilitiesCount | Int | Total number of vulnerabilities |
| criticalCount | Int | Number of critical vulnerabilities |
| highCount | Int | Number of high severity vulnerabilities |
| mediumCount | Int | Number of medium severity vulnerabilities |
| lowCount | Int | Number of low severity vulnerabilities |
| noneCount | Int | Number of informational findings |

#### TriageInfo

Provides information about triage status and history.

**Fields:**

| Field Name | Type | Description |
|---|---|---|
| status | EntityStatus | Current triage status |
| historyChanges | \[TriageTransactionalEvent\] | History of triage actions |
| snoozeDate | DateTime | Date until which this item is snoozed |

#### VulnerabilityTriage

Provides triage information specific to vulnerabilities.

**Fields:**

| Field Name | Type | Description |
|---|---|---|
| state | ActionState | Current triage state |
| historyChanges | \[TriageTransactionalEvent\] | History of triage actions |

#### ImageLocation

Provides location information for an image.

**Fields:**

| Field Name | Type | Description |
|---|---|---|
| path | String | Path to the image |
| origin | String | Origin of the image |

#### ImageRecommendationsResult

Provides recommendations for fixing vulnerable images.

**Fields:**

| Field Name | Type | Description |
|---|---|---|
| minorRecommendedImages | \[RecommendedImageModel\] | Recommended minor version upgrades |
| majorRecommendedImages | \[RecommendedImageModel\] | Recommended major version upgrades |
| alternativeRecommendedImages | \[RecommendedImageModel\] | Alternative image recommendations |
| nextRecommendedVersions | \[RecommendedImageModel\] | Next recommended versions |
| notOutdatedImages | \[RecommendedImageModel\] | Images that are not outdated |
| alternativeImageTags | \[String\] | Alternative tags for the image |

#### RecommendedImageModel

Represents a recommended image replacement.

**Fields:**

| Field Name | Type | Description |
|---|---|---|
| imageId | String | ID of the recommended image |
| lowVulnerabilitiesCount | Int | Number of low severity vulnerabilities |
| mediumVulnerabilitiesCount | Int | Number of medium severity vulnerabilities |
| highVulnerabilitiesCount | Int | Number of high severity vulnerabilities |
| criticalVulnerabilitiesCount | Int | Number of critical vulnerabilities |

### Enums

#### SeverityLevel

Represents the severity level of vulnerabilities.

```
enum SeverityLevel {
  NONE
  LOW
  MEDIUM
  HIGH
  CRITICAL
}
```

#### RuntimeUsage

Indicates if a package is used at runtime.

```
enum RuntimeUsage {
  USED
  UNUSED
  UNKNOWN
}
```

#### EntityStatus

Represents the triage status of an entity.

```
enum EntityStatus {
  ACTIVE
  INACTIVE
  IGNORED
  PENDING
  SNOOZED
}
```

#### ActionState

Represents the triage state of a vulnerability.

```
enum ActionState {
  APPROVED
  REJECTED
  FALSE_POSITIVE
  RISK_ACCEPTED
  PENDING
}
```

#### Status

Represents the status of a vulnerability.

```
enum Status {
  NEW
  FIXED
  RECURRING
}
```

## Query Operations

The API provides the following query operations:

### Scan by ID

```
scan(id: String!): Scan
```

Retrieves a scan by its ID.

### Images by Scan

```
imagesByScan(scanId: String!): [Image]
```

Retrieves all images from a specified scan.

### Packages by Scan

```
packagesByScan(scanId: String!): [Package]
```

Retrieves all packages across all images in a specified scan.

### Vulnerabilities by Scan

```
vulnerabilitiesByScan(scanId: String!): [Vulnerability]
```

Retrieves all vulnerabilities across all images in a specified scan.

### Layers by Scan

```
layersByScan(scanId: String!): [Layer]
```

Retrieves all layers across all images in a specified scan.

### Packages by Image

```
packagesByImage(scanId: String!, imageId: String!): [Package]
```

Retrieves all packages in a specific image.

### Vulnerabilities by Image

```
vulnerabilitiesByImage(scanId: String!, imageId: String!): [Vulnerability]
```

Retrieves all vulnerabilities in a specific image.

### Vulnerabilities by Package

```
vulnerabilitiesByPackage(scanId: String!, packageId: String!): [Vulnerability]
```

Retrieves all vulnerabilities in a specific package.

## Filtering and Sorting

The API supports comprehensive filtering and sorting capabilities:

### Image Filtering (ApiClientImageFilterType)

- `imageName`: Filter by image name
- `imageTag`: Filter by image tag
- `baseImage`: Filter by base image
- `runtime`: Filter by runtime status
- `fixable`: Filter by fixable status
- `isImageMalicious`: Filter by malicious status

### Layer Filtering (ApiClientLayerFilterType)

- `index`: Filter by layer index
- `id`: Filter by layer ID
- `size`: Filter by layer size
- `command`: Filter by layer command

### Package Filtering (ApiClientPackageFilterType)

- `packageName`: Filter by package name
- `packageVersion`: Filter by package version
- `type`: Filter by package type
- `isMalicious`: Filter by malicious status
- `runtimeUsage`: Filter by runtime usage
- `maxRiskSeverity`: Filter by maximum risk severity
- `vulnerabilitiesCount`: Filter by vulnerability count

### Vulnerability Filtering (ApiClientVulnerabilityFilterType)

- `cve`: Filter by CVE identifier
- `cwe`: Filter by CWE identifier
- `vulnerabilityLevel`: Filter by severity level
- `vulnerabilityScore`: Filter by CVSS score
- `status`: Filter by vulnerability status
- `publicationDate`: Filter by publication date

### Scan Filtering (ApiClientScanFilterType)

- `id`: Filter by scan ID
- `createdAt`: Filter by creation date
- `hasCriticalVulnerabilities`: Filter by presence of critical vulnerabilities
- `hasMaliciousPackages`: Filter by presence of malicious packages

## Pagination

The API supports offset-based pagination for queries that may return large result sets:

- `scan.images`: Paginated with a maximum page size of 1000
- `image.packages`: Paginated with a maximum page size of 1000
- `image.vulnerabilities`: Paginated with a maximum page size of 1000
- `ImagesByScan`: Paginated with a maximum page size of 1000
- `packagesByScan`: Paginated with a maximum page size of 1000
- `vulnerabilitiesByScan`: Paginated with a maximum page size of 1000
- `layersByScan`: Paginated with a maximum page size of 1000
- `packagesByImage`: Paginated with a maximum page size of 1000
- `vulnerabilitiesByImage`: Paginated with a maximum page size of 1000
- `vulnerabilitiesByPackage`: Paginated with a maximum page size of 1000

## Usage Examples

Below are examples of common queries that can be executed against the API.

### 1. Get Complete Scan Information with Pagination

This comprehensive example shows how to retrieve a scan with all its related data, using pagination for images, packages, and vulnerabilities

```
query GetCompleteScanInfo($scanId: String!) {
  scan(id: $scanId) {
    id
    createdAt
    imagesCount
    fixableCount
    vulnerabilityCounters {
      totalVulnerabilitiesCount
      criticalCount
      highCount
      mediumCount
      lowCount
      noneCount
    }

    # Get images with offset pagination
    images(skip: 0, take: 100) {
      # Offset pagination metadata
      pageInfo {
        hasNextPage
        hasPreviousPage
      }
      totalCount

      items {
        id
        imageName
        imageTag
        imageId
        baseImage
        imageHash
        size
        runtime
        fixable
        isImageMalicious
        maliciousDescription
        packagesCount
        maliciousPackagesCount

        imageLocations {
          path
          origin
        }

        triage {
          status
          snoozeDate
          historyChanges {
            user
            comment
            createDate
            events {
              actionType
              newValue
              oldValue
            }
          }
        }

        recommendations {
          minorRecommendedImages {
            imageId
            lowVulnerabilitiesCount
            mediumVulnerabilitiesCount
            highVulnerabilitiesCount
            criticalVulnerabilitiesCount
          }
          majorRecommendedImages {
            imageId
            lowVulnerabilitiesCount
            mediumVulnerabilitiesCount
            highVulnerabilitiesCount
            criticalVulnerabilitiesCount
          }
          nextRecommendedVersions {
            imageId
            lowVulnerabilitiesCount
            mediumVulnerabilitiesCount
            highVulnerabilitiesCount
            criticalVulnerabilitiesCount
          }
          alternativeRecommendedImages {
            imageId
            lowVulnerabilitiesCount
            mediumVulnerabilitiesCount
            highVulnerabilitiesCount
            criticalVulnerabilitiesCount
          }
          notOutdatedImages {
            imageId
            lowVulnerabilitiesCount
            mediumVulnerabilitiesCount
            highVulnerabilitiesCount
            criticalVulnerabilitiesCount
          }
          alternativeImageTags
        }

        vulnerabilityCounters {
          totalVulnerabilitiesCount
          criticalCount
          highCount
          mediumCount
          lowCount
          noneCount
        }

        # Get image layers (not paginated)
        layers {
          id
          command
          index
          size
          packagesCount
        }

        # Get image packages with offset pagination
        packages(skip: 0, take: 100) {
          # Offset pagination metadata
          pageInfo {
            hasNextPage
            hasPreviousPage
          }
          totalCount

          items {
            id
            packageName
            packageVersion
            distribution
            type
            packageId
            vulnerabilitiesCount
            maxRiskSeverity
            isMalicious
            maliciousDescription
            runtimeUsage
            licenses
            isSource

            # Get triage information if available
            triage {
              status
              snoozeDate
              historyChanges {
                user
                comment
                createDate
                events {
                  actionType
                  newValue
                  oldValue
                }
              }
            }

            # Get vulnerabilities for this package (not paginated)
            vulnerabilities {
              cve
              cwe
              vulnerabilityLevel
              vulnerabilityScore
              description
              publicationDate
              fixedVersion
              epssScore
              originalScore
              originalSeverityLevel
              status
              firstScanId
              firstFoundDate

              triage {
                state
                historyChanges {
                  user
                  comment
                  createDate
                  events {
                    actionType
                    newValue
                    oldValue
                  }
                }
              }
            }
          }
        }
      }
    }
  }
}
```

### 2. Flat Access to Vulnerabilities with Filtering and Sorting

This example demonstrates how to use flat access to get vulnerabilities directly, with filtering and sorting

```
query GetFilteredAndSortedVulnerabilities($scanId: String!) {
  vulnerabilitiesByScan(
    scanId: $scanId,
    # Skip the first 0 items and take 100
    skip: 0,
    take: 100,
    # Filter to only critical and high severity vulnerabilities
    where: {
      vulnerabilityLevel: { in: [CRITICAL, HIGH] },
      # Only include vulnerabilities published after 2023-01-01
      publicationDate: { gte: "2023-01-01T00:00:00Z" }
    },
    # Sort by severity level (descending) and then by score (descending)
    order: [
      { vulnerabilityLevel: DESC },
      { vulnerabilityScore: DESC }
    ]
  ) {
    # Pagination metadata
    pageInfo {
      hasNextPage
      hasPreviousPage
    }
    totalCount

    items {
      cve
      cwe
      description
      vulnerabilityLevel
      vulnerabilityScore
      publicationDate
      status

      # Include package information
      affectedPackages {
        packageName
        packageVersion
        type
      }

      # Include image information
      affectedImages {
        imageName
        imageTag
      }

      # Include triage information
      triage {
        state
        historyChanges {
          user
          comment
          createDate
        }
      }
    }
  }
}
```

### 3. Complex Package Filtering Across All Images

This example shows how to get packages across all images with complex filtering criteria

```
query GetHighRiskPackages($scanId: String!) {
  packagesByScan(
    scanId: $scanId,
    skip: 0,
    take: 100,
    # Complex filtering using logical operators
    where: {
      or: [
        # High risk packages with vulnerabilities
        {
          and: [
            { maxRiskSeverity: { in: [CRITICAL, HIGH] } },
            { vulnerabilitiesCount: { gt: 0 } }
          ]
        },
        # Any malicious packages
        { isMalicious: { eq: true } },
        # Packages with specific name patterns (e.g., known problematic packages)
        {
          or: [
            { packageName: { contains: "log4j" } },
            { packageName: { contains: "spring" } }
          ]
        }
      ]
    },
    # Sort by risk severity (highest first), then by vulnerability count (highest first)
    order: [
      { maxRiskSeverity: DESC },
      { vulnerabilitiesCount: DESC }
    ]
  ) {
    pageInfo {
      hasNextPage
      hasPreviousPage
    }
    totalCount

    items {
      id
      packageName
      packageVersion
      type
      distribution
      maxRiskSeverity
      vulnerabilitiesCount
      isMalicious
      maliciousDescription
      runtimeUsage
      licenses

      # Include triage information
      triage {
        status
        snoozeDate
      }

      # Include the most severe vulnerabilities (limited to top 5)
      vulnerabilities(
           order: [{ vulnerabilityLevel: DESC }]
      ) {
        cve
        vulnerabilityLevel
        vulnerabilityScore
        description
        triage {
          state
        }
      }

      # Show which images contain this package
      images {
        imageName
        imageTag
      }

      # Show which layers contain this package
      layers {
        index
        command
      }
    }
  }
}
```

### 4. Get Packages with Malicious Status in a Specific Image

```
query GetMaliciousPackages($scanId: String!, $imageId: String!) {
  packagesByImage(
    scanId: $scanId,
    imageId: $imageId,
    where: { isMalicious: { eq: true } }
  ) {
    totalCount
    items {
      packageName
      packageVersion
      type
      maliciousDescription
      vulnerabilitiesCount
    }
  }
}
```

### 5. Get Vulnerabilities for a Specific Package

```
query GetPackageVulnerabilities($scanId: String!, $packageId: String!) {
  vulnerabilitiesByPackage(
    scanId: $scanId,
    packageId: $packageId,
    order: { vulnerabilityLevel: DESC }
  ) {
    totalCount
    items {
      cve
      vulnerabilityLevel
      vulnerabilityScore
      description
      publicationDate
      triage {
        state
      }
    }
  }
}
```

### 6. Get Layers for a Specific Image

```
query GetImageLayers($scanId: String!) {
  layersByScan(
    scanId: $scanId,
    skip: 0,
    take: 20,
    order: {
      index: ASC
    }
  ) {
    items {
      id
      command
      index
      size
      packages {
        packageName
        packageVersion
      }
    }
    pageInfo {
      hasNextPage
      hasPreviousPage
    }
    totalCount
  }
}
```

### 7. Get Image Recommendations for Fixing Vulnerabilities

```
query GetImageRecommendations($scanId: String!, $imageId: String!){
  imagesByScan(
    scanId: "c9102440-67e2-49d9-a114-6b062db16dca"
    where: {
      imageName: { eq: "mysql" }
      imageTag: { eq: "5.7" }
    }
  ) {
    items {
      imageName
      imageTag
      recommendations {
        minorRecommendedImages {
          imageId
          criticalVulnerabilitiesCount
          highVulnerabilitiesCount
        }
        majorRecommendedImages {
          imageId
          criticalVulnerabilitiesCount
          highVulnerabilitiesCount
        }
        alternativeImageTags
      }
    }
  }
}
```

### 8. Search for Packages by Name Across All Images in a Scan

```
query SearchPackages($scanId: String!, $packageName: String!) {
  packagesByScan(
    scanId: $scanId,
    where: { packageName: { contains: $packageName } }
  ) {
    totalCount
    items {
      packageName
      packageVersion
      type
      maxRiskSeverity
      vulnerabilitiesCount
      images {
        imageName
        imageTag
      }
    }
  }
}
```

### 9. Get Recent Vulnerabilities (Published in the Last 30 Days)

```
query GetRecentVulnerabilities($scanId: String!, $date: DateTime!) {
  vulnerabilitiesByScan(
    scanId: $scanId,
    where: { publicationDate: { gte: $date } },
    order: { publicationDate: DESC }
  ) {
    totalCount
    items {
      cve
      description
      vulnerabilityLevel
      vulnerabilityScore
      publicationDate
      affectedPackages {
        packageName
        packageVersion
      }
    }
  }
}
```

### 10. Get Triage History for a Specific Image

```
query GetImageTriageHistory($scanId: String!, $imageId: String!) {
  scan(id: $scanId) {
    images(where: { id: { eq: $imageId } }) {
      imageName
      imageTag
      triage {
        status
        snoozeDate
        historyChanges {
          createDate
          user
          comment
          events {
            actionType
            newValue
            oldValue
          }
        }
      }
    }
  }
}
```

## Development Notes

### GraphQL Type Extensions

The API uses custom GraphQL type extensions to define the schema:

- **ApiClientGraphqlTypeAttribute**: Used to mark classes that should be exposed as GraphQL types
- **FilterInputType**: Used to define filtering capabilities for types
- **SortInputType**: Used to define sorting capabilities for types

### Pagination Implementation

The API uses offset-based pagination with the following options:

- **IncludeTotalCount**: Enables returning the total count of items
- **MaxPageSize**: Limits the maximum number of items that can be requested in a single page (1000 for all paginated queries)
- **DefaultPageSize**: Sets the default number of items per page if not specified

### Authorization

All queries require the `ContainerPermissions.ViewResults` permission, which is enforced at the operation level.

### Performance Considerations

- The API optimizes data fetching by retrieving related entities in parallel when possible
- For large datasets, pagination should be used to limit the amount of data returned
- When possible, specific endpoint methods (like `getVulnerabilitiesByScan`) should be used instead of traversing the entire object hierarchy

### Error Handling

- Invalid scan IDs or entity IDs will result in empty result sets rather than errors
- Authorization failures will result in standard GraphQL authorization errors
- Internal errors during data retrieval are logged and propagated as GraphQL errors

## Best Practices

### For Clients

1. **Use Pagination**: Always use pagination when retrieving large collections of data
2. **Limit Field Selection**: Only request the fields you need to minimize response size
3. **Use Flat Access Methods**: For direct access to entities across a scan, use the flat access methods rather than traversing the object hierarchy
4. **Filter Server-Side**: Use the provided filtering capabilities to filter data on the server rather than client-side
5. **Sort Server-Side**: Use the provided sorting capabilities to sort data on the server rather than client-side

### For Developers

1. **Maintain Consistency**: Follow the established patterns for adding new types and operations
2. **Consider Performance**: Be mindful of the performance implications of new queries or field resolvers
3. **Batch Operations**: Use batched data loading for new resolvers to minimize N+1 query issues
4. **Test with Large Datasets**: Ensure new operations perform well with large datasets
5. **Maintain Authorization**: Ensure all new operations enforce appropriate authorization
