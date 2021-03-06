---
title: SRI version
category: script
permalink: /sri
sriVersion: 6
sriHash: sha256-SsAnjogPdVtk4SMT17C1H4hnlmdROlA+F8e6HWisc4s= sha384-LyCEiwCP+ZHrg0L2SL6oSPengdhyuzj0UVZ5vk/Nb3D8Pdz5FHc2rDk/5Kvv+TxK sha512-G62RkDPYjOD3RbUpgAHIHpZ8hDCheNWZbPx7GG5S0HCOBtaA0ZkNpYK/ioAmcS7im1KQOTXQqcGfNGDaaOg6GA==
---

If you want to use SRI you can do this by using specific scripts. The default scripts are changing to reflect new features or code optimizations. You want to use SRI if you consider it a risk when our scripts change. You can also host our SRI script on your own server or CDN.

When you want to use our SRI version of our script you will need to update your script to `https://scripts.simpleanalyticscdn.com/sri/v{{ page.sriVersion }}.js`. The full embed script becomes:

<!-- prettier-ignore -->
```html
<script async defer src="https://scripts.simpleanalyticscdn.com/sri/v{{ page.sriVersion }}.js" integrity="{{ page.sriHash }}" crossorigin="anonymous"></script>
<noscript><img src="https://queue.simpleanalyticscdn.com/noscript.gif" alt="" referrerpolicy="no-referrer-when-downgrade" /></noscript>
```

When using a [custom domain](/bypass-ad-blockers) you need to use this script: `https://CUSTOM.DOMAIN/v{{ page.sriVersion }}/app.js`. Replace the `CUSTOM.DOMAIN` with your custom domain. To generate an SRI hash for your custom domain you can use [report-uri.com](https://report-uri.com/home/sri_hash) or [srihash.org](https://www.srihash.org/).

To verify if our script is an SRI version you can always check for `SRI-version` in the first line:

<img class="border" src="/images/script-in-safari-sri-version.png" alt="SRI script viewed in the Safari browser" />
