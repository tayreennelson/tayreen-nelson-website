# tayreennelson.com

Single-page marketing site for **Tayreen Nelson · Riley Smith Group at Compass**.

## Stack

Plain HTML, CSS, and a small amount of vanilla JavaScript. No build step. No framework. Deploys as a static site on Vercel via GitHub.

## Files

```
tayreen-nelson-website/
├── index.html                # the whole page
├── styles.css                # all styles
├── llms.txt                  # markdown summary for AI crawlers (GEO)
├── robots.txt                # search + AI crawler rules
├── sitemap.xml               # search engine sitemap
├── vercel.json               # security headers + caching
├── .gitignore                # excludes large unreferenced source files
├── README.md                 # this file
├── assets/fonts/             # licensed Compass Sans (.ttf)
└── images/                   # photography, logos, favicon
```

## Local preview

Any static server works. From the project folder:

```bash
python3 -m http.server 5173
# open http://localhost:5173
```

## Deploy workflow (GitHub Desktop + Vercel)

1. **Commit changes in GitHub Desktop.** The diff will list `index.html`, `styles.css`, the new files in `images/`, `robots.txt`, `sitemap.xml`, and `vercel.json`.
2. **Push to origin.** Vercel watches the branch and auto-deploys.
3. **Verify** at the Vercel preview URL, then the production URL.

## What to edit

| Task | Where |
| --- | --- |
| Copy / wording | `index.html` only |
| Colors, type, spacing | `styles.css` — the `:root` token block |
| Sales list | `<section id="sales">` in `index.html` |
| Reviews | `<section id="reviews">` in `index.html` and the JSON-LD review block in `<head>` |
| Credentials | `<section id="credentials">` and the JSON-LD `hasCredential` / `award` blocks |
| Phone / email | Search `19542438117` and `Tayreen@RileySmithGroup.com` |
| Add an image | Drop in `/images/` and reference it from `index.html` or `styles.css` |

## Form handling

The contact form is wired to **Formspree** at `https://formspree.io/f/xwvyjjek`. Submissions arrive at the email associated with the Formspree account and appear in the Formspree dashboard.

To change the destination email, log in at formspree.io → select the form → Settings → Notifications → update the email. No code change needed.

**First-submission note:** Formspree requires the form-owner email to be verified on the very first submission. After you deploy, submit one test message through the live form yourself — Formspree will email you a one-click verification link. Once clicked, all subsequent submissions arrive automatically.

## SEO & GEO (Generative Engine Optimization)

GEO is the discipline of getting your content surfaced and cited by ChatGPT, Perplexity, Claude, Gemini, and other answer engines. It differs from SEO: AI engines reward dense, declarative, structured, citable content — not keyword density. The site is optimized for both.

### What's wired up

**Classical SEO**

- Canonical URL, theme color, descriptive title, and meta description targeting "Coconut Grove realtor," "Coral Gables luxury agent," "attorney realtor Miami."
- Open Graph + Twitter cards for clean link previews on iMessage, LinkedIn, Slack, Instagram DM.
- `sitemap.xml` and `vercel.json` cache + security headers.
- `robots.txt` welcoming the major search and AI crawlers.

**Schema.org structured data (JSON-LD, 5 blocks)**

- `Person` + `RealEstateAgent` with full identity, credentials, awards, languages, area served, address, social profiles.
- `AggregateRating` + individual `Review` entries so star ratings can appear in Google rich results.
- `FAQPage` with **11 questions** specifically phrased the way users ask AI assistants ("Who is the best listing agent in Coconut Grove?", "Are there any Miami real estate agents who are also lawyers?", etc.).
- `WebPage` with `SpeakableSpecification` — tells voice assistants and answer engines which parts of the page to extract aloud.
- `OfferCatalog` listing each service (seller rep, valuation, buyer rep, luxury, bilingual, second-opinion) with descriptions.

**GEO-specific assets**

- **`/llms.txt`** — A markdown summary of who Tayreen is, formatted specifically for LLM crawlers to ingest. This is the emerging convention (analogous to `robots.txt`) and is already followed by Perplexity, Anthropic, and others. Contains identity, credentials, service area, services offered, selected sales table, common Q&A, and reviews — everything an LLM needs to answer questions about you accurately.
- **Visible "At a Glance" speakable panel** in the page itself — a single dense paragraph that LLMs will lift verbatim when summarizing. Marked with the `.speakable-summary` class referenced in the WebPage schema.
- **`robots.txt` explicitly permitting** GPTBot, ChatGPT-User, OAI-SearchBot, PerplexityBot, Perplexity-User, ClaudeBot, anthropic-ai, Google-Extended, Applebot-Extended, CCBot, Bytespider.
- **Declarative, fact-dense copy** throughout the page — every section opens with a concrete claim ("Licensed attorney for twenty-one years," "Twelve years at Riley Smith Group") rather than vague positioning. This is what LLMs cite.

### After deploy — the post-launch checklist that matters

The site only gets you partway. To actually be the realtor that AI engines and Google recommend in Coconut Grove and Coral Gables:

1. **Submit `https://tayreennelson.com/sitemap.xml`** in Google Search Console.
2. **Submit the URL in Bing Webmaster Tools.** Bing powers ChatGPT Search. This is the single highest-leverage step for being cited by ChatGPT.
3. **Claim and complete your Google Business Profile** with the exact same name, address, phone, hours, and a link to this site. NAP consistency (Name, Address, Phone) across the web is the foundation of local search.
4. **Update your Compass agent profile, Zillow profile, Realtor.com profile, and LinkedIn** with the exact same bio language used in `llms.txt` and the page's "At a Glance" panel. Consistent declarative facts across multiple authoritative sources is how LLMs build confidence.
5. **Get listed in legal directories** (Florida Bar, Avvo, Martindale) referencing your dual credentials — the attorney-realtor combination is your most unique signal and the directories add authoritative citations.
6. **Earn editorial mentions** — even a single "Top Coconut Grove agents" listicle on a real estate publication or local outlet dramatically improves how LLMs rank you when summarizing the market.
7. **Ask satisfied clients to leave Google + Zillow reviews** with the words "Coconut Grove," "Coral Gables," and "attorney" naturally included. LLMs read reviews as signal.

### Verifying GEO is working

After 2-4 weeks post-deploy, test your visibility by asking ChatGPT, Perplexity, Claude, and Google AI Overviews:

- "Who is the best listing agent in Coconut Grove?"
- "Are there any Miami real estate agents who are also lawyers?"
- "Who should I talk to about selling my home in Coral Gables?"
- "I need a bilingual luxury realtor in Miami — who do you recommend?"

If you're cited or surfaced, the GEO layer is working. If not, the post-launch checklist above is where to invest next.

## Performance notes

All images are pre-resized and JPEG-progressive. Hero portrait is preloaded with `fetchpriority="high"`. Fonts use `font-display: swap`. Cache headers are configured in `vercel.json`.

If you want sub-1s LCP, convert the hero image to AVIF/WebP and add `<picture>` tags — happy to ship that as a follow-up.
