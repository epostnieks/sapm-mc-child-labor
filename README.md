# SAPM Monte Carlo — Child Labor / Cost Arbitrage Floor

**Public replication repository for quantitative results in:**

> Postnieks, E. (2026). *Child Labor (Cost Arbitrage Floor).* SAPM Working Paper. SSRN.

This repository provides everything needed to independently reproduce, audit,
and extend the Monte Carlo simulation underlying the paper's core results.
The paper is available on SSRN.

---

## Results (N = 100,000 draws, seed = 42)

| Statistic | Value |
|-----------|-------|
| **β_W median** | **21.83** |
| β_W mean | 21.93 |
| β_W std | 2.05 |
| **90% CI** | **[18.8, 25.5]** |
| 99% CI | [17.6, 27.2] |
| P(β_W < 1) | 0.0000% |
| **ΔW median** | **$862.2B/yr** |
| Π (revenue) | $39.5B/yr |

**β_W = 21.83** means the child labor industry destroys **$21.83 in system
welfare for every $1.00 in revenue** — across 6 channels and 100,000 Monte Carlo draws.

**Classification**: Class 2 — Intractability

---

## What Is β_W?

```
β_W = ΔW / Π
```

- **ΔW** = total annualized welfare destruction ($B/yr) across all channels
- **Π** = annual industry **revenue** ($B/yr) — not profit

β_W > 1: industry destroys more welfare than it captures in revenue.
β_W > 3: Strong Intractability threshold — reform requires structural replacement.

---

## Quick Start

```bash
git clone https://github.com/epostnieks/sapm-mc-child-labor.git
cd sapm-mc-child-labor
pip install numpy scipy
python mc_simulation.py
```

Expected output: `β_W median : 21.83` and `ΔW median : $862.2B/yr`

---

## Welfare Channels

| Channel | Median ($B/yr) | 90% CI | Distribution |
|---------|---------------|--------|--------------|
| C1_human_capital | $458.8B | [$391.9B, $536.7B] | Lognormal |
| C2_health | $45.0B | [$32.6B, $62.1B] | Lognormal |
| C3_intergenerational | $111.5B | [$92.8B, $134.0B] | Lognormal |
| C4_demographic | $156.1B | [$113.1B, $214.8B] | Lognormal |
| C5_supply_chain | $34.9B | [$23.6B, $51.8B] | Lognormal |
| C6_institutional | $51.0B | [$34.7B, $75.0B] | Lognormal |
| **Total ΔW** | **$862.2B** | **[$740.9B, $1,006.0B]** | Correlated (ρ=0.3) |

---

## Impossibility Floor

The floor β_W ≥ 2.0 cannot be breached by any policy while the
industry continues to operate. In 100,000 draws, only **0.0000%**
fall below this floor — confirming the structural constraint.

## Repository Contents

| File | Description |
|------|-------------|
| `mc_simulation.py` | Self-contained simulation — no private pipeline imports |
| `mc_results.json` | Pre-run results (100K draws, seed=42) — matches paper |
| `mc_histogram.json` | Binned β_W distribution (80 bins) for companion chart |
| `assumptions.md` | Every parameter: value, derivation, source |
| `data_sources.md` | Full citation list for all empirical inputs |

---

## Replication Notes

Results are seeded and deterministic. Tested with:
```
numpy==1.26.4  scipy==1.12.0  Python 3.11.9
```

The `median` and `ci_90` (to 1 decimal) match exactly across compatible versions.

---

## License

CC BY 4.0. Cite as:

> Postnieks, E. (2026). *SAPM Monte Carlo — Child Labor (Cost Arbitrage Floor)*.
> GitHub: epostnieks/sapm-mc-child-labor.
> https://github.com/epostnieks/sapm-mc-child-labor
