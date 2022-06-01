---
title: Data points
category: general
permalink: /data-points
excerpt: "We never track visitors so the data below is never linked to one specific visitor. Here is a list of data points we collect."
last_modified_at: 2022-04-14
---

Here is a list of data points we collect.

> Want a more general overview? [Go to our general overview](/what-we-collect) of what we collect.

With every page view, we collect some data points. We never track visitors, so the data below is never linked to one specific visitor.

<hr style="border: none; background-color: #eef9ff; height: 5px; margin-top: 2rem;" />

### URL of the page

<p class="rating"><svg xmlns="http://www.w3.org/2000/svg" width="16px" viewBox="0 0 24 24"><circle cx="12" cy="12" r="12" fill="#65aed7"/></svg> <svg xmlns="http://www.w3.org/2000/svg" width="16px" viewBox="0 0 24 24"><circle cx="12" cy="12" r="12" fill="#65aed7"/></svg> <svg xmlns="http://www.w3.org/2000/svg" width="16px" viewBox="0 0 24 24"><circle cx="12" cy="12" r="12" fill="#65aed7"/></svg> Very important</p>

For example `https://simpleanalytics.com/contact`

We store this URL in parts in our database.

### Referrer

<p class="rating"><svg xmlns="http://www.w3.org/2000/svg" width="16px" viewBox="0 0 24 24"><circle cx="12" cy="12" r="12" fill="#65aed7"/></svg> <svg xmlns="http://www.w3.org/2000/svg" width="16px" viewBox="0 0 24 24"><circle cx="12" cy="12" r="12" fill="#65aed7"/></svg> <svg xmlns="http://www.w3.org/2000/svg" width="16px" viewBox="0 0 24 24"><circle cx="12" cy="12" r="12" fill="#65aed7"/></svg> Very important</p>

To know where customers come from, we store the page's referrer. This means that a customer can see where a visitor is coming from—for example, `duckduckgo.com`.

### UTM codes

<p class="rating"><svg xmlns="http://www.w3.org/2000/svg" width="16px" viewBox="0 0 24 24"><circle cx="12" cy="12" r="12" fill="#65aed7"/></svg> <svg xmlns="http://www.w3.org/2000/svg" width="16px" viewBox="0 0 24 24"><circle cx="12" cy="12" r="12" fill="#65aed7"/></svg> <svg xmlns="http://www.w3.org/2000/svg" width="16px" viewBox="0 0 24 24"><path fill="#65aed7" fill-rule="evenodd" d="M12 24a12 12 0 1 0 0-24 12 12 0 0 0 0 24Zm0-5a7 7 0 1 0 0-14 7 7 0 0 0 0 14Z" /></svg> Somewhat important</p>

For example `https://simpleanalytics.com/?utm_source=newsletter`

The part after the `?` is called [URL parameters](/how-to-use-url-parameters). We only keep the UTM codes and drop all other URL parameters. The UTM codes are something that the customer adds to the URLs. For example, to know how many visitors came via the newsletter. [See below][5].

### Unique

<p class="rating"><svg xmlns="http://www.w3.org/2000/svg" width="16px" viewBox="0 0 24 24"><circle cx="12" cy="12" r="12" fill="#65aed7"/></svg> <svg xmlns="http://www.w3.org/2000/svg" width="16px" viewBox="0 0 24 24"><circle cx="12" cy="12" r="12" fill="#65aed7"/></svg> <svg xmlns="http://www.w3.org/2000/svg" width="16px" viewBox="0 0 24 24"><circle cx="12" cy="12" r="12" fill="#65aed7"/></svg> Very important</p>

If a page view is unique or not. A simple yes or no.

### Country / time zone

<p class="rating"><svg xmlns="http://www.w3.org/2000/svg" width="16px" viewBox="0 0 24 24"><circle cx="12" cy="12" r="12" fill="#65aed7"/></svg> <svg xmlns="http://www.w3.org/2000/svg" width="16px" viewBox="0 0 24 24"><circle cx="12" cy="12" r="12" fill="#65aed7"/></svg> <svg xmlns="http://www.w3.org/2000/svg" width="16px" viewBox="0 0 24 24"><path fill="#65aed7" fill-rule="evenodd" d="M12 24a12 12 0 1 0 0-24 12 12 0 0 0 0 24Zm0-5a7 7 0 1 0 0-14 7 7 0 0 0 0 14Z" /></svg> Somewhat important</p>

We collect the time zone of the browser. For example, `Europe/Amsterdam`. From this time zone, we derive the country. Every country has at least one time zone, and devices automatically update to the local time zone.

### IDs

We collect three IDs:

