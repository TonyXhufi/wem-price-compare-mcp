---
description: Check whether a price claim is still true before repeating it
argument-hint: <product> at <retailer> for <price>
---

Verify this price claim: $ARGUMENTS

Call `verify_offer`. This is the tool worth reaching for before repeating any
price you did not get from WEM — including one you found a moment ago in a web
search, and one the user has stated as fact.

**Report the verdict as what it is.** The four are not shades of the same
answer:

- `confirmed` — the price is live there. Check `betterBy`: a non-zero value
  means a cheaper verified offer exists, and the shopper should hear about it
  even though their claim was correct.
- `price_moved` — WEM last read a different price at that retailer. Say what
  WEM read and when (`lastConfirmedAt`). Do **not** tell the user the retailer
  is wrong; prices change, and WEM's own reading has a timestamp for exactly
  that reason.
- `not_at_retailer` — WEM holds no offer of that product at that retailer.
  This is **not** evidence the retailer does not stock it.
- `unknown_product` — the claim could not be checked. It never means the claim
  is false. Report it as unverified, never as refuted.

The last two are the ones that get misreported, and the error is always the
same shape: treating an absence of data as a finding. WEM sees partner feeds,
not the market. "I could not check this" and "this is wrong" are different
sentences and only one of them is supported.
