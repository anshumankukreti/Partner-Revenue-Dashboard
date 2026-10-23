# Partner MRR – OND planning dashboard

A single-page dashboard (`index.html`) that reads three published Google Sheets tabs as CSV every time it is opened. It covers MRR summary, MRR delta and ARR implication, the partner list with zone and business model, rooftop penetration, Smartview / cross-sell scope, and blockers and levers. Click any summary card to open the rows behind it.

## Data sources

The links live in the `CONFIG` block near the top of the `<script>` in `index.html`:

| Key | Sheet → tab |
|---|---|
| `ond_sheet` | Partner Arali RAG Dashboard → OND Planning Draft |
| `rag_sheet` | Partner Arali RAG Dashboard → RAG Dashboard |
| `rooftops` | Partner Data (AMER + EMEA) → A |

To get a link: in the sheet, go to File → Share → Publish to web. Pick the tab (not "Entire document"), choose **Comma-separated values (.csv)**, tick "Automatically republish when changes are made", then Publish. Copy the link into `CONFIG`.

Check each link in a private/incognito window. If it asks you to sign in, your Google Workspace only allows publishing inside the organisation, and the page will not be able to read it.

The partner website research (website, offerings, Smartview fit) is a snapshot from Oct 23, 2026, stored inside `index.html` as `PARTNER_RESEARCH`.

## Hosting on GitHub Pages

1. Create a repo and upload `index.html` (and this README) to the top level.
2. Go to Settings → Pages → Source: "Deploy from a branch" → branch `main`, folder `/ (root)` → Save.
3. The site is live at `https://<user>.github.io/<repo>/` within a minute or two.

Sheet edits show up after Google republishes the CSV, which usually takes about 5 minutes; then refresh the page.

**Privacy:** on a free GitHub account the site, and the published CSV links, can be opened by anyone who has the URL. The page tells search engines not to index it, but that does not restrict access. For a login-protected version, host the same file on Cloudflare Pages with Cloudflare Access.
