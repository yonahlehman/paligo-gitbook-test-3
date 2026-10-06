# JFrog Artifactory Integration for SCA Scanner

## Step 1 - Setting up an Integration

**To set up a JFrog Artifactory Private Artifactory Integration:**

1. In the main navigation, select **Integrations** <img src="../../../assets/Integrations.png" alt="" data-size="line">> **Cloud Connections**.
2. In the **Setup** tab, under **Private Registries for Containers**, hover over the **JFrog Artifactory** tile and click on **Configuration**. then click **Start**.
3. In the side panel that opens, click **Start**.

   The **JFrog Artifactory Integration** wizard opens.

   <figure><img src="../../../assets/Image_1784.png" alt="" width="360"><figcaption></figcaption></figure>
4. **Name Your Account** and optionally fill in the **Description** and **Associate Tags** fields, then click **Next**.

   Make a note of the name that you designated, as you will need to use this name in the following step.
5. Under **Username** enter the Username for your JFrog account.

   <figure><img src="../../../assets/Image_1784.png" alt="" width="360"><figcaption></figcaption></figure>
6. In the **API Key** field, enter the API key for your JFrog Artifactory (as described above in Prerequisites).
7. In the **URL** field, enter the URL for your JFrog account using the format `https://<subdomain>.jfrog.io`.

   Alternatively, if you have configured a CxLink to access this repo, enter the CxLink (using the following format: https://\<subdomain>.\<domain>/link/\<UUID>). Learn more about CxLink here.
8. Click **Add Account**.

### Monitoring Integration Status

You can monitor the status of your JFrog integrations to see whether or not the integration is connected. Possible statuses are:

- **Pending** - The integration was just set up and hasn't connected yet.
- **Connected** - The integration is running and you are able to scan images in your JFrog Artifactory.
- **Disconnected** - Checkmarx One is not currently able to access your private JFrog Artifactory.

**To monitor the integration status:**

1. In the main navigation, select **Integrations** <img src="../../../assets/Integrations.png" alt="" data-size="line">> **Cloud Connections**.
2. In the **Cloud Connections** tab, check the **Status** column for each of your integrations.

### Step 2 - Project Configuration

For each project you want to scan, you must configure access to your private package repositories. This is done by using the templates provided below and applying them to your project configuration.

1. **Prepare the configuration template**

   Copy the relevant template and replace the placeholder \<MASK_NAME> with the name of the integration you defined in the JFrog integration wizard in the previous step.

   **Templates**

   **Nuget**

   **./.checkmarx/sca/nuget/NuGet.Config**

   ```
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
     <packageSources>
       <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />
       <add key="Artifactory" value="${{cx.<MASK_NAME>.url}}/artifactory/api/nuget/v3/automatedtests-nuget/" />
     </packageSources>
     <packageSourceCredentials>
       <Artifactory>
         <add key="Username" value="${{cx.<MASK_NAME>.username}}" />
         <add key="ClearTextPassword" value="${{cx.<MASK_NAME>.password}}" />
       </Artifactory>
     </packageSourceCredentials>
   </configuration>
   ```

   **Maven**

   **./.checkmarx/sca/maven/settings.xml**

   ```
   <?xml version="1.0" encoding="UTF-8"?>
   <settings xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.2.0 http://maven.apache.org/xsd/settings-1.2.0.xsd" xmlns="http://maven.apache.org/SETTINGS/1.2.0"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
     <servers>
       <server>
         <id>jfrog</id>
         <username>${{cx.<MASK_NAME>.username}}</username>
         <password>${{cx.<MASK_NAME>.password}}</password>
       </server>
     </servers>
     <profiles>
       <profile>
         <id>artifactory</id>
         <repositories>
           <repository>
             <id>central</id>
             <name>cx-virtual</name>
             <url>${{cx.<MASK_NAME>.url}}/artifactory/automatedtests-maven/</url>
             <snapshots>
               <enabled>true</enabled>
             </snapshots>
           </repository>
         </repositories>
       </profile>
     </profiles>
     <activeProfiles>
       <activeProfile>artifactory</activeProfile>
     </activeProfiles>
   </settings>
   ```

   **Npm**

   **./.checkmarx/sca/npm/.npmrc**

   ```
   registry=https://registry.npmjs.org/

   email = ${{cx.<MASK_NAME>.username}}
   always-auth = true
   @checkmarx:registry=${{cx.<MASK_NAME>.url}}/artifactory/api/npm/automatedtests-npm/
   //${{cx.<MASK_NAME>.url|no_protocol}}/artifactory/api/npm/automatedtests-npm/:_authToken=${{cx.<MASK_NAME>.password}}
   ```

   **Gradle**

   **./.checkmarx/sca/gradle/init.gradle**

   ```
   allprojects{
     repositories {
       maven {
         name = 'private.repositories'
         url = '${{cx.<MASK_NAME>.url}}/artifactory/automatedtests-gradle/'
         credentials {
         username = '${{cx.<MASK_NAME>.username}}'
         password = '${{cx.<MASK_NAME>.password}}'
         }
       }
     }
   }
   ```

   **Pip**

   **./.checkmarx/sca/pip/pip.conf**

   ```
   [global]
   extra-index-url =
   https://${{cx.<MASK_NAME>.username}}:${{cx.<MASK_NAME>.password}}@${{cx.<MASK_NAME>.url}}/artifactory/api/pypi/automatedtests-pypi/simple
   ```
2. **Apply the configuration to your project**

   You can apply the configuration using one of the following methods.

   - **Option A – Add configuration files to your repository**

     Add the relevant template to your project’s source code using the folder structure shown below, based on your package manager.

     {% hint style="info" %}
     If the config files already exist in your project, then you can add the template content to your existing file.
     {% endhint %}

     - NuGet - `./.checkmarx/sca/nuget/NuGet.Config`
     - Maven: - `./.checkmarx/sca/maven/settings.xml`
     - npm - `./.checkmarx/sca/npm/.npmrc`
     - Gradle - `./.checkmarx/sca/gradle/.npmrc`
     - Pip - `./.checkmarx/sca/pip/pip.conf`
   - **Option B – Apply configuration via API (no files added)**

     Apply the configuration without adding any files to your project’s source code by sending one of the above templates in the request body of an API call.

     This approach is useful if you prefer not to commit registry configuration or credentials to your repository.

     For full details, see the `SCA Private Registry Configuration API` documentation.
