---
title: Tools API
category: api
permalink: /api/tools
created_at: 2026-11-13
last_modified_at: 2026-11-13
---

The Tools API runs the tools of our [MCP server](/mcp) over HTTPS. It's for AI agents that can't connect over MCP, and for your own scripts. You can read stats, set up websites and events, and manage goals, annotations, email reports, custom views and more. See [all tools](/tools).

It works with a token that you approve in your dashboard, on every plan, including Free. [API keys](/api/authenticate) don't work here: use them with the [Stats API](/api/stats), [Export API](/api/export-data-points) and [Admin API](/api/admin).

## With an AI agent

You don't need this page to give an AI agent access. The [Integrate AI tab](https://dashboard.simpleanalytics.com/select-website/ai) of your dashboard has instructions to copy and paste in Claude Code, Codex, Cursor or another agent. The agent then asks for a token itself and shows you a link and a code to approve. See [Cursor and other agents](/mcp#cursor-and-other-agents).

## Get a token

Getting a token takes three steps: your script asks for a token, you approve it in your browser, and your script picks it up.

### 1. Ask for a token

```sh
curl -s -X POST https://dashboard.simpleanalytics.com/api/agent/request \
  -H 'Content-Type: application/json' \
  -d '{"name":"My script"}'
```

The `name` is what you see when you approve the token, and later in the list of apps and agents with access. The response looks like this:

```json
{
  "device_code": "BCDF-GHJK.9uWq…",
  "user_code": "BCDF-GHJK",
  "verification_uri": "https://dashboard.simpleanalytics.com/agent",
  "verification_uri_complete": "https://dashboard.simpleanalytics.com/agent?code=BCDF-GHJK",
  "expires_in": 600,
  "interval": 5
}
```

The code works for 10 minutes.

### 2. Approve it

Open the `verification_uri_complete` link in your browser, logged in to Simple Analytics. Check that it shows the same code as the `user_code`. Pick how long the token works: 1 hour, 3 hours (the default), 1 day, 1 week, 1 month or 1 year. When you're in more than one team, also pick the team. Then click **Approve**.

What the token can do depends on your [role and plan](/tools#roles-and-plans), like in your dashboard. You confirm deletions and other sensitive changes yourself, see [changes you confirm](/tools#changes-you-confirm).

### 3. Pick up the token

```sh
curl -s -X POST https://dashboard.simpleanalytics.com/api/agent/token \
  -H 'Content-Type: application/json' \
  -d '{"device_code":"BCDF-GHJK.9uWq…"}'
```

Until you approve it, this returns HTTP `400` with the error `authorization_pending`. Wait for the number of seconds in `interval` and try again. After you approved it, you get the token:

```json
{
  "access_token": "eyJhbGciOi…",
  "token_type": "Bearer",
  "expires_in": 10800,
  "scope": "websites:read stats:read websites:write account:write sso:read billing:read billing:write support:write",
  "team_name": "Acme"
}
```

You get the token only once. After that, or when the code expired, the error is `expired_token`. When you clicked **Deny**, it's `access_denied`.

Keep the token secret. Store it outside your project, where only you can read it, and don't print it in logs.

## List the tools

```sh
curl -s https://dashboard.simpleanalytics.com/api/v1/tools
```

This needs no token. The response has `instructions` for AI agents to read first, and all `tools` with their `name`, `description` and their inputs as JSON Schema in `input_schema`. The [tools page](/tools) shows the same list.

## Call a tool

Send a `POST` request with the name of the tool in the URL, your token in the `Authorization` header and the inputs as JSON:

```sh
curl -s -X POST https://dashboard.simpleanalytics.com/api/v1/tools/get_stats \
  -H 'Authorization: Bearer eyJhbGciOi…' \
  -H 'Content-Type: application/json' \
  -d '{"hostname":"example.com","start":"today-7d","lists":["pages"],"limit":2}'
```

The response is the result of the tool:

```json
{
  "hostname": "example.com",
  "start": "2026-11-06",
  "end": "2026-11-13",
  "timezone": "Europe/Amsterdam",
  "pageviews": 4210,
  "visitors": 1893,
  "seconds_on_page": 42,
  "lists": {
    "pages": [
      { "value": "/", "pageviews": 1620, "visitors": 804, "seconds_on_page": 31 },
      { "value": "/pricing", "pageviews": 512, "visitors": 377, "seconds_on_page": 58 }
    ]
  },
  "warnings": [],
  "notes": [
    "Visitors are unique pageviews, not people: a pageview is unique when it has no referrer or comes from another website. Simple Analytics needs no cookies or identifiers for this, so it needs no cookie banner.",
    "Time on page is the median time a page was visible, in seconds. Pageviews under 5 seconds are left out of it."
  ]
}
```

A tool without inputs, like `list_websites`, takes an empty body or `{}`. The body can be up to 64 KB.

## Errors

| Status | When                                                                                                             |
| ------ | ---------------------------------------------------------------------------------------------------------------- |
| `400`  | The tool didn't run or failed. The `error` tells why, like an invalid input, or a role or plan that doesn't allow it |
| `401`  | The token is missing, wrong, expired or revoked. Ask for a new token                                             |
| `404`  | There is no tool with this name                                                                                  |
| `405`  | Use `GET` for the list of tools and `POST` to call a tool                                                         |
| `413`  | The body is larger than 64 KB                                                                                    |
| `429`  | Too many token requests, try again later                                                                         |

Errors of a tool look like this:

```json
{
  "error": "Exports need the analyst role or higher"
}
```

A token is for one team. When a tool answers `Invalid team access`, the website belongs to another team. Ask for a new token and pick that team when you approve it.

## Use the token with MCP

The token also works on our MCP server. In an MCP client that can't log in to Simple Analytics but can send headers, use `https://mcp.simpleanalytics.com/mcp/v1` with the header `Authorization: Bearer` followed by your token.

## Revoke a token

A token stops working when its time is up. To end it sooner, open the [Integrate AI tab](https://dashboard.simpleanalytics.com/select-website/ai), find it under **AI apps and agents with access** and click **Revoke**.

## Versions

The `v1` in the URL is the version of the tools. We do our best to keep `v1` backwards compatible: we add tools and optional inputs instead of changing the ones that are there. That's not a guarantee, so check the [list of tools](#list-the-tools) when a request stops working. The older URL `/api/tools` is the same as `/api/v1/tools`.
