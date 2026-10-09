---
title: How to delete my account
category: account
permalink: /delete-account
last_modified_at: 2026-10-09
---

It's very easy to delete your account. Go to your [account settings](https://simpleanalytics.com/account) and click the button "Delete your account".

## What happens to your teams

The account deletion page lists the teams you belong to. Teams are kept by default. If you have permission to delete a team, you can check that team to delete it together with your account. Teams you do not have permission to delete are always kept.

When you own a team that is kept, ownership moves to another active owner or admin. A team must be deleted when you are its only member or when you are the departing owner and there is no active owner or admin who can take ownership.

Deleting a team also deletes its websites and analytics data. Other members are removed from the deleted team. Members who belong to another team keep their accounts; members who have no other team lose their accounts as well.

## Automatic removal of unused accounts and teams

We automatically remove accounts and teams that never collected any data. This applies to free teams and to teams whose paid subscription has ended. It never applies to teams with a running subscription, a custom trial, or a partner.

A team becomes a candidate when it is at least 7 days old and none of its websites has received a single visitor. We then email every active member with a link to keep the team. The email lists the websites that would be removed. If nobody uses that link, we delete the team 3 days later, including its websites. Members who have no other team lose their accounts as well, exactly as described above.

When such a team was billed through Stripe before, its Stripe customer is removed together with the team. Your payment history in Stripe is kept, because we need it for taxes.

Using the "Keep this team" (or "Keep my account") link in that email stops the removal and keeps the team for at least another 90 days. You do not have to log in to use the link.

As soon as one of the websites in the team receives its first visitor, the team is no longer unused and will not be removed automatically.

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
