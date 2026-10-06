# Checkmarx One Maven Plugin

The Checkmarx One **Maven Plugin** enables you to interact with Checkmarx One directly from a Maven lifecycle phase. It provides a wrapper around the *Checkmarx One CLI Tool*. The plugin provides easy integration into Maven while using the full functionality and flexibility of the CLI tool.

{% hint style="info" %}
The plugin code can be found [here](https://github.com/CheckmarxDev/ast-cli-maven-plugin).
{% endhint %}

## Main Features

- Use any CLI command from a Maven lifecycle phase

## Prerequisites

- You have a Checkmarx One account and you have an **OAuth Client** or **API Key** for Checkmarx One authentication. To generate the required authentication, see [Authentication for Checkmarx One CLI and Plugins](../authentication-for-checkmarx-one-cli-and-plugins/README.md).

## Checkmarx One Maven Plugin Initial Setup

Before running Checkmarx One CLI commands from a Maven lifecycle phase, you need to configure access to Checkmarx One. This is done by specifying the server URLs, tenant account, and authentication credentials for accessing your Checkmarx One environment. There are two methods for doing this:

- Environment Variables
- Global Flags

Checkmarx One uses the following URLs, depending on your environment:

- **Server URL**

  **Checkmarx One Server Base URLs**

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
- **Checkmarx One Cloud Platform Authentication URL**

  **Checkmarx One Authentication URLs**

  - US Environment - https://iam.checkmarx.net
  - US2 Environment - https://us.iam.checkmarx.net
  - EU Environment - https://eu.iam.checkmarx.net
  - EU2 Environment - https://eu-2.iam.checkmarx.net
  - DEU Environment - https://deu.iam.checkmarx.net
  - Australia & New Zealand – https://anz.iam.checkmarx.net
  - India - https://ind.iam.checkmarx.net
  - Singapore - https://sng.iam.checkmarx.net
  - UAE - https://mea.iam.checkmarx.net
  - Israel - https://gov-il.iam.checkmarx.net

{% hint style="warning" %}
**Don’t** include your credentials directly in your pom.xml. Use environment variables or properties instead.
{% endhint %}

## Running CLI Commands Using the Checkmarx One Maven Plugin

You can run any CLI command using the Maven plugin, including running scans, retrieving scan results and CRUD actions on Projects and Applications. For an explanation of the CLI commands, see Checkmarx One CLI Commands.

**To run a Checkmarx One CLI command in Maven:**

1. Activate the plugin by specifying the **artifactId**: `ast-cli-maven-plugin` and the current **version** of the plugin.
2. Run Maven in the lifecycle phase `test`, with the goal of `run`.
3. Enter the CLI Command and the request parameters under **configuration** > **arguments**.

### Usage Example - Running a Checkmarx One Scan Using the Plugin

The following snippet shows how you can run a Checkmarx One scan in Maven using the Checkmarx One Maven plugin.

The snippet uses the `scan create` command with the minimum required parameters `-s` (location of the source code), `--project-name` (name of the Checkmarx One Project), and `--branch` (name of the branch of the Checkmarx One Project).

```
    <build>
        <plugins>
            <!-- Checkmarx One CLI Maven Plugin -->
            <plugin>
                <groupId>com.checkmarx</groupId>
                <artifactId>ast-cli-maven-plugin</artifactId>
                <version>0.0.1</version>
                <executions>
                    <execution>
                        <phase>
                            test
                        </phase>
                        <goals>
                            <goal>
                                run
                            </goal>
                        </goals>
                        <configuration>
                            <arguments>scan create -s . --project-name ${project.artifactId} --branch master</arguments>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
```

## Running a Checkmarx One Scan in Maven Using the Checkmarx One CLI Tool

There is an alternative method for accessing Checkmarx One functionality in Maven without using the plugin. In this case you would simply use the standard Checkmarx One CLI Tool directly in Maven. The following example shows how to run a scan using this method.

```
    <build>
        <plugins>
            <!-- Generic exec-maven-plugin -->
            <plugin>
                <groupId>org.codehaus.mojo</groupId>
                <artifactId>exec-maven-plugin</artifactId>
                <version>3.0.0</version>
                <executions>
                    <execution>
                        <phase>
                            test
                        </phase>
                        <goals>
                            <goal>exec</goal>
                        </goals>
                    </execution>
                </executions>
                <configuration>
                    <executable>/path/to/cx</executable>
                    <arguments>
                        <argument>scan</argument>
                        <argument>create</argument>
                        <argument>-s</argument>
                        <argument>.</argument>
                        <argument>--project-name</argument>
                        <argument>${project.artifactId}</argument>
                        <argument>--branch</argument>
                        <argument>master</argument>
                    </arguments>
                </configuration>
            </plugin>
        </plugins>
    </build>
```

{% hint style="info" %}
Check for updates to the code samples in [GitHub](https://github.com/CheckmarxDev/ast-cicd-templates/tree/main/Maven).
{% endhint %}
