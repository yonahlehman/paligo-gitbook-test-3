# Container Security Filter Usage

Checkmarx One offers robust settings to enhance container security by enabling users to configure their scans for precision and relevance. Below is an explanation of the four available settings, designed to reduce noise and focus on critical vulnerabilities in your scans.

## Overview

The following table provides an overview of the functionality of each filter. Additional details about the usage and syntax for these filters is available in the following sections.

| Filter name | Description | Syntax | Examples |
|---|---|---|---|
| Folder/file filter | Specify **files and folders** to be included (allow list) or excluded from (block list) scans. You can create complex filters that combine include and exclude patterns. | `*.abc` - include specific file types<br>`!*.abc` - exclude specific file types<br>`!/folder-name/` - exclude a specific folder<br>{% hint style="success" %}<br>You can submit multiple items separated by a comma.<br>{% endhint %} | `!Dockerfile*` - exclude all Dockerfiles in the root folder<br>`*.yaml,*.yml` - include all yaml and yml files |
| Image/tag filter | Include or exclude **images** by image name and/or tag. | `image-name:image-tag` - include by image name and tag<br>`image-name` - include by image name<br>`!:image-tag` - exclude by image tag<br>{% hint style="success" %}<br>You can use wildcard (\*) at the beginning, end or both.<br>{% endhint %} | `!*test-image*` - to exclude all images that contain "test-image" in their name<br>`!:*latest` - to exclude all image tags that end with "latest" |
| Package Regex Filter | Prevent sensitive **packages** from being sent to the cloud for analysis. Exclude packages by package name or file path using regex.<br>{% hint style="success" %}<br>Excluded packages will nonetheless appear in the scan results. However, no vulnerabilities will be identified in those packages since their info wasn't sent to the cloud for analysis.<br>{% endhint %} | Regex | `^internal-.*` - filters out any package names starting with "internal-" |
| Exclude non-final stages filter | Exclude all images that are not from the final stage of the build process, so that only the final deployable image is scanned.<br>{% hint style="success" %}<br>Only supported for Dockerfile images.<br>{% endhint %} | True - apply filter<br>False - don't apply filter | |

## Filter Usage Details

The following sections provide syntax details and usage examples for Container Security filters.

### Folder/File Filter

The File/Folder Filter allows you to include or exclude specific files or folders from container security scans. This allows for greater flexibility and precision in your scans. Note that file and folder matching is case-sensitive.

#### Filter rules

The File/Folder Filter allows you to specify patterns to include or exclude files and folders. By default, all files and folders in the container are included in the scan, so most use cases only require exclusion rules - add a `!` prefix to exclude a path. Inclusion patterns (without `!`) are only needed when you want to re-include something within a broader exclusion, for example to re-include a specific subfolder after excluding its parent directory.

- `*.extension`: Includes/Excludes files with a specific extension at the root level. For example, `*.yaml` will include/exclude all files ending in `.yaml` in the root directory.
- `**/filename`: Includes/Excludes files with a specific name at any level within the directory structure. For example, `**/Dockerfile` will include/exclude any file named `Dockerfile` anywhere in the container.
- `folder-name/**`: Includes/Excludes a specific folder at the root level and all its contents. For example, `config/**` will include/exclude the `config` folder and everything inside it.
- `**/folder-name/**`: Includes/Excludes a specific folder at any level and all its contents. For example, `**/tests/**` will include/exclude the `tests` folder and all its subfolders and files, regardless of where the `tests` folder is located.
- `!`: The exclamation mark `!` is used as a prefix to *exclude* files or folders that match the pattern.

##### Important notes

- Patterns are case-sensitive. `Dockerfile` is different from `dockerfile`.
- Multiple patterns can be specified, separated by commas.
- The order of patterns matters, especially when combining inclusions and exclusions. For example, if you include a directory and then exclude a sub-directory, the exclusion will take precedence.
- Wildcards (`*`) can be used within patterns. `*` matches zero or more characters.

#### Usage examples

1. **Include all YAML files at the root level:**

   ```
   *.yaml
   ```
2. **Include all Dockerfiles at any level:**

   ```
   **/Dockerfile
   ```
3. **Include the** `config` **folder and its contents at the root level:**

   ```
   config/**
   ```
4. **Include the** `tests` **folder and its contents at any level:**

   ```
   **/tests/**
   ```
5. **Exclude a Dockerfile at the root level:**

   ```
   !Dockerfile
   ```
6. **Exclude all Dockerfiles at any level:**

   ```
   !**/Dockerfile, !**/dockerfile (Note: Case-sensitive, so both are needed)
   ```
7. **Exclude "Dockerfile", "Dockerfile-test", and "DockerfileCI" inside the "Tests" directory at any level:**

   ```
   !**/Tests/Dockerfile*
   ```
8. **Exclude all files and folders inside the "Tests" directory at any level:**

   ```
   !**/Tests/**
   ```
