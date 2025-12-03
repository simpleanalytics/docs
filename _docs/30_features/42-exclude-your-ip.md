---
title: Exclude your IPs
category: features
permalink: /exclude-ips
last_modified_at: 2025-01-09
---

This feature allows you to exclude specific IP addresses from being tracked or block your own visits locally on your computer by modifying its hosts file. Excluded IPs or blocked domains ensure visits from internal users or other known sources don’t impact your analytics data. This is helpful for maintaining cleaner, more accurate insights.

## Block IPs in the dashboard

The exclusion applies only to visits from the moment you save the IP addresses. Previous visits from these IPs will remain in your analytics data. To ensure privacy, we never store the IP addresses of visitors. The only IPs stored are the ones you manually input into this feature. Currently, only IPv4 addresses are supported.

Steps to exclude IP addresses:

1.	Go to the [“Excluded IP Addresses” section](https://dashboard.simpleanalytics.com/account#blocked-ips) in your account settings.
2.	Enter the IPv4 addresses you want to exclude, separated by commas. Example: `80.100.12.45, 145.38.50.41`
3.	Use the “Use your current IP address” option to quickly add your current IP to the list.
4.	Click the Save excluded IPs button to apply the changes.

This exclusion is applied globally across all websites linked to your account.

## Block a domain locally on a computer

> This part of the tutorial is for advanced computer users only.

You can prevent Simple Analytics from collecting your visits by modifying your computer’s hosts file. This method works for both Mac and Windows. If you want to block a custom domain, replace `scripts.simpleanalyticscdn.com` with your own custom domain.

### Block visits on Mac

1. Launch the Terminal app. You can find it by searching for “Terminal” in Spotlight.
2. Run the following command to open the hosts file in a text editor:

       sudo nano /etc/hosts

    Enter your password when prompted.

3. Scroll to the bottom of the file and add the following line:

       0.0.0.0 scripts.simpleanalyticscdn.com

4. Press Control + O to save the changes.
5. Press Enter to confirm the filename.
6. Press Control + X to exit the editor.
7. Run the following command to apply the changes:

       sudo dscacheutil -flushcache; sudo killall -HUP mDNSResponder

Your computer will now block requests to Simple Analytics from your browser.

### Block visits on Windows
1. Search for “Notepad” in the Start menu.
2. Right-click and select Run as administrator.
3. In Notepad, open the file located at:

       C:\Windows\System32\drivers\etc\hosts

    If you don’t see the file, change the file type dropdown to All Files.

4. Add the following line at the end of the file:

       0.0.0.0 scripts.simpleanalyticscdn.com

5. Save the file by clicking File > Save or pressing Control + S.
6. Open Command Prompt as administrator and run:

       ipconfig /flushdns

Your computer will now block requests to Simple Analytics from your browser.

By following these steps, you can ensure your own visits are excluded from analytics tracking.
