---
title: Export your data
category: features
permalink: /export-data
last_modified_at: 2026-10-17
---

As a privacy-friendly business, we care a lot about who owns the data. We are very clear in our terms of service ([section 10](https://simpleanalytics.com/general-terms-and-conditions#intellectual-property)) that you (our customer) own the analytics data. We don't. To not just have that in words in our terms, we care about making it easy for you to export your data. You can export your data through [our APIs](/api) or use [our user interface](https://simpleanalytics.com/select-website/export) to export the raw data.

{%
  include video.html
  red="true"
  slug="export-raw-data-gui"
  formats="mp4,ogg,webm,wmv"
%}

> The video above is slightly out-dated, for a more recent version, check the [Generate export URL](/api/helpers#generate-export-url) in the API helpers or [the live version](https://simpleanalytics.com/select-website/export).

Go to [the export your data](https://simpleanalytics.com/select-website/export) in your dashboard to download your data. You can export page views, events, or both, and pick the fields you need. If you collect [metadata](/metadata), you can include metadata fields as well.

You can download your export in these formats:

- CSV
- Excel CSV
- TSV
- JSON
- NDJSON
- Avro
- Parquet

The export page also shows an API URL for your selection, so you can download the same export through [our export API](/api/export-data-points). You need a plan that includes the export API. See our [pricing page](https://www.simpleanalytics.com/pricing).

If you want to get aggregated data, you'll have to use [our Stats API](/api/stats) for that.
