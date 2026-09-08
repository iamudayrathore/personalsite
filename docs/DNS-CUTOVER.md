# DNS cutover — Namecheap → Cloudflare Pages

Do this **after** the site is deployed on its `*.pages.dev` URL and looks right. Nothing here needs to happen before session 6.

## Before you start
- Screenshot every DNS record currently in Namecheap (Advanced DNS tab). Especially any MX records if the domain has email — those must survive the move.
- Confirm the `*.pages.dev` deploy is the build you want live.

## Steps
1. **Cloudflare → Add a site** → enter the domain → Free plan. Cloudflare scans and imports existing records. Compare against your screenshot; add anything it missed (MX, TXT for SPF/DKIM, verification records).
2. Cloudflare shows two nameservers, e.g. `ada.ns.cloudflare.com` / `kirk.ns.cloudflare.com`.
3. **Namecheap → Domain List → Manage → Nameservers** → switch from "Namecheap BasicDNS" to **Custom DNS** → paste the two Cloudflare nameservers → save.
4. Wait. Usually 15–60 min, up to 24h. Cloudflare emails when the site is active.
5. **Cloudflare → Workers & Pages → personalsite → Custom domains → Set up a custom domain** → apex domain. Cloudflare adds the CNAME (flattened at apex) automatically. Repeat for `www`.
6. **SSL/TLS → Overview → Full (strict)**. **Edge Certificates → Always Use HTTPS: on.**
7. **Rules → Redirect Rules**: `www.<domain>/*` → `https://<domain>/$1`, 301.
8. Verify: `https://<domain>` loads the site, `http://` redirects, `www` redirects, email (if any) still sends and receives.

## Rollback
Switch Namecheap nameservers back to BasicDNS. Records are still there; propagation is the only delay.

## Not doing
- Domain transfer to Cloudflare Registrar — unnecessary; revisit at renewal if the price difference matters.
