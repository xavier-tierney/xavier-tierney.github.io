# Academic website

A single hand-written page served by GitHub Pages. There's no build step and no framework: what's in this folder is exactly what visitors get.

| File | What it is |
|---|---|
| `index.html` | All content. Edit this to change text. |
| `style.css` | All appearance. Colours and fonts are variables at the top. |
| `files/Tierney_CV.pdf`, `files/Tierney_JMP.pdf` | Add these yourself. **Keep the filenames fixed.** To update, replace the file and push. The URL then never changes, so links in applications and cover letters keep working. |
| `images/photo.jpg` | Your headshot, 648×648 (cropped square automatically). The page works without it. |
| `favicon.svg` | The "XT" browser-tab icon. |
| `.nojekyll` | Tells GitHub to serve the files as-is rather than running its default Jekyll build. |

## Restoring the Job Market Paper links

The JMP links are hidden until `files/Tierney_JMP.pdf` exists. To restore them, add the PDF, then uncomment the blocks marked `JMP-LINK` in `index.html` and in `~/research/cv/Tierney_CV.tex`, recompile the CV and copy it over `files/Tierney_CV.pdf`. `grep -n JMP-LINK index.html` finds them.

## Before publishing

Every placeholder is wrapped in `<span class="todo">`, which shows as bright yellow. To list them:

```bash
grep -n 'class="todo"' index.html
```

When you've replaced a placeholder's text, delete its `<span class="todo">` wrapper too. Publish only once that command prints nothing.

## Preview locally

```bash
open index.html
```

## First-time deployment

1. On github.com, create a new **public** repository named exactly `xavier-tierney.github.io`. Don't add a README; this folder already has one. Free accounts can only publish Pages from public repos.
2. From this folder:
   ```bash
   git init -b main
   git add .
   git commit -m "Initial site"
   git remote add origin git@github.com:xavier-tierney/xavier-tierney.github.io.git
   git push -u origin main
   ```
3. On GitHub: **Settings → Pages → Build and deployment → Deploy from a branch → `main` / `(root)`**. The site appears at `https://xavier-tierney.github.io` within a minute or two.

## Updating

Edit, then `git add . && git commit -m "Update CV" && git push`. Changes go live in about a minute.

Note: git keeps every past version of the PDFs, and on a public repo anyone can browse that history. That's normally harmless, but it means early drafts stay retrievable.

## Custom domain (optional)

1. Buy the domain from any registrar (Cloudflare, Porkbun and Namecheap all cost about £8–12 a year for `.com`).
2. GitHub **Settings → Pages → Custom domain**: enter the domain. This commits a `CNAME` file to the repo.
3. At the registrar, add DNS records:
   - four `A` records for the bare domain → `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   - one `CNAME` record for `www` → `xavier-tierney.github.io`
4. Once the certificate is issued (up to an hour), tick **Enforce HTTPS**.

The `github.io` address keeps working and redirects to the custom domain.
