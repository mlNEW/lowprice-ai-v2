# LowPrice AI v2

## Features
- Product search with side-by-side BDT offers.
- Lowest feed-reported price appears first.
- Displays product link and checked time.
- PWA manifest and service worker.
- Node backend endpoint `/api/search?q=...`.

## Critical: no live feeds are pre-connected
The app shows no prices until authorized store APIs/product feeds are configured. This avoids inventing prices. GitHub Pages cannot run the Node backend; deploy this project as a Node web service (for example, connect the GitHub repository to Render and use the included render.yaml).

## Feed configuration
Set server environment variable `PRODUCT_FEEDS` as comma-separated entries:
`Store One|https://provider.example/search?q={query},Store Two|https://provider2.example/api?q={query}`

Each endpoint must return JSON array or `{ "items": [...] }`, `{ "results": [...] }`, or `{ "offers": [...] }`.
Each item needs `title` or `name`, `price` (number in BDT), and `productUrl` or `url` (absolute http/https URL). Optional: `store`, `imageUrl`, `inStock`.
This basic adapter supports public feeds without secret headers. Providers needing API keys require a provider-specific backend adapter; store keys only as hosting secrets, never in public frontend files.

Connect only official/authorized APIs, affiliate feeds, or feeds for which you have permission. Respect provider terms; do not bypass login, CAPTCHA, rate limits, robots rules or technical protections. Store names shown in the UI are coverage targets, not claims that their feeds are connected.

Prices are feed-reported at check time and may change. Confirm model/variant, stock, warranty and delivery charges before purchase.
