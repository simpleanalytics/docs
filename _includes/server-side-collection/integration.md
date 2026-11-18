Write the integration in the website's own code and language. Use the standard library or an HTTP client the app already has, and keep it in one small piece of code, like a middleware, plus its configuration.

### Where it runs

Run it for every request, in a middleware, filter or hook that sees the request and, when the framework allows it, the response. It must never make a page slower or break it, so report a request after the response is sent, or alongside it:

- Use the framework's hook for work after the response when it has one, like the `terminate` method of a Laravel middleware, `res.on("finish")` in Express or `rack.after_reply` in Puma. In plain PHP, call `fastcgi_finish_request()` first when it exists.
- On serverless platforms the code stops when the response is sent, so hand the report to the platform's `waitUntil`, like `ctx.waitUntil` in Cloudflare Workers or `waitUntil` from `@vercel/functions` on Vercel.
- Otherwise start it in the background without waiting for it, like in a goroutine or a thread pool.

### Configuration

- **Hostname:** the hostname of the website in Simple Analytics, like `example.com`. Keep it in the app's configuration, where its other settings live, as `SIMPLE_ANALYTICS_HOSTNAME` when the app uses environment variables. Never read it from the request's `Host` header. Without a hostname the integration does nothing, so leave it empty on staging and preview deployments.
- **Extra query parameters:** the parameters to report besides the default ones, empty unless the website needs more.
- **Test mode:** off by default, on when the environment variable `SIMPLE_ANALYTICS_TEST_MODE` is `1` or `true`. See test mode below.

Outside test mode, report only from production, the way the app already tells production apart, like `NODE_ENV`, `APP_ENV`, `RAILS_ENV` or Django's `DEBUG`. Otherwise the requests you make while developing are recorded too.

### Which requests it reports

Report a request only when all of these are true:

1. Its method is `GET`.
2. Its path doesn't end in the file extension of a stylesheet, JavaScript, image, font, audio, video or JSON file, in any case: `.css`, `.js`, `.mjs`, `.cjs`, `.apng`, `.avif`, `.bmp`, `.gif`, `.ico`, `.jpg`, `.jpeg`, `.png`, `.svg`, `.tif`, `.tiff`, `.webp`, `.eot`, `.otf`, `.ttf`, `.woff`, `.woff2`, `.aac`, `.flac`, `.m4a`, `.mp3`, `.oga`, `.ogg`, `.opus`, `.wav`, `.weba`, `.m4v`, `.mov`, `.mp4`, `.ogv`, `.webm`, `.json`, `.map` or `.webmanifest`.
3. When the integration sees the response: its status is `200`, and its media type isn't one of those either: `text/css`, `text/javascript`, `application/javascript`, anything that starts with `image/`, `font/`, `audio/` or `video/`, `application/json`, or anything that ends in `+json`. The media type is the part before any `;` of the response's `Content-Type`, trimmed and compared case-insensitively, so `application/json; charset=utf-8` and `Text/CSS` are skipped and `text/html; charset=utf-8` is reported.

Pages are reported, also `.html`, `.txt`, `.xml` and `.pdf` files. Don't filter on anything else: no lists of user agents or addresses, and no checks of other request headers. Simple Analytics decides who made each request, so the requests of people are sent too.

### What it sends

One `POST` request to `https://queue.simpleanalyticscdn.com/requests`, with the header `Content-Type: application/json` and one flat JSON object as its body:

```json
{
  "version": 1,
  "platform": "laravel",
  "hostname": "example.com",
  "path": "/pricing",
  "query": "utm_source=chatgpt.com",
  "status": 200,
  "content_type": "text/html; charset=utf-8",
  "user_agent": "Mozilla/5.0 AppleWebKit/537.36 (KHTML, like Gecko); compatible; ChatGPT-User/1.0; +https://openai.com/bot",
  "referer": "https://chatgpt.com/",
  "accept": "text/html,application/xhtml+xml",
  "accept_language": "en-US",
  "sec_fetch_mode": "navigate"
}
```

| Field | Sent | Value |
| --- | --- | --- |
| `version` | Always | The number `1` |
| `platform` | Always | The framework, or the runtime or language when there is no framework, in lower case letters, digits and hyphens: `laravel`, `symfony`, `wordpress`, `php`, `django`, `flask`, `fastapi`, `python`, `rails`, `sinatra`, `ruby`, `express`, `fastify`, `nestjs`, `hono`, `sveltekit`, `nuxt`, `astro`, `remix`, `nodejs`, `cloudflare-workers`, `phoenix`, `go`, `aspnet`, `spring` and so on. `nextjs` is for the Next.js package. |
| `hostname` | Always | The hostname from the configuration |
| `path` | Always | The path the visitor requested, in full: it starts with `/`, includes any prefix the app is served under, has no query string, and keeps the percent-encoding of the request. Not a route pattern. |
| `query` | When at least one allowed parameter is present | Only the allowed query parameters, in the order they came in, as `name=value` pairs joined by `&`, percent-encoded and without `?`. Leave the field out when none is present. Other parameters, like tokens, never leave the server. |
| `status` | When the integration sees the response | The number `200`, because only those are reported |
| `content_type` | When the integration sees the response | The response's `Content-Type` header, unchanged |
| `test` | In test mode only | `true` |
| Copied request headers | When the request has the header, even when it's empty | The header's value, unchanged, under the field in the table below |

