Use `trackRequest` from [`@simpleanalytics/next`](https://www.npmjs.com/package/@simpleanalytics/next), version 1.2.0 or later, instead of writing an integration. It sends the same payload and addresses. It runs before Next.js answers, so it doesn't know the response: it sends no `status` or `content_type`, and it also reports pages that don't exist.

1. Install or update the package with the project's package manager, like `npm install @simpleanalytics/next@latest`.
2. Set these environment variables for the production deployment. Server-side collection is off until the second one is set, and removing it turns it off again:

   ```sh
   SIMPLE_ANALYTICS_HOSTNAME=example.com
   SIMPLE_ANALYTICS_SERVER_SIDE_COLLECTION=1
   ```

3. Call `trackRequest` in `proxy.ts`, or in `middleware.ts` before Next.js 16, next to the `app` or `pages` folder. When the file exists, add the `event.waitUntil` line at the top of its function and keep the rest. When it has a `matcher`, make sure it matches every page.

   ```ts
   import { type NextFetchEvent, type NextRequest, NextResponse } from "next/server";
   import { trackRequest } from "@simpleanalytics/next/server";

   export function proxy(request: NextRequest, event: NextFetchEvent) {
     event.waitUntil(trackRequest({ request }));

     return NextResponse.next();
   }
   ```

   In `middleware.ts` the function is called `middleware` instead of `proxy`.

4. To report query parameters besides the default ones, add them as `allowParams`, like `trackRequest({ request, allowParams: ["promo"] })`.

Test mode is on when `SIMPLE_ANALYTICS_TEST_MODE` is `1`. It asks Simple Analytics to store nothing, works under `next dev`, and prints what was sent and the reply on the server console. A static export (`output: "export"`) has no server, so `trackRequest` never runs there. See also [the package's documentation](https://simpleanalytics-next-docs.vercel.app/docs/server-side-collection).
