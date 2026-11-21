# Next steps

## 1. Keep accounts and posts (important)
The real app lives at https://hasanai.net/sports/ (inside the portfolio). Render has **no `DATABASE_URL`**, so the site uses a SQLite file inside the container and **everything resets on each deploy or restart** (free instances restart after ~15 min idle).

1. Neon (https://neon.tech) → your project → **Connect** → copy the connection string (`postgresql://…?sslmode=require`).
2. Render → **PersonalPortfolio → Environment → Add Environment Variable**: Key `DATABASE_URL`, Value: the string. Save.
   (There are currently two variables named `username` and `password` there; the app doesn't use them. Delete them unless you added them on purpose.)
3. Render → **Manual Deploy → Deploy latest commit**. On start-up the tables are created in Neon and the resume, walkthroughs and admin user are filled in again.
4. Check https://hasanai.net/sports/ : sign up, post, log out, redeploy, and the post should still be there.

## 2. Deploying the portfolio
Auto-deploy is off for PersonalPortfolio. After merging to `main`, use **Manual Deploy → Deploy latest commit** (or turn auto-deploy on in Settings).

## 3. sports.hasanai.net (optional)
The page is already reachable at https://hasanai.net/sports/. A separate subdomain is only needed if you want that exact address. Render's plan allows 2 custom domains and both are used. Options:
- **Cloudflare redirect rule** (free, quick): `sports.hasanai.net/*` → `https://hasanai.net/sports/`.
- Upgrade Render, or host this repo on Cloudflare Pages (demo-only copy, no accounts).

## 4. This repo vs the live app
`index.html` here is a copy of `static/sports/index.html` from the portfolio. Without the portfolio's API it runs in demo-only mode. Edit the portfolio copy first, then copy it here.
