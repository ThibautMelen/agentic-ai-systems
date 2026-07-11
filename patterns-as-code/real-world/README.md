# 🛰️ Real-World Radars

**These are the actual files running the [nika](https://github.com/supernovae-st/nika) distribution campaign** (July 2026) — copied verbatim from the operator's daily rhythm, not demos. Each one is checked by this repo's CI on every push.

| File | What it does every morning | Cost |
|---|---|---|
| [`reddit-keyword-radar.nika.yaml`](reddit-keyword-radar.nika.yaml) | Target-subreddit feeds → keyword filter → diff vs yesterday → only NEW threads | $0 · zero model |
| [`github-traffic-ledger.nika.yaml`](github-traffic-ledger.nika.yaml) | GitHub traffic + release downloads (human/CI split) across 4 repos → one NDJSON line/day | $0 · zero model |
| [`deps-release-radar.nika.yaml`](deps-release-radar.nika.yaml) | Release feeds of the real workspace deps → only the new ships | $0 · zero model |

## Why they're interesting as *patterns*

- **State-file diff** — read last run (`on_error: recover:` a literal on first run — never a sibling-task reference, that's a [race](https://github.com/supernovae-st/nika/issues/402)) → compare → write next state. You only ever see what's NEW.
- **Resilient fan-out** — `for_each` + `fail_fast: false` + per-item `recover:`: one rate-limited feed yields empty instead of killing the batch.
- **Type-guarded state** — a corrupted state file folds to `[]` instead of crashing the diff (`try fromjson catch []`, then an array-type check).
- **Receipts** — every run writes a hash-chained trace; `nika trace verify` exits 0 or names the first broken link.

## Run them

```bash
brew install supernovae-st/tap/nika
nika check reddit-keyword-radar.nika.yaml   # static audit, offline
nika run  reddit-keyword-radar.nika.yaml    # zero keys needed
```

The traffic ledger needs `gh` authenticated against your own repos — swap the `repos:` var and it measures *your* campaign instead.