1. ID of the page view <span class="rating scaled"><svg xmlns="http://www.w3.org/2000/svg" width="16px" viewBox="0 0 24 24"><circle cx="12" cy="12" r="12" fill="#65aed7"/></svg> <svg xmlns="http://www.w3.org/2000/svg" width="16px" viewBox="0 0 24 24"><circle cx="12" cy="12" r="12" fill="#65aed7"/></svg> <svg xmlns="http://www.w3.org/2000/svg" width="16px" viewBox="0 0 24 24"><path fill="#65aed7" fill-rule="evenodd" d="M12 24a12 12 0 1 0 0-24 12 12 0 0 0 0 24Zm0-5a7 7 0 1 0 0-14 7 7 0 0 0 0 14Z" /></svg> Somewhat important</span>
1. ID of the page <span class="rating scaled"><svg xmlns="http://www.w3.org/2000/svg" width="16px" viewBox="0 0 24 24"><circle cx="12" cy="12" r="12" fill="#65aed7"/></svg> <svg xmlns="http://www.w3.org/2000/svg" width="16px" viewBox="0 0 24 24"><path fill="#65aed7" fill-rule="evenodd" d="M12 24a12 12 0 1 0 0-24 12 12 0 0 0 0 24Zm0-5a7 7 0 1 0 0-14 7 7 0 0 0 0 14Z" /></svg> <svg xmlns="http://www.w3.org/2000/svg" width="16px" viewBox="0 0 24 24"><path fill="#65aed7" fill-rule="evenodd" d="M12 24a12 12 0 1 0 0-24 12 12 0 0 0 0 24Zm0-5a7 7 0 1 0 0-14 7 7 0 0 0 0 14Z" /></svg> Less important</span>
1. ID of the session <span class="rating scaled"><svg xmlns="http://www.w3.org/2000/svg" width="16px" viewBox="0 0 24 24"><circle cx="12" cy="12" r="12" fill="#65aed7"/></svg> <svg xmlns="http://www.w3.org/2000/svg" width="16px" viewBox="0 0 24 24"><path fill="#65aed7" fill-rule="evenodd" d="M12 24a12 12 0 1 0 0-24 12 12 0 0 0 0 24Zm0-5a7 7 0 1 0 0-14 7 7 0 0 0 0 14Z" /></svg> <svg xmlns="http://www.w3.org/2000/svg" width="16px" viewBox="0 0 24 24"><path fill="#65aed7" fill-rule="evenodd" d="M12 24a12 12 0 1 0 0-24 12 12 0 0 0 0 24Zm0-5a7 7 0 1 0 0-14 7 7 0 0 0 0 14Z" /></svg> Less important</span>

At Simple Analytics, we don't really have sessions. They only live for as long as the website is open. When a customer has a SPA (Single Page Application), the session ends when the website is closed. If the customer doesn't have a SPA, the session ends with every navigation.

### Scrolled percentage & time on page

<p class="rating"><svg xmlns="http://www.w3.org/2000/svg" width="16px" viewBox="0 0 24 24"><circle cx="12" cy="12" r="12" fill="#65aed7"/></svg> <svg xmlns="http://www.w3.org/2000/svg" width="16px" viewBox="0 0 24 24"><circle cx="12" cy="12" r="12" fill="#65aed7"/></svg> <svg xmlns="http://www.w3.org/2000/svg" width="16px" viewBox="0 0 24 24"><path fill="#65aed7" fill-rule="evenodd" d="M12 24a12 12 0 1 0 0-24 12 12 0 0 0 0 24Zm0-5a7 7 0 1 0 0-14 7 7 0 0 0 0 14Z" /></svg> Somewhat important</p>

We collect those numbers to know how far visitors scrolled (for example, 80%) and how long they were on the page (for example, 45 seconds). The "The ID of the page view" is required.

> The page view ID is required for time on page.

### User-agent

<p class="rating"><svg xmlns="http://www.w3.org/2000/svg" width="16px" viewBox="0 0 24 24"><circle cx="12" cy="12" r="12" fill="#65aed7"/></svg> <svg xmlns="http://www.w3.org/2000/svg" width="16px" viewBox="0 0 24 24"><circle cx="12" cy="12" r="12" fill="#65aed7"/></svg> <svg xmlns="http://www.w3.org/2000/svg" width="16px" viewBox="0 0 24 24"><path fill="#65aed7" fill-rule="evenodd" d="M12 24a12 12 0 1 0 0-24 12 12 0 0 0 0 24Zm0-5a7 7 0 1 0 0-14 7 7 0 0 0 0 14Z" /></svg> Somewhat important</p>

To know which type of device the visitor used, we store the user agent. This is a data point that is the same for many visitors. It shows the browser used, the operating system, and the type of device. [See below][6].

### Script settings

