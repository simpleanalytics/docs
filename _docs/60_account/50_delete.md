---
title: How to delete my account
category: account
permalink: /delete-account
last_modified_at: 2026-08-11
---

It's very easy to delete your account. Go to your [account settings](https://simpleanalytics.com/account) and click the button "Delete your account".

## What happens to your teams

The account deletion page lists the teams you belong to. Teams are kept by default. If you have permission to delete a team, you can check that team to delete it together with your account. Teams you do not have permission to delete are always kept.

When you own a team that is kept, ownership moves to another active owner or admin. A team must be deleted when you are its only member or when you are the departing owner and there is no active owner or admin who can take ownership.

Deleting a team also deletes its websites and analytics data. Other members are removed from the deleted team. Members who belong to another team keep their accounts; members who have no other team lose their accounts as well.

## What we will delete

- Your user account and personal account data are deleted from our databases
- For every team that is deleted, its websites and analytics data are deleted
- Subscriptions belonging to deleted teams are cancelled
- For deleted teams billed through Stripe, the customer email and saved payment details are removed from Stripe

## What we will keep

- Teams you keep, including their websites, analytics data, subscriptions, and billing details
- Your payment history in Stripe (this is needed for taxes)
- If your data is part of our log files (in case of an error) it will be kept for 90 days
- We keep database backups for 90 days in case something went wrong
- For deleted websites, we keep a [hash of their domain names](/explained/domain-privacy) to prevent others from linking those domains to their account

> If you have any questions feel free to contact us at <a href="mailto:{{ site.email }}">{{ site.email }}</a>.
