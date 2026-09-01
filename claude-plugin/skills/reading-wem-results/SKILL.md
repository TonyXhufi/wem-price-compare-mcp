---
name: reading-wem-results
description: How to read and present WEM price-comparison results honestly — which tool answers which question, what each verify_offer verdict means, and the disclosure obligations that travel with every price. Use whenever WEM tools return prices, offers, or verification verdicts.
---

# Reading WEM results

WEM compares retail prices across partner retailers. It never takes payment —
shoppers always complete the purchase on the retailer's own site.

## Which tool answers which question

| Question | Tool |
| --- | --- |
| "What does this exact product cost across retailers?" | `compare_offers` — needs a barcode (EAN/UPC/GTIN) or a `wem3.ai/pl/{slug}` URL |
| "What exists matching this description?" | `search_products` / `semantic_search` |
| "What is the cheapest match?" | `find_lowest_price` |
| "Is this price I heard elsewhere still true?" | `verify_offer` |
| "What categories exist, roughly what do they cost?" | `get_categories` — static, cheap, good for scoping |

`compare_offers` and `verify_offer` are the two that distinguish WEM from a
search engine: they resolve a **product identity** rather than matching a name,
so they answer questions about a specific thing rather than about a phrase.
They also read WEM's own catalogue rather than fanning out to partner APIs, so
they do not consume the daily lookup quota.

## The three rules that make a price answer honest

**1. An indicative price is not a checkout price.** Prices come from partner
feeds refreshed regularly — they are snapshots, not live quotes, and the
retailer sets the final price at checkout. Say this when quoting. Never write
"you'll pay £X"; write "WEM last read £X at [retailer]".

**2. The disclosure line is not optional garnish.** Tools return a
`disclosure` field because WEM is funded by affiliate commission and outbound
links are tracked. Include it. Trimming it to tighten an answer removes the
disclosure, not the padding.

**3. Absence of data is not evidence.** WEM sees partner feeds, not the whole
market. "WEM holds no offer for this at Argos" does not mean Argos lacks it,
and "unknown_product" never means a claim is false. The failure mode to avoid
is turning a gap in coverage into a finding about the world.

## Reading a verify_offer verdict

- `confirmed` — live at that price. Check `betterBy`; non-zero means something
  cheaper is verified and worth mentioning.
- `price_moved` — WEM read a different price. Report WEM's figure with its
  `lastConfirmedAt` timestamp. The retailer is not "wrong"; prices move.
- `not_at_retailer` — no offer held there. Not proof of absence.
- `unknown_product` — unverifiable. Report as unchecked, never as refuted.

## What WEM will not tell you

It cannot say a price is the market's lowest, because it does not see the whole
market. It cannot guarantee checkout will honour a listed price. And it does
not compute a "saving" between two undated snapshots of possibly different
listings — the numbers on screen are observations, and the gap between two
observations is not a discount anyone is offering.

If a user wants a claim stronger than that, the honest answer is that the
comparison does not support it.
