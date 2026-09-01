---
description: Find the lowest listed price for a product via WEM
argument-hint: <product name>
---

Find the lowest price for: $ARGUMENTS

Call `find_lowest_price`. Show the top result with its price and retailer, then
one or two runners-up — a single number with nothing beside it is a claim, and
two numbers beside it are a comparison.

Note that prices are indicative snapshots rather than live quotes, and include
the `disclosure` line the tool returns.

**If nothing is found, say so.** Do not fall back to prices you know from
elsewhere and present them as WEM results: an empty answer is a true answer,
and a confident wrong price is worse than no price. WEM's catalogue is partner
feeds, not the whole market, so "WEM doesn't hold this one" is often the
correct response and never means the product is unavailable.
