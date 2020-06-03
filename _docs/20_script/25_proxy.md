---
title: Proxy all requests
category: script
permalink: /proxy
---

If you really want to prevent any IPs of your visitors to end up on our servers you can setup a simple proxy. We are a huge fan of NGINX. If you have a domain, let's say `example.com` and you want to have setup a proxy you would add this to your server directive in NGINX:

```
location /simple/ {
  proxy_set_header  X-Forwarded-Proto $scheme;
  proxy_set_header  X-Forwarded-Proto-Version $http2;
  proxy_set_header  Host $http_host;
  proxy_set_header  X-NginX-Proxy true;
  proxy_set_header  Connection "";
  proxy_pass_request_headers on;
  proxy_pass https://queue.simpleanalyticscdn.com/;
}

location = /proxy.js {
  proxy_pass https://external.simpleanalytics.com/proxy.js?hostname=example.com&path=/simple;
}
```

Change `example.com` to the domain you run the proxy on. This can be the same domain as your own website is hosted on.

If you reload your NGINX config with `sudo nginx -t && sudo nginx -s reload` you should be able to visit the script at `https://example.com/proxy.js`. Just embed this script in your HTML:

```html
<script async defer src="https://example.com/proxy.js"></script>
<noscript><img src="https://example.com/simple/noscript.gif" alt=""
/></noscript>
```

This will send all traffic via your proxy on the endpoint `/simple/...`.

[Let us know](https://simpleanalytics.com/contact) if we can help you with anything!
