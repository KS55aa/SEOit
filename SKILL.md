---
name: seoit
description: SEO audit skill that actively checks a website and generates a comprehensive, interactive SEO report. Trigger this skill immediately and without hesitation whenever the user types /SEOIT or /seoit, or asks for an SEO audit, SEO check, SEO analysis, or wants to review their website's SEO. Also trigger when user asks "check my SEO", "SEO review", "audit my website", or any similar phrasing related to auditing or improving a website's search engine optimization.
---

# SEOIT — Live SEO Audit Agent

## Trigger
Activate whenever the user types `/SEOIT` or asks for an SEO audit, SEO check, or website SEO review.

---

## Step 1 — Ask for the Domain

Ask the user:
> "What's your website's domain? (e.g. `https://yourdomain.com`)"

Wait for their answer.

---

## Step 2 — Run All Checks

Once you have the domain, tell the user you're starting the audit and run ALL checks below using web fetch and web search tools. Do as many in parallel as possible.

For every single check, record one of three results:
- ✅ **PASS** — requirement met
- ⚠️ **WARNING** — partially met or could not be verified automatically
- ❌ **FAIL** — requirement not met

---

## Checks to Perform

### 1. Indexing
- Site is publicly accessible (no password, no `noindex` on homepage)
- Google Search Console can be verified (check for GSC meta tag or DNS TXT in HTML)
- Canonical tags present on homepage
- No `noindex` meta tag on homepage
- No duplicate content signals (check for multiple pages with identical titles)

*How:* Fetch homepage HTML, look for meta robots, canonical link, title tags.

---

### 2. robots.txt
- File exists at `/robots.txt`
- Googlebot is not blocked
- No important paths (e.g. `/`, `/blog`, `/products`) are disallowed
- Sitemap URL is listed inside robots.txt

*How:* Fetch `[domain]/robots.txt` and parse the content.

---

### 3. Sitemap
- `/sitemap.xml` or `/sitemap_index.xml` exists
- File is valid XML (not a 404 or HTML error page)
- Contains URLs (not empty)
- Sitemap URL matches what's listed in robots.txt

*How:* Fetch `[domain]/sitemap.xml` and `[domain]/sitemap_index.xml`, inspect content.

---

### 4. Meta Tags
- Every page has a unique `<title>` tag (ideal: 50–60 characters) — check homepage
- Meta description present (ideal: 140–160 characters)
- Keywords present in title and description
- Open Graph tag `og:title` present
- Open Graph tag `og:description` present
- Open Graph tag `og:image` present
- Viewport meta tag correctly set
- No obviously duplicate title or description (compare a few pages if sitemap is available)

*How:* Fetch homepage HTML and parse `<head>` section.

---

### 5. URL Structure
- URLs are clean and readable (e.g. `/about-us` not `?page_id=42`)
- URLs use lowercase and hyphens
- No obvious parameter-based URLs being indexed

*How:* Check homepage links and sitemap URLs for patterns.

---

### 6. Performance
- Page load time appears optimized (check for signs of heavy resources)
- Images are referenced in modern formats (WebP/AVIF) where visible in HTML
- Lazy loading attribute present on images (`loading="lazy"`)
- No obvious render-blocking scripts in `<head>`
- CSS and JS appear minified (check file references)

*How:* Fetch homepage HTML, inspect `<img>` tags, `<script>` and `<link>` tags.
Also search: `site:[domain] PageSpeed` or fetch `https://pagespeed.web.dev/report?url=[domain]`

---

### 7. Mobile SEO
- Viewport meta tag present and correctly configured
- Page uses responsive CSS (check for media queries or responsive framework)
- No fixed pixel widths that would break on mobile

*How:* Check homepage HTML for viewport tag and CSS references.

---

### 8. Content SEO
- Homepage has exactly one `<h1>` tag
- Page uses `<h2>` and `<h3>` subheadings
- Content appears substantial (not thin/empty)
- No obvious keyword stuffing in visible text

*How:* Fetch homepage HTML and inspect heading structure and body content.

---

### 9. Image SEO
- Images have `alt` attributes set
- Image file names appear descriptive (not `IMG_1234.jpg`)
- Images are not excessively large (check `<img>` src attributes for clues)

*How:* Parse `<img>` tags from homepage HTML.

---

### 10. Technical SEO
- HTTPS is active (site loads on `https://`)
- HTTP redirects to HTTPS
- Custom 404 page exists (not a generic server error)
- 301 redirects functioning (www → non-www or vice versa)
- No obvious broken links on homepage
- Core Web Vitals signals: check PageSpeed report for LCP, CLS, INP values

