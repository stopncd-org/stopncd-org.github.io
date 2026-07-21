# Plan: Rebuild stopncd.org on GitHub Pages

## Current Site Audit (https://www.stopncd.org)

### Pages
| Route | Title | Notes |
|---|---|---|
| `/` | Home | Mission statement, partner logos, contact |
| `/top-10-problems` | Top 10 Problems | Intro + list of problem sets |
| `/top-10-problems/india` | Diabetes in India | Subpage |
| `/top-10-problems/rural-georgia` | Diabetes in Rural Georgia, USA | Subpage |
| `/hackathons` | Hackathons | DiaTech 10X competition info, event dates, Devpost links |
| `/about-us` | About Us | Partner org descriptions, contact |

### Navigation
- Home
- Top 10 Problems
- Hackathons
- About Us

### Partner Organizations (logos in footer)
- Emory Global Diabetes Research Center (diabetes.emory.edu)
- IIT Madras (mst.iitm.ac.in)
- IIT Madras Shankar CoE for Diabetes Research (mst.iitm.ac.in/shankar-coe)
- Georgia Tech IPaT (research.gatech.edu/ipat)

### Contact
- innovate@stopncd.org

---

## Tech Stack Decision

Use **Jekyll** — it is natively supported by GitHub Pages (zero-config CI/CD), has Markdown-based content authoring, supports layouts/includes, and requires no build step configuration.

Alternatives considered:
- Hugo: faster, but requires GitHub Actions workflow
- Plain HTML: no templating, hard to maintain
- Next.js/React: overkill for a content-only site

---

## Repository Structure

```
stopncd-org.github.io/
├── _config.yml              # Site title, URL, baseurl, plugins
├── _layouts/
│   └── default.html         # Shared HTML shell (head, nav, footer)
├── _includes/
│   ├── nav.html             # Navigation bar
│   └── footer.html          # Partner logos + contact
├── assets/
│   ├── css/
│   │   └── main.css         # Global styles
│   └── images/
│       ├── partners/        # Partner org logos
│       └── hero/            # Hero/banner images
├── index.md                 # Home page
├── top-10-problems/
│   ├── index.md             # Top 10 Problems listing
│   ├── india.md             # Diabetes in India subpage
│   └── rural-georgia.md     # Diabetes in Rural Georgia subpage
├── hackathons/
│   └── index.md             # Hackathons page
├── about-us/
│   └── index.md             # About Us page
├── agents/
│   └── plan.agents.md       # This file
└── README.md
```

---

## Phase-by-Phase Build Plan

### Phase 1 — Project Scaffold
- [ ] Initialize Jekyll project (`bundle init`, `_config.yml`)
- [ ] Configure GitHub Pages settings in `_config.yml`:
  - `url: https://www.stopncd.org`
  - `baseurl: ""`
  - `title: StopNCD`
  - `theme: minima` (or custom — see Phase 3)
- [ ] Set up `_layouts/default.html` with `<head>`, nav, `{{ content }}`, footer
- [ ] Create `_includes/nav.html` and `_includes/footer.html`
- [ ] Add `Gemfile` with `github-pages` gem
- [ ] Verify local build with `bundle exec jekyll serve`

### Phase 2 — Content Migration
- [ ] **Home (`index.md`)**: Mission statement, hero tagline ("Together, We Can Stop Non-Communicable Diseases"), intro paragraph, partner logos section
- [ ] **Top 10 Problems (`top-10-problems/index.md`)**: Intro paragraph + cards/links to subpages
- [ ] **India subpage (`top-10-problems/india.md`)**: Copy content from `/top-10-problems/india`
- [ ] **Rural Georgia subpage (`top-10-problems/rural-georgia.md`)**: Copy content from `/top-10-problems/rural-georgia`
- [ ] **Hackathons (`hackathons/index.md`)**: DiaTech 10X description, competition dates (Apr 4–13 2025), Devpost link, Demo Day (Dec 6 2025) info
- [ ] **About Us (`about-us/index.md`)**: Partner org descriptions, contact email
- [ ] Download and commit all partner logos to `assets/images/partners/`
- [ ] Download and commit all hero/banner images to `assets/images/hero/`

### Phase 3 — Design & Styling
- [ ] Decide: use Minima theme (quick) or write custom CSS (matches original branding)
- [ ] Recreate the dark header/hero banner style from the original site
- [ ] Style partner logos row in footer (flexbox, linked images)
- [ ] Ensure mobile responsiveness
- [ ] Match original color palette and typography as closely as possible

### Phase 4 — GitHub Pages Deployment
- [ ] Push repository to `stopncd-org.github.io` on GitHub (org: `stopncd-org`)
- [ ] Enable GitHub Pages from `Settings → Pages → Source: Deploy from branch (main)`
- [ ] Verify site builds and is live at `https://stopncd-org.github.io`
- [ ] Add custom domain: set `CNAME` file to `www.stopncd.org`
- [ ] In Squarespace DNS (or registrar): update `CNAME` record for `www` → `stopncd-org.github.io`
- [ ] Update `A` records for apex domain (`stopncd.org`) to GitHub Pages IPs:
  - `185.199.108.153`
  - `185.199.109.153`
  - `185.199.110.153`
  - `185.199.111.153`
- [ ] Enable "Enforce HTTPS" in GitHub Pages settings once DNS propagates

### Phase 5 — QA & Cutover
- [ ] Check all internal links work
- [ ] Check all external links (Devpost, partner sites, mailto)
- [ ] Verify partner logos load and link correctly
- [ ] Test on mobile (iOS + Android)
- [ ] Test on Chrome, Firefox, Safari
- [ ] Confirm HTTPS is active and cert is valid on both `www.stopncd.org` and `stopncd.org`
- [ ] Cancel or put Squarespace site into "Not Published" mode after verifying DNS is live

---

## Open Questions
- Do you have the original hero/banner images, or should they be re-sourced?
- Should the design closely match the current Squarespace site, or is a redesign in scope?
- Is there additional content not visible on the public pages (e.g., gated resources, blog posts)?
- Should the Hackathons page be structured to easily add future events?
- Who will own ongoing content updates — should a CMS-like admin experience (e.g., Decap CMS / Forestry) be added on top of Jekyll?