The allowed query parameters are `utm_source`, `utm_medium`, `utm_campaign`, `utm_content`, `utm_term`, `source`, `medium`, `campaign`, `content`, `term` and `ref`, plus the extra ones from the configuration. Names must match exactly. A parameter that appears twice is sent twice.

| Field | Request header |
| --- | --- |
| `user_agent` | `User-Agent` |
| `referer` | `Referer` |
| `accept` | `Accept` |
| `accept_language` | `Accept-Language` |
| `sec_fetch_mode` | `Sec-Fetch-Mode` |
| `sec_fetch_dest` | `Sec-Fetch-Dest` |
| `sec_fetch_site` | `Sec-Fetch-Site` |
| `sec_fetch_user` | `Sec-Fetch-User` |
| `sec_ch_ua` | `Sec-CH-UA` |
| `signature_agent` | `Signature-Agent` |
| `from` | `From` |

These request headers travel in the body, not as headers, because HTTP clients like Node.js's `fetch` set their own `User-Agent`, `Accept`, `Accept-Language` and `Sec-Fetch-Mode`. Send no other fields: never cookies, the `Authorization` header, other request headers, the full URL or addresses in the body.

### Addresses

The request to Simple Analytics carries the visitor's addresses in its headers:

- **`X-Forwarded-For`:** the `X-Forwarded-For` header of the incoming request, unchanged, then `, ` and the address of the connection the request came in on. Without an incoming header, only the address of the connection. Don't remove, reorder or check entries, and add nothing else, because Simple Analytics needs the order to tell the visitor apart from proxies.
- **`CF-Connecting-IP` and `True-Client-IP`:** when the incoming request has them, pass them on unchanged, under the same names.

Send no other headers of the incoming request: never `Cookie` or `Authorization`.

The address of the connection is the address at the other end of the network connection, without a port, like `req.socket.remoteAddress` in Node.js, `$_SERVER['REMOTE_ADDR']` in PHP, `request.META["REMOTE_ADDR"]` in Django, `request.remote_addr` in Rails or the address part of `r.RemoteAddr` in Go. Helpers that take the visitor's address from `X-Forwarded-For` give the wrong value, like `req.ip` in Express, `$request->ip()` in Laravel or `request.remote_ip` in Rails. When the app has middleware that replaces the connection's address or `X-Forwarded-For`, like Flask's `ProxyFix`, the proxy headers of Uvicorn or the forwarded headers middleware of ASP.NET Core, read the original values it keeps, or read them before it runs.

When the code gets no connection address, like behind a Unix socket or on a serverless platform, send the incoming `X-Forwarded-For` unchanged:

- **Vercel functions:** Vercel [sets `X-Forwarded-For`](https://vercel.com/docs/headers/request-headers#x-forwarded-for) to the address of the client that made the request.
- **Cloudflare Workers:** Cloudflare documents that [`CF-Connecting-IP`](https://developers.cloudflare.com/fundamentals/reference/http-headers/#cf-connecting-ip) holds the client's address, and that a Worker [controls the `CF-Connecting-IP`](https://developers.cloudflare.com/fundamentals/reference/http-headers/#cf-connecting-ip-in-worker-subrequests) it sends to a destination outside Cloudflare. Pass it on. Cloudflare doesn't document whether an `X-Forwarded-For` header a Worker sets arrives unchanged, so say so in your report.

Simple Analytics uses these addresses in memory only and never stores or logs them.

### How it sends

- **One attempt** that gives up after 2 seconds, reading the reply included, like with `AbortSignal.timeout(2000)` in JavaScript or a 2 second timeout on the HTTP client. Never retry, queue or batch reports.
- **Errors are swallowed:** catch every error, timeouts too, and carry on. A failed report never changes the response.
- **Silent:** outside test mode, log nothing: no errors, addresses, headers or replies.
- **Any reply is fine:** `202` with an empty body means Simple Analytics accepted the request, whether it stores it or not. `400` means the payload is wrong. Outside test mode, don't read the reply.

### Test mode

Test mode lets you check the integration without storing anything. When it's on:

1. Add `"test": true` to the body. Simple Analytics then stores nothing, and replies `200` with JSON that says what it would store.
2. Report requests also outside production, so it works on a development computer.
3. Wait for the reply, still at most 2 seconds, and print one block to the server's console or log, in this form:

   ```
   Simple Analytics test mode: sent {"version":1,"platform":"express","hostname":"example.com","path":"/","test":true,...}
   with address headers {"X-Forwarded-For":"127.0.0.1"}
   queue replied 200: {"test":true,"outcome":"ai_agent","name":"ChatGPT-User",...}
   ```

   When the request fails, print `Simple Analytics test mode: the request was not reported:` and the error.
4. Never print the incoming URL or other request headers, so tokens in them stay out of the log.

The reply has these fields:

- `outcome`: `ai_agent`, `robot`, `person` or `health_checker`. People and health checkers, like `kube-probe`, are never stored.
- `name`: the name Simple Analytics would store, like `ChatGPT-User`, `Googlebot`, `curl` or `Unidentified`, the health checker's name, or `null` for a person.
- `reason`: why, like `ai_agent_name`, `robot_name`, `robot_word`, `not_a_browser`, `datacenter_addresses`, `health_checker` or `person`.
- `would_store`: the page view it would store, without addresses, or `null`.
- `addresses`: each address it received, the header it came in, what it belongs to (`private`, `own_proxy`, `cdn`, `datacenter` or `other`), and whether it was judged.

An invalid payload gets `400` with `errors`, a list of what is wrong. Test mode prints visitors' addresses and stores nothing, so it's never on in production.
