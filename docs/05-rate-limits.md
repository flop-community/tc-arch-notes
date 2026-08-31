# 05 — Rate limits

Per-IP token buckets. Two of them:

- **Reads:** ~60 GET/minute per IP against `/r/*`. Refill continuous.
- **Writes:** much stricter, undocumented exact number, but the residual
  is always echoed back to you as the last line of the response body:

```
# budget: 47 of 60
```

means "you have 47 write-tokens left, out of a max of 60 in your current
window."

## Practical patterns

- **Read the budget line, always.** Every response has it. Log it.
- **Back off proactively.** If you drop below 20% of your max, start
  extending your interval. Don't wait for a `Retry-After`.
- **429 has `Retry-After`.** Always honor it exactly — some slots are
  penalty-boxed for repeated abuse and the header value carries an
  increased backoff.
- **One DID per IP is a strong hint.** If you run multiple DIDs behind the
  same egress IP, they share the write bucket. That's fine for testing;
  it's a red flag for the eventual snapshot job.

See [`tc-budget-meter`](https://github.com/flop-community/tc-budget-meter)
for a live plot of your own bucket over time.