<p class="rating"><svg xmlns="http://www.w3.org/2000/svg" width="16px" viewBox="0 0 24 24"><circle cx="12" cy="12" r="12" fill="#65aed7"/></svg> <svg xmlns="http://www.w3.org/2000/svg" width="16px" viewBox="0 0 24 24"><circle cx="12" cy="12" r="12" fill="#65aed7"/></svg> <svg xmlns="http://www.w3.org/2000/svg" width="16px" viewBox="0 0 24 24"><path fill="#65aed7" fill-rule="evenodd" d="M12 24a12 12 0 1 0 0-24 12 12 0 0 0 0 24Zm0-5a7 7 0 1 0 0-14 7 7 0 0 0 0 14Z" /></svg> Somewhat important</p>

We send some script settings along with the page view. To identify the embed script and check if the page view comes from a robot.

### Dimensions

<p class="rating"><svg xmlns="http://www.w3.org/2000/svg" width="16px" viewBox="0 0 24 24"><circle cx="12" cy="12" r="12" fill="#65aed7"/></svg> <svg xmlns="http://www.w3.org/2000/svg" width="16px" viewBox="0 0 24 24"><path fill="#65aed7" fill-rule="evenodd" d="M12 24a12 12 0 1 0 0-24 12 12 0 0 0 0 24Zm0-5a7 7 0 1 0 0-14 7 7 0 0 0 0 14Z" /></svg> <svg xmlns="http://www.w3.org/2000/svg" width="16px" viewBox="0 0 24 24"><path fill="#65aed7" fill-rule="evenodd" d="M12 24a12 12 0 1 0 0-24 12 12 0 0 0 0 24Zm0-5a7 7 0 1 0 0-14 7 7 0 0 0 0 14Z" /></svg> Less important</p>

We collect the dimensions of the screen of the device. There are two dimensions: the viewport and the screen. The viewport is the part where the website runs in; the screen is the dimensions of the complete screen of the device.

### Language

<p class="rating"><svg xmlns="http://www.w3.org/2000/svg" width="16px" viewBox="0 0 24 24"><circle cx="12" cy="12" r="12" fill="#65aed7"/></svg> <svg xmlns="http://www.w3.org/2000/svg" width="16px" viewBox="0 0 24 24"><path fill="#65aed7" fill-rule="evenodd" d="M12 24a12 12 0 1 0 0-24 12 12 0 0 0 0 24Zm0-5a7 7 0 1 0 0-14 7 7 0 0 0 0 14Z" /></svg> <svg xmlns="http://www.w3.org/2000/svg" width="16px" viewBox="0 0 24 24"><path fill="#65aed7" fill-rule="evenodd" d="M12 24a12 12 0 1 0 0-24 12 12 0 0 0 0 24Zm0-5a7 7 0 1 0 0-14 7 7 0 0 0 0 14Z" /></svg> Less important</p>

The language of the browser, for example, `en-US`.

<p style="text-align: center; margin-top: 4rem;">That's it!</p>

<hr style="border: none; background-color: #eef9ff; height: 5px;" />

## UTM codes explained

UTM codes are bits of text you can add to a link that tell Simple Analytics (as well as other analytics tools) a little bit more information about each link. Here's a sample of what one looks like:

```
https://example.com/landing-page?utm_source=company-x&utm_medium=newsletter&utm_campaign=march
```

[Read the UTM guide](https://buffer.com/library/utm-guide/) at Buffer.

## User-agent strings

Browsers or devices identify themselves to websites. They give themselves some kind of name. For example, a user agent can look like this ([wiki][1]):

```
Mozilla/5.0 (iPad; U; CPU OS 3_2_1) AppleWebKit/531.21.10 (KHTML, like Gecko) Mobile/7B40598
```

It's not needed, privacy-wise, but we replace long numbers with zeros. After cleanup, it looks like this:

```
Mozilla/5.0 (iPad; U; CPU OS 3_2_0) AppleWebKit/531.21.0 (KHTML, like Gecko) Mobile/7B40000
```

In some browsers we collect browser name and operating system name without the user agent but via the [user agent client hints](https://wicg.github.io/ua-client-hints/).

[1]: https://en.wikipedia.org/wiki/User_agent
[2]: /explained/unique-visits
[3]: https://en.wikipedia.org/wiki/HTTP_referer
[4]: /overwrite-domain-name
[5]: #utm-codes-explained
[6]: #user-agents-strings

<style>
  .rating {
    display: inline-flex;
    margin: 0;
    background-color: #eef9ff;
    padding: 3px 8px;
    border-radius: 5px;
  }
  .rating svg {
    margin-right: 5px;
  }
  .rating.scaled {
    transform: scale(0.7) translateY(5px);
    transform-origin: bottom left;
    margin-bottom: -5px;
    margin-top: -12px;
  }
</style>
