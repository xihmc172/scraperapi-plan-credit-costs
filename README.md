# WebScrapingAPI alternative: is ScraperAPI the right switch, which plan fits your targets, and what do the credits really cost per 1,000 requests?

Three kinds of tools come up when you search for a WebScrapingAPI alternative: proxy networks with a scraping API wrapped around them, LLM-first crawlers that hand back markdown, and managed services that deliver a finished dataset. ScraperAPI sits in the first group, and within that group it is the one that also ships pre-parsed endpoints for Amazon, Google, Walmart, eBay and Redfin. G2's own alternative page for WebScrapingAPI.com says buyers in this category compare on reliability and ease of use, so the numbers below are about what you pay per usable request rather than the sticker price of a plan.

A ScraperAPI credit is not the same thing as a request. The multiplier moves with the target domain and with whatever features you turn on, which means the $49 Hobby plan buys 100,000 standard pages or 4,000 Google searches. Both figures are accurate. What follows is every plan on the pricing page, the complete credit table, the cost per 1,000 requests for four common workloads, and the billing rules that decide whether a plan works for you at all.

> **Default pick:** Hobby at $49/month for 100,000 credits if your targets are ordinary pages. If Google SERPs or Amazon make up most of your volume, start at Startup ($149/month, 1,000,000 credits), because one SERP request burns 25 of them.
> 👉 [See every ScraperAPI plan and its current price](https://www.scraperapi.com/pricing?fp_ref=coupons)

## Every ScraperAPI plan and what each tier changes

| Plan | Monthly | Annual (per month) | Credits / month | Threads | Sign up |
| --- | --- | --- | --- | --- | --- |
| Free | $0 | — | 1,000 | 5 | [Free](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Hobby | $49 | $44 | 100,000 | 20 | [Hobby](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Startup | $149 | $134 | 1,000,000 | 50 | [Startup](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Business | $299 | $269 | 3,000,000 | 100 | [Business](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Scaling | $475 | $427 | 5,000,000 | 200 | [Scaling](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Enterprise | Custom | Custom | Custom (3M+) | Custom | [Options](https://www.scraperapi.com/pricing?fp_ref=coupons) |

Annual billing takes 10% off every paid tier, which is roughly $60 a year on Hobby alone. The free plan is permanent, not a trial that quietly expires: 1,000 credits a month and 5 concurrent connections, with a separate 7-day, 5,000-credit trial on signup that does not ask for a card. ScraperAPI also sells Professional and Advanced tiers above Scaling. Both include pay-as-you-go overage at a fixed per-credit rate up to a monthly cap you set, and Advanced drops auto-upgrade. Check the pricing page for their current rates if 5 million credits a month is not enough.

Country-level targeting is the one feature that changes tiers rather than credit cost. US and EU regions are available on the lower plans; anything beyond that starts at Business.

## What a single credit costs, by target and by feature

ScraperAPI publishes its multiplier table, and it is the most useful page on the site if you are trying to forecast a bill.

| Request type | Credits |
| --- | --- |
| Standard page | 1 |
| Amazon, Walmart, eBay | 5 |
| Google, Bing (including subdomains) | 25 |
| LinkedIn | 30 |
| Bot-protection bypass (Cloudflare, Turnstile, DataDome, PerimeterX/HUMAN, Akamai) | +10 |
| JS rendering (`render=true`) | +10 |
| Premium proxies (`premium=true`) | +10 |
| Screenshot (`screenshot=true`) | +10 |
| Ultra premium (`ultra_premium=true`) | 30, or 75 with rendering |
| Geotargeting, sessions, device type, output format, auto-parsing | 0 |

The zero-cost row is worth reading twice. Passing `output_format=markdown`, pinning a session, choosing a device type and asking for parsed output do not add credits. Rendering, bypassing and premium IPs do. A rendered page on an ordinary site is 11 credits, not 1, and a rendered page behind Cloudflare is 21.

## The same plans, priced per 1,000 requests

Multiplying the plan's per-credit rate by the request's credit cost gives you the number that actually matters. Figures below use monthly billing and are rounded.

| Plan | Standard page | Amazon | Google SERP | LinkedIn |
| --- | --- | --- | --- | --- |
| Hobby ($49 / 100K) | $0.49 | $2.45 | $12.25 | $14.70 |
| Startup ($149 / 1M) | $0.15 | $0.75 | $3.73 | $4.47 |
| Business ($299 / 3M) | $0.10 | $0.50 | $2.49 | $2.99 |
| Scaling ($475 / 5M) | $0.10 | $0.48 | $2.38 | $2.85 |

Two conclusions fall out of this. First, Hobby's 100,000 credits is a large allowance for blog pages and a small one for search results: 4,000 SERP requests, or 3,333 LinkedIn pages, or about 9,000 JS-rendered standard pages. Second, the jump from Hobby to Startup cuts your per-request cost by two thirds, so a team whose workload already costs more than $149 a month on Hobby is overpaying for the privilege of staying on the small plan.

If you want the same math for your own URL list, the dashboard's Domain Cost Estimator returns the credit cost for a single URL before you commit, and the `sa-credit-cost` response header reports what each real request actually spent.

👉 [Check the current plan rates before you run the numbers](https://www.scraperapi.com/pricing?fp_ref=coupons)

## Billing rules that decide whether a plan fits

**Pay-as-you-go starts at Scaling.** On Hobby, Startup and Business there is no overage billing; when credits run out, scraping pauses until renewal unless you have opted into auto-upgrade, which bumps you to the next tier automatically. If your traffic spikes in one week of the month and idles the rest, the cheap plan is the expensive one.

**Hitting your concurrency cap returns a 429.** The request is turned away rather than queued, and you are not charged for it. Retry logic has to live in your code. Thread counts run from 5 on the free tier to 200 on Scaling.

**Credits do not roll over.** The balance resets at renewal, so an uneven workload either wastes credits or runs dry, never both comfortably.

**There is no documented low-credit alert on the pricing page.** The guidance ScraperAPI gives is procedural: watch the dashboard, set `max_cost` per request so one expensive URL cannot quietly drain a day's budget, and check the Domain Cost Estimator before adding a new target. Teams that need push notifications on spend will have to build them from the API or the dashboard data.

**Ultra premium is a platform-scale line item.** At 30 credits a request, or 75 with rendering, a single thousand-request job costs more than a Hobby month. It exists for targets that nothing else gets through, and it should be scoped to those targets only.

## How ScraperAPI compares with Firecrawl, Zyte, Apify and Bright Data

ScraperAPI is not on the G2 alternatives list for WebScrapingAPI.com, and it would be dishonest to pretend otherwise. Here is where it wins and loses against the tools that are.

| Tool | Pricing model | Strongest at | Watch out for |
| --- | --- | --- | --- |
| ScraperAPI | Credits with domain and feature multipliers | Proxy infrastructure plus pre-parsed Amazon, Google, Walmart, eBay and Redfin endpoints | Multipliers make forecasting harder; country targeting needs Business |
| Firecrawl | $0 for 1,000 credits/month, paid from $19/month ($16 annual); 1 credit per successful page | LLM-ready markdown and JSON by default; open source (AGPL-3.0) and self-hostable | Blocks Instagram, YouTube and TikTok outright; no custom CSS selectors or headers |
| Zyte | Per URL: $0.13 for an HTTP response, $0.06 after a $500/month commitment, from $1.01 for a rendered page; 14-day trial | Handing the whole pipeline to a managed team; Scrapy lineage | Per-URL pricing gets expensive fast on rendered pages |
| Apify | $0 free tier, compute-unit billing | A marketplace of 20,000+ pre-built Actors and full Playwright/Puppeteer control | Costs depend on runtime, not request count, so budgeting takes work |
| Bright Data | Custom and enterprise, pay-per-GB for proxies | 150M+ IPs across 195 countries, Web Unlocker, 120+ pre-built scrapers | Enterprise sales cycle and pricing |

If your pipeline exists to feed clean text into a model, Firecrawl's flat one credit per successful page is easier to forecast than any multiplier scheme, and self-hosting removes the per-page cost entirely. If you want someone else to run the scraping operation, Zyte's managed delivery is the honest answer. ScraperAPI's case rests on breadth of proxy infrastructure plus parsed JSON for the five domains most teams actually monitor.

## Picking a plan from your target list

- **Mostly standard pages under about 90,000 requests a month** → Hobby. The 100,000 credits cover it, and $49 is the cheapest entry point that gives you 20 threads.
- **Google SERPs or marketplace data as a core workload** → Startup. A million credits is 40,000 searches, and the per-request cost drops from $12.25 to $3.73 per thousand.
- **Country-level targeting outside the US and EU** → Business. There is no way around this gate on the lower tiers.
- **One or two spike months a year** → Scaling for pay-as-you-go, or stay on a lower tier with auto-upgrade switched on and accept the tier bump when it happens.
- **Evaluating, not buying yet** → the free plan plus the 7-day trial. Run your actual URLs, not the demo ones, and check the credit cost per request in the dashboard before you spend anything.

## FAQ

**Is 1,000 free credits enough to test with?** For a smoke test, yes: it is roughly 40 Google searches or 200 Amazon products. The 7-day, 5,000-credit trial on signup is the better window, and it does not require a card.

**Do unused credits carry over?** No. The balance resets at renewal on every tier.

**What happens if I run out mid-month?** Requests pause. On Hobby through Professional you can opt into auto-upgrade to the next tier; on Scaling and above you can enable pay-as-you-go at a fixed per-credit rate with a cap you set.

**Can I get markdown or JSON instead of HTML?** Yes. HTML is the default, `output_format=markdown` switches the output, and the structured data endpoints return parsed JSON. Neither costs extra credits.

**How much does annual billing save?** 10% on every paid plan, so Hobby goes from $49 to $44 a month.

**What is the refund policy?** The trial is the documented risk-reduction route. Third-party write-ups of the plan terms cite a 7-day refund window, so confirm it on the billing page before you commit to an annual plan.

## Before you enter a card

Match the plan to the credit cost of your targets, not to the credit number in the plan name. A team scraping 60,000 blog pages a month needs Hobby. A team scraping 60,000 Google SERPs needs 1.5 million credits, which is Startup plus a conversation about Scaling. Get that calculation wrong in either direction and you either waste budget or hit a wall in week two.

Two things to confirm before checkout: the current price on the pricing page, since plans above Scaling are quoted rather than listed, and the real per-request credit cost for your top five URLs from the Domain Cost Estimator. Those two numbers turn the whole table above into a single monthly figure you can defend.

👉 [Start on the free plan, then pick the tier your credit math points to](https://www.scraperapi.com/pricing?fp_ref=coupons)
