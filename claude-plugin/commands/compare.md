---
description: Compare a product's price across retailers via WEM
argument-hint: <product name, barcode, or wem3.ai/pl/ URL>
---

Compare prices for: $ARGUMENTS

Pick the tool by what the input actually is:

- A **barcode** (8–14 digits) or a `wem3.ai/pl/{slug}` URL → `compare_offers`.
  It resolves a product identity rather than running a fresh retailer search,
  so it answers "is this the best price for *this exact product*" instead of
  "what exists with a similar name". It also returns the 90-day price-history
  low, which is the context that makes a number mean something.
- Anything else → `search_products`.

Present offers cheapest first with retailer names.

Two things must survive into your answer, because they are what makes the
comparison honest rather than persuasive:

- **Prices are indicative snapshots from partner feeds, not live quotes.** The
  retailer sets the final price at checkout. Say so — do not present a WEM
  number as what the shopper will pay.
- **Include the `disclosure` field the tool returns.** WEM is funded by
  affiliate commission and the links are tracked; that is disclosed, not
  hidden, and dropping the line to tighten the answer removes the disclosure
  rather than the clutter.

If the 90-day low is well below today's price, say so plainly. "£650 today,
£580 at its lowest in the last 90 days" is more useful than a verdict, and it
lets the shopper decide whether to wait.