*How:* Fetch `http://[domain]` to check redirect, fetch `[domain]/404-test-page-xyz` to check 404, check PageSpeed results.

---

### 11. Structured Data
- JSON-LD `<script type="application/ld+json">` block present in HTML
- Organization or LocalBusiness schema present
- Product or Service schema present (if applicable)
- No obvious schema errors visible in markup

*How:* Parse homepage HTML for `application/ld+json` script blocks.

---

### 12. Backlinks
- Site appears indexed in Google (`site:[domain]` returns results)
- No obvious signs of toxic/spammy backlink patterns
- Social media profiles link back to domain (search for brand name)
- Domain has some web presence and mentions

*How:* Web search `site:[domain]`, web search `[brand name]`, web search `[domain] backlinks`.

---

### 13. Internal Linking
- Homepage links to main sections/pages
- Navigation structure is clear
- No obvious orphan pages (pages linked from nowhere)
- Anchor texts appear descriptive (not all "click here")

*How:* Parse `<a>` tags from homepage HTML.

---

### 14. Analytics & Tracking
- Google Analytics or equivalent tracking script present in HTML
- Cookie consent banner or script present
- Google Search Console meta verification tag visible (or DNS verified)

*How:* Fetch homepage HTML, search for GA script (`gtag`, `analytics.js`, `_ga`), cookie scripts.

---

### 15. Trust & Legal
- Impressum / Legal Notice page exists
- Privacy Policy / Datenschutz page exists
- Contact page exists
- Trust signals visible (testimonials, reviews, certifications)

*How:* Fetch `[domain]/impressum`, `[domain]/legal`, `[domain]/privacy-policy`, `[domain]/datenschutz`, `[domain]/contact`, `[domain]/kontakt`.

---

### 16. Local SEO *(if applicable)*
- Google Business Profile found via web search
- NAP (Name, Address, Phone) consistent across web
- Reviews visible on Google or other platforms

*How:* Web search `[brand name] Google Business`, `[brand name] reviews`.

---

### 17. Crawlability
- Homepage renders meaningful HTML content (not JS-only blank page)
- No excessive redirect chains detected
- SSR or pre-rendering signs visible if JavaScript framework detected

*How:* Inspect fetched HTML — if `<body>` is nearly empty, likely a JS-only SPA. Check for Next.js, Nuxt, or similar meta tags.

---

### 18. Duplicate Content
- www and non-www versions redirect to one canonical version
- HTTP redirects to HTTPS (not both accessible)
- Canonical tags consistent across pages

*How:* Fetch `http://[domain]`, `http://www.[domain]`, `https://www.[domain]` and check which redirect to which.

---

### 19. Keyword Strategy
- Homepage targets one clear primary topic/keyword in title + H1
- Long-tail keywords visible in subheadings and content
- Content matches likely search intent for the primary keyword
- No obvious keyword stuffing or over-optimization

*How:* Read homepage title, H1, H2s and visible content.

---

### 20. Quick Wins
Summarize the fastest, highest-impact fixes based on all findings above. List up to 5 items the user should fix first.

---

## Step 3 — Generate the HTML Report

After completing all checks, generate a **self-contained HTML report** and save it to the outputs directory as `SEO_Audit_Report.html`.

The report must include:

- **Header** with domain name, audit date, and overall score (0–100)
  - Score = (PASS × 1 + WARNING × 0.5) / total checks × 100
- **Summary bar** showing count of ✅ PASS / ⚠️ WARNING / ❌ FAIL
- **One card per section** (sections 1–20) containing:
  - Each check as a row with status icon + check name + what was actually found
  - A "How to fix" note for every FAIL or WARNING
- **Priority Fix List** at the bottom — all FAILs sorted by importance with actionable instructions
- **Design:** dark navy background, green for PASS, yellow for WARNING, red for FAIL, Space Mono font for scores, clean readable body font, fully responsive, print-friendly

---

## Step 4 — Present Results

Share the report file with the user, then give a short chat summary:

> "✅ X passed · ⚠️ X warnings · ❌ X failed — Score: XX/100
>
> Top priorities to fix: [list top 3 FAILs]"

---

## Rules

- **Never make up results.** Only report what you actually found.
- If a fetch fails or is blocked, mark as ⚠️ WARNING: *"Could not be verified — check manually."*
- If the site appears to be a JS-only SPA, note that HTML-level checks are limited.
- Always check both `www.` and non-`www.` versions.
