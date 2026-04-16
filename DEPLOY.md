# Dune Ventures — Deployment Runbook

**Objective:** Get `duneventures.ai` live so Stripe can verify the business and unblock Vensho processing.

**Total time:** ~20–30 minutes, mostly waiting on DNS.

---

## Step 1 — Buy the domain (5 min)

Go to Vercel's domain purchase flow (fastest path — DNS and SSL are auto-configured):

1. Log in at https://vercel.com
2. Click **Domains** in your team dashboard
3. Search `duneventures.ai`
4. Purchase (2-year registration is ~$185.96 — already logged in your Financial Hub)

Alternative if you'd rather keep domains consolidated at Namecheap: buy there at ~$85–95/yr and point DNS at Vercel manually. Slightly more work, not meaningfully better.

---

## Step 2 — Deploy to Vercel (2 min)

1. Go to https://vercel.com/new
2. Click **Browse** or drag-and-drop the entire `duneventures-landing` folder into the upload zone
3. Vercel auto-detects it as static HTML — no build config needed
4. Click **Deploy**
5. Live in ~30 seconds on a temporary `*.vercel.app` URL

Verify the page loads cleanly and renders the three pillars.

---

## Step 3 — Attach the custom domain (5 min + DNS wait)

In the Vercel project settings:

1. **Settings → Domains**
2. Add `duneventures.ai` and `www.duneventures.ai`
3. If you bought through Vercel, DNS and SSL propagate automatically (usually under 5 minutes)
4. If you bought through Namecheap: Vercel will show the exact DNS records to paste into Namecheap's advanced DNS panel

Confirm: https://duneventures.ai resolves and shows the page.

---

## Step 4 — Set up `hello@duneventures.ai` (10 min)

Stripe checks the contact email on the site. It needs to not bounce.

**Cheapest path (free, sufficient for Stripe):**
1. Point domain to Cloudflare (free plan)
2. Enable **Email Routing** in the Cloudflare dashboard
3. Create a forward: `hello@duneventures.ai` → `dune.brandon@gmail.com`
4. Send a test email to confirm it lands

**Upgrade path (credibility):**
- Google Workspace at $7/month gets you a real inbox with Gmail interface
- Worth it once revenue comes in; not required for Stripe verification

---

## Step 5 — Re-submit to Stripe (5 min)

In the Stripe dashboard (the EZvnts account that got rejected):

1. Navigate to **Settings → Business settings → Business details**
2. Update:
   - **Business name**: Dune Ventures LLC
   - **Business website**: https://duneventures.ai
   - **Business description**: Nevada-based holding company, software incubator, and AI advisory
   - **EIN**: 41-5178067
   - **Jurisdiction**: Nevada
3. Re-submit for verification
4. Typical approval: 24–48 hours

Once approved, Vensho (and any future ventures operating under Dune Ventures LLC) can process live transactions.

---

## If Stripe rejects again

Before resubmitting a second time, check:
- Does the landing page load in under 2 seconds on mobile? (It should — single file, no framework.)
- Does "Dune Ventures LLC" appear in the hero, the footer, and the page metadata? (Yes in the shipped version.)
- Does the contact email domain match the site domain? (`hello@duneventures.ai`, yes.)
- Are three service pillars clearly described? (Holding, Incubation, AI Advisory — yes.)
- Is there any password wall, gated content, or under-construction messaging? (No — clean.)

If all of those check out and Stripe still flags it, escalate through their support chat and reference the rejection reason specifically.

---

## What to log in Notion after deployment

Append to the Command Center decisions log and the Financial Hub:
- Deployment timestamp
- Live URL confirmation
- Any Stripe correspondence / approval timestamp
- Email routing setup method (Cloudflare vs Google Workspace)
