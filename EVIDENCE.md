# IBIS Evidence Report — 2026-07-10 00:19

Auto-generated from the live decision database, daily CSVs, and
current quotes. Regenerates daily from the live loop, or on demand:
`python src\evidence.py`. History of these snapshots accumulates in
`data/evidence_history.csv`. The backtest contributes no numbers here.

## Headline verdict (computed, not editorial)

**No trading-edge claim is possible: 2 independent episode(s) exist and 0 have resolved at their hold horizon.**

Signal-days: 8. Independent episodes: 2. Resolved: 0. These are different numbers and only the resolved-episode count is a sample size.

## Plain-Language Verdict (LLM narration of the numbers above)

_ManifoldAuditor narration, generated 2026-07-10T00:19:19. The computed numbers nearby are the source of truth; this text only describes them._

No trading-edge claim is possible because there are no resolved episodes at their hold horizon. The number of resolved episodes is 0, which falls below the power threshold for a perfect record (5 episodes) and all other thresholds listed (37, 67, and 153 episodes). Therefore, based on these numbers alone, it cannot be concluded that an edge claim is justified.

## Episodes

| Asset | Dir | Started | Signal-days | Hold | Status |
|---|---|---|---|---|---|
| BTC | DOWN | 2026-07-03 | 1 | 20 | open (+2.22% so far, resolves +20 bars) |
| BTC | UP | 2026-07-04 | 7 | 20 | open (+1.34% so far, resolves +20 bars) |

## Signal-day horizon scoring

P0 = signal-date daily close (fallback: detection price). Live detections evaluate a provisional intraday bar; at small n this convention can flip individual marks — stated, not hidden.

| Date | Asset | Dir | Conf | +1b | +3b | +5b | +10b | +20b | Now |
|---|---|---|---|---|---|---|---|---|---|
| 2026-07-03 | BTC | DOWN | 0.66 | +0.87% ✗ | +2.32% ✗ | -0.46% ✓ | — | — | +2.22% ✗ |
| 2026-07-04 | BTC | UP | 0.64 | +0.73% ✓ | +0.33% ✓ | +1.23% ✓ | — | — | +1.34% ✓ |
| 2026-07-05 | BTC | UP | 0.64 | +0.70% ✓ | -2.03% ✗ | — | — | — | +0.61% ✓ |
| 2026-07-06 | BTC | UP | 0.64 | -1.09% ✗ | -0.21% ✗ | — | — | — | -0.09% ✗ |
| 2026-07-07 | BTC | UP | 0.64 | -1.64% ✗ | — | — | — | — | +1.01% ✓ |
| 2026-07-08 | BTC | UP | 0.71 | +2.58% ✓ | — | — | — | — | +2.69% ✓ |
| 2026-07-09 | BTC | UP | 0.71 | +2.17% ✓ | — | — | — | — | +2.29% ✓ |
| 2026-07-10 | BTC | UP | 0.71 | — | — | — | — | — | +0.11% ✓ |

## Baseline comparison (same dates, same horizons)

| Horizon | n | IBIS correct | Always-UP correct |
|---|---|---|---|
| +1 bars | 7 | 4 | 5 |
| +3 bars | 4 | 1 | 2 |
| +5 bars | 2 | 2 | 1 |
| now | 8 | 6 | 7 |

A coin flip expects n/2. If IBIS does not clearly beat BOTH columns at meaningful n, no edge claim survives.

## Statistical power and time-to-significance

| If true hit rate is | Resolved episodes needed | Have | ETA (observed cadence) | ETA (backtest-prior cadence) |
|---|---|---|---|---|
| perfect record (min possible) | 5 | 0 | 2026-08-16 | 2026-09-12 |
| 70% | 37 | 0 | 2026-12-06 | 2027-06-25 |
| 65% | 67 | 0 | 2027-03-21 | 2028-03-20 |
| 60% | 153 | 0 | 2028-01-16 | 2030-04-28 |

Cadence assumptions: observed 8.7 episodes/month
(measured over the live record so far — a tiny sample, treat as rough); backtest-prior 3.4 episodes/month for the currently-live assets (BTC, SOL). Activating GOLD+SPY would roughly double the prior cadence.

## Reliability (separate axis from edge)

**Uptime, trailing 7 days: 70.0%.** Since continuous operation began (2026-07-03): 68.3%. A gap is any >45min stretch without a completed cycle; the gap from the last cycle to now counts, so a live freeze shows up here within the day it happens.

Gaps in the last 7 days:
- 2026-07-03 13:10 → 2026-07-03 14:59 (1.8h)
- 2026-07-07 00:20 → 2026-07-08 14:00 (37.7h)
- 2026-07-08 14:00 → 2026-07-08 20:35 (6.6h)
- 2026-07-09 14:31 → 2026-07-09 18:55 (4.4h)

Per-asset live coverage:

| Asset | Cycles | Signals | First cycle | Last cycle |
|---|---|---|---|---|
| BTC | 222 | 212 | 2026-07-02T17:32 | 2026-07-10T00:18 |
| SOL | 19 | 0 | 2026-07-08T21:11 | 2026-07-10T00:18 |

Watchdog: run_ibis.py supervises the loop (heartbeat file, 45-minute timeout, logged restarts in data/watchdog.log). Freeze detection is now bounded to under an hour — previously a freeze went unnoticed for 37 hours (2026-07-07, root-caused: unbounded network call, since fixed).

## What this supports / does not support

Supports: the pipeline runs, captures, refuses stale data, and publishes pre-outcome receipts (github.com/aiempaths/ibis-ledger). Failures are logged and root-caused in the open.

Does not support: any claim of predictive skill or live profitability until the resolved-episode thresholds above are met. Directional accuracy alone will not suffice even then — closed-trade P&L is the final metric (the backtest's own SPY case shows hit rate and payoff can rank opposite ways).
