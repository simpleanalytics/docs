---
title: API Authenticate
menu: Authenticate
category: api
permalink: /api/authenticate
last_modified_at: 2022-04-14
---

For some API features you'll need to authenticate. You can do this with an `Api-Key`-header where the key starts with `sa_api_key_...`.

In your [account settings](https://simpleanalytics.com/account) you can create this key.

To test if your API key works correctly you can replace the example values of this cURL example with your own:

```bash
curl "https://simpleanalytics.com/example.com.json?version={{ site.api_version }}&fields=histogram" \
     -H 'Content-Type: application/json' \
     -H 'Api-Key: sa_api_key_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'
```

For some API calls you'll need a user ID:

```bash
curl "https://simpleanalytics.com/api/websites" \
     -H 'Content-Type: application/json' \
     -H 'Api-Key: sa_api_key_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx' \
     -H 'User-Id: sa_user_id_00000000-0000-0000-0000-000000000000'
```

Your user ID is shown in [your account settings](https://simpleanalytics.com/account).

If you have any problems, drop us a line via [our contact page](https://simpleanalytics.com/contact).
