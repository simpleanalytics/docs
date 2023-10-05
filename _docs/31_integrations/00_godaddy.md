---
title: Install Simple Analytics on GoDaddy
hidden: true
category: integrations
permalink: /install-simple-analytics-on-godaddy
last_modified_at: 2023-10-05
---

Follow the steps below to add the Simple Analytics script to your GoDaddy website. This script will help in tracking the analytics of your website. Make sure to set the height to `1px` in the HTML section while following these steps.

1. Login to Your GoDaddy Account
    - Navigate to GoDaddy's website and log into your account.
    - Click on your profile name in the upper right-hand corner and select `My Products`.

2. Access Your Website
    - Under the `My Products` tab, find the website you want to add the analytics script to and click `Manage`.

3. Enter the Website Builder
    - Once in your website dashboard, click on `Edit Site` to enter the Website Builder.

4. Access the HTML section
    - Locate the `Add Section` button typically found on the right side or bottom of the editor.
    - Choose the `HTML` section from the list of available sections.

5. Adjust HTML section height
    - Set the height of the HTML section to `1px`. This ensures that the script section does not affect your webpage’s layout.

6. Insert the script
    - Now, copy the script below and paste it into the HTML section:

      ```html
      <script type="text/javascript">
      // Simple Analytics script for GoDaddy Sites
      // Fill in your hostname and the path for every page on your GoDaddy site
      // If your page is https://example.com/ then the hostname is "example.com" and the path is "/"
      // If your page is https://example.com/blog then the hostname is "example.com" and the path is "/blog"
      var hostname = "yoursite.godaddysites.com";
      var path = "/";
      
      // Do not change anything below this line
      function goDaddyPathOverwriter() { return path; }
      
      var script = document.createElement("script");
      script.src = "https://scripts.simpleanalyticscdn.com/latest.js";
      script.setAttribute("data-hostname", hostname);
      script.setAttribute("data-path-overwriter", "goDaddyPathOverwriter");
      document.head.appendChild(script);
      </script>
      ```

7. Save and publish
    - After inserting the script, click on `Done` to exit the HTML editor.
    - Click on `Publish` in the upper right-hand corner to make the changes live.
  
8. Redo for all pages
    - Do this for every page you want to track. Make sure to update the `path` in the script for every page.

Your GoDaddy website should now have the Simple Analytics script running, which will collect data based on the parameters you've set in the script.
