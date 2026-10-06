# Too Many Secrets (2ms)

Too many secrets (2ms) is an open source tool, powered by Checkmarx, used for secret detection. It provides a CLI tool that enables you to identify sensitive data such as secrets, authentication keys and passwords that are stored in your system in unencrypted text. This application is written in Go language and is based on the framework provided by gitleaks.

The CLI tool supports scanning of internal communication platforms (Slack, Discord), content management (Confluence, Paligo) and source code storage locations (Git repo, local directory). It checks the content using a series of rules that are designed to identify a wide range of sensitive items such as AWS access token, Bitbucket Client ID, GitHub PAT etc.

Learn more and get the free tool [here](https://github.com/Checkmarx/2ms/blob/master/README.md).
