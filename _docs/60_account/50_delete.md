---
title: How to delete my account
category: account
permalink: /delete-account
last_modified_at: 2026-10-17
---

It's very easy to delete your account. Go to your [account settings](https://simpleanalytics.com/account#delete) and click "Delete account" at the bottom of the page. The next page first asks why you're leaving (you can skip this), then shows what will be deleted before you confirm.

## What happens to your teams

The account deletion page lists the teams you belong to. Teams are kept by default. If you can delete a team (you are its owner or its only member), you can check that team to delete it together with your account. Teams you can't delete are always kept.

When you own a team that is kept, ownership moves to another active member. We pick an owner first, then an admin, then any other active member, and you can choose a different active member on the deletion page. The new owner receives an email. A team must be deleted when you are its only member or when you are the departing owner and no other active member remains. Members who haven't accepted their invitation don't count.

Deleting a team also deletes its websites and analytics data. Other members are removed from the deleted team and receive an email. Their accounts are not deleted, even when they have no other team.

## Automatic removal of unused accounts and teams

We automatically remove accounts and teams that never collected any data. This applies to free teams and to teams whose paid subscription has ended. It never applies to teams with a running subscription, a custom trial, or a partner.

A team becomes a candidate when it is at least 7 days old and none of its websites has received a single visitor. We then email every active member with a link to keep the team. The email lists the websites that would be removed. If nobody uses that link, we delete the team 3 days later, including its websites. Members who have no other team lose their accounts as well.

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
