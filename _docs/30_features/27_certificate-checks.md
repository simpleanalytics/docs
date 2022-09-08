---
title: SSL expiry alerts
category: features
permalink: /ssl-expiry-alerts
last_modified_at: 2022-09-08
---

Secure Sockets Layer (SSL) are cryptographic protocols that provide security and data integrity for data transfers over the internet. When you visit a website that starts with HTTPS or has a (green) lock pad next to the URL, it uses an SSL certificate. Most websites have those, and those certificates have an expiry date. Sometimes it might happen that the certificate will expire before it's renewed. Your website will not be available to your visitors.

To prevent this from happening, Simple Analytics developed a feature where you get alerts via email when an SSL certificate is about to expire. We usually send out two emails, one four days before the expiry date and another one day before the expiry date. That gives you and your team some time to renew the certificate before it's too late.

You can always check the SSL expiry date for your websites yourself via [our free SSL check tool](https://simpleanalytics.com/check-ssl).

Here is an example email for such an alert:

<img src="https://assets.simpleanalytics.com/docs/ssl-expiry-alerts/ssl-expiry-email.png" alt="SSL expiry alert email" class="border" />

You can disable the alerts right from those emails. You can either disable all SSL expiry alerts for all websites or just for that one website you got the alert for.
