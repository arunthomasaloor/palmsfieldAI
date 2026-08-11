# Palmsfield AI — Website

`index.html` is the whole site (HTML, CSS, JS inline). `images/` holds your two photos.

---

## 1. Photos

- `images/team-at-work.jpg` — hero (1200x800, 201 KB)
- `images/about-onsite.jpg` — about section (1200x800, 170 KB)
- `images/og-cover.jpg` — 1200x630 link-preview card, generated from the hero photo
- `images/logo.svg` — brand mark, referenced by the JSON-LD `logo` property

**Your full-resolution originals are in `~/Downloads/palmsfieldai-originals/`**, outside this
folder so they don't get deployed. They were 6720x4480 at 2.0–2.6 MB each and displayed at about
420 px wide, so they were resized to 1200 px and re-encoded. That folder also holds
`about-onsite-ALT.jpg`, a *different* photo that was sitting unused in `images/` (it is not a
duplicate of `about-onsite.jpg`). Drop it back in if you want it.

If you swap in new photos, resize before committing:

```bash
sips -Z 1200 --setProperty formatOptions 70 yourphoto.jpg --out images/team-at-work.jpg
```

**Your own team photos beat stock every time** — the page argues you actually show up in person,
and obvious stock imagery undercuts that.

## 2. Replace placeholders

| Find | Where | Replace with |
|---|---|---|
| `https://calendly.com/YOUR-LINK/intro-call` | 2 places | Your booking link |
| Logo | inline SVG in header + footer | Swap if you commission a real mark |
| `hello@palmsfieldai.com` | 4 places incl. the JSON-LD block | **The domain has no MX records — this address bounces today.** Set up mail routing before launch. |
| LinkedIn link | footer (**removed** — it was a dead `href="#"`) | Restore the commented-out `ft-col` block with your real profile URL |

---

## 3. Read this before publishing — claims you'd be making

I wrote these as realistic placeholders. Some are **promises to customers**, so review each:

**Commitments in the trust strip and FAQ** — "60-day fix guarantee," "no lock-in / cancel any month," "fixed scope, quoted up front," "reply within one business day," "no extra travel charge" inside the service area, "documentation and staff training in every handover." Keep only what you'll actually honor.

**Sector time-savings** — "10–15 admin hours back per week," "15–20 hours cut across a small ops team," and similar lines across all six categories. Plausible industry figures, not your results. Soften them or attach a real client before publishing.

**Testimonials section** — currently bracketed placeholders with a visible warning note. **Replace with real, permitted quotes or delete the whole section.** Invented testimonials are deceptive advertising and an FTC complaint risk. An empty section beats a fabricated one. Delete the `<!-- QUOTES -->` block and the `qt-note` paragraph together.

**"We take no commissions from any vendor"** — in the "What we don't do" section. Only true if you never accept referral fees. Remove if you plan to.

**The calculator** — transparent and conservative: assumes 40% of the repetitive hours entered are automatable, over 48 working weeks, and says on the page that it's an estimate. Keep that caveat. To change the assumption, edit `SHARE` in the script.

**The chat widget** — the answers are pre-written and matched on keywords. **It is not a language model**, and the panel says so ("short pre-written answers"). Don't relabel it as an AI assistant while it's still scripted; on a site selling AI services that's the kind of claim that costs you trust on the first question it fumbles. Edit answers in the `KB` array. To make it real: keep the markup, change `reply()` to POST the question to a Netlify Function that holds your API key, and drop the "pre-written" line from the header. **Never put an API key in `index.html`** — it's a static file and anyone can read it.

**The four capabilities in "What we actually build"** — these describe what you'd build, not results you've delivered, which is the right side of the line while you have no case studies. The bilingual claim is the one to sanity-check: only keep it if you can actually support a Spanish-speaking customer end to end, including the follow-up call.

---

## 4. Domain, email, booking

