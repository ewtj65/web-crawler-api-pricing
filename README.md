# The Complete Guide to Choosing a Web Crawler API: How to Pick the Right Scraping Service, Avoid Credit Traps, and Scale Without Bill Shock — Plus a Full Plan Breakdown (With Real Cost Math and Use Case Match)

If you've ever tried to scrape a website at scale, you already know the story. You write a clean little script, point it at a product page or a search result, and within twenty requests your IP gets blocked. You rotate proxies. The site deploys Cloudflare. You switch to a headless browser. The site adds a CAPTCHA. You solve the CAPTCHA. The site changes its layout and your parser breaks. By the third week you're not scraping anymore — you're maintaining infrastructure, and the actual data collection has become a side project.

This is the gap a **web crawler API** is supposed to fill. The pitch is simple: you send a URL, the API handles proxies, browser rendering, CAPTCHAs, and retries, and you get back HTML or structured JSON. No proxy pool to babysit, no headless Chrome to keep patched, no 2 a.m. alerts because Amazon changed a CSS class.

The question is whether that pitch holds up, and which service actually delivers on it without quietly draining your budget. This guide walks through what a web crawler API really is, how the credit-based pricing models work (and where they bite), how to match a plan to your actual use case, and what to look at before you commit. We'll use **ScraperAPI** — one of the more established names in the space, founded in 2018 and now processing tens of billions of API requests per month — as the running example, because its plan structure and credit system surface most of the decisions you'll face with any provider.

## What a Web Crawler API Actually Is (and Isn't)

There's a terminology tangle worth clearing up before going further. "Web crawling" and "web scraping" are often used interchangeably, but they describe different jobs. Crawling is about discovery — following links across a site to find pages. Scraping is about extraction — pulling specific fields (price, title, rating, availability) out of those pages. A "web crawler API" in common usage usually means a service that does both: it can traverse a site and return structured data from each page it visits.

A web crawler API is not the same as a website's official API. An official API is a stable, versioned interface the site itself publishes; you ask for data and it hands it over in a documented format. A scraping API, by contrast, fetches pages the way a browser would and then extracts data from the HTML — which means it works on sites that offer no official API at all, but it's also more fragile when layouts change.

The practical appeal of a managed scraping API is that it absorbs the parts of scraping that are genuinely hard to do well at scale:

- **Proxy rotation** across millions of residential and datacenter IPs so no single address gets flagged
- **JavaScript rendering** for single-page applications that load content dynamically
- **CAPTCHA and anti-bot bypass** for sites behind Cloudflare, DataDome, or PerimeterX
- **Automatic retries** so a failed request doesn't kill your whole batch
- **Geotargeting** so you can fetch pages as if you were in a specific country

Doing all of that yourself means running and patching infrastructure that has nothing to do with your actual data goal. A web crawler API bundles it into a single endpoint.

## The Credit System: The Part That Trips Everyone Up

Here's where most people lose money without realizing it. Most web crawler APIs — ScraperAPI included — bill in **credits**, not requests. A credit and a request are not the same thing, and the gap between them depends on two factors: the domain you're scraping and the features you enable.

ScraperAPI's credit multipliers look like this:

| Request Type | Credits per Request |
| --- | --- |
| Standard HTML request | 1 |
| JavaScript rendering (`render=true`) | 10 |
| Premium residential proxies | 10 |
| Ultra-premium proxies | 25 |
| Structured data endpoints (Amazon, Google, etc.) | 5 |
| E-commerce domains (Amazon, eBay, Walmart) | 5 base |
| SERP domains (Google, Bing) | 25 base |
| Social media (LinkedIn) | 30 base |

The multipliers stack, and not always linearly. Premium proxy plus JavaScript rendering costs 25 credits — not the 20 you'd get from adding the two individually. Ultra-premium plus rendering costs 75 credits. Anti-bot bypass credits (for Cloudflare, DataDome, PerimeterX) are added automatically when detected; you don't opt into them.

This is the single most important thing to understand before picking a plan. A Hobby plan advertised as "100,000 credits" delivers 100,000 plain HTML requests — or 10,000 JavaScript-rendered pages — or roughly 1,333 ultra-premium rendered requests. The headline number is only true for the cheapest possible request type.

