# POC Example Multi-Zone Next.js Application

This is a remake of the multi-zones example that demonstrates how to serve multiple Next.js applications from a single domain, called [Multi Zones](https://nextjs.org/docs/advanced-features/multi-zones).

Multi Zones are an approach to micro-frontends that separate a single large application on a domain into smaller applications that each serve a set of paths.
This is useful when there are collections of pages unrelated to the other pages in the application. By moving those pages to a separate zone, you can reduce the size of the application which improves build times and removes code that is only necessary for one of the zones.

Multi-Zone applications work by having one of the applications route requests for some paths to the other pages using the [`rewrites` feature](https://nextjs.org/docs/pages/api-reference/config/next-config-js/rewrites) of `next.config.js`. All URL paths should be unique across all the zones for the domain. For example:

- There are two zones in this application: `main-app` and `sub-app-one`.
- The `main-app` app is the main app and therefore it includes the rewrites that map to the `sub-app-one` app in [next.config.js](home/next.config.js)
- `main-app` will serve all paths that are not specifically routed to `sub-app-one`.
- `sub-app-one` will serve the `/sub-app-one` and `/sub-app-one/*` paths.
- The `sub-app-one` app sets [`basePath`](https://nextjs.org/docs/app/api-reference/config/next-config-js/basePath) to `/sub-app-one` so that generated pages, Next.js assets and public assets are unique to the `sub-app-one` zone and won't conflict with anything from the other zones.

NOTE: A `basePath` will prefix all pages in the application with the `basePath` automatically, including relative links. If you have many pages that don't share the same path prefix (for example, `/main-app` and `/sub-app-one` live in the same zone), you can use [`assetPrefix`](https://nextjs.org/docs/app/api-reference/config/next-config-js/assetPrefix) to add a unique prefix for Next.js assets without affecting the other pages.
