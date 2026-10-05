# Prospect Qualification Guide: Tier 1 Only (v4)

**Tools:** `Fastr_Prospect_Testability_Scorer.xlsx` (see the **Tier 1 Decision** column) · `Testability_Tiers.html`

## The rule

**Engage only Tier 1 brands.** A Tier 1 brand can run a purchase test that reads a **5% lift at 95% confidence (80% power) within 3 weeks**, or within 2 weeks at the target level. Below the minimums, don't offer a trial, however large the brand.

## Tier 1 minimums

| Measure | **Minimum (3-week read)** | **Target (2-week read)** | Notes |
|---|---|---|---|
| **Online orders per week** | **4,500** | **6,500** | The deciding number. Ask for it first. |
| Online orders per month | 19,500 | 28,000 | De-duplicated orders. |
| Online orders per year | 234,000 | 340,000 | Weekly orders × 52. |
| Monthly unique visitors | 490,000 | 715,000 | At a 3.5% conversion rate. See the table below for other rates. |
| Conversion rate | ≥ 2% | ≥ 2% | Guidance, not a statistical limit. Every current Tier 1 customer converts at 2.8% or more. |
| AOV | Any | Any | AOV doesn't affect test speed. It sets how much revenue is needed to produce the orders. |
| **Annual online revenue** | **$30M** at a $130 AOV, **$73M** at $310 | **$44M** at a $130 AOV, **$105M** at $310 | Annual orders × AOV. |

Order figures are rounded up so they hold at any conversion rate from 1% to 10%. A prospect must clear **both** the order minimum and the 3-week read. Mackenzie Childs shows why both matter: it has about 4,800 orders a week, but at a 2.2% conversion rate a 5% lift takes 3.1 weeks to read, so it's a no.

### Monthly unique visitors needed, by conversion rate

| Conversion rate | Minimum | Target |
|---|---|---|
| 1% | 1,770,000 | 2,570,000 |
| 2% | 875,000 | 1,270,000 |
| 3.5% | 490,000 | 715,000 |
| 5% | 340,000 | 490,000 |
| 8% | 205,000 | 300,000 |

Visitors means unique people, not sessions. Sessions overstate reach by about 1.5–2×.

### Annual online revenue needed, by AOV

| AOV | Measured on | Minimum | Target |
|---|---|---|---|
| $130 | Express ($128) | $30M | $44M |
| $230 | Apparel median | $54M | $78M |
| $310 | Bonobos, AG Jeans, RM Williams | $73M | $105M |
| $500 | | $117M | $170M |
| $1,450 | Watches & jewelry median | $339M | $493M |
| $1,850 | Furniture median | $433M | $629M |

High-AOV categories rarely qualify. A $1,850-AOV furniture brand needs about 14× the online revenue of a $130 apparel brand to reach the same order volume.

## What today's Tier 1 customers look like

These figures come from PostHog: the last 14 days of orders tracked by Fastr, annualized. Customers' actual totals may be higher.

| Customer | Orders / week | Monthly unique visitors | Conversion | AOV | Online revenue / yr |
|---|---|---|---|---|---|
| Express | 22,400 | 2,757,000 | 2.8% | $128 | $148M |
| JR Cigars | 8,800 | 223,000 | 10.9% | $201 | $92M |
| Bonobos | 8,300 | 354,000 | 7.2% | $293 | $127M |
| AG Jeans\* | 8,100 | 314,000 | 8.2% | $340 | $143M |
| The Sak\* | 5,700 | 491,000 | 4.3% | $153 | $45M |
| **Range** | **5,700–22,400** | **223K–2.8M** | **2.8–10.9%** | **$128–$340** | **$45M–$148M** |

\* These sites record purchases through a Shopify webhook. Before a purchase can be credited to a test variant, the cart-token bridge has to be in place.

All 228 PostHog projects were scanned for the 30 days to 4 Oct 2026. Of these, 28 customers had usable visitor and purchase data, and **5 of the 28 meet the Tier 1 minimum**. The other 23 don't, including:

- Mackenzie Childs, Omnicheer, RM Williams and GK Elite. These four can only read bold (10%) lifts in 3 weeks.
- Ethan Allen. Its tests work only because they're scored on design-center CTA clicks, not purchases.

## How to decide

1. **Ask for weekly online orders,** from Shopify, GA4 or the prospect's order system. Below 4,500 means **do not engage.**
2. **Check the conversion rate.** Below 2% means the purchase tracking needs checking, and the site needs a lot more traffic to qualify.
3. **Run the Scorer or the prospect check on the page.** It needs to show **"Engage — minimum"** or **"Engage — target"**.
4. **Treat a borderline estimate as a no.** If orders were estimated from revenue or traffic and land within 25% above the minimum (4,500–5,625 a week), the answer is "do not engage" until the prospect shares real order data.
5. **Plan tests that reach the whole site or funnel.** A test on one page type, such as PDP only, reaches about half the buyers and needs about twice the volume.

## Method

The method matches the Experiment Feasibility by Client workbook:

- Visitors are unique people, not sessions.
- Conversion rate = converting visitors ÷ visitors.
- Orders are de-duplicated on transaction id.
- Reach grows sub-linearly: V(t) ∝ t^b, with b = 0.92 (median measured across customers).
- Orders per buyer = 1.1 (median measured across customers).
- Test sizing uses the two-proportion z-test at 95% confidence and 80% power (see [Evan Miller's sample-size calculator](https://www.evanmiller.org/ab-testing/sample-size.html)).

**Caveat:** PostHog counts only what Fastr tracks, so some customers' total orders may be higher than shown. The minimums are set on the Assumptions tab of the workbook and can be changed there.
