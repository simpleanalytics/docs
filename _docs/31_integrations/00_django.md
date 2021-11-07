---
title: Install Simple Analytics with Django
hidden: true
category: integrations
permalink: /install-simple-analytics-with-django
---

Install the plugin:

```bash
pip install simpleanalytics
```

## Using it

Add the package to the `INSTALLED_APPS`:

```python
INSTALLED_APPS = [
   ...,
   simpleanalytics,
]
```

Next use the `templatetag` in your template:

```html
<!DOCTYPE html>
\{\% load static simpleanalytics_tags %}
<html>
  <head>
    <meta charset="utf-8" />
    <title>\{\% block page_title %}\{{ site.name }}\{\% endblock %}</title>
    <meta
      name="viewport"
      content="width=device-width, initial-scale=1.0, user-scalable=no"
    />
    ... \{\% simpleanalytics_sync %} ...
  </head>
  <body>
    \{\% simpleanalytics_noscript_block %}
  </body>
</html>
```

This will translate to roughly this:

```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>example.com</title>
		<meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    ...
    <script type="text/javascript" src="https://cdn.simpleanalytics.io/hello.js"></script>
    ...
    </head>
    <body>
      <noscript><img src="https://api.simpleanalytics.io/hello.gif" alt="hello"></noscript>
    </body>
</html>
```

## Template tags

This app has four template tags:

- `simpleanalytics_sync`
- `simpleanalytics_async`
- `simpleanalytics_noscript_block`
- `simpleanalytics_noscript_img`

`simpleanalytics_sync` converts to a plain `<script>` tag without the `async`
keyword.

`simpleanalytics_async` converts to a plain `<script>` tag with the `async`
keyword.

`simpleanalytics_noscript_block` converts to an `<noscript>` block, which
includes an `img` element that is used to load the image. Use this when you
don't have and don't need a `<noscript>` block on your page at all.

`simpleanalytics_noscript_img` converts to an `<img>` tag which src points to
the hello.img. Use this when you're using a `<noscript>` block, and you want to
add privacy-friendly stats to your page.
