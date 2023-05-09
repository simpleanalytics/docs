---
title: Proxy all requests
category: install-script
permalink: /proxy
last_modified_at: 2023-05-08
---

Are you concerned about your visitors' privacy when using Simple Analytics? We understand that keeping your visitors' IP addresses private is important, which is why we offer a simple proxy setup using Caddy or NGINX. We never store your visitors' IP addresses but with a proxy you don't have to trust us. The rest of this article is targeted at your development team.

If you prefer to use Caddy, you can easily configure it to act as a proxy by adding a few lines to your Caddyfile. Similarly, if you're already using NGINX, you can add the necessary configuration to your server directive.

By setting up a proxy, you can prevent any IPs from your visitors from ending up on our servers. It's a quick and easy way to protect your visitors' privacy, and it's something we recommend if you have the resources.

<details markdown="1">
  <summary>Set up proxy in NGINX</summary>

> Trailing slashed are very important here. Keep them as they are in this example.

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
  expires 7d;
  add_header Strict-Transport-Security "max-age=31536000; includeSubDomains" always;
  proxy_pass https://simpleanalyticsexternal.com/proxy.js?hostname=example.com&path=/simple;
}
```

Change `example.com` to the domain you run the proxy on. This can be the same domain as your own website is hosted on.

> You can change the path that you proxy from (`/simple/`) to something else. Make sure to also update that in the second `proxy_pass` (`&path=/simple`).

If you reload your NGINX config with `sudo nginx -t && sudo nginx -s reload` you should be able to visit the script at `https://example.com/proxy.js`. 

</details>

<details markdown="1">
  <summary>Set up proxy in Caddy</summary>
  
```
example.com {
  handle /simple/* {
    uri strip_prefix /simple
    reverse_proxy https://queue.simpleanalyticscdn.com {
      header_up X-Caddy-Proxy "true"
    }
  }
  handle /proxy.js {
    rewrite * /proxy.js?{query}&hostname=example.com&path=/simple
    reverse_proxy https://simpleanalyticsexternal.com
  }
}
```

Change `example.com` to the domain you run the proxy on. This can be the same domain as your own website is hosted on.

> Thanks to [captcha.eu](https://www.captcha.eu/) to provide us the Caddy configuration.

</details>

After these changes you should be able to visit the script at `https://example.com/proxy.js`.

The embed script should be changed into this:

```html
<script async defer src="https://example.com/proxy.js"></script>
<noscript
  ><img
    src="https://example.com/simple/noscript.gif"
    alt=""
    referrerpolicy="no-referrer-when-downgrade"
/></noscript>
```

> Note the `/simple` prefix in the `noscript.gif` image and the non prefix in `proxy.js`.

This will send all traffic via your proxy on the endpoint `/simple/...`.

[Let us know](https://simpleanalytics.com/contact) if we can help you with anything!
