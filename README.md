# Palmsfield AI — Website

`index.html` is the whole site (HTML, CSS, JS inline). `images/` holds your two photos.

---

## 1. Add your photos

The page reserves two image slots and shows a styled placeholder until you fill them:

- `images/team-at-work.jpg` — hero, people working at computers
- `images/about-onsite.jpg` — about section

See `images/README.txt` for free licensed sources and sizing. **Your own team photos beat stock every time** — the page argues you actually show up in person, and obvious stock imagery undercuts that.

## 2. Replace placeholders

| Find | Where | Replace with |
|---|---|---|
| `https://calendly.com/YOUR-LINK/intro-call` | 2 places | Your booking link |
| Logo | inline SVG in header + footer | Swap if you commission a real mark |
| `hello@palmsfieldai.com` | 4 places incl. the JSON-LD block | Confirm once email is live |
| `<a href="#" ...>LinkedIn</a>` | footer | Your LinkedIn URL |

---

## 3. Read this before publishing — claims you'd be making

I wrote these as realistic placeholders. Some are **promises to customers**, so review each:

**Commitments in the trust strip and FAQ** — "60-day fix guarantee," "no lock-in / cancel any month," "fixed scope, quoted up front," "reply within one business day," "no extra travel charge" inside the service area, "documentation and staff training in every handover." Keep only what you'll actually honor.

**Sector time-savings** — "10–15 admin hours back per week," "15–20 hours cut across a small ops team," and similar lines across all six categories. Plausible industry figures, not your results. Soften them or attach a real client before publishing.

**Testimonials section** — currently bracketed placeholders with a visible warning note. **Replace with real, permitted quotes or delete the whole section.** Invented testimonials are deceptive advertising and an FTC complaint risk. An empty section beats a fabricated one. Delete the `<!-- QUOTES -->` block and the `qt-note` paragraph together.

**"We take no commissions from any vendor"** — in the "What we don't do" section. Only true if you never accept referral fees. Remove if you plan to.

**The calculator** — transparent and conservative: assumes 40% of the repetitive hours entered are automatable, over 48 working weeks, and says on the page that it's an estimate. Keep that caveat. To change the assumption, edit `SHARE` in the script.

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
- Interactive cost calculator — sliders with live hours/dollars output
- Two-question service picker that recommends a starting point
- Plain service-area list covering San Antonio and 15 surrounding towns
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
