# Pre-Commit Secret Scanning

## Overview

The Pre-Commit Secret Scanning feature helps prevent accidental exposure of sensitive information such as passwords, API keys, and access tokens. If secrets are detected, the commit is blocked, and developers receive a detailed report to help remediate the issue.

This feature supports both local and global installation modes. In **local installations**, it uses the [pre-commit framework](https://pre-commit.com/); in **global mode**, it installs the hook directly at the Git level without requiring the framework.

The Pre-Commit Secret Scanning feature is available to users with a Secret Detection license.

## Requirements

- Checkmarx One CLI. For the instructions on downloading and installing the Checkmarx One CLI, refer to [this page](https://docs.checkmarx.com/en/34965-68622-checkmarx-one-cli-installation.html).
- Pre-commit framework (for local installations only)
- Git
- Python (required by pre-commit)
- A valid **Secret Detection** license

## Difference Between Local and Global Installation

| | **Local Installation** | **Global Installation** |
|---|---|---|
| **Scope** | Specific to one Git repository | Applied to all Git repositories, both existing and new. |
| **Config Location** | `.pre-commit-config.yaml` is added to the repository root | Config is placed in the Git global template directory |
| **Hook Application** | Installed only in the selected repository | Installed in all repositories, both existing and new |
| **Flexibility** | Ideal for project-specific settings | Useful for enforcing organization-wide policies |
| **Override Behavior** | Does not override existing pre-commit hooks | Adds config to template; will not override if already set manually |

{% hint style="warning" %}
Do not install both globally and locally on the same machine. This may lead to conflicts or duplicate scans.
{% endhint %}

## Running Secret Detection Locally

To install and run the pre-commit hook for a **single repository**:

1. Navigate to the repository directory:
2. Install the pre-commit hook locally by running:

   ```
   cx hooks pre-commit secrets-install-git-hook
   ```
3. This will:

   - Install the hook and configure it to run on every commit.
   - Automatically add a `.pre-commit-config.yaml` file to the repository root. This file defines the hook to run the `cx secrets-scan` command using the Checkmarx CLI. Example content of the file is shown below:

   ```
   repos:
     - repo: local
       hooks:
         - id: cx-secret-detection
           name: Cx Secret Detection
           entry: cx
           description: Run Cx CLI secret detection
           stages:
             - pre-commit
           args:
             - hooks
             - pre-commit
             - secrets-scan
           language: system
           pass_filenames: false
           minimum_pre_commit_version: 3.2.0
   ```
4. When you attempt to commit a file containing a secret, the pre-commit hook runs automatically. It detects a secret in `secret.txt` and blocks the commit.

   The console output shows:

   - The detection status (`Failed`)
   - The file and line where the secret was found
   - The type of secret (e.g., `github-pat`)
   - A risk score
   - A masked version of the detected secret
   - A unique result ID.

For example:

```
Cx Secret Detection............................Failed
- hook id: cx-secret-detection
- exit code: 1

Commit scanned for secrets:
Detected 1 secret in 1 file

#1 File: secret.txt
1 Secret detected in file

Secret detected: github-pat
Result ID: 26e21a528aa2799cbbef30e4b47f6971f64a40f4
Risk Score: 8.2
Location: Line 1
  1 | ghp_*******************************
```

### Options for proceeding with the commit

After the scan fails, the CLI provides **three possible paths** for proceeding, clearly indicating which options are recommended and which are discouraged:

#### Option 1: Remediate Detected Secrets (Recommended)

This is the safest and recommended approach. The developer should:

1. Remove the secrets from the source file.
2. Store them securely using any of the following methods:

   - Environment variables
   - Secret management tools (e.g., HashiCorp Vault, AWS Secrets Manager)
   - Configuration management systems
   - Encrypted files (least secure)
3. Commit the cleaned or updated file.

This method ensures secrets don’t accidentally get stored in source control or exposed to others.

#### Option 2: Ignore Detected Secrets (Not Recommended)

If the developer is confident the secret is a false positive or not a risk, they may choose to ignore it using one of the following commands:

- To ignore **all** currently detected secrets:

  ```
  cx hooks pre-commit secrets-ignore --all
  ```
- To ignore specific results using their IDs (as shown in the scan output):

  ```
  cx hooks pre-commit secrets-ignore --resultIds=ID1,ID2
  ```

{% hint style="info" %}
If the developer chooses to ignore a detected secret, only the secret’s hash is saved to the `.checkmarx_ignore` file - **not the secret itself**.

The full details of the secret are shown only at the time of the commit. After the secret is ignored, only its hash is retained for future reference, ensuring the secret itself is not exposed or stored elsewhere.
{% endhint %}

#### Option 3: Bypass the Hook Entirely (Not Recommended)

For urgent situations or testing, the hook can be bypassed. This skips the secret scan entirely.

**Commands vary by shell/OS:**

- **Bash/Zsh**:

  ```
  SKIP=cx-secret-detection git commit -m "<your message>"
  ```
- **Windows CMD**:

  ```
  set SKIP=cx-secret-detection && git commit -m "<your message>"
  ```
- **PowerShell**:

  ```
  $env:SKIP="cx-secret-detection"
  ```

{% hint style="warning" %}
Bypassing the scan removes all guardrails and may result in secrets being committed to your repository.
{% endhint %}

## Running Secret Detection Globally

When secret scanning is configured globally, the hook will be applied to **all Git repositories** on the machine. This is ideal for enforcing organization-wide secret detection without modifying individual projects.

To enable global secret detection, run the following command:

```
cx hooks pre-commit secrets-install-git-hook --global
```

The output confirms that the hook is installed in the Git global template directory:

```
Installing global pre-commit hooks...
cx-secret-detection hook installed successfully.
```

After running the command, a pre-commit hook is created at `C:\Users\[username]\.git\hooks\precommit` with the following content:

```
#!/bin/sh
cx hooks pre-commit secrets-scan
```

{% hint style="info" %}
The global hook does not use a `.pre-commit-config.yaml` file and does not rely on the Python pre-commit package.
{% endhint %}

Before the hook can work, each developer must:

1. Download and unzip the cx CLI tool.
2. Add the CLI location to their system PATH environment variable, or manually edit the precommit script to point to the full path of the CLI executable.

Without these steps, the hook will fail to run the scan properly.

## Uninstall

To remove the pre-commit secret detection hook, run one of the following commands:

- **Local uninstall** (from a specific repo):

  ```
  cx hooks pre-commit secrets-uninstall-git-hook
  ```
- **Global uninstall**:

  ```
  cx hooks pre-commit secrets-uninstall-git-hook --global
  ```

The CLI responds with confirmation:

```
Uninstalling cx-secret-detection hook... cx-secret-detection hook uninstalled successfully.
```

This command:

- Removes the pre-commit hook from `.git/hooks/pre-commit`
- Leaves the `.checkmarx_ignore` files intact (you may remove them manually if needed)
