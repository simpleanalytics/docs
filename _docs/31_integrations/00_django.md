---
title: Install Simple Analytics with Django
hidden: true
category: integrations
permalink: /install-simple-analytics-with-django
last_modified_at: 2026-11-13
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
   "simpleanalytics",
]
```

Next use the `templatetag` in your template:

{% raw %}
```html
<!DOCTYPE html>
{% load static simpleanalytics_tags %}
<html>
  <head>
    <meta charset="utf-8" />
    <title>{% block page_title %}{{ site.name }}{% endblock %}</title>
    <meta
      name="viewport"
      content="width=device-width, initial-scale=1.0, user-scalable=no"
    />
    ... {% simpleanalytics_async %} ...
  </head>
  <body>
    ...
  </body>
</html>
```
{% endraw %}

This will translate to roughly this:

```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>example.com</title>
		<meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    ...
    <script async type="text/javascript" src="https://scripts.simpleanalyticscdn.com/latest.js"></script>
    ...
    </head>
    <body>
      ...
    </body>
</html>
```

## Template tags

This app has two template tags:

- `simpleanalytics_async`
- `simpleanalytics_sync`

`simpleanalytics_async` converts to a plain `<script>` tag with the `async`
keyword. Use this one, so the script doesn't slow down your page.

`simpleanalytics_sync` converts to a plain `<script>` tag without the `async`
keyword.
