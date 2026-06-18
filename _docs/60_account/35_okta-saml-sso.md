---
title: Set up Okta SAML SSO
category: account
permalink: /okta-saml-sso
last_modified_at: 2026-06-16
---

Use this guide to connect Okta to your Simple Analytics team with SAML SSO.

Before you start, make sure you have admin access in Okta and access to the [team settings](https://dashboard.simpleanalytics.com/settings/team) in Simple Analytics. If you do not see the SSO settings in Simple Analytics yet, [contact us](https://dashboard.simpleanalytics.com/contact) and ask us to enable SSO setup for your team.

## 1. Create a Simple Analytics account (if you don't have one)

Create a Simple Analytics account if you do not have one yet. You need access to a team before you can connect Okta.

## 2. Create the Okta application

In Okta, create a new application integration and select **SAML 2.0** as the sign-in method.

Use these settings for the application:

1. Set the app name to **Simple Analytics**.
1. Optionally, add the Simple Analytics logo from our [media kit](https://www.simpleanalytics.com/media-kit).
1. For **Single sign-on URL**, use the SSO URL shown in the SSO section of your Simple Analytics [team settings](https://dashboard.simpleanalytics.com/settings/team).
1. Keep **Use this for Recipient URL and Destination URL** checked.
1. For **Audience URI**, use the SP Entity ID shown in the SSO section of your Simple Analytics [team settings](https://dashboard.simpleanalytics.com/settings/team).
1. Leave **Default RelayState** empty.
1. Set **Name ID format** to **EmailAddress**.
1. Set **Application username** to **Email**.
1. Set **Update application username on** to **Create and update**.

Save the Okta application when you are done.

## 3. Add Okta details to Simple Analytics

In Okta, open the **Sign On** tab for the Simple Analytics application and click **View SAML setup instructions**.

Then go to your Simple Analytics [team settings](https://dashboard.simpleanalytics.com/settings/team) and fill in the SSO setup form:

1. For **Your domain(s)**, enter the email domain your team uses for SSO. For example, if your users sign in with addresses like `name@example.com`, enter `example.com`.
1. For **Identity Provider Single Sign-On URL**, copy the URL from Okta's setup instructions.
1. For **Identity Provider Issuer / Entity ID**, copy the issuer from Okta's setup instructions.
1. For **Signing certificate**, copy the X.509 certificate from Okta's setup instructions.
1. Leave the attribute mapping fields unchanged if you used the Okta settings from this guide.
1. Click **Save SSO draft**.

Your Single sign-on status should now show **Draft**.

## 4. Ask us to confirm the setup

After saving the draft, [contact us](https://dashboard.simpleanalytics.com/contact) and let us know your Okta settings are ready for confirmation.

We will check the setup and let you know when it is ready to test.

## 5. Test SSO login

Once we confirm the setup, test logging in from the Simple Analytics application in your Okta dashboard.

You can also use the SSO login link shown in the SSO section of your Simple Analytics [team settings](https://dashboard.simpleanalytics.com/settings/team).

When the login works, let us know if you want SSO to be required for your team.

## 6. Add team members

To add more people to your team:

1. Assign them to the Simple Analytics application in Okta.
1. Invite them from your Simple Analytics [team settings](https://dashboard.simpleanalytics.com/settings/team).
1. Ask them to log in through Okta.

After they log in, they can accept the invitation and join your Simple Analytics team.
