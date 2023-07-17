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

## Fields

| Field               | Type     | Description |
|---------------------|----------|-------------|
| Date & time         | date     | The date of the data point |
| Path                | string   | The path of the data point |
| Is unique           | boolean  | Is this page view unique |
| UTM source          | string   | UTM source (specify via `ref=` or `utm_source` in your URL) |
| UTM medium          | string   | UTM medium (specify via `utm_medium` in your URL) |
| UTM campaign        | string   | UTM campaign (specify via `utm_campaign` in your URL) |
| UTM content         | string   | UTM content (specify via `utm_content` in your URL) |
| UTM term            | string   | UTM term (specify via `utm_term` in your URL) |
| Scrolled percentage | number   | How far did a visitor scroll on the page (in steps of 5%) |
| Duration seconds    | number   | How many seconds did a visitor stay on this page (we stop the counter when a page is hidden) |
| Screen width        | number   | Screen width in pixels |
| Screen height       | number   | Screen height in pixels |
| Country code        | string   | 2 letter country code |
| Browser name        | string   | Browser name |
| Browser version     | string   | Browser version (do note this is a string) |
| OS name             | string   | OS name |
| OS version          | string   | OS version (do note this is a string) |
| Device type         | string   | Either desktop, mobile, tablet, or tv |
| Lang region         | string   | The region part of [navigator.language](https://developer.mozilla.org/en-US/docs/Web/API/NavigatorLanguage/language) |
| Lang language       | string   | The language part of [navigator.language](https://developer.mozilla.org/en-US/docs/Web/API/NavigatorLanguage/language) |
| Referrer hostname   | string   | The hostname of the referring page/website |
| Referrer path       | string   | The path of the referring page/website |

<style>
tbody tr td:first-child,
tbody tr td:nth-child(2) {
  white-space: nowrap;
}
</style>
