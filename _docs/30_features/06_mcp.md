---
title: Connect AI apps with MCP
menu: MCP server
category: features
permalink: /mcp
created_at: 2026-11-08
last_modified_at: 2026-11-13
---

Connect Simple Analytics to Claude, ChatGPT, Claude Code, Codex or another AI app. Then ask about your stats and set up websites and events right from the chat. It works on every plan, including Free.

When you connect, you log in to Simple Analytics and approve what the app can do. When you're in more than one team, you also pick the team. This is the URL of our MCP server:

```
https://mcp.simpleanalytics.com/mcp/v1
```

Other apps and agents connect with a temporary token that you approve, like an API key that expires. See [Cursor and other agents](#cursor-and-other-agents).

## Claude

In Claude, on claude.ai or in Claude Desktop:

1. Open **Customize → Connectors** and click **+ Add → Add custom connector**.
2. Enter a name, like Simple Analytics, paste the URL and click **Continue** twice.
3. Keep **Use Claude's published identity** as the OAuth client, Simple Analytics doesn't support **Register automatically**.
4. Click **Add** and log in when Claude asks.

In a chat, turn it on with **+ → Connectors**.

On a Team or Enterprise plan, an owner adds the connector first, the same way in **Organization settings → Connectors** with **Add → Custom → Web**. Members then click **Connect** next to it in **Customize → Connectors**.

## ChatGPT

On ChatGPT on the web, open [Plugins](https://chatgpt.com/plugins):

1. Click **+ → Add custom MCP server**.
2. Enter a name, paste the URL as the server URL and pick **OAuth**.
3. Accept the warning and click **Create as a plugin**.
4. Install the plugin and log in.

In a chat, type `@` and pick the plugin. In a workspace, its permissions decide whether you can add custom MCP servers.

## Claude Code

Run this and log in when your browser opens:

```sh
claude mcp add --scope user --transport http simple-analytics https://mcp.simpleanalytics.com/mcp/v1
claude mcp login simple-analytics
```

With `--scope user`, Simple Analytics is available in all your projects.

## Codex

Run this and log in when your browser opens:

```sh
codex mcp add simple-analytics --url https://mcp.simpleanalytics.com/mcp/v1
```

Codex starts the login itself. If no browser opens, log in with:

```sh
codex mcp login simple-analytics
```

## Cursor and other agents

Cursor and some other agents can't log in to Simple Analytics over MCP yet. Give them instructions from your dashboard instead:

1. Open the [Integrate AI tab](https://dashboard.simpleanalytics.com/select-website/ai) of your website.
2. Pick an option, like **Improve tracking**, and copy its instructions.
3. Paste them in your agent, in the project of your website.
4. The agent asks for access and shows you a link and a code. Open the link and check that it shows the same code. You can also enter the code on [dashboard.simpleanalytics.com/agent](https://dashboard.simpleanalytics.com/agent).
5. Pick the team, when you're in more than one, and how long the agent has access: 1 hour, 3 hours (the default), 1 day, 1 week, 1 month or 1 year. Then click **Approve**.

The agent then uses the same tools over our [Tools API](/api/tools). You can also get such a token for your own scripts, or for an MCP client that can send it in a header.

## More than one team

Each connection has access to one team. To use another team, connect Simple Analytics once more under another name and pick that team when you log in. For example, in Claude Code:

```sh
claude mcp add --scope user --transport http simple-analytics-acme https://mcp.simpleanalytics.com/mcp/v1
claude mcp login simple-analytics-acme
```

Agents without MCP login get access to one team too. To use another team, approve a new code and pick that team.

## What apps can do

Ask in plain language, for example _"Which pages got the most visitors from Google last week?"_, _"Is the script working on example.com?"_ or _"Add an annotation for today's launch"_.

- **Your stats:** visitors and pageviews over time, pages, referrers, countries, UTM codes, browsers, operating systems, devices, time on page and metadata. Apps can [filter](/filters) them like your dashboard does, with several values at once, exclusions and the filters you saved. They can split search engines into paid and organic visits, and compare everything with the period before.
- **Events and goals:** how often events happened, and events grouped by one of their fields like in the [Events Explorer](/events-explorer), also as a CSV, Excel or Numbers file. Apps create, change and reorder [goals](/goals) and show their conversions and where visitors drop off.
- **Latest hits and raw data:** the latest pageviews and events, including robots, to check a new setup. Raw data is available on plans with the [Export API](/api/export-data-points).
- **Set up websites:** add websites, change their settings, get the instructions to [install the script](/script) and [collect events](/events), and check the script on your live website.
- **Your dashboards:** add [annotations](/annotations) and [email reports](/email-reports), create and change [custom views](/custom-views), save filters, and change how your dashboard shows stats, like rounding, the chart style and [trend lines](/trend-lines).
- **Your account:** see who is in your team, your plan and subscription, the websites you transfer, your Google Analytics imports, the single sign-on setup, and the apps, agents and API keys with access. Apps can change settings like [excluded IP addresses](/exclude-ips) and [advanced robot blocking](/robot-blocking), and check the [Free plan badge](/free-plan-badge).
- **Support:** when troubleshooting doesn't solve a problem, an app can send a request to our support from your email address. It asks you first. On the Free plan that's only for problems that look like a bug on our side.

See [all tools](/tools) for everything apps can use, with their inputs.

Answers explain the data when it matters, like that visitors are [unique pageviews](/explained/unique-visits) because we don't use cookies, or that each step of a goal counts on its own.

## What you confirm yourself

Apps ask you before they change something. Some changes they can't make at all. They can't delete or reset anything, apart from filters you saved. They also can't invite or remove team members, change who has access, transfer websites or cancel your subscription.

For those changes, an app gives you a link. You review the change and confirm it there, logged in to Simple Analytics. The link works for 1 hour.

Payments, plan changes, new API keys, the single sign-on setup and Google consent for imports only happen in your browser. Apps tell you where things stand and give you the page to continue on.

What an app can do also depends on your [role](/explained/team-roles) and your plan, like in your dashboard. Apps only get email addresses of team members when you ask for them.

## Ready-made instructions

The [Integrate AI tab](https://dashboard.simpleanalytics.com/select-website/ai) has instructions for AI agents, like **Improve tracking**, **Fix broken links** and **Clean up UTM codes**. Copy one and paste it in Claude Code, Codex, Cursor or another agent, in the project of your website. The agent uses your stats and asks you before it changes anything.

## Disconnect

Open the [Integrate AI tab](https://dashboard.simpleanalytics.com/select-website/ai) and find your app or agent under **AI apps and agents with access**. Click **Disconnect** for apps or **Revoke** for agents. Access ends right away.
