---
title: Domain privacy
category: explained
permalink: /explained/domain-privacy
---

We believe adding a website to Simple Analytics should be a painless process.

## Painless process

We have many ways to make this process easier:

- Our onboarding flow is fantastic:
  - it recommends plugins that a specifically relevant for the just added website,
  - it shows the required steps in a beautiful format,
  - and customers can forward it to their tech team.
- When adding our embed script is that you don't have to create a website in our dashboard first.
- Customers also don't need to verify their domain.
- Customers don't need to create a website ID every time they add a website.

We think it should be as painless as possible to add our embed script, without thinking.

## Privacy

Our embed script works by grabbing the website name from the URL _(you [can overwrite](/overwrite-domain-name) this)_ so our customers don't have to. When a customer leaves Simple Analytics we don't want other customers to be able to collect data for an embed script that might still be installed. That's why we store a website hash of every website that is deleted. When another customer tries to add a website we compare this with a list of website hashes that are deleted. If there is a match, we require to verify that domain.

This way it's super easy to add our script, and your data will never fall in the wrong hands.