- **Domain:** Namecheap, Cloudflare, or Porkbun. `.com` reads more trustworthy to local business owners than `.ai`.
- **Email:** Cloudflare Email Routing is free and forwards `hello@yourdomain.com` to your personal inbox. Google Workspace (~$7/mo) if you want real hosted mail.
- **Booking:** Calendly free tier covers one event type.

## 5. Deploy

**Netlify is the right choice here** — the contact form is already wired for Netlify Forms and will work with zero setup.

1. netlify.com → sign up
2. Drag the whole output folder (not just index.html — you need `images/`) onto the manual deploy box
3. Site settings → Domain management → add your domain
4. Form submissions appear under the Forms tab; set up email notifications there

Vercel or GitHub Pages also work, but the form needs a different service (Formspree's free tier is the easiest swap — change the `<form>` action to your Formspree endpoint and drop the `data-netlify` attribute).

---

## What's on the page

**Beyond a standard services site:**
- "What we actually build" — the four named offerings (AI phone answering and missed-call recovery, bilingual front office, ask-your-documents assistant, paperwork extraction)
- "Who we help" industries collapsed to headers, expanded by a gold button (native `<details>`, no JS)
- Scripted chat widget with quick-reply chips and a handoff to the contact form
- Interactive cost calculator — sliders with live hours/dollars output
- Two-question service picker that recommends a starting point
- Service area (San Antonio plus 15 surrounding towns) reduced to a single line inside the About section, still anchored at `#area` for the nav link
- Hero lists the four build capabilities above the industry tags, linked to `#build`
- "What we don't do" — trust through disqualification
- First-30-days timeline so buyers know exactly what happens
- Data-handling section (a top objection for owners handing over systems)
- Contact form *and* Calendly *and* email — different buyers prefer different paths
- Sticky mobile call-to-action bar
- LocalBusiness structured data (JSON-LD) with `areaServed` for local SEO
- Open Graph tags for link previews
- Palm-frond logo mark as inline SVG + matching favicon (no image files needed)
- Light/dark toggle, remembered between visits
- Skip-to-content link, keyboard focus rings, reduced-motion support

## Editing

Colors are CSS variables at the top of the `<style>` block. Change `--navy` and `--amber` to reshade everything at once. Dark-mode values are in the `html[data-theme="dark"]` block right below.

**`--amber` vs `--amber-ink`.** `--amber` (`#B0761C`) is the decorative gold used for markers,
bullets, borders and icon fills. `--amber-ink` (`#90601A`) is a slightly deeper shade used for
amber *text* — the section eyebrows, the two hero panel labels, the FAQ `+`. The decorative shade
only reaches 3.6:1 against the light backgrounds, which fails WCAG AA for small text, so anything
you set in amber **type** should use `--amber-ink`. In dark mode both resolve to the same `#E8B45C`.

## Two things still open before launch

1. **Email bounces.** `palmsfieldai.com` publishes no MX records, so `hello@palmsfieldai.com`
   cannot receive mail. Netlify DNS is already authoritative for the domain, so either add
   Netlify's email forwarding or move the zone's mail to Cloudflare Email Routing. Verify with
   `dig +short MX palmsfieldai.com` — it should return at least one host.
2. **Nothing here is deployed or version-controlled.** The live site is still the original build.
   This folder is not a git repo, so `index.html` exists in exactly one place.

## Reliability notes

- The scroll-reveal styles are scoped to `.js`, which an inline head script adds before first
  paint. With JS disabled or blocked the page renders fully visible instead of blank. Don't
  change `.js .rise` back to a bare `.rise`.
- Each feature in the main script is wrapped in `safe(name, fn)`, so one broken feature logs to
  the console instead of taking down the rest of the page. The reveal runs first, and a 3-second
  timer force-reveals anything still hidden.
- The calculator rounds once on the team total (`hours * 0.4 * people`) rather than per person.
  Rounding per person made small inputs collapse to zero. If you edit it, keep that order.
- The picker uses both answers: "things keep breaking" wins outright, otherwise it recommends the
  **earlier** of the two stages (review &lt; workshop &lt; build), because that's where the gap is.
