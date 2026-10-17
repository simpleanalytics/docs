---
title: Admin API
category: api
permalink: /api/admin
last_modified_at: 2026-10-17
---

Use this if you want to administer your account. With this API you can do a few things, for example, list all websites and add websites to your dashboard.

Both endpoints need an [API key and your user ID](/api/authenticate).

## List websites

> `GET` [https://simpleanalytics.com/api/websites](https://simpleanalytics.com/api/websites)

```bash
curl "https://simpleanalytics.com/api/websites" \
     -H 'Content-Type: application/json' \
     -H 'Api-Key: sa_api_key_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx' \
     -H 'User-Id: sa_user_id_00000000-0000-0000-0000-000000000000'
```

Your user ID and API key are shown in [your account settings](https://dashboard.simpleanalytics.com/account#api). The team ID does not have any effect on this endpoint. It always returns all websites for a user.

The response looks like this:

```json
{
  "success": true,
  "websites": [
    {
      "hostname": "example.com",
      "is_public": false,
      "timezone": "Europe/Amsterdam",
      "has_ssl": true,
      "has_script": true,
      "own_hostname": null,
      "label": "customer note",
      "pageviews": 12345,
      "events": 678
    }
  ]
}
```

`own_hostname` is the custom domain used to [bypass ad-blockers](/bypass-ad-blockers). `pageviews` and `events` estimate the number of page views and events per 30 days, based on recent usage.

## Add a website

> `POST` [https://simpleanalytics.com/api/websites/add](https://simpleanalytics.com/api/websites/add)

To add a website, you need the owner, admin, or developer [role](/explained/team-roles) in the team, and the team can't have reached the website limit of its plan.

You can specify a time zone via `timezone` and set the website to public or private via the `isPublic` boolean (defaults to `false`). [See wikipedia](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) for a list of valid time zones. If you don't specify a valid time zone we will set it to UTC.

We add the website to your default team.

```bash
curl -X "POST" "https://simpleanalytics.com/api/websites/add" \
     -H 'Content-Type: application/json' \
     -H 'Api-Key: sa_api_key_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx' \
     -H 'User-Id: sa_user_id_00000000-0000-0000-0000-000000000000' \
     -d $'{
  "isPublic": false,
  "hostname": "example.com",
  "timezone": "Europe/Amsterdam"
}'
```

The response looks like this:

```json
{
  "ok": true,
  "success": true,
  "hostname": "example.com",
  "customDomain": null,
  "public": false,
  "timezone": "Europe/Amsterdam",
  "validDNS": true
}
```

When the website can't be added, the API returns HTTP `400` with `"ok": false` and an `error` message.

### Labels

If you want to keep track of your websites in a different way, a label could help. This is how a labels looks on the websites overview page:

<img loading="lazy" src="https://assets.simpleanalytics.com/docs/dashboard/labels-in-website-overview.png" alt="Simple Analytics websites overview with custom labels" class="border">

Add `"label": "customer note"` to your request body to set a label. Only strings are allowed.

## Custom endpoints

For bigger customers we make custom endpoints. If you are in the need of a custom endpoint, [let us know](https://simpleanalytics.com/contact).