Before you commit to any plan, model your actual workload: list your target domains, note whether they need rendering, and multiply. That math is the difference between a plan that lasts the month and one that runs dry in week one.

## What You're Actually Paying For: The Plan Tiers

ScraperAPI's plan ladder runs from a permanent free tier up to custom enterprise pricing. Here's every plan currently on the official pricing page, with the configurations that actually matter for deciding between them:

| Plan | Monthly Price | Annual (per month) | API Credits | Concurrent Threads | Geotargeting | Analytics History | Pay-As-You-Go | Get Started |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| **Free** | $0 | — | 1,000/mo | 5 | No | Limited | No | [Start Free](https://www.scraperapi.com/?fp_ref=coupons) |
| **Hobby** | $49/mo | $44.10/mo | 100,000 | 20 | US & EU only | 30 days | No | [Choose Hobby](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| **Startup** | $149/mo | $134.10/mo | 1,000,000 | 50 | US & EU only | 30 days | No | [Choose Startup](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| **Business** | $299/mo | $269.10/mo | 3,000,000 | 100 | Global (50+ countries) | Unlimited | No | [Choose Business](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| **Scaling** | $475/mo | $427.50/mo | 5,000,000 | 200 | Global | Unlimited | Yes | [Choose Scaling](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| **Professional** | $975/mo | $877.50/mo | 10,500,000 | 300 | Global | Unlimited | Yes | [Choose Professional](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| **Advanced** | $1,975/mo | $1,777.50/mo | 21,500,000 | 500 | Global | Unlimited | Yes | [Choose Advanced](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| **Enterprise** | Custom | Custom | 22M+ | 500+ | Global | Unlimited | Yes | [Contact Sales](https://www.scraperapi.com/contact-sales/?fp_ref=coupons) |

All plans include JavaScript rendering, rotating proxy pools, custom headers, CAPTCHA and anti-bot detection, custom sessions, desktop and mobile user agents, automatic retries, unlimited bandwidth, and a 99.9% uptime SLA. The free tier also includes a 7-day trial that bumps you to 5,000 credits with no credit card required — enough to actually test success rates on your real target sites before paying anything.

A few things in that table deserve attention:

**Geotargeting unlocks at Business.** Hobby and Startup are limited to US and EU IPs. If you need to fetch pages as if from Japan, Brazil, or India, Business ($299/mo) is the floor.

**Pay-As-You-Go unlocks at Scaling.** This is the feature that makes Scaling the most popular tier. On Hobby, Startup, and Business, when you exhaust your monthly credits you're simply cut off until renewal — your only option is upgrading. On Scaling and above, you keep scraping past the included credits at a fixed per-credit overage rate, with a configurable spending cap so you don't get a surprise bill. For any workload where volume is hard to predict, that safety net is worth more than the price gap from Business.

**Annual billing saves exactly 10%.** On Hobby that's about $60/year; on Professional it's $1,170/year. If you're confident you'll use the service for 12 months, annual is straightforward math. If you're still calibrating volume, stay monthly until you know.

## Matching a Plan to Your Real Use Case

Plan tables are only useful if you can map them to what you're actually trying to do. Here's how the tiers line up against common web crawler API workloads.

### Hobby ($49/mo) — Solo projects and side experiments

100,000 credits is genuinely a lot for plain HTML scraping — 100K pages a month covers most personal projects, hobby data collection, or a single small site monitored daily. The catch is the 20-thread concurrency limit, which makes bulk jobs slow, and the US/EU-only geotargeting. If your targets are simple static sites and you're scraping for yourself, this is where to start after the free trial.

### Startup ($149/mo) — Small teams and early-stage pipelines

The jump from Hobby to Startup is significant: 10x the credits (1M vs 100K) and 2.5x the threads (50 vs 20) for 3x the price. This is where the economics start working for daily product monitoring, weekly competitive analysis, or a small team running a few concurrent jobs. Still US/EU only, so check your geotargeting needs before assuming this is enough.

### Business ($299/mo) — Production workflows needing global reach

This is the tier where ScraperAPI starts feeling like a real production tool. You unlock global country-level geotargeting across 50+ countries, unlimited analytics history, and 100 concurrent threads. Three million credits covers most mid-scale operations — if you're running 30,000 plain requests a day, you're comfortably inside the envelope. The lack of Pay-As-You-Go is the main limitation; if your volume is spiky, you'll want to look at Scaling.

### Scaling ($475/mo) — Variable-volume operations

ScraperAPI marks this as their most popular plan, and the reason is Pay-As-You-Go. Five million credits, 200 threads, global geotargeting, and crucially the ability to keep scraping past your limit at a predictable overage rate. For agencies, growing data teams, or any operation where monthly volume is hard to forecast, this is the tier that prevents midnight cutoffs. 👉 [Explore the Scaling plan](https://www.scraperapi.com/pricing/?fp_ref=coupons) if your workload has unpredictable spikes.

### Professional ($975/mo) — High-volume recurring scraping

10.5 million credits, 300 threads, and priority support. At this tier the per-credit cost drops noticeably and the priority support channel becomes useful when something breaks at scale. This is the entry point where the service starts behaving like an enterprise vendor rather than a developer tool.

### Advanced ($1,975/mo) — Continuous multi-source pipelines

21.5 million credits, 500 threads, and priority routing (your requests jump the queue). If your business depends on near-real-time web data at scale — pricing intelligence across hundreds of retailers, SERP tracking across thousands of keywords — this is where the infrastructure earns its keep.

### Enterprise (Custom) — 22M+ requests and custom SLAs

For organizations running tens of millions of requests monthly or needing custom SLAs, dedicated support, and negotiated pricing. You'd reach out to the sales team directly rather than self-serve.

## Structured Data Endpoints: The Feature That Saves Developer Time

Beyond raw HTML retrieval, ScraperAPI offers **structured data endpoints** (SDEs) that return parsed JSON for popular domains instead of raw HTML you have to parse yourself. These cover:

- **Amazon** — product details by ASIN, search results, competitor offers, with 18+ fields including price, ratings, BSR, variants, images, and seller info across 21 regional marketplaces
- **Google** — SERP results, Shopping, Maps, News, and Jobs
- **Walmart** — product, search, category, and reviews
- **eBay** — product and search
- **Redfin** — search, agent details, rentals, and for-sale listings

SDEs cost 5 credits per request and are available on every plan including Free. The tradeoff is straightforward: 5 credits is more expensive than a 1-credit raw HTML request, but you skip the developer time of building and maintaining a parser that breaks every time the site changes its layout. For small teams without dedicated scraping engineers, SDEs are often the cheaper option in practice. For teams with engineering capacity scraping at very high volume, the 5-credit premium is harder to justify and a custom parser may win on cost.

Independent benchmarks put ScraperAPI's success rate on Amazon at around 98% and on Zillow at 100% — strong results for the domains the SDEs are built for. The same benchmarks show weaker performance on social media (Instagram and Twitter/X at 0% success) and on some travel sites, so SDE coverage is a real differentiator but not a universal solution.

## The Real Cost Per 1,000 Requests

Headline pricing only means something once you factor in the credit multipliers. Here's the effective cost per 1,000 requests across plan tiers and request types:

| Plan | Standard (1 credit) | JS Rendering (10) | E-commerce (5) | SERP (25) | Ultra-Premium + JS (75) |
| --- | --- | --- | --- | --- | --- |
| Hobby ($49) | $0.49 | $4.90 | $2.45 | $12.25 | $36.75 |
| Startup ($149) | $0.15 | $1.49 | $0.75 | $3.73 | $11.18 |
| Business ($299) | $0.10 | $1.00 | $0.50 | $2.49 | $7.48 |
| Scaling ($475) | $0.10 | $0.95 | $0.48 | $2.38 | $7.13 |

The pattern is clear: the per-credit cost drops sharply as you move up the tiers, but the multiplier effect means the spread between a "cheap" request and an "expensive" one is enormous within any tier. A Hobby plan that looks like $0.49 per 1,000 requests for simple pages is actually $36.75 per 1,000 for ultra-premium rendered requests — a 75x difference. This is why modeling your actual workload before choosing a plan matters more than any other single decision.

## Common Pain Points (and How to Avoid Them)

A few issues come up consistently across user reviews on G2, Capterra, Trustpilot, and Reddit. Knowing them in advance saves real money.

**Credits don't roll over.** Unused credits expire at the end of each billing cycle. There's no banking of credits for a busy month later. If your volume is irregular, Pay-As-You-Go (Scaling and above) is the safer model than trying to size a fixed plan.

**404 responses consume credits.** ScraperAPI charges for both 200 and 404 status codes — only truly failed requests (timeouts, blocks) are free. If you're scraping a list of URLs where some are dead, those dead links still cost you.

**Domain-based pricing is automatic.** You don't opt into the 5-credit Amazon multiplier or the 25-credit Google multiplier; it's applied the moment the API detects the domain. Anti-bot bypass credits are also added automatically when Cloudflare, DataDome, or PerimeterX are detected. You can't disable them.

**Pay-As-You-Go is gated.** If you're on Hobby, Startup, or Business and you exhaust credits mid-cycle, you're cut off until renewal. The only options are upgrading or waiting. This is the single most common reason users report being surprised by downtime.

**No proactive usage alerts.** The dashboard shows usage stats, but there's no email or SMS when credits are running low. You have to check manually. Set a calendar reminder for the first month until you build intuition for how fast credits burn on your specific targets.

**A 10-minute forced cache on difficult targets.** For heavily protected sites, ScraperAPI may serve results up to 10 minutes old. If you're scraping time-sensitive data like live pricing or stock levels, factor that latency into your freshness requirements.

**The DataPipeline feature uses a different credit schedule.** ScraperAPI's no-code scheduled scraping product (DataPipeline) charges 6 credits for a basic request that would cost 1 credit via the standard API. If you're using the no-code scheduler, check the separate credit table before assuming standard costs apply.

On the positive side, the **7-day no-questions-asked refund policy** is real and consistently honored — if you sign up, test, and decide the service doesn't fit, support will refund within 7 days. And **failed requests (true failures, not 404s) don't cost credits**, which is more consumer-friendly than providers that charge for every attempt.

## What Real Users Say

Aggregating reviews across the major platforms gives a consistent picture:

| Platform | Rating | Review Count |
| --- | --- | --- |
| G2 | 4.4/5 | 16 |
| Capterra | 4.6/5 | 62 |
| Trustpilot | 4.5/5 | 43 |

Capterra sub-ratings put Ease of Use at 4.9/5, Customer Service at 4.6/5, Features at 4.5/5, and Value for Money at 4.5/5. The positive themes cluster around easy initial setup, clean documentation, and reliable performance on well-supported targets like Amazon and Google. The negative themes cluster around pricing transparency (credit multipliers being confusing, prices having increased over time) and reliability on harder targets where success rates drop.

The honest summary: ScraperAPI is well-regarded for getting started quickly and performing reliably on popular, well-supported domains. The complaints are real but predictable — they're almost all things you can avoid by understanding the credit system before you commit, modeling your workload, and testing on the free tier first.

## How to Get Started Without Wasting Money

The recommended path is the same regardless of which provider you're evaluating:

1. **Start with the free trial.** ScraperAPI's free tier gives 1,000 credits a month permanently, plus a 7-day trial with 5,000 credits and no credit card required. Use the trial to test success rates on your actual target sites — not generic test pages. 👉 [Start the free trial here](https://www.scraperapi.com/?fp_ref=coupons) to test before paying anything.

2. **Document which sites need rendering or premium proxies.** While testing, note which targets require `render=true`, which need premium proxies, and which trigger anti-bot detection. Each of those multiplies your credit cost.

3. **Estimate realistic monthly volume with multipliers applied.** Take your target request count and multiply by the credit cost per request for your specific domains. That number — not the headline credit count — is what determines which plan you need.

4. **Pick the smallest plan that covers your modeled volume with headroom.** If your volume is predictable, a fixed plan is fine. If it's spiky, prioritize a plan with Pay-As-You-Go (Scaling and above) so a busy week doesn't take you offline.

5. **Check geotargeting needs.** If you need IPs outside the US and EU, Business is the minimum tier. Don't assume you can scrape Asia-Pacific pricing from a US-IP-only plan — you'll get US-priced results.

6. **Use structured data endpoints where available.** For Amazon, Google, Walmart, and the other SDE-supported domains, the 5-credit cost is usually worth skipping parser maintenance. For unsupported domains, you're on raw HTML and your own parser.

7. **Monitor credit consumption daily for the first month.** There are no proactive alerts, so check the dashboard yourself until you have intuition for your burn rate.

## A Note on the Wider Market

ScraperAPI isn't the only option, and depending on your use case it may not be the cheapest. Independent benchmarks suggest that for basic HTML scraping, several competitors are competitive on per-request cost; for JavaScript rendering, the credit multiplier varies meaningfully across providers; and for the hardest anti-bot targets, different providers have different strengths. The right approach is to model your specific workload — target domains, rendering needs, volume, geotargeting — and compare effective per-1,000-request costs across two or three providers before committing.

That said, ScraperAPI's combination of a genuine free tier, a clean API, structured data endpoints for the most commonly scraped domains, and a plan ladder that scales from $49 to custom enterprise pricing makes it a reasonable default to evaluate first — especially if your targets overlap with Amazon, Google, Walmart, or Zillow, where its SDEs and success rates are strongest.

## Frequently Asked Questions

**Is there a free web crawler API?**
Yes. ScraperAPI offers a permanent free tier with 1,000 API credits per month and a 7-day trial with 5,000 credits, no credit card required. The free tier is enough to test integrations and validate success rates on real target sites. Credit multipliers still apply — 1,000 credits is 1,000 plain HTML requests, but only 100 JavaScript-rendered pages or roughly 40 Amazon requests.

**How much does a web crawler API cost per request?**
It depends entirely on the request type. A standard HTML request costs 1 credit; JavaScript rendering adds 10; premium proxies add 10; ultra-premium proxies add 25; structured data endpoints cost 5; and combining features can push a single request to 75 credits. On the Hobby plan ($49/mo, 100K credits), that's anywhere from $0.00049 per request (standard) to $0.0368 per request (ultra-premium plus rendering). Always model your specific workload.

**Can a web crawler API scrape sites that require login?**
ScraperAPI supports session persistence (same IP across multiple requests via `session_number`), but it explicitly forbids scraping data behind login walls and cannot handle form filling or two-factor authentication. If your targets require login, you'll need a different approach — typically a browser-based tool that operates within an authenticated session.

**What's the difference between a web crawler API and an official API?**
An official API is a stable, versioned interface the site itself publishes; you request data and receive it in a documented format. A web crawler API fetches pages the way a browser would and extracts data from the HTML, which means it works on sites with no official API but is more fragile when layouts change. Official APIs are preferable when available; scraping APIs are the fallback for the majority of sites that don't offer one.

**Do unused credits roll over?**
No. Unused credits expire at the end of each billing cycle on ScraperAPI. If your volume is irregular, prioritize a plan with Pay-As-You-Go (Scaling at $475/mo and above) so you can keep scraping past your included credits at a predictable overage rate rather than losing unused credits at month-end.

**Which plan should I pick?**
If you're testing or running a hobby project, start with the free trial and move to Hobby ($49) if you need more. Small teams and early startups usually fit Startup ($149). Production workflows needing global geotargeting need Business ($299) at minimum. Variable-volume operations should jump to Scaling ($475) for Pay-As-You-Go. High-volume recurring scraping fits Professional ($975), continuous multi-source pipelines fit Advanced ($1,975), and anything above that is a custom Enterprise conversation. 👉 [Compare all plans side by side](https://www.scraperapi.com/pricing/?fp_ref=coupons) to see which fits your modeled volume.

## The Bottom Line

A web crawler API is the right tool when you need to collect data from public websites at scale and don't want to build and maintain the proxy, rendering, and anti-bot infrastructure yourself. The decision that matters most isn't which provider to pick — it's understanding the credit system before you commit, modeling your actual workload with multipliers applied, and choosing a plan tier that matches your real volume rather than the headline credit count.

ScraperAPI is a reasonable default to evaluate: a genuine free tier that lets you test before paying, structured data endpoints that save real development time on the most commonly scraped domains, and a plan ladder that scales cleanly from a $49 side project to custom enterprise pricing. The credit multiplier system is the main thing to understand going in — get that right and the rest of the decision follows from your actual use case.

Start with the free trial, point it at your real targets, and let the numbers tell you which plan you need. 👉 [Start your free 7-day trial — no credit card required](https://www.scraperapi.com/?fp_ref=coupons).
