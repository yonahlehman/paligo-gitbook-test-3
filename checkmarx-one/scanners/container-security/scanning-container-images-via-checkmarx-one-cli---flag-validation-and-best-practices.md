# Scanning Container Images via Checkmarx One CLI - Flag Validation and Best Practices

## Overview

{% hint style="info" %}
This article focusses on the precise syntax for image references used in Checkmarx One CLI scans. For an explanation of the general procedure for running Container Security scans via the CLI, see [Running Container Security Scans via the CLI](README.md#running-container-security-scans-via-the-cli).
{% endhint %}

The `--container-images` flag accepts a comma-separated list of container image references. Each reference can be:

1. An image name with tag: `<image-name>:<image-tag>`
2. A tar file path: `<filename>.tar`
3. A prefixed reference using supported providers

{% hint style="info" %}
**Related Documentation:** See [Syft Supported Sources](https://checkmarx.atlassian.net/wiki/x/I4DCFAI) for more information about the underlying scanning engine capabilities.
{% endhint %}

## Supported Image Formats

### 1. Standard Image References (with tags)

- **Format:** `<image-name>:<tag>` or `<registry>/<namespace>/<image>:<tag>`
- **Examples:** `alpine:latest nginx:1.21 docker.io/library/ubuntu:22.04`

### 2. Tar Files (Docker/Podman saved images)

- **Format:** `<filename>.tar` or `file:<path/to/file>.tar`
- **Examples:** `my-image.tar file:./images/nginx.tar docker-archive:path/to/image.tar`
- **Note:** Images with 0 packages are automatically skipped and excluded from scan results.

### 3. OCI Directory Format (Skopeo/Buildah-created images)

- **Format:** `oci-dir:<path/to/oci/directory>` (tag is read from `index.json`)
- **Examples:** `oci-dir:docker.io/library/alpine oci-dir:/absolute/path/to/oci-image oci-dir:./my-alpine-image`
- **Important:** Tags are automatically extracted from the `index.json` file, not from the command line
- **Requirements:**
- Directory must contain valid OCI layout (`oci-layout`, `index.json`, `blobs/`)
- `index.json` must include `org.opencontainers.image.ref.name` annotation for tag extraction
- Image name is extracted from the last directory segment

### 4. Daemon References

- **Format:** `<daemon>:<image-name>:<tag>`
- **Supported:** `docker:`, `podman:`, `containerd:`, `registry:`
- **Examples:** `docker:nginx:latest podman:alpine:3.18 registry:myregistry.io/myimage:v1.0`

### 5. Archive Formats

- **Formats:** `docker-archive:`, `oci-archive:`, `file:`
- **Examples:** `docker-archive:./images/myimage.tar oci-archive:/path/to/image.tar`

## Supported Prefixes

| Prefix | Purpose | Expected Format | Example |
|---|---|---|---|
| `docker:` | Pull from Docker daemon | `image:tag` | `docker:nginx:latest` |
| `podman:` | Pull from Podman daemon | `image:tag` | `podman:alpine:3.18` |
| `containerd:` | Pull from containerd daemon | `image:tag` | `containerd:ubuntu:22.04` |
| `registry:` | Pull from registry | `image:tag` | `registry:myregistry.io/app:v1.0` |
| `docker-archive:` | Load from Docker tar archive | `path/to/file.tar` | `docker-archive:./image.tar` |
| `oci-archive:` | Load from OCI tar archive | `path/to/file.tar` | `oci-archive:/tmp/image.tar` |
| `oci-dir:` | Load from OCI directory layout | `path/to/dir` | `oci-dir:./oci-layout/` |
| `file:` | Load from file | `path/to/file.tar` | `file:./alpine.tar` |

## Image Name and Tag Extraction Rules

| Input Format | Image Name | Image Tag | Example |
|---|---|---|---|
| Standard registry | Last part before `:` | After `:` | `alpine:latest` → `alpine:latest` |
| OCI directory | Last directory segment | From `index.json` annotation | `oci-dir:docker.io/library/alpine` → `alpine:latest` |
| OCI archive | From filename (before first `_`) | From `index.json` annotation | `traefik_v2.tar` → `traefik:v2` |
| Tar file | From internal `manifest.json` | From `RepoTags` field | Extracted from tar contents |

## Using Skopeo with Checkmarx CLI - Best Practices

### What is Skopeo?

Skopeo is a command-line utility for working with container images without requiring a container runtime. Perfect for CI/CD environments where Docker/Podman daemons are not available.

### Installation

```
# macOS
brew install skopeo

# Ubuntu/Debian
sudo apt-get install skopeo

# Red Hat/CentOS/Fedora
sudo dnf install skopeo
```

### Best Practice: OCI Directory Format

**Recommended approach:** Save images in OCI directory format with proper annotations.

#### Step 1: Create OCI Directory

```
# Create structured directory
mkdir -p docker.io/library

# Copy image with tag annotation - IMPORTANT: include :tag in destination
skopeo copy --override-os linux --override-arch amd64 \
  docker://alpine:latest oci:docker.io/library/alpine:3.19
```

**Critical:** Always include the tag (`:latest`, `:3.19`) in the Skopeo **destination path** to ensure proper annotation in `index.json`. Without it, the CLI won't be able to determine the image tag.

#### Step 2: Verify Tag Annotation

```
cat docker.io/library/alpine/index.json | python3 -m json.tool
```

Expected output should include:

```
"annotations": {
  "org.opencontainers.image.ref.name": "3.19"
}
```

If this annotation is missing, the image will be skipped during scanning.

#### Step 3: Scan with CxOne CLI

```
cx scan create \
  --project-name my-project \
  -s ./source \
  --branch main \
  --scan-types container-security \
  --container-images "oci-dir:docker.io/library/alpine" \
  --containers-local-resolution
```

**Note:** Do NOT add the tag `:3.19` to the `--container-images` value. The tag is automatically read from `index.json`.

### Common Scenarios

#### Scenario 1: Private Registry with Authentication

```
# Save image with authentication
skopeo copy --src-creds username:password \
  --override-os linux --override-arch amd64 \
  docker://private-registry.com/myapp:v1.0 \
  oci:private-registry.com/myapp:v1.0

# Scan (no tag needed in CLI command)
cx scan create --project-name myapp \
  -s . --scan-types container-security \
  --container-images "oci-dir:private-registry.com/myapp" \
  --containers-local-resolution
```

#### Scenario 2: Multiple Images

```
# Save multiple images with tags
skopeo copy docker://nginx:1.21 oci:docker.io/library/nginx:1.21
skopeo copy docker://postgres:14 oci:docker.io/library/postgres:14

# Scan all (no tags in CLI command)
cx scan create --project-name my-app \
  -s ./source --scan-types container-security \
  --container-images "oci-dir:docker.io/library/nginx,oci-dir:docker.io/library/postgres" \
  --containers-local-resolution
```

#### Scenario 3: Multi-Architecture Images

```
# Save different architectures with tags
skopeo copy --override-arch amd64 \
  docker://alpine:latest oci:images/alpine-amd64:latest

skopeo copy --override-arch arm64 \
  docker://alpine:latest oci:images/alpine-arm64:latest

# Scan both architectures (no tags in CLI command)
cx scan create --project-name multi-arch \
  -s . --scan-types container-security \
  --container-images "oci-dir:images/alpine-amd64,oci-dir:images/alpine-arm64" \
  --containers-local-resolution
```

### Troubleshooting

#### Error: "no image tag found in OCI index.json annotations"

**Cause:** OCI directory created without tag annotation in the destination path.

**Solution:**

```
# Wrong - no tag in destination
skopeo copy docker://alpine:latest oci:my-alpine-image

# Correct - tag included in destination
skopeo copy docker://alpine:latest oci:my-alpine-image:latest
```

The tag must be specified in the Skopeo `copy` command's **destination** (after `oci:`), not in the CLI scan command.

#### Warning: "Image has 0 packages, skipping"

**Cause:** Image contains no analyzable packages or is corrupted/empty.

**Solution:** 1. Verify image integrity: `skopeo inspect oci:path/to/image` 2. Re-pull and save the image 3. Check if base image actually contains packages (e.g., `scratch` images have none)

#### Error: "path does not exist"

**Cause:** OCI directory path is incorrect or not accessible.

**Solution:** - Use absolute paths: `oci-dir:/absolute/path/to/image` - Or ensure relative paths are correct from the CLI execution directory

## Using Buildah with Checkmarx CLI - Best Practices

### What is Buildah?

Buildah is a tool that facilitates building OCI and Docker container images without requiring a container daemon. Like Skopeo, it's ideal for CI/CD environments and follows the same daemonless architecture. Buildah can both build images from scratch/Dockerfiles AND export them in various formats that are fully compatible with Checkmarx CLI.

### Installation (MacOS)

{% hint style="warning" %}
Buildah is Linux-only and does not have native macOS support.
{% endhint %}

The following options are available:

- Use Podman (which includes a Linux VM) **\[option1\]**
- or run Buildah in a container **\[option2\]**
- or run a containers and install Buildah **\[option3\]**

```
# brew install podman
# After installation, you must start the Podman machine
podman machine init
podman machine startx (Ubuntu/Debian)
sudo apt-get update
sudo apt-get install -y buildah

# Linux (Red Hat/CentOS/Fedora)
sudo dnf install -y buildah

# macOS - Buildah is not natively supported
# Option 1: Use Podman (includes Buildah-compatible functionality)
brew install podman
podman machine init --rootful
podman machine start

# Option 2: Run Buildah in a container with volume mount
podman run --rm -it --privileged -v $(pwd):/output quay.io/buildah/stable

# Option 3: Use Fedora (Docker or Podman installed and running on your macOS)
# Since Buildah requires a Linux kernel, run a privileged Fedora container
# on the macOS host to act as your test environment.

# Using Docker (or swap 'docker' for 'podman' if preferred)
docker run --rm -it --privileged -v $(pwd):/mnt/output fedora:latest bash

# 1. Install Buildah and standard tools (now that we are inside the Fedora container)
dnf -y install buildah curl

# 2. Install Syft (using standard installation script for quick setup)
curl -sSfL https://raw.githubusercontent.com/anchore/syft/main/install.sh | sh -s -- -b /usr/local/bin

# Verify installation
buildah version # Linux
podman --version # macOS
syft --version
```

### Best Practice: OCI Directory Format

**Recommended approach:** Build and save images in OCI directory format with proper tag annotations.

#### Step 1: Build Image with Buildah

```
# Option 1: Build from Dockerfile
buildah bud -t myapp:v1.0 .

# Option 2: Build from scratch (no Dockerfile)
buildah from scratch
buildah copy working-container /etc/os-release /
buildah commit working-container myapp:v1.0

# Option 3: Build from an existing image
# Create a working container from a specific, full image name - in this case, traefik:v2
new_container=$(buildah from docker.io/library/traefik:v2)

# You can now run commands, add files, or set config
buildah run $new_container -- touch /newfile.txt
buildah config --author "Your Name" $new_container

# Commit your changes to a new image
buildah commit $new_container myapp:v1.0
```

#### Step 2: Save to OCI Directory or Archive

```
# Option A: Push to OCI directory
# IMPORTANT: include :tag in destination
buildah push localhost/myapp:v1.0 oci:/output/docker.io/library/myapp:v1.0

# Option B: Save to docker-archive tar (includes tag in tar metadata)
# IMPORTANT: include both imagename and tag in destination
# in this case: myapp.tar:testapp:v1.0 -> file-name=myapp.tar, image-name=testapp, image-tag=v1.0)
buildah push localhost/myapp:v1.0 docker-archive:/output/myapp.tar:testapp:v1.0

# Option C: Save to oci-archive tar
# IMPORTANT: include :tag in destination
# in this case: myapp.tar:v1.0 -> image-name=myapp, image-tag=v1.0
buildah push localhost/myapp:v1.0 oci-archive:/output/myapp.tar:v1.0
```

**Critical:** Always include the tag (`:v1.0`, `:latest`) in the Buildah **destination path** to ensure proper annotation in `index.json` (for OCI formats) or tar metadata (for docker-archive). This is identical to Skopeo's requirement.

#### Step 3: Verify Tag Annotation (OCI Directory)

```
# Check that tag annotation exists
cat /output/docker.io/library/myapp/index.json | grep -A2 "annotations"

# Or use jq for formatted output
cat /output/docker.io/library/myapp/index.json | jq '.manifests[].annotations'
```

Expected output:

```
{
  "org.opencontainers.image.ref.name": "v1.0"
}
```

#### Step 4: Scan with CxOne CLI

```
# For OCI directory (Step 2 -> Option A)
cx scan create \
  --project-name myapp \
  -s ./source \
  --branch main \
  --scan-types container-security \
  --container-images "oci-dir:/output/docker.io/library/myapp" \
  --containers-local-resolution

# For docker-archive (Step 2 -> Option B)
cx scan create \
  --project-name myapp \
  -s ./source \
  --branch main \
  --scan-types container-security \
  --container-images "docker-archive:/output/myapp.tar"

# For oci-archive (Step 2 -> Option C)
cx scan create \
  --project-name myapp \
  -s ./source \
  --branch main \
  --scan-types container-security \
  --container-images "oci-archive:/output/myapp.tar"
```

**Note:** For OCI directory, the tag is NOT specified in the CLI command - it's automatically read from `index.json`.

### Common Scenarios

#### Scenario 1: Multi-Stage Dockerfile Build

```
# Build multi-stage Dockerfile
buildah bud -t frontend:v2.0 -f Dockerfile.frontend .

# Save to OCI directory with tag
buildah push frontend:v2.0 oci:builds/frontend:v2.0

# Scan
cx scan create --project-name frontend \
  -s . --scan-types container-security \
  --container-images "oci-dir:builds/frontend" \
  --containers-local-resolution
```

#### Scenario 2: Multiple Images from Same Build Context

```
# Build multiple images with different tags
buildah bud -t myapp:latest .
buildah bud -t myapp:v1.0 .
buildah bud -t myapp:stable .

# Save all with tags
buildah push myapp:latest oci:images/myapp:latest
buildah push myapp:v1.0 oci:images/myapp-v1:v1.0
buildah push myapp:stable oci:images/myapp-stable:stable

# Scan all versions
cx scan create --project-name myapp \
  -s . --scan-types container-security \
  --container-images "oci-dir:images/myapp,oci-dir:images/myapp-v1,oci-dir:images/myapp-stable" \
  --containers-local-resolution
```

#### Scenario 3: Private Registry Integration

```
# Pull from private registry, modify, and save for scanning
buildah pull --creds username:password private-registry.com/baseimage:v1.0
buildah bud -t myapp:v2.0 --from private-registry.com/baseimage:v1.0 .

# Save to OCI directory
buildah push myapp:v2.0 oci:registry-mirror/myapp:v2.0

# Scan
cx scan create --project-name myapp \
  -s . --scan-types container-security \
  --container-images "oci-dir:registry-mirror/myapp" \
  --containers-local-resolution
```

#### Scenario 4: Multi-Architecture Builds

```
# Build for different architectures
buildah bud --arch amd64 -t myapp:v1.0-amd64 .
buildah bud --arch arm64 -t myapp:v1.0-arm64 .

# Save each architecture
buildah push myapp:v1.0-amd64 oci:images/myapp-amd64:v1.0
buildah push myapp:v1.0-arm64 oci:images/myapp-arm64:v1.0

# Scan both architectures
cx scan create --project-name myapp \
  -s . --scan-types container-security \
  --container-images "oci-dir:images/myapp-amd64,oci-dir:images/myapp-arm64" \
  --containers-local-resolution
```

### Troubleshooting

#### Error: "no image tag found in OCI index.json annotations"

**Cause:** OCI directory created without tag annotation in the destination path.

**Solution:**

```
# Wrong - no tag in destination
buildah push myapp:v1.0 oci:myapp-dir

# Correct - tag included in destination
buildah push myapp:v1.0 oci:myapp-dir:v1.0
```

The tag must be specified in the Buildah `push` command's **destination** (after `oci:`), matching the Skopeo requirement.

#### Error: "Image has 0 packages, skipping"

**Cause:** Built image contains no analyzable packages (e.g., scratch-based images with only binaries).

**Solution:** 1. Verify image was built correctly: `buildah images` 2. Inspect image contents: `buildah inspect myapp:v1.0` 3. If using `FROM scratch`, ensure you're installing packages or using a base image with an OS 4. For minimal images, this is expected behavior - Checkmarx skips images with no packages

#### Issue: Buildah Image Not Found After Build

**Cause:** Image exists in Buildah's local storage but not properly tagged.

**Solution:**

```
# List all Buildah images
buildah images

# If image is missing tag, re-tag it
buildah tag <image-id> myapp:v1.0

# Then push with proper tag
buildah push myapp:v1.0 oci:path/to/dir:v1.0
```

#### Permission Issues on Linux

**Cause:** Buildah requires proper permissions for rootless operation.

**Solution:**

```
# Ensure subuid/subgid are configured
cat /etc/subuid
cat /etc/subgid

# Run buildah in rootless mode
buildah unshare buildah bud -t myapp:v1.0 .
```

### OCI Directory Tag Extraction Logic

When scanning OCI directories created with Skopeo or Buildah:

1. **Image Name:** Extracted from the last directory segment in the path - `oci-dir:docker.io/library/alpine` → Image Name: `alpine`
2. **Image Tag:** Extracted from `index.json` annotation (`org.opencontainers.image.ref.name`) - Tags are read from the OCI metadata, NOT from the command line - If multiple manifests exist, prefers tags that differ from the image name - Example: If manifests have tags "alpine" and "latest", prefers "latest"
3. **Fallback:** If no tag annotation found, the image is skipped with a warning

{% hint style="info" %}
**Note:** Unlike daemon sources (docker:, podman:), OCI directories do NOT support explicit tag syntax like `oci-dir:path:tag`. Tags must be embedded in the OCI directory's `index.json` file.
{% endhint %}

## Examples

### Valid Inputs

```
# Standard image with tag
--container-images "nginx:latest"

# Multiple images
--container-images "nginx:latest,alpine:3.18,ubuntu:22.04"

# With spaces (normalized)
--container-images "nginx:latest, alpine:3.18, ubuntu:22.04"

# With quotes (normalized)
--container-images "'nginx:latest', 'alpine:3.18'"

# Local tar file
--container-images "alpine.tar"

# Absolute path tar file
--container-images "/path/to/image.tar"

# File prefix
--container-images "file:alpine.tar"

# File prefix with quotes
--container-images "file:'/path/to/image.tar'"

# Docker daemon
--container-images "docker:nginx:latest"

# Docker archive
--container-images "docker-archive:./saved-image.tar"

# OCI archive
--container-images "oci-archive:/tmp/oci-image.tar"

# OCI directory (tag from index.json)
--container-images "oci-dir:docker.io/library/alpine"

# OCI directory with relative path
--container-images "oci-dir:./my-alpine-image"

# OCI directory with absolute path
--container-images "oci-dir:/home/user/images/alpine"

# Registry
--container-images "registry:myregistry.io/myapp:v1.0"

# Mixed formats
--container-images "nginx:latest,file:alpine.tar,oci-dir:docker.io/library/postgres"
```

### Invalid Inputs

```
# Missing tag (non-prefixed)
--container-images "nginx"
# Error: image does not have a tag

# Non-existent tar file
--container-images "nonexistent.tar"
# Error: file 'nonexistent.tar' does not exist

# Compressed tar
--container-images "image.tar.gz"
# Error: file 'image.tar.gz' is compressed, use non-compressed format (tar)

# Wrong extension (looks like tar)
--container-images "image.tar.bz"
# Error: image does not have a tag. Did you try to scan a tar file?

# File prefix with image name
--container-images "file:nginx:latest"
# Error: file 'nginx:latest' does not exist. Did you try to scan an image using image name and tag?

# Archive prefix with image name
--container-images "docker-archive:nginx:latest"
# Error: file 'nginx:latest' does not exist. Did you try to scan an image using image name and tag?

# OCI directory without tag annotation in index.json
--container-images "oci-dir:path/to/oci-dir"
# Warning: no image tag found in OCI index.json annotations (image skipped)

# OCI directory with explicit tag (NOT SUPPORTED)
--container-images "oci-dir:./my-image:latest"
# Will fail: tries to read ./my-image:latest/index.json which doesn't exist
# Use "oci-dir:./my-image" instead (tag read from index.json)

# Tar file with tag suffix (invalid)
--container-images "oci-dir:image.tar:latest"
# Error: tar files cannot have tags
```

## Error Messages

### Consolidated Error Format

When validation fails, all errors are collected and presented in a single, user-friendly message:

```
User input error for --container-images flag. Expected format: <image-name>:<image-tag> or <filename>.tar,
or use a supported prefix (docker:, podman:, containerd:, registry:, docker-archive:, oci-archive:, oci-dir:, file:)

  - User input: 'check.tar' error: file 'check.tar' does not exist
  - User input: 'alpine' error: image does not have a tag
  - User input: 'test.tar.gz' error: file 'test.tar.gz' is compressed, use non-compressed format (tar)
```

### Error Types with Helpful Hints

| Error Type | Error Message | Helpful Hint |
|---|---|---|
| Missing tag | `image does not have a tag` | - |
| Looks like tar | `image does not have a tag` | `Did you try to scan a tar file?` |
| File not found (with colon) | `file 'X' does not exist` | `Did you try to scan an image using image name and tag?` |
| Compressed tar | `file 'X' is compressed, use non-compressed format (tar)` | - |
| File not found | `file 'X' does not exist` | - |
| OCI missing tag | `no image tag found in OCI index.json annotations` | Image skipped with warning |
| OCI archive missing tag | `no image tag found in OCI archive index.json annotations` | Image skipped with warning |
| OCI explicit tag | Path with `:tag` suffix fails | Use path without tag, embed in index.json |