9. **Include all YAML files within the "YamlFiles" directory at any level:**

   ```
   **/YamlFiles/*.yaml
   ```
10. **Combined inclusion and exclusion:**

    ```
    *.yaml, **/Dockerfile, !**/test_files/**, !*.log
    ```

    This example includes all `.yaml` files at the root level, all `Dockerfile` files at any level, *but excludes* any files or folders within the `test_files` directory at any level, and also excludes all `.log` files at the root level.

### Image/Tag Filter

The Image/Tag Filter allows you to include or exclude container images from scans. It uses simple wildcard matching, not regular expressions.

#### Filter rules

The Image/Tag Filter allows you to specify patterns to include or exclude images based on their name and tag. Exclusion is performed by placing a `!` character at the start of the pattern. If no `!` is present, the pattern is treated as an inclusion rule. However, it is generally recommended to use exclusion rules (`!`) for most scenarios.

- `!image-name:image-tag`: Excludes a specific image and tag. For example, `!my-app:latest` will exclude the `my-app` image with the `latest` tag.
- `!image-name`: Excludes any tag for the given image name. For example, `!my-app` will exclude the `my-app` image, regardless of its tag (e.g., `my-app:latest`, `my-app:dev`, etc.).
- `!*:image-tag`: Excludes any image with the given tag. For example, `!*:dev` will exclude any image that has the `dev` tag, regardless of its name.
- `*`: A wildcard that matches zero or more characters. This is used *within* the patterns (like `!*test*`) and isn't a standalone exclusion rule. It's used to create patterns like `!*test*` (contains "test") or `!*:dev` (ends with "dev").

##### Important notes

- Exclusion patterns start with `!`. Inclusion patterns (without `!`) are possible, but usually not necessary since all images are included by default unless specifically excluded.
- Multiple patterns can be specified, separated by commas.
- Wildcards (`*`) are used to match parts of image names or tags.
- Matching is generally case-sensitive.

#### Usage examples

1. **Exclude a specific image and tag:**

   ```
   !my-database:production
   ```

   This will exclude the `my-database` image with the `production` tag.
2. **Exclude all images with a specific tag:**

   ```
   !*:staging
   ```

   This will exclude all images that have the `staging` tag, regardless of their name.
3. **Exclude all versions of a specific image:**

   ```
   !web-server
   ```

   This will exclude the `web-server` image, no matter what tag it has.
4. **Exclude images containing a specific string in their name:**

   ```
   !*test*
   ```

   This will exclude any image whose name contains the string "test" (e.g., `integration-test-image`, `unit-test-runner`).
5. **Exclude images with a specific tag prefix:**

   ```
   !*:rc*
   ```

   This will exclude any images with tags that *contain* the string `rc`. For example, it would exclude images tagged `rc1`, `rc2-beta`, `my-app:rc-final`, etc.
6. **Combined exclusions:**

   ```
   !my-database:v1, !*:dev, !another-service
   ```

   This will exclude:

   - The `my-database` image with the `v1` tag.
   - All images with the `dev` tag.
   - All versions of the `another-service` image.

### Package Regex Filter

The Package Regex Filter allows you to exclude private packages from the payload sent to the Checkmarx One SCA cloud. This is achieved using regular expressions.

#### Filter rules

The Package Regex Filter allows you to specify regular expression patterns to identify and exclude packages (e.g., private packages). Filters are applied to package *names* only; file paths or specific filenames are not considered.

- **Regular Expression:** A regular expression (regex) is a powerful pattern-matching language. It allows you to define complex search criteria.
- **Matching:** The filter uses your provided regex to match against package names. Matching packages are *excluded* from the scan.

##### Important notes

- The regex is applied to the *package name* only, not the full file path.
- The matching is case-sensitive.

#### Usage examples

Exclude private packages matching the pattern `^internal-.*`. This regex filters out any package names starting with "internal-".

**Explanation of the Example Regex** `^internal-.*` **:**

- `^`: This symbol means "the beginning of the string." The package name must start here.
- `internal-`: This is the literal text that must be present at the beginning of the package name.
- `.*`: This part means "any character (except newline) zero or more times." It allows for any characters to follow "internal-".

**Examples of Matching Package Names:**

- `internal-data`
- `internal-api`
- `internal-123`
- `internal-`
- `internal-something-else`

**Examples of Package Names That Do NOT Match:**

