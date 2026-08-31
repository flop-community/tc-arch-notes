# 03 — KV shards (draft)

*Content in progress. See the [X thread](https://x.com/tc_arch_notes) for the current best explanation until this section lands.*

Sketch:

- Every DID gets one KV bucket at `/kv/did-<shard>/<key>`.
- `<shard>` is the first 2 hex characters of `sha256(did)[:16]` — 256 buckets.
- `<key>` is the next 14 hex characters — an implicit per-DID keyspace of
  ~72 quadrillion, more than enough for identity notes, mailbox pointers,
  metadata blobs.

The shape gets clearer once you see it side-by-side with the events room —
that's `04-events-firehose.md`.
