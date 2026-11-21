# Next steps: connecting sports.hasanai.net

The site already works at https://sports-prototype.onrender.com.
Render will not take a third custom domain on your current workspace plan (2 of 2 are used by hasanai.net and healthcompass.hasanai.net).

Choose one option:

## Option A: Cloudflare Pages (free, recommended)
Your DNS is already on Cloudflare, so this is the simplest route.
1. Cloudflare dashboard → Workers & Pages → Create → Pages → Connect to Git → choose `sports-prototype`. GitHub may ask for your 2FA code.
2. Framework: None. Build command: empty. Output directory: `/` (or `.`).
3. After the first deploy: Custom domains → add `sports.hasanai.net`. Cloudflare creates the DNS record itself.
4. Optionally, delete the Render site `sports-prototype` afterwards so it doesn't run twice.

## Option B: Upgrade the Render workspace
1. Render → Billing → upgrade to a plan with more custom domains (this costs money).
2. sports-prototype → Settings → Custom Domains → add `sports.hasanai.net` and note the target (`sports-prototype.onrender.com`).
3. Cloudflare → hasanai.net → DNS → Add record: CNAME, name `sports`, target `sports-prototype.onrender.com`, **Proxy off (DNS only)**.
4. Back in Render, click Verify.

## Option C: Redirect only (free, quick)
In Cloudflare, add a redirect rule from `sports.hasanai.net` to `https://sports-prototype.onrender.com`. The address bar will then show the onrender.com address.
