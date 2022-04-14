---
title: Mini websites
category: features
permalink: /mini-websites
last_modified_at: 2022-04-14
---

Referral links are so boring. Why not make them beautiful? That's why we created mini websites. Screenshots of the websites but then very mini!

<img class="border" style="width: 100%;" src="/images/mini-websites-simple-analytics.gif" alt="">

You will find them if you click on one of the referrals below the main graph. The screenshots are cached when they are created and will only be regenerated when you click on the little circular arrow. You see this arrow when you hover over the mini website:

<img class="border" style="width: 348px;" src="/images/mini-websites-arrow.jpg" alt="">

It takes a few seconds before the new mini website will be regenerated.

## Hide parts of your website in the screenshots

If you want to hide certain parts from your own screenshots you can hide them. You or your developers can add `data-screenshot="hidden"` to the elements that you don't want to see in your screenshots. The Simple Analytics Screenshots Grabber will add a CSS style to the page where those elements get the style `display: none !important;`. This way those specific elements will be hidden from the screenshots.

> If you want to edit the screenshots, you can help us by [submitting a pull request on GitHub](https://github.com/simpleanalytics/screenshot-grabber).
