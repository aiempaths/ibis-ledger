# IBIS Evidence Report — 2026-07-18 18:15

Auto-generated from the live decision database, daily CSVs, and
current quotes. Regenerates daily from the live loop, or on demand:
`python src\evidence.py`. History of these snapshots accumulates in
`data/evidence_history.csv`. The backtest contributes no numbers here.

## Headline verdict (computed, not editorial)

**No trading-edge claim is possible: 3 independent episode(s) exist and 0 have resolved at their hold horizon.**

Signal-days: 10. Independent episodes: 3. Resolved: 0. These are different numbers and only the resolved-episode count is a sample size.

## Plain-Language Verdict (LLM narration of the numbers above)

_ManifoldAuditor narration, generated 2026-07-18T18:15:48. The computed numbers nearby are the source of truth; this text only describes them._

No trading-edge claim is possible because there are no resolved episodes at their hold horizon. The number of resolved episodes is 0, which is below the power threshold for a perfect record (5) and all other thresholds listed (37 for 70%, 67 for 65%, and 153 for 60%).

## Episodes

| Asset | Dir | Started | Signal-days | Hold | Status |
|---|---|---|---|---|---|
| BTC | DOWN | 2026-07-03 | 1 | 20 | open (+3.62% so far, resolves +20 bars) |
| BTC | UP | 2026-07-04 | 8 | 20 | open (+2.72% so far, resolves +20 bars) |
| BTC | UP | 2026-07-15 | 1 | 20 | open (+0.14% so far, resolves +20 bars) |

## Signal-day horizon scoring

P0 = signal-date daily close (fallback: detection price). Live detections evaluate a provisional intraday bar; at small n this convention can flip individual marks — stated, not hidden.

| Date | Asset | Dir | Conf | +1b | +3b | +5b | +10b | +20b | Now |
|---|---|---|---|---|---|---|---|---|---|
| 2026-07-03 | BTC | DOWN | 0.66 | +0.87% ✗ | +2.32% ✗ | -0.46% ✓ | -0.49% ✓ | — | +3.62% ✗ |
| 2026-07-04 | BTC | UP | 0.64 | +0.73% ✓ | +0.33% ✓ | +0.17% ✓ | +2.96% ✓ | — | +2.72% ✓ |
| 2026-07-05 | BTC | UP | 0.64 | +0.70% ✓ | -2.03% ✗ | +0.91% ✓ | +1.83% ✓ | — | +1.98% ✓ |
| 2026-07-06 | BTC | UP | 0.64 | -1.09% ✗ | -1.25% ✗ | -0.30% ✗ | +0.51% ✓ | — | +1.27% ✓ |
| 2026-07-07 | BTC | UP | 0.64 | -1.64% ✗ | +1.31% ✓ | +0.73% ✓ | — | — | +2.38% ✓ |
| 2026-07-08 | BTC | UP | 0.71 | +1.50% ✓ | +2.48% ✓ | -0.03% ✗ | — | — | +4.09% ✓ |
| 2026-07-09 | BTC | UP | 0.71 | +1.48% ✓ | +0.89% ✓ | +2.79% ✓ | — | — | +2.55% ✓ |
| 2026-07-10 | BTC | UP | 0.71 | -0.51% ✗ | -2.94% ✗ | +0.91% ✓ | — | — | +1.06% ✓ |
| 2026-07-12 | BTC | UP | 0.71 | -2.38% ✗ | +1.50% ✓ | — | — | — | +1.64% ✓ |
| 2026-07-15 | BTC | UP | 0.72 | -0.61% ✗ | — | — | — | — | +0.14% ✓ |

## Baseline comparison (same dates, same horizons)

| Horizon | n | IBIS | Always-UP | Persistence | Anti-persistence |
|---|---|---|---|---|---|
| +1 bars | 10 | 4 | 5 | 7 | 3 |
| +3 bars | 9 | 5 | 6 | 3 | 6 |
| +5 bars | 8 | 6 | 5 | 5 | 3 |
| +10 bars | 4 | 4 | 3 | 3 | 1 |
| now | 10 | 9 | 10 | 6 | 4 |

A coin flip expects n/2. Persistence = yesterday's direction continues; anti-persistence = it reverses. If IBIS does not clearly beat EVERY baseline column at meaningful n, no edge claim survives — the cross-domain test showed that grading against a weaker-than-best trivial rule produces false positives.

## Statistical power and time-to-significance

| If true hit rate is | Resolved episodes needed | Have | ETA (observed cadence) | ETA (backtest-prior cadence) |
|---|---|---|---|---|
| perfect record (min possible) | 5 | 0 | 2026-09-01 | 2026-09-20 |
| 70% | 37 | 0 | 2027-02-08 | 2027-07-03 |
| 65% | 67 | 0 | 2027-07-08 | 2028-03-28 |
| 60% | 153 | 0 | 2028-09-10 | 2030-05-06 |

Cadence assumptions: observed 6.1 episodes/month
(measured over the live record so far — a tiny sample, treat as rough); backtest-prior 3.4 episodes/month for the currently-live assets (BTC, SOL). Activating GOLD+SPY would roughly double the prior cadence.

## Reliability (separate axis from edge)

**Uptime, trailing 7 days: 23.4%.** Since continuous operation began (2026-07-03): 38.8%. A gap is any >45min stretch without a completed cycle; the gap from the last cycle to now counts, so a live freeze shows up here within the day it happens.

Gaps in the last 7 days:
- 2026-07-12 21:32 → 2026-07-14 13:14 (39.7h)
- 2026-07-15 01:20 → 2026-07-18 18:15 (88.9h)

Per-asset live coverage:

| Asset | Cycles | Signals | First cycle | Last cycle |
|---|---|---|---|---|
| BTC | 301 | 264 | 2026-07-02T17:32 | 2026-07-15T01:20 |
| SOL | 98 | 0 | 2026-07-08T21:11 | 2026-07-15T01:20 |

Watchdog: run_ibis.py supervises the loop (heartbeat file, 45-minute timeout, logged restarts in data/watchdog.log). Freeze detection is now bounded to under an hour — previously a freeze went unnoticed for 37 hours (2026-07-07, root-caused: unbounded network call, since fixed).

## What this supports / does not support

Supports: the pipeline runs, captures, refuses stale data, and publishes pre-outcome receipts (github.com/aiempaths/ibis-ledger). Failures are logged and root-caused in the open.

Does not support: any claim of predictive skill or live profitability until the resolved-episode thresholds above are met. Directional accuracy alone will not suffice even then — closed-trade P&L is the final metric (the backtest's own SPY case shows hit rate and payoff can rank opposite ways).
