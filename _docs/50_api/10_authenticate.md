---
title: API Authenticate
menu: Authenticate
category: api
permalink: /api/authenticate
last_modified_at: 2026-10-17
---

For some API features you'll need to authenticate. You can do this with an `Api-Key`-header where the key starts with `sa_api_key_...`.

In your [account settings](https://dashboard.simpleanalytics.com/account#api) you can create this key. Creating a key requires an active trial or a plan that includes API access ([see pricing](https://www.simpleanalytics.com/pricing)). API keys belong to your user, not to a team. If you are removed from a team, your keys stop working for the websites of that team.

To test if your API key works correctly you can replace the example values of this cURL example with your own:

```bash
curl "https://simpleanalytics.com/example.com.json?version={{ site.api_version }}&fields=histogram" \
     -H 'Content-Type: application/json' \
     -H 'Api-Key: sa_api_key_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'
```

The [Admin API](/api/admin) also needs your user ID in a `User-Id` header. The Stats API and Export API only need the API key.

```bash
curl "https://simpleanalytics.com/api/websites" \
     -H 'Content-Type: application/json' \
     -H 'Api-Key: sa_api_key_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx' \
     -H 'User-Id: sa_user_id_00000000-0000-0000-0000-000000000000'
```

Your user ID is shown in [your account settings](https://dashboard.simpleanalytics.com/account#api) after you create a key.

If an API key fails authentication 20 times within 15 minutes, we reject all requests with that key for up to 15 minutes. The Stats API and Admin API then return the error `Too many failed attempts, please try again later`.

If you have any problems, drop us a line via [our contact page](https://simpleanalytics.com/contact).
