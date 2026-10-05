# Prospect Qualification Guide: Testability Tiers (v3)

**Tool:** `Fastr_Prospect_Testability_Scorer.xlsx`

## The bar

Being able to run a test doesn't mean the test will reach a result. A **fast, high-impact programme** needs a purchase test to read at **95% confidence (80% power) within 2–3 weeks**. The order volume that clears that bar is the minimum we should require before bringing a customer on.

## What the data says: all Workspace customers in PostHog

We scanned all 228 PostHog projects over the 30 days to 4 Oct 2026:

- 48 projects had Workspace data.
- 28 had usable visitor and purchase data, and those 28 are tiered.

| Tier | Customers | Who |
|---|---|---|
| **Tier 1**: a 5% lift reads in ≤ 2–3 weeks | 5 | Express, Bonobos, AG Jeans\*, JR Cigars, The Sak\* (3 weeks) |
| **Tier 2**: only a 10% lift reads in ≤ 3 weeks | 4 | Mackenzie Childs, Omnicheer\*, RM Williams, GK Elite\* |
| **Tier 3**: only a 20% lift reads in ≤ 3 weeks | 2 | Cigars.com, Nassau Candy |
| **Not a fit** for purchase tests | 17 | Ethan Allen†, Citizen, Bulova, The 1916 Company, Hardwood Lumber, … |

\* These sites record purchases through a Shopify webhook. Before a purchase can be credited to a test variant, the cart-token bridge has to be in place (see the Feasibility by Client data-quality log).

† Ethan Allen works as a customer because its tests are scored on design-center CTA clicks, not purchases.

## Minimum volume per tier

These figures assume a test that reaches 100% of visitors and the apparel median conversion rate of 3.5%:

| Tier | **Weekly orders** | Monthly orders | Monthly unique visitors |
|---|---|---|---|
| Tier 1: 5% lift in ≤ 2 weeks | **≈ 6,400** | ≈ 27,500 | ≈ 715,000 |
| Tier 1: 5% lift in ≤ 3 weeks | **≈ 4,400** | ≈ 19,000 | ≈ 490,000 |
| Tier 2: 10% lift in ≤ 3 weeks | **≈ 1,100** | ≈ 4,800 | ≈ 126,000 |
| Tier 3: 20% lift in ≤ 3 weeks | **≈ 290** | ≈ 1,270 | ≈ 33,000 |

**The required order count barely changes with conversion rate.** What changes is the number of visitors a site needs to produce those orders. A 1%-converting site needs about 2.6M monthly visitors for Tier 1, while an 8%-converting site needs about 300K. So **qualify on weekly orders first.**

## What that volume means in revenue, using PostHog-measured AOVs

These figures also use the 3.5% conversion rate:

| AOV | Example | Tier 1 (2 weeks) | Tier 1 (3 weeks) | Tier 2 | Tier 3 |
|---|---|---|---|---|---|
| $130 | Express ($128) | $43M/yr | $30M | $8M | $2M |
| $230 | Apparel median | $76M | $52M | $13M | $3.5M |
| $310 | Bonobos, AG Jeans, RM Williams | $102M | $71M | $18M | $4.7M |
| $1,450 | Watches & jewelry median | $479M | $330M | $84M | $22M |
| $1,850 | Furniture median | $611M | $421M | $108M | $28M |

AOV doesn't change the statistics, but it does change how much revenue a site needs to produce enough orders. A $2,000-AOV furniture retailer needs about 14× the online revenue of a $130 apparel site to test at the same speed.

## Rules of thumb for reps

1. **Ask for weekly online orders first.** About 6,400 a week puts a site in the fast programme. Under about 1,100 a week, only bold tests are possible, and under about 300 a week, purchase tests can't be run.
2. **High-AOV categories (furniture, watches, jewelry) rarely qualify on purchases.** Pitch micro-conversion testing (CTA clicks, appointments, leads) instead, as with Ethan Allen.
3. **Testing a single template, such as PDP only, needs about twice the volume.**
4. **Borderline accounts (within ~25% of a threshold)** go in the lower tier until they share real analytics.

## Method

The method matches the Feasibility by Client workbook:

- Visitors are unique people, not sessions.
- Conversion rate = converting visitors ÷ visitors.
- Orders are de-duplicated on transaction id.
- Reach grows sub-linearly: V(t) ∝ t^b, with b = 0.92 (median measured across customers).
- Orders per buyer = 1.1 (median measured across customers).
- Test sizing is the two-proportion z-test (see [Evan Miller's sample-size calculator](https://www.evanmiller.org/ab-testing/sample-size.html)).

**Caveat:** PostHog counts only what Fastr tracks, so some customers' total orders may be higher than shown.
