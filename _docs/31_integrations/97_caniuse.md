---
title: Use website data in Can I Use
menu: Can I use...
category: integrations
permalink: /use-website-data-in-caniuse
---

If you ware a developer you know the website caniuse.com. Can I use provides up-to-date browser support tables for support of front-end web technologies on desktop and mobile web browsers. It's super useful when you develop features for your visitors.

Can I use shows percentages of support of features you can use in the browser. Let's say you develop a new feature and you want to know how many of your visitors support Flexbox. You would [search for Flexbox](https://caniuse.com/?search=Flexbox) and find out the percentage of visitors around the world who support Flexbox. But, this does not say much about **your** visitors.

That's where the Simple Analytics integrations comes in. Want to try it?

First you need to export your website data:

1. Replace `example.com` with your website name in this URL: `https://simpleanalytics.com/example.com.json?version=1`
2. Go to that URL
3. Save the output as a .json file, `caniuse.json` for example
4. Go to [caniuse.com/ciu/import](https://caniuse.com/ciu/import)
5. You will see this screen:
  ![image](https://user-images.githubusercontent.com/1079135/147510047-7145a023-cdf3-4c85-beaf-a9a2f0865349.png)
1. Click "Simple Analytics"
1. Select the json file:
  ![image](https://user-images.githubusercontent.com/1079135/147510563-a7d55d28-98d6-41ad-a1f1-cdccc02eaadf.png)
1. Click "Import"
2. You will see a list of browser that are imported:
  ![image](https://user-images.githubusercontent.com/1079135/147510708-e246e55f-be7e-4463-8543-8956454167e7.png)
1. When searching for features, you will see your own visitors support:
  ![image](https://user-images.githubusercontent.com/1079135/147510810-ff0f6e32-c4bf-49a6-9343-628bda87ea47.png)
