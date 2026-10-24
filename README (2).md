# Partner MRR – OND planning dashboard

A single-page dashboard (`index.html`) for partner revenue planning. It reads four published Google Sheets tabs as CSV every time it is opened, so sheet edits show up without changing the file.

Current version: **2026-10-24 v4**. The version is shown at the start of the grey line at the bottom of the page.

## What it shows

- **MRR summary:** last 3-month average MRR (Jul–Sep), last month (September), October predicted MRR, MRR delta (October minus September) and the ARR implication (MRR delta × 12, with October run-rate ARR).
- **All partners:** zone, business model (Subscription, or Usage including PayG), live products, October MRR and change from September, rooftop penetration, partner offerings, Smartview fit and open cross-sell scope.
- **Rooftop penetration:** onboarded ÷ total rooftops per partner, plus totals. Pending rooftops are an estimate.
- **Blockers, levers and cross-sell:** per-partner blockers and levers, and cross-sell / expansion notes, with filters.
- **Click-through rows:** click any summary card to open the rows behind its number.

Partners with $0 MRR in both September and October are left out everywhere. Partners missing from the OND sheet are left out too. A partner reappears automatically once either month is above $0.

## Cross-sell rules

- **Smartview VDP agent** is in scope for any client on Studio or with a marketing offering. Smartview is a widget on the inventory thumbnail plus a sales inbound agent that books the appointment or enquiry against that vehicle. Fit levels:
  - **High:** the partner runs dealer websites.
  - **Medium:** the partner sells marketing or feeds dealer sites.
  - **Base:** Studio only.
- **Sales outbound** and **acquisition (inbound / outbound)** agents are listed for each client.
- **360 and video upsells** are listed only where Studio is live without them.
- Client-level items are listed once per client. For example, Vincue_Benjamin and Vincue_Merchandising count as one client.

## Data sources

The links live in the `CONFIG` block near the top of the `<script>` in `index.html`.

| Key | Google Sheet → tab | Used for |
|---|---|---|
| `ond_sheet` | Partner Arali RAG Dashboard → OND Planning Draft | MRR by month, blockers/levers, expansion notes |
| `rag_sheet` | Partner Arali RAG Dashboard → RAG Dashboard (tab id in `RAG_GID`) | Partner list, zone, billing type, products live |
| `rooftops` | Partner Data (AMER + EMEA) → A | Rooftops, partner offerings |
| `induction` | Partner Induction Sheet → Master Sheet | Current issue (added as a blocker) and quantified opportunity (added to cross-sell notes) |

The `induction` source is optional. Without it, the page runs as normal, just without the induction-sheet lines.

The partner website research (website, what they do, offerings, Smartview fit) is a snapshot stored inside `index.html` as `PARTNER_RESEARCH`. It does not update from the sheets.

## Publishing a sheet tab

1. In the sheet, go to File → Share → Publish to web.
2. Pick the tab, choose **Comma-separated values (.csv)**, and tick "Automatically republish when changes are made".
3. Click **Publish** and copy the link into `CONFIG`.
4. Open the link in a private/incognito window. If it asks you to sign in, publishing is limited to your organisation and the page can't read it.

## Hosting on GitHub Pages

1. Upload `index.html` (and this README) to the top level of the repo.
2. Go to Settings → Pages → Source: "Deploy from a branch" → branch `main`, folder `/ (root)` → Save.
3. The site is at `https://<user>.github.io/<repo>/`. The URL stays the same after every update.

## Updating

- **Sheet data changes:** nothing to do. Google republishes within about 5 minutes; refresh the page.
- **Dashboard changes (new file):** go to Add file → Upload files, drop in the new `index.html` (exact name, top level) and click Commit changes. Wait for the green tick under the Actions tab, then hard-refresh with Ctrl+Shift+R (Cmd+Shift+R on Mac). Check that the version at the bottom of the page matches.
- **Errors:** if a tab can't load, a red note at the top of the page names it.

## Privacy

On a free GitHub account, the site and the published CSV links can be opened by anyone with the URL. That includes revenue, rooftop and induction-sheet data (POCs, pricing, payment status). The page tells search engines not to index it, but that does not restrict access. For a login-protected version, host the same file on Cloudflare Pages with Cloudflare Access.
