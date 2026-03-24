# 🔍 SEOIT — Live SEO Audit Agent

> Ask your agent to clone this repo into his skills.

---

## What is SEOIT?

SEOIT is an AI skill that turns your AI agent into a live SEO audit tool. Once installed, you simply type `/SEOIT` and your agent will ask for your domain, actively crawl and check your entire website across all 20 SEO categories, and return a full HTML audit report — including a score, pass/fail results for every check, and a prioritized list of fixes.

No manual work. No forms to fill out. Just one command.

---

## How it works

1. Type `/SEOIT`
2. Your agent asks: *"What's your domain?"*
3. It fetches and checks everything automatically
4. You get a downloadable HTML report with ✅ PASS · ⚠️ WARNING · ❌ FAIL for every check, real findings, fix instructions, and an overall score (0–100)

---

## What gets checked

| # | Category | What's verified |
|---|---|---|
| 1 | **Indexing** | Public accessibility, noindex tags, canonical tags, duplicate content signals |
| 2 | **robots.txt** | File exists, Googlebot not blocked, sitemap listed |
| 3 | **Sitemap** | sitemap.xml exists, valid XML, contains URLs |
| 4 | **Meta Tags** | Title (50–60 chars), meta description (140–160 chars), Open Graph tags, viewport |
| 5 | **URL Structure** | Clean URLs, no parameter-based URLs, lowercase + hyphens |
| 6 | **Performance** | PageSpeed score, image formats (WebP/AVIF), lazy loading, minified CSS/JS |
| 7 | **Mobile SEO** | Viewport tag, responsive CSS, no fixed-pixel layouts |
| 8 | **Content SEO** | H1 present, H2/H3 structure, no keyword stuffing, content depth |
| 9 | **Image SEO** | Alt tags, descriptive file names, no oversized images |
| 10 | **Technical SEO** | HTTPS, HTTP→HTTPS redirect, 404 page, 301 redirects, Core Web Vitals (LCP, CLS, INP) |
| 11 | **Structured Data** | JSON-LD present, Organization/Product/Service schema |
| 12 | **Backlinks** | Google indexing status, web presence, no toxic link signals |
| 13 | **Internal Linking** | Navigation structure, no orphan pages, descriptive anchor texts |
| 14 | **Analytics & Tracking** | Google Analytics present, cookie banner, Search Console tag |
| 15 | **Trust & Legal** | Impressum, Privacy Policy, Contact page, trust signals |
| 16 | **Local SEO** | Google Business Profile, NAP consistency, reviews |
| 17 | **Crawlability** | Not JS-only rendering, no redirect chains, SSR/pre-rendering |
| 18 | **Duplicate Content** | www vs non-www canonical, HTTP/HTTPS duplicates |
| 19 | **Keyword Strategy** | One primary keyword per page, long-tail usage, search intent match |
| 20 | **Quick Wins** | Top 5 highest-impact fixes based on all findings |

---

## Files

```
seoit/
├── SKILL.md       ← The skill instructions (works with any AI agent)
└── seoit.skill    ← Packaged skill file (Claude drag & drop install)
```

---

## Requirements

Your AI agent needs web access / web search enabled to perform live checks.

---

## License

MIT — free to use, modify, and share.
