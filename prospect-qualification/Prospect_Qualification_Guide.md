# Prospect Qualification Guide: Testability Tiers (v2)

**Tool:** `Fastr_Prospect_Testability_Scorer.xlsx`

## The problem

We keep offering free trials to sites that are too small to test on. If a site doesn't get enough orders, an A/B test can't reach statistical significance in a reasonable time. Tests then run for months, finish inconclusive, and we have nothing to show for the optimization work.

## What decides test speed: orders per week

Neither revenue nor traffic decides how fast a site can test. **The number of conversions per week decides it.** We checked this against Fastr's own customers in PostHog over the last full weeks (Sep–Oct 2026):

| Customer | Visitors / wk | Conv. rate | **Orders / wk** | Result |
|---|---|---|---|---|
| Express | 650K | 2.84% | **~18,450** | Tests fast |
| Bonobos | 131K | 3.93% | **~5,140** | Tests fast |
| Ethan Allen | 221K | 0.13% | **~280** | Works only because tests are scored on design-center CTA clicks |
| The 1916 Company | 80K | 0.015% | **~12** | Purchase tests cannot finish |

Revenue on its own misleads. Bonobos tests fast on about $79M a year of tracked orders, while Brilliant Earth ($438M) has a $2,000 AOV and therefore few orders.

## The math

| Lift you want to detect | Conversions needed per variant |
|---|---|
| 10% (a bold test) | ≈ 1,650 |
| 5% (a typical win) | ≈ 6,450 |

**Weeks to read a test** = (conversions per variant × variants) ÷ (orders per week × share of buyers who enter the test).

The calculation uses 95% confidence and 80% power, and assumes 50% of buyers enter a test. Every test runs at least 2 weeks. Sources: [Evan Miller: How Not To Run an A/B Test](https://www.evanmiller.org/how-not-to-run-an-ab-test.html) and his [sample size calculator](https://www.evanmiller.org/ab-testing/sample-size.html).

## Tiers

| Tier | Online orders / week | Meaning | Action |
|---|---|---|---|
| **Tier 1: Pursue** | **≥ 5,000** (about 21,700 a month) | Reads a 10% lift in about 1 week and a 5% lift in about 5 weeks | Offer the trial. Plan 2-week tests on purchases. |
| **Tier 2: Qualify** | **1,500–5,000** | Reads a 10% lift in 1.5–4.5 weeks | Trial on top-traffic pages only, with bold tests. |
| **Tier 3: Don't trial** | **< 1,500** | Purchase tests take months | No A/B trial, unless tests can be scored on a micro-conversion with ≥ 1,500 events a week (the Ethan Allen model). |

## Inputs, in order of reliability

1. **Monthly online orders.** Ask the prospect, or look in GA4 or Shopify.
2. **Monthly visitors.** The tool multiplies them by a vertical conversion rate (benchmarks are on the Assumptions tab).
3. **Annual US digital revenue.** The tool divides it by AOV. This is the least reliable input, because public "digital revenue" often includes stores, phone orders, Amazon or international sales.

## Open questions before we lock the thresholds

- **The order math says almost any retailer with $40M+ a year in online orders clears Tier 1.** That doesn't fit our experience that only 3–5 of 100+ customers test fast. Possible explanations:
  - Fastr's tracking captures only part of each customer's orders. Express tracks about $164M a year, which is probably below its total online sales.
  - Tests run on narrow page sections, so far fewer buyers than 50% enter them.
  - Some customers lack the operational capacity to ship tests.
- **Next step:** measure tracked orders per week for every customer in PostHog and compare against which customers actually test fast. That shows whether orders per week alone separates them.

## Rules of thumb for reps

- **Ask for orders, not revenue.** "How many online orders a week?" decides the tier.
- **AOV above $500:** expect Tier 2 or 3 unless traffic is very large.
- **Borderline accounts (within ~25% of a threshold):** score them at the lower tier until real analytics are shared.
