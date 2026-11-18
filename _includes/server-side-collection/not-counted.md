An integration only sees the requests that reach the website's server. These pages are not counted, and there's no fix for them yet:

- **Pages a CDN or cache in front of the server answers,** like Cloudflare, Fastly or CloudFront when they cache pages and not only files, Varnish, or the `proxy_cache` of Nginx.
- **Pages the web server answers without the app,** like HTML files that Nginx or Apache serve from disk, or a full-page cache that answers before the app's code runs, which many WordPress caching plugins do.
- **Websites without a server,** like static exports, GitHub Pages, or files on a CDN or in a storage bucket.
- **Responses other than `200`,** like `304 Not Modified` when a browser or robot checks a page it already has.

With Next.js, `trackRequest` runs before the cache of Next.js and Vercel, so their cached and static pages are counted. A CDN in front of Next.js still answers without it.
