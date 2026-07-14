# IBIS Evidence Report — 2026-07-14 13:14

Auto-generated from the live decision database, daily CSVs, and
current quotes. Regenerates daily from the live loop, or on demand:
`python src\evidence.py`. History of these snapshots accumulates in
`data/evidence_history.csv`. The backtest contributes no numbers here.

## Headline verdict (computed, not editorial)

**No trading-edge claim is possible: 2 independent episode(s) exist and 0 have resolved at their hold horizon.**

Signal-days: 9. Independent episodes: 2. Resolved: 0. These are different numbers and only the resolved-episode count is a sample size.

## Plain-Language Verdict (LLM narration of the numbers above)

_ManifoldAuditor narration, generated 2026-07-14T13:14:51. The computed numbers nearby are the source of truth; this text only describes them._

No trading-edge claim is possible because there are 0 resolved episodes at their hold horizon, which is below the power threshold for a perfect record (5 episodes) and all other thresholds. The exact numbers are: 0 resolved episodes out of an unknown total, with no binomial p-value available to compare against a 50% baseline.

## Episodes

| Asset | Dir | Started | Signal-days | Hold | Status |
|---|---|---|---|---|---|
| BTC | DOWN | 2026-07-03 | 1 | 20 | open (+3.27% so far, resolves +20 bars) |
| BTC | UP | 2026-07-04 | 8 | 20 | open (+2.38% so far, resolves +20 bars) |

## Signal-day horizon scoring

P0 = signal-date daily close (fallback: detection price). Live detections evaluate a provisional intraday bar; at small n this convention can flip individual marks — stated, not hidden.

| Date | Asset | Dir | Conf | +1b | +3b | +5b | +10b | +20b | Now |
|---|---|---|---|---|---|---|---|---|---|
| 2026-07-03 | BTC | DOWN | 0.66 | +0.87% ✗ | +2.32% ✗ | -0.46% ✓ | -0.49% ✓ | — | +3.27% ✗ |
| 2026-07-04 | BTC | UP | 0.64 | +0.73% ✓ | +0.33% ✓ | +0.17% ✓ | +1.10% ✓ | — | +2.38% ✓ |
| 2026-07-05 | BTC | UP | 0.64 | +0.70% ✓ | -2.03% ✗ | +0.91% ✓ | — | — | +1.64% ✓ |
| 2026-07-06 | BTC | UP | 0.64 | -1.09% ✗ | -1.25% ✗ | -0.30% ✗ | — | — | +0.93% ✓ |
| 2026-07-07 | BTC | UP | 0.64 | -1.64% ✗ | +1.31% ✓ | +0.73% ✓ | — | — | +2.04% ✓ |
| 2026-07-08 | BTC | UP | 0.71 | +1.50% ✓ | +2.48% ✓ | -0.03% ✗ | — | — | +3.74% ✓ |
| 2026-07-09 | BTC | UP | 0.71 | +1.48% ✓ | +0.89% ✓ | +0.93% ✓ | — | — | +2.21% ✓ |
| 2026-07-10 | BTC | UP | 0.71 | -0.51% ✗ | -2.94% ✗ | — | — | — | +0.72% ✓ |
| 2026-07-12 | BTC | UP | 0.71 | -2.38% ✗ | — | — | — | — | +1.30% ✓ |

## Baseline comparison (same dates, same horizons)

| Horizon | n | IBIS | Always-UP | Persistence | Anti-persistence |
|---|---|---|---|---|---|
| +1 bars | 9 | 4 | 5 | 6 | 3 |
| +3 bars | 8 | 4 | 5 | 3 | 5 |
| +5 bars | 7 | 5 | 4 | 4 | 3 |
| +10 bars | 2 | 2 | 1 | 1 | 1 |
| now | 9 | 8 | 9 | 6 | 3 |

A coin flip expects n/2. Persistence = yesterday's direction continues; anti-persistence = it reverses. If IBIS does not clearly beat EVERY baseline column at meaningful n, no edge claim survives — the cross-domain test showed that grading against a weaker-than-best trivial rule produces false positives.

## Statistical power and time-to-significance

| If true hit rate is | Resolved episodes needed | Have | ETA (observed cadence) | ETA (backtest-prior cadence) |
|---|---|---|---|---|
| perfect record (min possible) | 5 | 0 | 2026-08-30 | 2026-09-16 |
| 70% | 37 | 0 | 2027-02-22 | 2027-06-29 |
| 65% | 67 | 0 | 2027-08-06 | 2028-03-24 |
| 60% | 153 | 0 | 2028-11-21 | 2030-05-02 |

Cadence assumptions: observed 5.5 episodes/month
(measured over the live record so far — a tiny sample, treat as rough); backtest-prior 3.4 episodes/month for the currently-live assets (BTC, SOL). Activating GOLD+SPY would roughly double the prior cadence.

## Reliability (separate axis from edge)

**Uptime, trailing 7 days: 42.9%.** Since continuous operation began (2026-07-03): 49.1%. A gap is any >45min stretch without a completed cycle; the gap from the last cycle to now counts, so a live freeze shows up here within the day it happens.

Gaps in the last 7 days:
- 2026-07-08 14:00 → 2026-07-08 20:35 (6.6h)
- 2026-07-09 14:31 → 2026-07-09 18:55 (4.4h)
- 2026-07-10 19:45 → 2026-07-12 16:55 (45.2h)
- 2026-07-12 21:32 → 2026-07-14 13:14 (39.7h)

Per-asset live coverage:

| Asset | Cycles | Signals | First cycle | Last cycle |
|---|---|---|---|---|
| BTC | 272 | 261 | 2026-07-02T17:32 | 2026-07-14T13:14 |
| SOL | 69 | 0 | 2026-07-08T21:11 | 2026-07-14T13:14 |

Watchdog: run_ibis.py supervises the loop (heartbeat file, 45-minute timeout, logged restarts in data/watchdog.log). Freeze detection is now bounded to under an hour — previously a freeze went unnoticed for 37 hours (2026-07-07, root-caused: unbounded network call, since fixed).

## What this supports / does not support

Supports: the pipeline runs, captures, refuses stale data, and publishes pre-outcome receipts (github.com/aiempaths/ibis-ledger). Failures are logged and root-caused in the open.

Does not support: any claim of predictive skill or live profitability until the resolved-episode thresholds above are met. Directional accuracy alone will not suffice even then — closed-trade P&L is the final metric (the backtest's own SPY case shows hit rate and payoff can rank opposite ways).
