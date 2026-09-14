# Domain Redirect: jgwalsh.net → jgwalsh.com

This is a tiny static site whose primary job is to return an **HTTP 301** for any request to `jgwalsh.net`, preserving the path (and query string) to `jgwalsh.com`.

## Cloudflare Pages redirects

Cloudflare Pages reads redirects from a file named `_redirects` placed in your **static asset output directory**.

This repo includes the same rule in two locations so it works whether your Pages project is configured to publish the repo root or the `public/` folder:

- `_redirects`
- `public/_redirects`

Rule:

```txt
/*   https://jgwalsh.com/:splat   301
```

Examples:

- `https://jgwalsh.net/about` → `https://jgwalsh.com/about`
- `https://jgwalsh.net/about?x=1` → `https://jgwalsh.com/about?x=1`

## About `index.html`

`index.html` is intentionally **not** a client-side redirect. It is only a minimal fallback page with a link to `jgwalsh.com` in case the redirect rule is not being applied by the hosting configuration.

## Verifying

After deploy, these should show a real 301:

```bash
curl -I https://jgwalsh.net/
curl -I https://jgwalsh.net/about
curl -I "https://jgwalsh.net/about?x=1"
```
