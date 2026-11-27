---
title: Server-side collection (beta)
category: install-script
permalink: /server-side-collection
last_modified_at: 2026-11-18
created_at: 2026-11-18
---

AI agents and robots request your pages without running the script, so the script can't count them. With server-side collection, your website's server reports the page requests it answers to Simple Analytics, and we decide whether an AI agent, a robot or a person made each one. Requests from people are discarded right away, because the script already counts them, so keep the script on your website.

- **AI agents,** like ChatGPT-User and Claude-User fetching your page because someone asked an AI product, show up in your reports and count toward your usage. Your numbers go up when you set it up.
- **Robots,** like Googlebot, GPTBot and curl, are stored but hidden by default, and don't count toward your usage.
- **No token or setting:** the small piece of code on your server, the integration, is all you need.
- **Privacy:** your server sends the addresses of a request, which we use in memory only and never store or log. It never sends cookies or authorization headers, and only the query parameters you allow.

> **Beta:** the beta covers how we classify and show AI agents and robots. What your integration sends is fixed, so it keeps working after the beta.

## Install with AI

Using Claude Code, Codex, Cursor or another AI agent? Let it write the integration and test it. In the dashboard, your website's settings have **Copy AI instructions** for server-side collection, with your hostname filled in. Paste them into your agent. Or ask your agent:

```
Set up Simple Analytics server-side collection for example.com, follow https://docs.simpleanalytics.com/server-side-collection.md
```

The agent asks you which query parameters to report, tells you which pages it can't count, and tests the integration without storing anything. Nothing is sent to us automatically: when something doesn't work, the agent gives you a list to send to [our support](https://simpleanalytics.com/contact).

## Install with Next.js

{% include server-side-collection/nextjs.md %}

## Install on other frameworks

Your integration has to send exactly what's described here. [The guide for AI agents](/server-side-collection.md) has the same rules, with the steps around them.

{% include server-side-collection/integration.md %}

## Pages that are not counted

{% include server-side-collection/not-counted.md %}

## Test it

{% include server-side-collection/tests.md %}

Need help? Send us what you tried through [our support channels](https://simpleanalytics.com/contact).
