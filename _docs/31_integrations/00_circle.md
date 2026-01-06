---
title: Install Simple Analytics on Circle
hidden: true
category: integrations
permalink: /install-simple-analytics-on-circle
last_modified_at: 2025-01-01
---

You can track conversions and successful payments in Simple Analytics when using Circle paywalls. Circle allows you to add custom JavaScript code to your paywall thank you page, which is perfect for tracking conversion events.

> **Warning:** This is an advanced feature, and we recommend working with your developer to ensure the correct setup.

## Add conversion tracking code

To track successful payments in Simple Analytics when [creating](https://help.circle.so/p/payments/paywall-setup/set-up-a-paywall) or [editing](https://help.circle.so/p/payments/paywall-management/updating-a-paywall) your paywall:

1. In the paywall setup, navigate to the **Tracking** tab and add your code in the tracking code field.

1. To track a conversion event, use the following code that dynamically loads Simple Analytics and waits for it to be ready:

```html
<script>
  (function () {
    // Load Simple Analytics script dynamically
    const script = document.createElement("script");
    script.setAttribute(
      "src",
      "https://scripts.simpleanalyticscdn.com/latest.js"
    );
    script.setAttribute("async", "true");

    // Wait for script to load and then send event
    script.onload = function () {
      if (window.sa_event && window.sa_loaded) {
        sa_event("circle_payment_success");
      }
    };

    document.head.appendChild(script);
  })();
</script>
```

1. To add dynamic variables from Circle (like payment amount or member email), click the **"Add variable {…}"** icon and select an option from the list. You can use the following variables:

   - `{member_email}` - The email address of the member who made the payment
   - `{amount_paid}` - The amount paid
   - `{coupon_code}` - The coupon code used (if any)
   - `{paywall_internal_name}` - The internal name of the paywall
   - `{paywall_display_name}` - The display name of the paywall
   - `{paywall_trial_days}` - The number of trial days
   - `{paywall_price_amount}` - The price amount

   Example with metadata:

```html
<script>
  (function () {
    // Load Simple Analytics script dynamically
    const script = document.createElement("script");
    script.setAttribute(
      "src",
      "https://scripts.simpleanalyticscdn.com/latest.js"
    );
    script.setAttribute("async", "true");

    // Wait for script to load and then send event with metadata
    script.onload = function () {
      if (window.sa_event && window.sa_loaded) {
        sa_event("circle_payment_success", {
          amount: "{amount_paid}",
          email: "{member_email}",
          paywall: "{paywall_display_name}",
          coupon: "{coupon_code}",
        });
      }
    };

    document.head.appendChild(script);
  })();
</script>
```

1. Save changes to the paywall.

## Good to know

The `<script>` tags are required and must wrap your code. Be sure your code is valid and has no runtime issues before you save your paywall.

The code dynamically loads the Simple Analytics script and uses the `onload` event to wait for it to be ready before sending the event. This ensures the event is properly tracked once the script has loaded and initialized.

## Example: Complete conversion tracking

Here's a complete example that dynamically loads Simple Analytics and tracks the conversion with all available metadata:

```html
<script>
  (function () {
    // Load Simple Analytics script dynamically
    const script = document.createElement("script");
    script.setAttribute(
      "src",
      "https://scripts.simpleanalyticscdn.com/latest.js"
    );
    script.setAttribute("async", "true");

    // Wait for script to load and then send event with all metadata
    script.onload = function () {
      if (window.sa_event && window.sa_loaded) {
        sa_event("circle_payment_success", {
          amount: "{amount_paid}",
          email: "{member_email}",
          paywall_name: "{paywall_display_name}",
          paywall_internal: "{paywall_internal_name}",
          trial_days: "{paywall_trial_days}",
          price: "{paywall_price_amount}",
          coupon: "{coupon_code}",
        });
      }
    };

    document.head.appendChild(script);
  })();
</script>
```

## Viewing your conversions

After setting up conversion tracking, you can view your payment events in Simple Analytics:

1. Go to your Simple Analytics dashboard
2. Navigate to the [Events Explorer](/events-explorer) to see all conversion events
3. Create a [Goal](/goals) to track conversion rates over time

If you encounter issues, don't hesitate to contact us via [our support channels](https://simpleanalytics.com/contact).
