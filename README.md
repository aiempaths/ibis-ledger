# IBIS public ledger

A timestamped public record of every signal and trade produced by IBIS, a
private quantitative trading system. Entries are pushed here automatically
when they occur — **before their outcomes are known** — so the record can be
watched forming in real time rather than assembled after the fact.

## Not investment advice

Nothing in this repository is investment, financial, trading, or legal
advice, or an offer or solicitation of any kind. It is a research record
of an experimental system trading a simulated (paper) account. Do not
make investment decisions based on it. If you do anything with these
records, you do so entirely at your own risk.

## What's here

- **[signals.md](signals.md)** — every signal-day the system has computed:
  direction, confidence, price at first detection.
- **[account.md](account.md)** — the paper account: open positions with
  their exit rules stated up front (max hold, target, stop), and every
  closed trade with its outcome.
- **[EVIDENCE.md](EVIDENCE.md)** — the system's auto-generated
  self-grading report: independent-episode counts, resolution status,
  baseline comparisons, statistical power thresholds, and uptime. Its
  verdict is computed from the data, not written by a person.
- **[notes/cross-domain-test.md](notes/cross-domain-test.md)** — a
  documented negative result from testing the prediction core on
  non-financial data, including the false positive the grading system
  caught.

## What this record claims

- Each entry was published at the git timestamp shown in the commit
  history, which is recorded by GitHub, not by us.
- Positions are opened with their exit rules declared in advance and are
  closed only by those rules (stop, breakeven lock, or time expiry) — never
  by discretion.
- The record includes everything: losing trades and expired signals stay.

## What this record does not claim

- **No real money.** This is a paper account with simulated fills at
  observed prices. Slippage and liquidity in live execution would differ.
- **No proven edge.** The system's backtest results are in-sample by
  definition; this ledger exists because those numbers shouldn't be
  trusted until an out-of-sample record accumulates. That takes months.
  As of the first publication there are **zero closed trades**.
- **Not literally immutable.** Git history can in principle be rewritten
  by the repo owner (force-pushes are disabled, but ownership is
  ownership). What the ledger offers is third-party timestamps and
  tamper-evidence: anyone watching the repo would see a rewrite.
- **No methodology.** How signals are generated stays private. This
  record is only about whether the calls, made in advance, are any good.

## Provenance note

The repo went live on 2026-07-06. The signal rows and the open position
dated before that were backfilled from the system's local log at first
publication — their detection timestamps are as recorded locally, but
their *publication* timestamp is the first commit. Everything after
2026-07-06 is published as it happens. The one open position's outcome
(BTC short, max hold through 2026-07-23) was unknown at publication time.
