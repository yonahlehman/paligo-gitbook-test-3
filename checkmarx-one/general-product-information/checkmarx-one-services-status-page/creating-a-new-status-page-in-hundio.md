# Creating a New Status Page in Hund.io

To create a new status page in Hund.io, proceed as follows:

1. Click [here](https://cxone-dashboard.hund.io/dashboard/index) to open Hund.
2. In the Global Dashboard drop-down list, select **New Status Page**.
3. Enter a Status Page Name, Status Page Address, and Subdomain.
4. Under **Components**, add a new Group.
5. Add new components into the new group

   <figure><img src="../../../assets/CID_721acf42b1a63af008dc7ec931d01afd.png" alt="" width="700"><figcaption></figcaption></figure>
6. Choose the **PagerDuty** option.

   <figure><img src="../../../assets/CID_02efb27ed46ce4b456fe67d3d161bc87.png" alt="" width="550"><figcaption></figcaption></figure>
7. Enter the PagerDuty API key and click on **Connect PagerDuty Account**.
8. Enter the component name and description according to the client’s license on the BO. You can copy the required information from the MT status page (Services > `emptyservice_statuspage`”.
9. Click **Create component** and create as many components as needed.
10. Navigate to **Notifiers** and select **Email**.

    <figure><img src="../../../assets/CID_f6301c5c4b3a005f997cd620dce0595d.png" alt="" width="673"><figcaption></figcaption></figure>
11. Enter the following parameters: : [email-smtp.us-east-1.amazonaws.com](http://email-smtp.us-east-1.amazonaws.com)

    - SMTP hostname
    - SMTP User
    - SMTP Password
    - SMTP Authentication Method
    - Sender address
12. Click **Create Notifier** and select Webhook.

    <figure><img src="../../../assets/CID_e0e53d22dd221d8d7a796bac0d25bdfb.png" alt="" width="686"><figcaption></figcaption></figure>
13. Click **Create Notifier**.

    <figure><img src="../../../assets/CID_83f092ab62237d8e76ea2b6f0d359abf.png" alt="" width="313"><figcaption></figcaption></figure>
14. The status page is ready, but you still need to create a URL to access it. To do it, connect to the AWS account **CxAST-Production** and create a new record in Route53 > Hosted zones > [ast.checkmarx.net](http://ast.checkmarx.net).
15. Go back to status page and select **Domains**.

    <figure><img src="../../../assets/CID_88db81a9969beee3076eb580638b763a.png" alt="" width="209"><figcaption></figcaption></figure>
16. Enter the **Subdomain** and **Custom Domain** you just created in AWS Route53.
17. Click **Update Domain**.
