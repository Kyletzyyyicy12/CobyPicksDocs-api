# Coby Picks API reference website

This is a small, standalone static website for exploring the Coby Picks REST API. It does not contain or deploy the Coby Picks application or its backend. The OpenAPI document is embedded directly inside `index.html`, so the grouped, filterable endpoint list and expandable request/response details appear immediately—even if you upload or deploy just the HTML file. The page also provides a download link for the OpenAPI JSON. Interactive requests use the API origin entered on the page.

## Deploy this website to Vercel

1. Import this repository into Vercel as a **separate project**.
2. Set the project **Root Directory** to `coby-picks-api-docs`.
3. Select **Other** as the framework preset. No build command or environment variables are required for this static site.
4. Deploy, then open the assigned Vercel URL.
5. Open the docs deployment. The API server defaults to `https://coby-picks-web-csww.vercel.app`; the mobile application is linked separately from the page.

The endpoint list is embedded in the HTML and does not fetch a separate spec file. Each endpoint expands to show its description, request schema, response codes, and a **Try it** form. Use the **Authorize** button to apply a real Firebase ID token to requests that require authentication. Tokens stay in page memory only and are not persisted. Role presets are intentionally not provided because Coby Picks validates real Firebase accounts and admin roles on the server.

## Enable cross-origin interactive requests

If the docs and API are deployed on different origins, set `API_DOCS_ORIGIN` in the **Coby Picks API project's** Vercel environment variables to the exact docs website origin (for example, `https://coby-picks-api-docs.vercel.app`), then redeploy the API project. The API's Next.js middleware uses that origin to allow browser requests to `/api/*`. It does not allow arbitrary website origins. Without that deployed middleware configuration, the endpoint list still appears, but browsers may block cross-origin **Try it out** requests.

The docs page itself does not need an environment variable. Enter the API origin after deployment. Do not paste private keys, passwords, or other secrets into the docs page. Admin API operations expect a Firebase ID token, and some endpoints perform real actions such as sending emails or creating accounts.

## API scope

The OpenAPI document describes the web app's existing REST routes. Wheel, activity, and live-room features primarily use Firebase directly and are not represented as REST endpoints. A few legacy account operations that need stronger authorization are intentionally not part of the public API reference.
