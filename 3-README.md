# Product Dashboard

Live at https://arkcommerce1.github.io/product-dashboard/

Replaces Asana for Ark Commerce new-product development. Single-page app
(`index.html`) rendering `data.json`. No build step.

## Updating data (Instinct workflow)

Haim texts updates on WhatsApp ("oliver sent samples"). To apply one:

1. Edit ONLY `data.json` (one file, GitHub web editor or API commit).
2. Factory updates live at `products[].factories[]`:
   - `sample_status`, `quote_status` - enum strings, keep Asana's options.
   - `last_communication` - `YYYY-MM-DD`.
   - `notes` - free text, latest note.
   - `active` - false when a factory is going nowhere.
   - `log` - APPEND `{"at": "<ISO-8601 UTC>", "by": "Haim", "text": "..."}`
     for every update; never rewrite history. This is the auto-timestamped
     comment log; the page renders newest first.
   - `reminders` - `[{"date": "YYYY-MM-DD", "text": "..."}]`; the page shows
     them, Instinct does the actual pinging.
   - `files` - `[{"name": "...", "url": "..."}]` or with `summary` for text.
3. Bump `updated_at` at the top.
4. New product: add a `products[]` entry copying an existing shape
   (`skus`/`profitability` empty until the spec sheet exists).
5. Commit to `main`; GitHub Pages redeploys in ~1 min.

Spec/profitability columns mirror Haim's cost sheet: cost_per_pc,
monthly_sales, price, referral_fee, fba_fee, factory_cost, duties_tariffs,
shipping, storage, ppc. Profit columns are computed client-side.
