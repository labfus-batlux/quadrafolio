# Quadrafolio.com — Static Site (Cloudflare Pages)

A minimal, production-friendly static site for **quadrafolio.com** with version control on Git.

## Stack
- Pure static HTML/CSS (no build step required)
- Deploys via **Cloudflare Pages → Connect to Git**
- Preview deployments on every Pull Request
- Custom domain: `quadrafolio.com` (apex) + `www.quadrafolio.com`

## Local development
Open `index.html` directly in your browser, or run a lightweight server:
```bash
python3 -m http.server 5173
# then open http://localhost:5173
```

## Repository structure
```
.
├── assets/
│   ├── style.css
│   └── logo.svg
├── .editorconfig
├── .gitignore
├── CNAME.example
├── index.html
└── README.md
```

> If you prefer a framework (Astro/Next.js/SvelteKit), you can swap this out later and Pages will build it.

## Cloudflare Pages setup (CI/CD from Git)
1. Push this folder to a new GitHub/GitLab/Bitbucket repo (see commands below).
2. In **Cloudflare → Pages → Create project → Connect to Git**, select the repo.
3. **Build settings**: Framework preset = **None** (no build command). Output directory = `/`.
4. After the first deploy, in the Pages project → **Custom domains**:
   - Add `quadrafolio.com` and `www.quadrafolio.com`.
   - In the root domain settings, turn on **Always Use HTTPS**.
5. In **Rules → Redirect Rules**, set `www` → apex (301). Example:
   - If **Hostname** equals `www.quadrafolio.com` → **Static** `https://quadrafolio.com/$1` (301).

### Optional: Protect main & use PR previews
- In your Git host, protect the `main` branch (require PR + review).
- Pages will post a **Preview URL** on each PR for easy review.

## Git commands (first push)
```bash
git init
git add .
git commit -m "feat: initial site for quadrafolio.com"
git branch -M main
# create an empty repo on GitHub, then:
git remote add origin git@github.com:<you>/quadrafolio.com.git
git push -u origin main
```

## DNS records (reference)
These are managed automatically when you attach custom domains in Pages, but FYI:
- `CNAME www` → your `*.pages.dev` hostname (orange cloud on).
- Apex `quadrafolio.com` is handled by Pages without an A record (Cloudflare maps apex to Pages).

## Email links
The header includes a `mailto:hello@quadrafolio.com`. Once your provider (Workspace/Fastmail/Zoho) is set up, that’s live.

## License
MIT — do what you like. 
