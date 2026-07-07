---
name: asset-caching
description: The desired cache configuration for static assets served from /public/assets. Use when adding, editing, or reviewing next.config.ts headers, when setting Cache-Control for assets, or when another skill configures the asset pipeline.
---

# Asset caching

Files under `/public/assets` (images + vectors) are **content-addressed**: they never change in place — editing an asset means renaming it. That discipline is what makes an aggressive immutable cache safe.

Serve them with a year-long immutable `Cache-Control` via the `headers()` function in `next.config.ts`:

```ts
async headers() {
  return [
    {
      source: '/assets/:path*',
      headers: [
        { key: 'Cache-Control', value: 'public, max-age=31536000, immutable' },
      ],
    },
  ]
}
```

Rules:

- `source` matches `/assets/:path*` only — never widen it to all of `/public`. Files that change in place (e.g. `og-image.jpg` at the root) must not inherit this cache.
- `max-age=31536000, immutable` is the desired value, not a starting point. A shorter TTL means every deploy re-fetches unchanged bytes; a longer one is meaningless. Don't tune it.
- To change a cached asset, rename the file and update its references. Never edit bytes under a name that's already shipped — a client holding the immutable copy will never see the change.
