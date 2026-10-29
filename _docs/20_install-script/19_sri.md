---
title: SRI version
category: install-script
skip_pjax: true
permalink: /sri
sriVersion: 12
sriHash: sha256-iSFbgQEAJgoeLh+lTWPVLouX2RiBERlq4qAOgM8aK+g= sha384-VVOeJV8okLf6owAyITVK14p3AX78fPOStksa5tYEruAngS4yv5EYM26KP9bvcZ/L sha512-DrEJKCUTeTeOenmoMwQa6d3KSiKXCFdZjjbsJhzh4vYFXPxjoU8dfd8oISmIDqrkkRYeCriuEC5TEah3aONxsg==
last_modified_at: 2026-10-29
---

If you want to use SRI you can do this by using specific scripts. The default scripts are changing to reflect new features or code optimizations. You want to use SRI if you consider it a risk when our scripts change. You can also host our SRI script on your own server or CDN.

When you want to use our SRI version of our script you will need to update your script to `https://scripts.simpleanalyticscdn.com/sri/v{{ page.sriVersion }}.js`. The full embed script becomes:

<!-- prettier-ignore -->
```html
<script async src="https://scripts.simpleanalyticscdn.com/sri/v{{ page.sriVersion }}.js" integrity="{{ page.sriHash }}" crossorigin="anonymous"></script>
<noscript><img src="https://queue.simpleanalyticscdn.com/noscript.gif" alt="" referrerpolicy="no-referrer-when-downgrade" /></noscript>
```

When using a [custom domain](/bypass-ad-blockers), use `https://CUSTOM.DOMAIN/sri/v{{ page.sriVersion }}.js` instead. That script contains your custom domain, so its hash differs from the one above. Enter your custom domain to get the embed script with its hash, calculated in your browser:

<form id="sri-custom-domain" data-version="{{ page.sriVersion }}">
  <input type="text" name="domain" placeholder="custom.domain.com" aria-label="Custom domain" autocomplete="off" autocapitalize="off" spellcheck="false" required />
  <button type="submit">Get the script</button>
</form>
<p id="sri-custom-domain-error" hidden></p>
<div id="sri-custom-domain-result" class="highlight" hidden><pre class="highlight"><code></code></pre></div>
<script>
  (function () {
    var form = document.getElementById("sri-custom-domain");
    if (!form || form.dataset.ready) return;
    form.dataset.ready = "true";
    var error = document.getElementById("sri-custom-domain-error");
    var result = document.getElementById("sri-custom-domain-result");
    var latest = 0;
    form.addEventListener("submit", async function (event) {
      event.preventDefault();
      // Only the latest submission may show its result
      var submission = ++latest;
      error.hidden = true;
      result.hidden = true;
      var domain = form.domain.value.trim().toLowerCase().replace(/^[a-z]+:\/\//, "").split(/[\/?#]/)[0];
      var src = "https://" + domain + "/sri/v" + form.dataset.version + ".js";
      try {
        var response = await fetch(src, { cache: "no-store" });
        var body = await response.arrayBuffer();
        // Only the SRI version is pinned; latest.js changes with every release
        var firstLine = new TextDecoder().decode(body.slice(0, 300)).split("\n")[0];
        if (!response.ok || firstLine.indexOf("SRI-version") === -1) throw new Error("Not an SRI script");
        var digest = new Uint8Array(await crypto.subtle.digest("SHA-384", body));
        if (submission !== latest) return;
        var hash = "sha384-" + btoa(String.fromCharCode.apply(null, digest));
        result.querySelector("code").textContent = '<script async src="' + src + '" integrity="' + hash + '" crossorigin="anonymous"></' + "script>";
        result.hidden = false;
      } catch (e) {
        if (submission !== latest) return;
        error.textContent = "We couldn't find the SRI script at " + src + ". Check that " + domain + " is set up as your custom domain.";
        error.hidden = false;
      }
    });
  })();
</script>

To verify if our script is an SRI version you can always check for `SRI-version` in the first line:

<img class="border" src="https://user-images.githubusercontent.com/1079135/147767570-1f7d86bb-b824-4e22-87e3-fbe2757e01c1.png" alt="SRI script viewed in a browser" />
