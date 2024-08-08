---
title: Compliance
menu: Compliance
category: legal
permalink: /compliance
last_modified_at: 2024-08-08
---

## GDPR and UK GDPR Compliance

Simple Analytics fully adheres to GDPR and UK GDPR regulations by **refraining from collecting any personal data from end users** (that is, visitors of a customer’s website or app users). We do not place cookies, collect IP addresses, or use device identifiers.

Our data minimization strategy is fundamental to our ethics and simplifies compliance. Since GDPR and UK GDPR govern personal data, our approach of not collecting such data ensures full compliance and significantly reduces our customers' compliance burdens as well.

Several providers of web analytics claim GDPR compliance by collecting non-personal data, but the claims are not always true. Sometimes the data is combined in a way that makes the user identifiable and enables tracking- which qualifies as personal data under the GDPR.

At Simple Analytics, **when we say we do not collect personal data, we mean it**. Our non-personal data collection is not combined in a way that can track or identify users- and would not be sufficient to do so anyway. We offer genuine compliance, not dubious legal workarounds.

## PECR

[ICO](https://ico.org.uk/), UK's independent body set up to uphold information rights, has updated its laws. They published a [blog](https://ico.org.uk/about-the-ico/news-and-events/news-and-blogs/2019/07/blog-cookies-what-does-good-look-like/) with the most common myths about cookies and [complete guidance](https://ico.org.uk/for-organisations/guide-to-pecr/guidance-on-the-use-of-cookies-and-similar-technologies/) on the use of cookies and similar technologies ([pdf](https://ico.org.uk/media/for-organisations/guide-to-pecr/guidance-on-the-use-of-cookies-and-similar-technologies-1-0.pdf)).

Simple Analytics is PECR compliant and does not need consent. We track page views from a script in the browser where we don't use cookies or similar technologies. We don't store IPs in any way and don't use techniques that identify or track a user. [Read here](/what-we-collect) what metrics we store and or collect.

### PECR vs. GDPR

Basically, the ICO says: "PECR first, GDPR second."

> The simplest way to understand it is that if your cookies require consent under PECR, then you cannot use one of the alternative lawful bases from the GDPR to set them. If you’re placing cookies, this is why you need to look to PECR first and comply with its specific rules before considering any of the general rules in the GDPR.
> <small>[source](https://ico.org.uk/for-organisations/guide-to-pecr/guidance-on-the-use-of-cookies-and-similar-technologies/how-do-the-cookie-rules-relate-to-the-gdpr/#GDPR3)</small>

### When do you need consent?

You need consent when cookies are not strictly necessary:

> 'Strictly necessary' means that storage of (or access to) information should be essential, rather than reasonably necessary. It is also restricted to what is essential to provide the service requested by the user. **It does not cover what might be essential for any other uses that you might wish to make of that data.** It is therefore clear that the strictly necessary exemption has a narrow application.

All cookies that are used for analytics do require consent. Simple Analytics does not use any cookies and does not require any consent.

### What ICO says about Simple Analytics

After contacting Daniel Morgan from ICO about the need for consent with Simple Analytics he replied:

> [Regulation 6](https://ico.org.uk/for-organisations/guide-to-pecr/guidance-on-the-use-of-cookies-and-similar-technologies/what-are-the-rules-on-cookies-and-similar-technologies/#rules1) of the PECR requires you to obtain consent from the user wherever you wish to store or gain access to information stored within their terminal equipment (a computer or device). This is applicable to the use of cookies and all [similar technologies](https://ico.org.uk/for-organisations/guide-to-pecr/guidance-on-the-use-of-cookies-and-similar-technologies/what-are-cookies-and-similar-technologies/#cookies5) and techniques, such as device fingerprinting.
>
> If you do not rely on techniques which involve storing or gaining access to information within users' devices in order to produce analytics data for your clients, then this will not fall under Regulation 6 and you will not need to obtain consent.

We do not rely on techniques to store or gaining access to information within users' devices. We do collect information about the devices (like screen size), but that is not applicable to the use of cookies and similar technologies.

Most competitors in the privacy space do use similar technologies like hashing an IP address. For those, you would need consent.

### Tool

Use [ICO's tool](https://ico.org.uk/for-organisations/where-does-consent-apply-for-cookies/) to determine where consent applies for your use of cookies.

We advise you to include us in your privacy policy. [Read more on that here](your-privacy-policy).

<small>Sources used: [insideprivacy.com](https://www.insideprivacy.com/data-privacy/ico-updates-guidance-on-cookies-and-similar-technologies/).</small>

## CCPA compliance

Simple Analytics is **CCPA compliant out of the box** because it avoids collecting any information that falls under the CCPA.

The CCPA applies to the personal information and defines “personal information” as “information that identifies, relates to, or could reasonably be linked with a user or their household”. Simple Analytics collects no such information from the end user.

## HIPAA Compliance

Simple Analytics can easily comply with HIPAA because **it does not collect any personally identifiable data from your visitors**. When no personally identifiable data are collected, the data we receive are not PHI and do not fall under the HIPAA Privacy Rule’s disclosure limitations.

In other words, **you don’t need to worry about HIPAA**.

### Why doesn’t Simple Analytics receive PHI?

Because we do not use cookies or other identifiers, we do not fingerprint users, either. In other words, **Simple Analytics is 100% tracking-free** and privacy-friendly. We only use visitors’ IP addresses for communication and drop them right after we serve requests- in other words, IP is never stored or used to track.

Using IP for communication without storing them is not considered collecting personal data. However, this could even be avoided altogether by implementing a proxy. This can be done easily by implementing a few lines of code on your website- click here for a [step-by-step guide](https://docs.simpleanalytics.com/proxy).

### Does Simple Analytics need a BAA?

You do not need a BAA to use Simple Analytics. You only need a BAA when an associate receives PHI from you. Since we do not receive any PHI, this is not relevant for Simple Analytics. Therefore, we do not qualify as Business Associates and do not require a BAA.

## ePrivacy and TTDSG Compliance

Article 5(3) of the EU’s ePrivacy Directive protects data stored on end-user devices. Simple Analytics complies effortlessly by not collecting such data.

This approach also ensures compliance with the PECR (UK) and TTDSG (Germany), which are implementations of the ePrivacy Directive within national laws.

## Compliance FAQ

### Does Simple Analytics collect personal data?

**Simple Analytics does not collect personal data**. We do not use cookies or similar tracking technologies. We are also careful to avoid collecting any metrics that could be used for finger-printing and singling out a user (Recital 26 GDPR). None of the data we collect fall under the GDPR.

Simple Analytics **drops IP addresses** and **never processes them**. 

### What does Simple Analytics do with IP addresses?

When IP addresses are sent to us, they are immediately discarded after each request. We do not process, log, store, or transfer IP addresses at any point.

Optionally, Simple Analytics can check IP addresses against a list of known bot addresses. This allows us to filter out the data for bots and keep your analytics accurate. Even in this scenario, IP addresses are discarded immediately after the check.

### What is Simple Analytics’ role in the processing of the data?

The notions of data controller and data processor are defined concerning personal data by the GDPR (see Articles 4(7) and (8) GDPR). We only collect anonymous metrics. Therefore, **we are neither data controllers nor data processors** concerning the data we collect and process for our customers.

Simple Analytics is a **sole** **data controller** concerning IP addresses.

### What are your legal bases for processing the data?

The anonymized metrics collected by Simple Analytics are not personal data. They do not fall under the GDPR, and Articles 5(1)(a) and 6 do not apply to them. **No legal basis is needed to process anonymous data**.

IP addresses are processed by Simple Analytics as a sole data controller based on its **legitimate interest** (Art. 6(1)(f) GDPR) to provide the service.

### What legal bases can I rely upon to process the data?

Using Simple Analytics does not make you a controller of personal data. **You do not need a legal basis** to process the data, as the GDPR and the principle of lawfulness (5(1)(a) GDPR) do not apply to anonymous data.

### Do I need a DPA to use Simple Analytics?

You do not need to sign a data processing agreement with Simple Analytics, as we do not collect personal data and are not considered a processor under GDPR and UK GDPR. However, we are available to discuss custom agreements regarding data protection issues.

### Does Simple Analytics use third-party providers?

We rely on Dutch companies Worldserver and Leaseweb to store data. We also rely on BunnyCDN to deliver content. BunnyCDN is part of Slovenian company BunnyWay.

Worldserver, Leaseweb, and Bunnyweb are **trusted, European, and GDPR-compliant providers with infrastructure located in the EU**. We don’t need to use European providers, as non-personal data can be transferred without limitations under the GDPR. We still choose to do so to ensure that the processing is as transparent and confidential as possible.

### Does Simple Analytics require a privacy notice or a privacy policy?

**Simple Analytics does not require a privacy notice**. Our customers are not controllers of personal data and are not required to provide any information under Art. 13 GDPR, as the provision only applies to the data controller.

For the same reason, it is not mandatory to include Simple Analytics in a website’s privacy policy. We still encourage our customers to do so to be as transparent as possible. [This page](/your-privacy-policy)

### How can I add Simple Analytics to my privacy policy?

Adding us to your privacy policy is not strictly necessary, but we still encourage you to do so in order to be as transparent as possible with your visitors. This is a template you can use or take inspiration from:

We use anonymous metrics to understand how you use your website and where our traffic comes from. We use this insight to improve our website and create a better experience for visitors. We do not track you, serve personalized advertising, or sell the data to anyone.

Our website is powered by Simple Analytics, a privacy-friendly web analytics provider. You can learn more about Simple Analytics on its website.
