---
title: Set up Microsoft Entra SAML SSO
category: account
permalink: /microsoft-entra-saml-sso
last_modified_at: 2026-07-08
---

Use this guide to connect Microsoft Entra to your Simple Analytics team with SAML SSO.

Before you start, make sure you have admin access in Microsoft Entra and access to the [team settings](https://dashboard.simpleanalytics.com/settings/team) in Simple Analytics. If you do not see the SSO settings in Simple Analytics yet, [contact us](https://dashboard.simpleanalytics.com/contact) and ask us to enable SSO setup for your team.

## 1. Create a Simple Analytics account

Create or invite the Simple Analytics account that will manage SSO for your team.

Use an email address that can receive email. The email address in Simple Analytics must match the email address Microsoft Entra sends in the SAML login.

## 2. Create the Microsoft Entra application

In Microsoft Entra, create a new Enterprise Application:

1. Open **Microsoft Entra ID**.
1. Go to **Enterprise applications**.
1. Click **New application**.
1. Click **Create your own application**.
1. Set the app name to something recognizable like **Simple Analytics**.
1. Select **Integrate any other application you do not find in the gallery**.
1. Click **Create**.

After creating the application, open **Single sign-on** and choose **SAML**.

## 3. Add Simple Analytics values to Entra

In the SAML setup page in Entra, open **Basic SAML Configuration**.

Copy these values from the SSO section of your Simple Analytics [team settings](https://dashboard.simpleanalytics.com/settings/team):

| Microsoft Entra field                      | Simple Analytics value    |
| ------------------------------------------ | ------------------------- |
| Identifier (Entity ID)                     | Identifier (SP Entity ID) |
| Reply URL (Assertion Consumer Service URL) | Reply URL (ACS URL)       |
| Sign on URL                                | Leave blank.              |
| Relay State                                | Leave blank.              |
| Logout URL                                 | Leave blank.              |

Save the Basic SAML Configuration.

## 4. Check Attributes & Claims

Open **Attributes & Claims** in Entra.

Edit **Unique User Identifier (Name ID)** and use:

1. **Name identifier format**: Email address
1. **Source**: Attribute
1. **Source attribute**: `user.mail`

If your users are external guests and `user.mail` is empty, use `user.othermail` instead. The value must be the same email address the user has in Simple Analytics.

You can keep Entra's default additional URI-style claims:

| Claim                                                                | Source attribute |
| -------------------------------------------------------------------- | ---------------- |
| `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` | `user.mail`      |
| `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`    | `user.givenname` |
| `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`      | `user.surname`   |

If you use external guest users and changed Name ID to `user.othermail`, also use `user.othermail` for the email address claim.

## 5. Add Entra details to Simple Analytics

In Entra, you can either import the metadata XML or copy the values manually. Both work.

Then go to your Simple Analytics [team settings](https://dashboard.simpleanalytics.com/settings/team) and fill in the SSO setup form:

1. For **Your domain(s)**, enter the email domain your team uses for SSO. For example, if your users sign in with addresses like `name@example.com`, enter `example.com`.
1. To import metadata:
   1. In Entra, go to the **SAML Certificates** section.
   1. Download **Federation Metadata XML**.
   1. Paste the XML into **IdP metadata XML** in Simple Analytics.
   1. Click **Import metadata**.
1. Or fill the fields manually:
   1. For **Login URL**, copy the **Login URL** from Entra's **Set up Simple Analytics** section.
   1. For **Microsoft Entra Identifier**, copy the **Microsoft Entra Identifier** from Entra's **Set up Simple Analytics** section.
   1. For **Certificate (Base64/Raw)**, download **Certificate (Base64)** from Entra and paste it into Simple Analytics.
1. Check that the Login URL, Microsoft Entra Identifier, and certificate are filled in.
1. For **Email attribute**, enter:

   ```text
   http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress
   ```

1. For **First name attribute**, enter:

   ```text
   http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname
   ```

1. For **Last name attribute**, enter:

   ```text
   http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname
   ```

1. Click **Save SSO draft**.

Your Single sign-on status should now show **Draft**.

## 6. Ask us to confirm the setup

After saving the draft, [contact us](https://dashboard.simpleanalytics.com/contact) and let us know your Microsoft Entra settings are ready for confirmation.

We will check the setup and let you know when it is ready to test. We keep SSO optional during testing.

## 7. Test SSO login

Once we confirm the setup, use the SSO login link shown in the SSO section of your Simple Analytics [team settings](https://dashboard.simpleanalytics.com/settings/team).

When the login works, let us know if you want SSO to be enforced for your team.

## 8. Add team members

To add more people to your team:

1. Assign them to the Simple Analytics Enterprise Application in Entra.
1. Invite them from your Simple Analytics [team settings](https://dashboard.simpleanalytics.com/settings/team).
1. Ask them to log in through Entra or the SSO login link in Simple Analytics.

The email address sent by Entra must match the email address of the Simple Analytics user.

Contact us before changing an active SSO setup, including domains, certificates, claim mappings, or enforcement.
