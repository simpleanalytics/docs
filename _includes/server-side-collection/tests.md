Replay these requests against the app in test mode and compare each reply with the expected one. Test mode stores nothing.

1. Start the app on the development computer with test mode on and the hostname set. For Next.js: `SIMPLE_ANALYTICS_HOSTNAME=example.com SIMPLE_ANALYTICS_SERVER_SIDE_COLLECTION=1 SIMPLE_ANALYTICS_TEST_MODE=1 npm run dev`. For other apps, add `SIMPLE_ANALYTICS_TEST_MODE=1` to the usual start command.
2. Send the requests from the same computer, straight to the app and not through a proxy or CDN, so the connection's address is a local one. Pick a page that answers `200` with HTML:

   ```sh
   APP=http://localhost:3000
   PAGE=/
   CHROME='Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/142.0.0.0 Safari/537.36'
   ```

3. Send one request at a time. After each, read the `Simple Analytics test mode:` block in the app's console or log, and compare `outcome` and `name` in the reply with the expected ones. Also check what was sent: the fields, the copied headers and `X-Forwarded-For`.

The requests:

1. **ChatGPT-User**, an AI agent. Expect `outcome` `ai_agent` and `name` `ChatGPT-User`.

   ```sh
   curl -sS -o /dev/null -A 'Mozilla/5.0 AppleWebKit/537.36 (KHTML, like Gecko); compatible; ChatGPT-User/1.0; +https://openai.com/bot' "$APP$PAGE"
   ```

2. **Claude-User**, an AI agent. Expect `outcome` `ai_agent` and `name` `Claude-User`.

   ```sh
   curl -sS -o /dev/null -A 'Mozilla/5.0 AppleWebKit/537.36 (KHTML, like Gecko; compatible; Claude-User/1.0; +Claude-User@anthropic.com)' "$APP$PAGE"
   ```

3. **ChatGPT agent**, an AI agent with a normal Chrome user agent and a `Signature-Agent` header. Expect `outcome` `ai_agent` and `name` `ChatGPT agent`.

   ```sh
   curl -sS -o /dev/null -A "$CHROME" -H 'Signature-Agent: "https://chatgpt.com"' "$APP$PAGE"
   ```

   The sent body has `signature_agent` with the quotes: `"https://chatgpt.com"`.

4. **Googlebot**, a robot. Expect `outcome` `robot` and `name` `Googlebot`.

   ```sh
   curl -sS -o /dev/null -A 'Mozilla/5.0 (compatible; Googlebot/2.1; +http://www.google.com/bot.html)' "$APP$PAGE"
   ```

5. **GPTBot**, an AI crawler, which is a robot. Expect `outcome` `robot` and `name` `GPTBot`.

   ```sh
   curl -sS -o /dev/null -A 'Mozilla/5.0 AppleWebKit/537.36 (KHTML, like Gecko; compatible; GPTBot/1.3; +https://openai.com/gptbot)' "$APP$PAGE"
   ```

6. **curl** with its own user agent, a robot. Expect `outcome` `robot` and `name` `curl`.

   ```sh
   curl -sS -o /dev/null "$APP$PAGE"
   ```

7. **kube-probe**, a health checker. Expect `outcome` `health_checker` and `name` `kube-probe`.

   ```sh
   curl -sS -o /dev/null -A 'kube-probe/1.33' "$APP$PAGE"
   ```

8. **A person in Chrome.** Expect `outcome` `person` and `name` `null`.

   ```sh
   curl -sS -o /dev/null -A "$CHROME" -H 'Accept: text/html,application/xhtml+xml' -H 'Accept-Language: en-US,en;q=0.9' -H 'Sec-Fetch-Mode: navigate' -H 'Sec-Fetch-Dest: document' -H 'Sec-Fetch-Site: none' -H 'Sec-Fetch-User: ?1' "$APP$PAGE"
   ```

   The sent body has `accept`, `accept_language`, `sec_fetch_mode`, `sec_fetch_dest`, `sec_fetch_site` and `sec_fetch_user`. A person is discarded. Is it a robot named `Unidentified` instead? Then the app saw a datacenter address as the connection, for example because you reached a cloud machine through its public address.

9. **Chrome from a datacenter address,** a robot. Expect `outcome` `robot` and `name` `Unidentified`.

   ```sh
   curl -sS -o /dev/null -A "$CHROME" -H 'X-Forwarded-For: 54.145.10.20' "$APP$PAGE"
   ```

   `54.145.10.20` is in the published addresses of Amazon EC2. The sent `X-Forwarded-For` is `54.145.10.20, ` followed by the local address of the connection, like `54.145.10.20, 127.0.0.1`. With Next.js, and wherever the code gets no connection address, it's `54.145.10.20` alone. When the app adds `CF-Connecting-IP` or `True-Client-IP` itself, or a proxy in front of it changes `X-Forwarded-For`, the reply can differ: its `addresses` show what Simple Analytics received.

10. **Query parameters,** from ChatGPT-User. Expect `outcome` `ai_agent` and `name` `ChatGPT-User`.

    ```sh
    curl -sS -o /dev/null -A 'ChatGPT-User/1.0' "$APP$PAGE?utm_source=chatgpt.com&token=secret123&ref=docs"
    ```

    The sent `query` is exactly `utm_source=chatgpt.com&ref=docs`: `token` is never sent, and the printed block doesn't contain `secret123`.

11. **A POST request.** Expect no report: nothing is printed.

    ```sh
    curl -sS -o /dev/null -X POST -A 'ChatGPT-User/1.0' "$APP$PAGE"
    ```

12. **An image.** Expect no report: nothing is printed.

    ```sh
    curl -sS -o /dev/null -A 'ChatGPT-User/1.0' "$APP/favicon.ico"
    ```

When a reply differs from the expected one, compare what was sent with the rules above and fix the integration. The reply's `reason` and `addresses` explain its decision.
