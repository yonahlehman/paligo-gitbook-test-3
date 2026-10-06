# Checkmarx One CLI Tool

Checkmarx One CLI is a standalone tool.

The tool is a fully functional Command Line Interface (CLI) that interacts with the Checkmarx One server.

The tool is able to perform all the functions that the REST APIs support, so the CLI users can perform all the tasks that are related to managing the Checkmarx One server.

The CLI tool supports the following actions:

- Manage Checkmarx projects (create / delete / show)
- Manage Checkmarx scanning (create / cancel / delete / show)
- Display scan results

The CLI also acts as the backbone for all the supported plugins. All the plugins use the CLI tool to initiate scans. This allows minimal updates to the plugins which decreases the need for constant updates and feature requests.

The tool is universal, managing all the Checkmarx One scan types (SAST, SCA, IaC Security, etc.)

## Supported OSs

The CLI should generally work on recent versions of Windows, Linux and MacOS on the architectures that we support.

The following is a list of versions that were **tested** and found to work reliably:

- Windows:

  - Client Versions: Windows 11 , Windows 10
  - Server Versions: Windows Server 2019 , Windows Server 2012 , Windows Server 2022, Windows Server 2016
- Linux: RedHat 8.9, Amazon Linux 2, Fedora 34, Ubuntu 20.4.3, CentOS 8
- MacOS tested version: Sequoia 15.5 (should work fine on later versions as well)

## In this section

- [Checkmarx One CLI Quick Start Guide](checkmarx-one-cli-quick-start-guide.md)
- [Downloading and Installing the Checkmarx One CLI](downloading-and-installing-the-checkmarx-one-cli.md)
- [Configuring the Checkmarx One CLI](configuring-the-checkmarx-one-cli/README.md)
- [Running Scans via the CLI](running-scans-via-the-cli.md)
- [Checkmarx One CLI Commands](checkmarx-one-cli-commands/README.md)
- [CLI Plugin - Changelog](cli-plugin---changelog.md)
