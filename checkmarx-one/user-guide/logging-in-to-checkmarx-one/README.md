# Logging in to Checkmarx One

{% hint style="warning" %}
For SSO login, please see [here](../user-management-and-access-control/general-settings.md#login-session-management). For SAML AD (Azure), see [here](../user-management-and-access-control/managing-identity-providers/configuring-a-saml-provider-with-azure-active-directory-ad.md).
{% endhint %}

To be able to perform initial login for Checkmarx One, first a **Tenant** is needed to be created by Checkmarx.

A Tenant is a dedicated account per customer.

Once the Tenant is successfully created, a Welcome email will be sent to the administrator.

The Welcome email contains the following information:

- Username (For the administrator initial log in).
- Account name (Tenant name)
- Link to Checkmarx One.

## New User Workflow

- After the creation of a new tenant, the Admin user will get an Email for the initial login and setup a new password (the link redirects to the Identity and Access Management).
- The Admin logs in to Checkmarx One using the procedure described in [Initial Log in](initial-log-in.md).
- After completing the initial setup process the Admin user will be able to create new users as described in [User Management and Access Control](../user-management-and-access-control/README.md) (see video below).
- The Admin will provide the new user with crdenctials (via mail or some other method).
- The user will log in to Checkmarx One, using the approriate base URL for the account's environment, and enter the provided credentials.

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
- When logging in for the first time, the user will be required to change the initial given password.
- The new user can freely access Checkmarx One.

## Authentication Method

Checkmarx One uses **Time-based One Time Passwords** (TOTP) protocol during the log in process to increase security.

Authenticator apps that support TOTP protocol and can enroll using QR codes will work with Checkmarx One.

Authenticator apps that support hash-based one-time password (HOTP) protocol are not officially supported, although Keycloak (The Open Source Identity and Access Management solution used by Checkmarx One) supports HOTP as well.

It is highly recommended to use authenticator apps that support TOTP protocol and not HOTP.

## In this section

- [Initial Log in](initial-log-in.md)
- [Access Control](access-control.md)
