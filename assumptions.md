# Monte Carlo Assumptions — Child Labor / Cost Arbitrage Floor

All values in $B USD (annualized). Every parameter traces to paper §4–§5
or the citations in `data_sources.md`. Run `python mc_simulation.py` to
reproduce bit-identical results.

---

## Simulation Parameters

| Parameter | Value | Justification |
|-----------|-------|---------------|
| Seed | 42 | Fixed for reproducibility |
| N draws | 100,000 | 4-decimal CI stability |
| Cross-channel correlation ρ | 0.3 | Shared macro drivers (GDP, population, regulation) |
| Private payoff Π | $39.5B/yr | Annual industry revenue — see `data_sources.md` |
| β_W median (result) | 21.83 | Confirmed by N=100,000 draws |
| ΔW median (result) | $862.2B/yr | Sum of channel medians (correlated) |

**Π = revenue, not profit.** SAPM Iron Law: βW = ΔW/Π where Π is annual
revenue. Using profit would inflate βW by 5–20× for low-margin industries.

---

## Channel Parameters

| Channel | Dist | Low | Mid | High | Description |
|---------|------|-----|-----|------|-------------|
| `C1_human_capital` | lognormal | $381B | $459B | $537B | Foregone education, lifetime earnings loss (160M children) |
| `C2_health` | lognormal | $28B | $45B | $62B | Physical injuries, chemical exposure, psychological trauma |
| `C3_intergenerational` | lognormal | $89B | $111.5B | $134B | Intergenerational poverty transmission |
| `C4_demographic` | lognormal | $97B | $156B | $215B | Demographic dividend foreclosure |
| `C5_supply_chain` | lognormal | $22B | $35B | $52B | Supply chain governance failure, audit theater |
| `C6_institutional` | lognormal | $35B | $51B | $75B | Structural impunity, enforcement deficit |


All ranges represent [P5, P95] of the channel-specific distribution as
calibrated from literature in paper §4.

---

## Impossibility Floor

The floor β_W ≥ 2.0 is the minimum ratio achievable while the industry operates.
This bounds the simulation from below: the theorem holds regardless of parameter values,
because even best-case scenarios exceed the floor.

In 100,000 draws: P(β_W < 2.0) = 0.0000%

## Sensitivity (VSL × Double-Counting Grid)

Central VSL (1.0×): no DC adj β_W = 21.71 | 20% DC adj = 17.37 | 40% DC adj = 13.03

See `mc_results.json` → `sensitivity_matrix` for full 5×5 grid.

## Distribution Robustness

The simulation uses a lognormal/normal mix calibrated to channel-specific
uncertainty structure. Results are robust: the central β_W changes by less
than ±0.3 under all-lognormal or all-normal configurations.

---

## Plausibility Checks (SAPM IL#28)

- **Annual flow**: All W_i are $/yr flows ✓
- **GDP bound**: ΔW = $862B = 0.8% of world GDP ($106T) ✓
- **β_W range**: 21.83 is within the [0.5, 100] plausible range ✓
- **P(β_W < 1)**: 0.0000% ✓
