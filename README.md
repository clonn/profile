# caesarchi-profile

Editorial profile page for **Caesar Chi**, deployed as a static site on **Cloudflare Pages**.

**Live:** <https://www.caesarchi.com/> · Cloudflare Pages default: <https://caesarchi-profile.pages.dev/>

## Structure

```
profile/
├── public/             # Static build output (served as-is)
│   ├── index.html
│   └── poster.png
├── wrangler.toml       # Cloudflare Pages config
├── package.json
└── .gitignore
```

No bundler, no framework — just HTML, CSS and a small inline script.

## Local preview

```bash
npm install
npm run pages:preview
# → http://localhost:8788
```

Or simply open `public/index.html` in a browser for quick visual checks.

## Deploy to Cloudflare Pages

### Option A — API-token deploy (recommended, matches `yi-insight_web`)

Non-interactive; works in any shell or CI without `wrangler login`.

1. Copy the template and fill in your credentials:

   ```bash
   cp .env.example .env
   ```

   Create the token at <https://dash.cloudflare.com/profile/api-tokens> with
   permissions: **Cloudflare Pages:Edit**, **Workers Scripts:Edit**,
   **Account Settings:Read**, **Memberships:Read**. Account ID is on your
   Cloudflare dashboard sidebar.

2. Load the env into your shell and deploy:

   ```bash
   set -a; source .env; set +a
   npm install
   npm run pages:deploy
   ```

   First run creates the `caesarchi-profile` project in your Cloudflare
   account automatically.

### Option B — Interactive login (local dev)

```bash
npx wrangler login
npm run pages:deploy
```

### Option C — Git-connected Pages project

1. Push this repo to GitHub / GitLab.
2. In the Cloudflare dashboard: **Workers & Pages → Create → Pages → Connect to Git**.
3. Select this repo, then set:
   - **Build command:** `npm run build`
   - **Build output directory:** `public`
   - **Root directory:** _(leave empty)_
4. Cloudflare reads `wrangler.toml` (`pages_build_output_dir = "public"`) and serves `public/` on every push.

## Editing

Edit `public/index.html` directly. The page supports EN / 中 via the language toggle in the top bar.
