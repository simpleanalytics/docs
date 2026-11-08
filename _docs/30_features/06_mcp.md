---
title: Connect AI apps with MCP
menu: MCP server
category: features
permalink: /mcp
created_at: 2026-11-08
last_modified_at: 2026-11-08
---

Connect Simple Analytics to Claude, ChatGPT, Claude Code, Codex or another AI app. Then ask about your stats and set up websites and events right from the chat. It works on every plan, including Free.

When you connect, you log in to Simple Analytics, pick a team and approve what the app can do. This is the URL of our MCP server:

```
https://mcp.simpleanalytics.com/mcp
```

Other apps that support remote MCP servers with OAuth can use the same URL.

## Claude

In Claude, on claude.ai or in Claude Desktop, open **Customize → Connectors**. Click **+ Add → Add custom connector** and paste the URL.

## ChatGPT

In ChatGPT, open **Plugins**. Click **+ → Add custom MCP server**, paste the URL and use it with OAuth.

## Claude Code

Run this and log in when your browser opens:

```sh
claude mcp add --scope user --transport http simple-analytics https://mcp.simpleanalytics.com/mcp
claude mcp login simple-analytics
```

With `--scope user`, Simple Analytics is available in all your projects.

## Codex

Run this and log in when your browser opens:

```sh
codex mcp add simple-analytics --url https://mcp.simpleanalytics.com/mcp
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

## More than one team

Each connection has access to one team. To use another team, connect Simple Analytics once more under another name and pick that team when you log in. For example, in Claude Code:

```sh
claude mcp add --scope user --transport http simple-analytics-acme https://mcp.simpleanalytics.com/mcp
claude mcp login simple-analytics-acme
```

Agents without MCP login get access to one team too. To use another team, approve a new code and pick that team.

## What apps can do

Ask in plain language, for example _"Which pages got the most visitors from Google last week?"_, _"Is the script working on example.com?"_ or _"Add an annotation for today's launch"_.

- **Your stats:** visitors and pageviews over time, pages, referrers, countries, UTM codes, browsers, operating systems, devices, time on page, events and metadata. Apps can [filter](/filters) them, for example on pages like `/blog/*`, referrers, countries or URL parameters, and compare them with the period before.
- **Latest hits and raw data:** the latest pageviews and events, including robots, to check a new setup. Raw data is available on plans with the [Export API](/api/export-data-points).
- **Set up websites:** add websites, change their settings, get the instructions to [install the script](/script) and [collect events](/events), and check the script on your live website.
- **Goals and more:** create and update [goals](/goals) and see their results, add [annotations](/annotations), [email reports](/email-reports) and [custom views](/custom-views), and check the [Free plan badge](/free-plan-badge).

Apps ask you before they change something. They can't delete anything, change your plan or billing, or manage users. They only get email addresses of team members when you ask for them.

Answers explain the data when it matters, like that visitors are [unique pageviews](/explained/unique-visits) because we don't use cookies, or that each step of a goal counts on its own.

## Ready-made instructions

The [Integrate AI tab](https://dashboard.simpleanalytics.com/select-website/ai) has instructions for AI agents, like **Improve tracking**, **Fix broken links** and **Clean up UTM codes**. Copy one and paste it in Claude Code, Codex, Cursor or another agent, in the project of your website. The agent uses your stats and asks you before it changes anything.

## Disconnect

Open the [Integrate AI tab](https://dashboard.simpleanalytics.com/select-website/ai) and find your app or agent under **AI apps and agents with access**. Click **Disconnect** for apps or **Revoke** for agents. Access ends right away.
