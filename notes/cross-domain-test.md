# A negative result: the prediction core on non-financial data

*2026-07-09. Method details that would reveal tuned parameters are
omitted; everything else is stated as measured.*

We tested whether the system's prediction core — pattern matching of
recent trajectory shapes against historically resolved analogs, the same
engine behind the trading signals — shows any skill on a non-financial
series: one year of real hourly request volume to en.wikipedia.org
(public Wikimedia API, 8,953 hourly points). The engine ran with its
financial defaults carried over as-is, no tuning. Signals were generated
causally (archive warmed on the first half of the data, predictions made
bar-by-bar on the second half), then graded by the same machinery that
grades the trading system: independent-episode deduplication, resolution
at a fixed horizon, binomial testing.

## The result, plainly

**No skill above naive baselines was demonstrated.** The engine resolved
345 independent episodes and called the direction correctly 71.6% of the
time — a rate that, tested against a coin flip, looks spectacular
(p ≈ 0). It is not. The series has a strong 24-hour cycle, and trivial
rules that merely exploit that cycle score as well or better on the
exact same episodes:

| Predictor | Hit rate (n = 345) |
|---|---|
| "Same direction as this window yesterday" | **92.5%** |
| "Reverse of the last move" | 73.0% |
| **The prediction engine** | **71.6%** |
| Coin flip (expected) | 50% |
| "Continuation of the last move" | 27.0% |

The engine's 71.6% is consistent with it having partially rediscovered
the daily cycle — and a simple lookup of yesterday's pattern beats it
decisively.

## Why we're publishing a failure

Two reasons. First, the record should contain what the system cannot do,
not only what it might. Second — and this is the part we think is worth
reading — the test nearly produced a **false positive**. The originally
specified baseline ("continuation of the last move") happened to be
anti-predictive on this cyclical series, scoring 27%. Graded against
that baseline alone, a 71.6% hit rate with p ≈ 0 would have looked like
a discovery. The grading process caught this by adding the trivial rules
the data's structure demanded, and the "discovery" evaporated.

The lesson transfers directly to the trading records in this repository:
**a hit rate only means something relative to the strongest trivial rule
available, and p-values against weak baselines are marketing, not
evidence.** We are applying that standard to our own trading results —
including the ones that haven't resolved yet.

## What this does and does not mean

- It does **not** prove the core is worthless — one series, one domain,
  untuned, with heavy seasonality the approach wasn't given the means to
  subtract out.
- It does **not** validate the trading system in any way.
- It **does** demonstrate, with a real example rather than a design
  claim, that the grading machinery attached to this project rejects
  impressive-looking numbers when a dumb rule explains them.
