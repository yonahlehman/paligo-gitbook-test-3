# Cloud Insights FAQ

<details>

<summary>Unable to log into CxSAST, even after resetting password. Error : “invalid credentials."</summary>

Problem: User unable to sign into CxSast portal with error “invalid credentials.” Resetting password does not help.

1. Check for SAST ingestion logs by going to **Settings** > **System Activity Log**, and filter for ActivityType = "Enrichment Integration".
2. Verify SAST vulnerability findings by going to **Findings** > **Vulnerability Findings**, and setting the following filters: ResourceType = "Repository Branch" and HasExternalSource = "True".

</details>

<details>

<summary>Q2: Why am I not seeing CxOne SAST results enrichment on Wiz ?</summary>

A: First, verify that you have the correct Wiz license, which supports scanning of source code repositories. Second, verify that the CxOne SAST scanner is scanning the same source code repos that are being scanned by Wiz.

</details>

<details>

<summary>Q3: Automatic detection of "Internet Facing" images is not always accurate. Is there a way to override the data?</summary>

A: Yes, It’s possible to manually override the data for specific container images. This is done in the Inventory table using a row action as described here.

</details>
