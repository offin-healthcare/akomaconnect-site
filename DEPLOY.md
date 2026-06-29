# Deploy — akomaconnect.offinhealthcaregh.com (GitHub Pages + Namecheap)

This repo is ready to publish. Site files are at the root (`index.html`, `styles.css`,
`assets/`, `CNAME`, `.nojekyll`). Follow the three steps.

## 1. Create the GitHub repo and push

Pick the owner:
- **Company org (recommended):** create a free GitHub org `offinhealthcaregh`, then a repo
  `offinhealthcaregh/akomaconnect-site`. Pages host becomes **`offinhealthcaregh.github.io`**.
- **Personal account:** repo `adala/akomaconnect-site`. Pages host **`adala.github.io`**.

Create an **empty** repo on github.com (no README/license), then from this folder:

```bash
cd /Users/imac/Projects/akomaconnect-site
git remote add origin https://github.com/<OWNER>/akomaconnect-site.git
git push -u origin main
```

(With the GitHub CLI installed you can do it in one line:
`gh repo create <OWNER>/akomaconnect-site --public --source . --remote origin --push`.)

## 2. Turn on GitHub Pages

Repo → **Settings → Pages**:
- **Source:** Deploy from a branch
- **Branch:** `main`, folder **`/ (root)`** → **Save**

Pages reads the committed `CNAME` file and sets the custom domain to
`akomaconnect.offinhealthcaregh.com` automatically. It will show "DNS check in progress"
until step 3 propagates.

## 3. Namecheap DNS — add ONE record

Namecheap dashboard → **Domain List** → **Manage** next to `offinhealthcaregh.com` →
**Advanced DNS** tab → **Host Records** → **Add New Record**:

| Field | Value |
|-------|-------|
| **Type** | `CNAME Record` |
| **Host** | `akomaconnect` |
| **Value / Target** | `<OWNER>.github.io.`  ← e.g. `offinhealthcaregh.github.io.` or `adala.github.io.` |
| **TTL** | `Automatic` |

Notes:
- **Host** is just the subdomain label `akomaconnect` (Namecheap appends the domain).
- The **Value** is the GitHub *account* host (owner of the repo) + `.github.io` — **not**
  the repo name. The trailing dot is fine.
- Make sure no other record uses the same `akomaconnect` host (delete duplicates).
- Namecheap's default **"CNAME Record" for `www`/URL-redirect/parking** can conflict with
  custom hosts — leave the `@`/`www` records alone; you're only adding `akomaconnect`.

Propagation is usually minutes (up to a few hours). Check:
```bash
dig +short akomaconnect.offinhealthcaregh.com   # should resolve to <OWNER>.github.io
```

## 4. Enforce HTTPS

Back in **Settings → Pages**, once the domain shows a green check, tick
**Enforce HTTPS** (GitHub provisions a free Let's Encrypt certificate).

Your site is then live at **https://akomaconnect.offinhealthcaregh.com**.

## Updating later

```bash
# edit index.html / styles.css, then:
git add -A && git commit -m "update copy" && git push
```
Pages redeploys automatically. The **Request a demo** button currently emails
`info@offinhealthcaregh.com` — swap the `mailto:` in `index.html` for a form when ready.
