# Houston Renal Group — website (clean rebuild)

Static replacement for houstonrenal.com after the InMotion-hosted WordPress site was
compromised (2026-07-01) and replaced with a cloaked "Nihao" spam storefront. This
rebuild is self-contained (single `index.html`, no build step, no server code) and is
designed to be hosted on **GitHub Pages** — the same place `pay.houstonrenal.com`
already lives (`roundingapp.github.io`). Nothing here depends on the hacked InMotion box.

## Files
- `index.html` — the entire site (one page, embedded CSS, no external dependencies).
- `CNAME` — tells GitHub Pages to serve this at `houstonrenal.com`.

## Content source
Rebuilt from the real site preserved in the Wayback Machine (2022–2024 snapshots):
practice name, tagline, the five service lines, address, phone, email, and hours are
all verbatim from the original. Physician list is the current active roster
(Sutaria, Koshti). Confirm the provider list + credentials before go-live.

Verified facts baked in:
- 2201 W. Holcombe Blvd., Ste. 320, Houston, TX 77030 (Texas Medical Center)
- Phone 346-570-1700 · office@houstonrenal.com · Mon–Fri 9am–5pm
- Pay portal → https://pay.houstonrenal.com

## Deploy (GitHub Pages)
1. Create a repo, e.g. `roundingapp/houstonrenal-site`, and push these files (or upload
   `index.html` + `CNAME` via the GitHub web UI).
2. Repo → **Settings → Pages** → Source: `main` branch, `/ (root)` → Save.
3. Pages will read `CNAME` and set the custom domain to `houstonrenal.com`.
4. In **Microsoft 365 admin center → Settings → Domains → houstonrenal.com → DNS**,
   point the domain at GitHub Pages (this also removes the hacked InMotion target):
   - Delete the current `A @ → 199.250.207.202` record.
   - Add four `A @` records: `185.199.108.153`, `185.199.109.153`,
     `185.199.110.153`, `185.199.111.153`.
   - Set `CNAME www → roundingapp.github.io` (or the chosen repo owner).
5. Back in GitHub Pages settings, tick **Enforce HTTPS** once the cert issues
   (can take up to an hour after DNS propagates).

Result: houstonrenal.com serves this clean page; the spam store is unreachable through
the domain. Separately, the compromised InMotion cPanel account still needs to be
cleaned or cancelled.
