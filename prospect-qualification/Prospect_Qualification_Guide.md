# Prospect Qualification Guide: Testability Tiers

**Tool:** `Fastr_Prospect_Testability_Scorer.xlsx`

## The problem

We keep offering free trials to sites that are too small to test on. Without enough traffic and conversions, an A/B test can't reach statistical significance in a reasonable time. Tests run for months, finish inconclusive, and we can't prove what optimization is worth. A trial on a site like that costs us time and leaves no proof to sell with.

**The fix:** before offering a trial, estimate how long a typical test would take on the prospect's traffic. If it's too slow, don't trial.

## The one number that matters: weeks to significance

The scorer only needs two inputs: **annual US digital revenue** and **monthly sessions**. AOV is optional.

| Step | Formula |
|---|---|
| Revenue per visitor (RPV) | Revenue ÷ 12 ÷ monthly sessions |
| Conversion rate (CVR) | RPV ÷ AOV |
| Visitors needed per variant | (Zα/2 + Zβ)² × [p₁(1−p₁) + p₂(1−p₂)] ÷ (p₂−p₁)², where p₂ = p₁ × (1 + MDE) |
| Weeks to significance | (Visitors per variant × variants) ÷ weekly visitors entering the test |

Default settings: 95% confidence, 80% power, 5% relative lift (MDE), 2 variants, and 50% of site traffic in the test. You can change all of them on the **Assumptions** tab.

New to these terms? See [Evan Miller: How Not To Run an A/B Test](https://www.evanmiller.org/how-not-to-run-an-ab-test.html), the [sample size calculator](https://www.evanmiller.org/ab-testing/sample-size.html) and [Minimum Detectable Effect (Optimizely)](https://www.optimizely.com/optimization-glossary/minimum-detectable-effect/).

## Tiers

| Tier | Rule (defaults) | What it means | Action |
|---|---|---|---|
| **Tier 1: Pursue** | ≤ 2 weeks to significance **and** ≥ $200M revenue | 20+ clean tests a year per surface | Offer the trial. Plan 2-week tests. |
| **Tier 2: Qualify** | ≤ 4 weeks **and** ≥ $50M revenue | About 1 test a month. Only top-traffic pages work. | Trial only with a scoped plan: high-traffic pages and bold tests (≥10% lift). |
| **Tier 3: Don't trial** | Everything else | 4+ weeks per test. Real wins of 2–8% won't show up. | No A/B trial. Nurture, or sell non-testing services. |

Note: revenue alone doesn't decide the tier. A $220M home-furnishings site with a high AOV and low traffic can still be Tier 2. That's why the scorer uses traffic math and not revenue bands.

## Rules of thumb for reps

- **Under ~1M monthly sessions:** almost always Tier 2 or 3.
- **"Smallest lift readable in 4 weeks" above 10%:** most real wins will be invisible. Treat this as a red flag.
- **Fewer than ~350 conversions per variant:** results can't be trusted, however long the test runs.
- **Borderline accounts (within ~25% of a threshold):** score them at the lower tier until the prospect shares real GA4/analytics data. Third-party estimates (Similarweb, Digital Commerce 360) can be off by 30% or more.

## Workflow

1. Pull revenue from [Digital Commerce 360](https://www.digitalcommerce360.com/), a 10-K or the prospect. Pull sessions from Similarweb/Semrush.
2. Enter them on **Prospect Scorer**. Filter by Tier.
3. On discovery calls, use **Single Calculator** to show prospects their own math. It shows why a fast-testing program fits them, or why it doesn't yet.
4. Use **Traffic Thresholds** as a quick reference for minimum sessions by conversion rate and lift.
