# ETisHA BD — Premium E-Commerce Starter

This project is prepared for the current domain `trustsolbd.com`. The brand is **ETisHA BD**. The future domain `etishabd.com` can be attached later without changing the product database.

## Included
- Responsive storefront (`index.html`)
- Shopping bag/cart and COD checkout UI
- Admin login, product CRUD, SKU, price, stock, variant/size, description
- Admin order list and order status updates
- Cloudflare Pages Function API
- D1 schema and R2 image upload endpoint

## Important before going live
This is a deployable starter, not a fully configured live store. Admin/API functions require Cloudflare bindings and secrets. Do not publish admin credentials in GitHub.

## Cloudflare setup
1. Create a D1 database named `etisha_store`.
2. In D1 Console, execute `schema.sql`.
3. Create an R2 bucket named `etisha-product-images`.
4. Configure an image hostname/public base for the R2 bucket (prefer a custom subdomain such as `images.trustsolbd.com`).
5. In Pages > your project > Settings > Functions > D1 database bindings, bind variable `DB` to `etisha_store`.
6. Bind R2 bucket as `PRODUCT_IMAGES`.
7. Add Pages environment variables/secrets:
   - `ADMIN_PASSWORD` — a strong, unique admin password (secret)
   - `AUTH_SECRET` — a long random secret (secret; 32+ random bytes)
   - `PUBLIC_IMAGE_BASE` — public image base URL, e.g. `https://images.trustsolbd.com`
8. Redeploy the Pages project after configuring bindings/secrets.

## Deploy from GitHub
Upload the contents of this ZIP to the root of repository `trustsolbd/etisha-bd-ecommerce`, commit to `main`, then in Cloudflare Pages use:
- Framework preset: None
- Build command: leave blank
- Build output directory: `/` (if Cloudflare rejects `/`, use `.`)
- Root directory: `/`

Pages Functions are in `/functions`; static assets are in the project root.

## First test
- Visit the `*.pages.dev` URL and confirm storefront loads.
- Visit `/admin/` and sign in using `ADMIN_PASSWORD`.
- Add a test product and confirm it appears on storefront.
- Place a test COD order and confirm it appears in Admin > Orders.

## Notes
- Store currency is BDT (৳).
- Current checkout is Cash on Delivery only. Payment gateway is not connected.
- Courier API is not connected.
- Before taking real orders, test stock handling, order notifications, privacy/terms/returns, backup and security.
- The API validates product existence for orders, but stock decrement, shipping calculation, email/SMS notifications, payment integration and advanced fraud controls still need implementation before production use.
- Admin authentication uses an HttpOnly Secure cookie. Use HTTPS and keep both secrets private.