- `external-data` (doesn't start with "internal-")
- `data-internal` (doesn't start with "internal-")
- `_internal-data` (doesn't start with "internal-")

**Creating Your Own Regex Patterns:**

You can adjust the regex based on your specific needs. Here are some general tips:

- Refer to online regex resources or tutorials to learn more about regex syntax. There are many excellent resources available.
- Test your regex patterns using online regex testers to ensure they match the package names you intend to exclude.
- Common regex elements include:

  - `^`: Matches the beginning of a string.
  - `$`: Matches the end of a string.
  - `.`: Matches any single character (except newline).
  - `*`: Matches the preceding element zero or more times.
  - `+`: Matches the preceding element one or more times.
  - `[abc]`: Matches any one of the characters a, b, or c.
  - `[a-z]`: Matches any character from a to z.
  - `\d`: Matches any digit.
  - `\w`: Matches any word character (letters, numbers, underscore).

### Exclude Non-Final Stages Filter

This setting controls whether or not intermediate stages of a Docker image build process are included in security scans. Enabling this filter helps reduce noise by focusing solely on the final, deployable image.

**Limitations:**

- **Dockerfile Focus:** This filter operates only on Dockerfiles.

**Possible Values:**

- `True`: Enables the filter. Only the final stage of the Dockerfile will be scanned.
- `False`: Disables the filter (default). All stages of the Dockerfile, including intermediate stages, will be scanned.

**Use Case Example:**

Exclude intermediate build stages (like builder or intermediate stages) to focus solely on the final deployable image.

**Example Dockerfile:**

```
Dockerfile
```

```
# Stage 1: Builder stage (intermediate)
FROM ubuntu:latest AS builder
RUN apt-get update && apt-get install -y --no-install-recommends some-build-tools
WORKDIR /app
COPY. /app
RUN make my-application

# Stage 2: Final stage (deployable)
FROM nginx:latest
COPY --from=builder /app/my-application /usr/share/nginx/html
```

**Behavior:**

- **Without the filter (default -** `False` **):** A security scan will analyze *both* stages:

  1. The `ubuntu:latest` stage (builder stage), which might contain build tools, dependencies, and temporary files that are *not* in the final image. This stage could have vulnerabilities that are irrelevant to the deployed application.
  2. The `nginx:latest` stage (final stage), which contains the built application and the web server.
- **With the filter enabled (** `True` **):** The scan will *only* analyze the `nginx:latest` stage. The `ubuntu:latest` stage (the builder stage) will be skipped.

**Benefits of Enabling the Filter:**

- **Reduced Noise:** You avoid getting alerts about vulnerabilities in build tools or intermediate files that are not present in your final, deployed image. This makes it easier to focus on real security risks.
- **Faster Scans:** Scanning only the final stage can significantly speed up the scanning process, especially for complex Dockerfiles with many stages.
- **More Relevant Results:** The scan results are more focused and relevant to your actual deployment environment.

**In summary:** The filter helps you focus your security efforts on the image that is actually being deployed, ignoring the potentially messy or insecure intermediate steps used to build it.

## Applying Filters in the Checkmarx One CLI

All of the filters described above can also be applied when running the `scan create` command via the Checkmarx One CLI tool. This focused approach improves scan efficiency and helps prioritize critical vulnerabilities. These filters can be combined for even more granular control. This section explains how to use the filters in the CLI tool.

**File/Folder Exclusion (** `--containers-file-folder-filter` **)**

To exclude files or folders from the scan, use the `--containers-file-folder-filter` parameter. For example, to exclude all `Dockerfile` files:

```
Bash
```

```
./cx scan create --project-name MyProject --branch Main --scan-types container-security -s /projects/myproject.zip --containers-file-folder-filter '!**/Dockerfile'
```

**Image Exclusion (** `--containers-image-tag-filter` **)**

The `--containers-image-tag-filter` parameter allows you to exclude specific container images based on their tag. The following example excludes all versions of the `postgres` image:

```
Bash
```

```
./cx scan create --project-name MyProject --branch Main --scan-types container-security -s /projects/myproject.zip --containers-image-tag-filter '!*postgres:*'
```

**Excluding Non-Final Stages (** `--containers-exclude-non-final-stages` **)**

To exclude images built from non-final stages within Dockerfiles, set the `--containers-exclude-non-final-stages` parameter to `true`:

```
Bash
```

```
./cx scan create --project-name MyProject --branch Main --scan-types container-security -s /projects/myproject.zip --containers-exclude-non-final-stages=true
```

**Package Exclusion (** `--containers-package-filter` **)**

You can exclude packages using regular expressions with the `--containers-package-filter` parameter. For instance, to exclude packages starting with `internal-`:

```
Bash
```

```
./cx scan create --project-name MyProject --branch Main --scan-types container-security -s /projects/myproject.zip --containers-package-filter ‘^internal-.*’
```

**Combining Filters**

You can combine these filters to create complex exclusion rules. For example, to exclude all Dockerfiles *and* all versions of the `redis` image, you would use:

```
Bash
```

```
./cx scan create --project-name MyProject --branch Main --scan-types container-security -s /projects/myproject.zip --containers-file-folder-filter '!**/Dockerfile' --containers-image-tag-filter '!*redis:*'
```

This command will exclude both the specified files and images, providing a more refined scan.
