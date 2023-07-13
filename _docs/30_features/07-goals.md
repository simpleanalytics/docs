---
title: Goals
category: features
permalink: /goals
created_at: 2022-12-22
last_modified_at: 2022-12-22
---

Our goals feature is really helpful for organizing and understanding your data. With it, you can set up filters for your data and view the results in these cool goal cards. The cards make it easy to see how you're doing at a glance.

## Overview

In the video below we give you a quick overview of the goals feature.

{%
  include video.html
  slug="2022-12-21-goals-overview"
  formats="mp4,mov,ogg,webm,wmv"
  poster="video.png"
  subtitles="subtitles.vtt"
  controls="true"
  autoplay="false"
%}

It's a good but simple introduction, but if you want to make the most of your goals, be sure to check out the rest of this article. We've included some helpful tips and information on how to use the feature to its full potential.

## Funnel

In our next video, we'll show you how to set up a new goal with a filter that targets page views from the home page. We'll also demonstrate how to add an additional step to the goal by filtering page views from the pricing page. This will give you a more comprehensive view of how your pircing page is performing.

{%
  include video.html
  slug="2022-12-22-goals-home-to-pricing"
  formats="mp4,mov,ogg,webm,wmv"
  poster="video.png"
  controls="true"
  autoplay="true"
%}

Go to [your dashboard](https://simpleanalytics.com/select-website/events) and start playing with goals.

## Filter Fields

<div markdown="1">

| Field               | Type    | Description                                                                                                                                                |
| ------------------- | ------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| added_unix          | number  | The time of the page view in unix time format                                                                                                              |
| added_iso           | date    | The time of the page view in ISO8601 format                                                                                                                |
| hostname            | string  | The hostname of the website                                                                                                                                |
| hostname_original   | string  | When the hostname is overwritten, we store the original hostname                                                                                           |
| path                | string  | The path of the page view                                                                                                                                  |
| query               | string  | The query parameters of the URL                                                                                                                            |
| is_unique           | boolean | Is this page view unique                                                                                                                                   |
| is_robot            | boolean | Is page view visited by a robot or crawler                                                                                                                 |
| document_referrer   | string  | The [JavaScript `document.referrer`](https://developer.mozilla.org/en-US/docs/Web/API/Document/referrer) of the page                                       |
| utm_source          | string  | UTM source (specify via `ref=` or `utm_source` in your URL)                                                                                                |
| utm_medium          | string  | UTM medium (specify via `utm_medium` in your URL)                                                                                                          |
| utm_campaign        | string  | UTM campaign (specify via `utm_campaign` in your URL)                                                                                                      |
| utm_content         | string  | UTM content (specify via `utm_content` in your URL)                                                                                                        |
| utm_term            | string  | UTM term (specify via `utm_term` in your URL)                                                                                                              |
| scrolled_percentage | number  | How far did a visitor scroll on the page (in steps of 5%)                                                                                                  |
| duration_seconds    | number  | How many seconds did a visitor stay on this page (we stop the counter when a page is hidden)                                                               |
| viewport_width      | number  | Viewport width in pixels                                                                                                                                   |
| viewport_height     | number  | Viewport height in pixels                                                                                                                                  |
| screen_width        | number  | Screen width in pixels                                                                                                                                     |
| screen_height       | number  | Screen height in pixels                                                                                                                                    |
| user_agent          | string  | The [`navigator.userAgent`](https://developer.mozilla.org/en-US/docs/Web/API/NavigatorID/userAgent) of a browser (in case of a fake one we don't store it. |
| device_type         | string  | Either desktop, mobile, tablet, or tv.                                                                                                                     |
| country_code        | string  | 2 letter country code                                                                                                                                      |
| browser_name        | string  | Browser name                                                                                                                                               |
| browser_version     | string  | Browser version (do note this is a string)                                                                                                                 |
| os_name             | string  | OS name                                                                                                                                                    |
| os_version          | string  | OS version (do note this is a string)                                                                                                                      |
| lang_region         | string  | The region part of [navigator.language](https://developer.mozilla.org/en-US/docs/Web/API/NavigatorLanguage/language)                                       |
| lang_language       | string  | The language part of [navigator.language](https://developer.mozilla.org/en-US/docs/Web/API/NavigatorLanguage/language)                                     |
| uuid                | string  | A UUID v4 of the page view (this is not always unique)                                                                                                     |
| metadata.\*\*\*     | N/A     | Metadata are your own specified fields followed by a type (e.g. `project_text`)                                                                            |

Data like `scrolled_percentage` and `duration_seconds` is not always added because it depends on the browser features of the visitor. [Metadata](/metadata) is found in `metadata.***` fields. They will only be exported when specified by key (e.g.: `metadata.dark_mode_bool`).

</div>
</details>

<details>
