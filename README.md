# tassytrucks-landing-deploy

The new Tassy Transportation landing page, v2, ready to ship.

## What's wired and what's not

### ✅ Working (real links)
- **Phone**: `(704) 941-8508` — click-to-call from nav, hero, modal, footer
- **Email**: `hello@tassytrucks.com` — Contact link in footer, Email button in modal
- **Driver application**: opens email to `hello@tassytrucks.com` with subject "Driver Application"
- **Facility partnership**: opens email to `hello@tassytrucks.com` with subject "Facility Partnership Inquiry"
- **SaaS sign-in**: nav "Sign in" + footer Customer/Facility/Driver/Staff links all point to `https://tassytrucksops.vercel.app/login`
- **Anchor nav**: Services / How it works / For Facilities / Drivers / About all scroll smoothly
- **About Phil** (footer) → scrolls to the founder section

### 🟡 Coming Soon modal (intercepts click, shows modal with phone + email)
- "Book a Ride" (nav + hero)
- "Book NEMT trip" / "Book VIP trip" / "Book accessible ride" / "Book pet pickup" (4 service cards)
- "Create facility account →"
- "Read Phil's full story →" (founder section)
- "Safety" (footer)
- All footer Services list items

## Deploy options

### Option A: Vercel — preview URL in 2 minutes (recommended first)

```bash
# Install Vercel CLI if you don't have it
npm i -g vercel

# Deploy
cd "/Users/philippetassy/Documents/Claude/Projects/Tassy Transportation Priorities/tassytrucks-landing-deploy"
vercel deploy

# You'll get a URL like: https://tassytrucks-landing-xxxxx.vercel.app
# Review it. If you like what you see, promote to production:
vercel --prod
```

Then in the Vercel dashboard:
1. Go to the project settings → Domains
2. Add `www.tassytrucks.com` and `tassytrucks.com`
3. Update your DNS A/CNAME records per Vercel's instructions

### Option B: Drop into existing tassytrucks.com repo

If your current www.tassytrucks.com is in a git repo (Lovable / GitHub):
1. Find the `index.html` (or `App.tsx` if it's React)
2. Replace the homepage content with this `index.html`
3. Commit + push — your existing deploy pipeline handles it

### Option C: Just upload via FTP / hosting panel

The `index.html` is fully self-contained (Tailwind CDN, Google Fonts, all assets via URL). You can drop it on any static host.

## DNS cutover checklist (if going production)

- [ ] Take a backup of the current www.tassytrucks.com (curl + save HTML, or git tag the current repo)
- [ ] Deploy to Vercel preview URL first — review side-by-side with current site
- [ ] Update DNS:
  - `A` record for `tassytrucks.com` → Vercel IP (Vercel will tell you)
  - `CNAME` for `www.tassytrucks.com` → `cname.vercel-dns.com`
- [ ] Wait 5-30 min for DNS propagation
- [ ] Verify https://www.tassytrucks.com loads the new page
- [ ] Test the phone link from your phone
- [ ] Test sending the partnership email from a fresh inbox to confirm it routes correctly
- [ ] Update Google Business Profile description if anything changed

## Rollback plan

If something goes wrong after DNS cutover:
1. Revert DNS records to previous values (write them down BEFORE you change them)
2. Or, if you replaced an existing repo, `git revert` the homepage commit + redeploy

## What to ship next (post-launch)

Once this is live, the Code Mode prompt sequence to wire it up properly:

1. **Service detail pages** — `/services/nemt`, `/vip`, `/wheelchair`, `/winnie` (one per service tile)
2. **Real `/book` page** — when Quick Book SaaS flow is solid, expose a public version
3. **`/about`** page with full founder story (Cameroon → Master's → Army → SDVOSB → Tassy)
4. **`/for-facilities`** page with the partnership pitch deck
5. **`/drivers`** page with the actual application form (not just an email link)
6. **Real "Live Trip Board"** — replace the rotating card animation with a live feed from your SaaS (last 3 completed trips, anonymized)

## File inventory

- `index.html` — the landing page (single file, ~33KB)
- `vercel.json` — deploy config (clean URLs + security headers)
- `README.md` — this file


_Last deploy trigger: PWA mockups (driver + sales)_
