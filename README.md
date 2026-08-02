[README.md](https://github.com/user-attachments/files/30634252/README.md)
# Portfolio Manager

A private, password-locked portfolio dashboard: buy ledger, sell ledger, and
dividend ledger, with capital-gains holding-period classification and
Excel/PDF/Word/Text export.

## How to publish this on GitHub Pages

1. Create a new **public** repository on GitHub (e.g. `portfolio-manager`).
2. Upload `index.html` from this folder to the root of that repository.
   (It's already named `index.html`, so no renaming needed.)
3. Go to the repo's **Settings → Pages**.
4. Under "Build and deployment" → Source, choose **Deploy from a branch**,
   branch `main`, folder `/ (root)`, then **Save**.
5. Wait 1–2 minutes, refresh the Pages settings screen, and your live link
   will appear at the top:
   `https://<your-username>.github.io/portfolio-manager/`

## Notes

- All data (buys, sells, dividends, your vault password) is saved in the
  browser's own storage for that exact URL. It does **not** sync across
  different browsers or devices — each browser/URL combination has its own
  separate vault.
- The repository is public by default on the free GitHub plan, so avoid
  putting sensitive identifiers (PAN, account numbers) in description
  fields — anyone with the link can view the raw `index.html` source.
- To update the dashboard later, re-upload a new `index.html` to the same
  repo (Add file → Upload files → same filename) and commit — the live
  site updates automatically within a minute or two.
