# FIFA World Cup 2026: Prescriptive Analytics

Group assignment report for IB9190: Advanced Analytics. Three sequential
optimisation models for the 2026 FIFA World Cup (Canada, Mexico, USA).

## Models

### 1. Group Formation
Assigns 48 qualified nations to 12 balanced groups by **maximising the
minimum group FIFA-points total** (Chebyshev objective).

- 48 binary variables × 12 groups
- Constraints: one team per pot per group, UEFA cap (≤2 per group),
  non-UEFA confederations (≤1 per group)
- **Result:** Minimum group total raised from 6,141 → 6,337 points (+3.2%);
  standard deviation of group strengths reduced from 114.46 → 26.83

### 2. Group-Letter Assignment
Assigns each of the 12 groups to a letter (A–L) to **maximise the spread
of row-set popularity** across 16 stadium date-slots.

- 12×12 one-to-one assignment with Big-M selector mechanism
- Objective: maximise wmin + wmax (lower + upper row-set popularity)
- **Result:** wmin raised by 50.6% (5.308 → 7.995); objective value 24.923

### 3. Stadium Assignment
Assigns 16 row-sets to 16 stadiums to **maximise total popularity value**
(stadium capacity × row-set popularity).

- 16×16 Linear Assignment Problem (256 binary variables, 32 constraints)
- Solved to global optimality via GLPK through Pyomo
- **Result:** Total value 9,561,316 vs naive baseline 9,441,244 (+1.27%)

## Key Results

| Model | Metric | Baseline | Optimised |
|-------|--------|----------|-----------|
| Group Formation | Min group total (pts) | 6,141 | 6,337 |
| Group Formation | Std dev of group strengths | 114.46 | 26.83 |
| Letter Assignment | wmin (row-set popularity) | 5.308 | 7.995 |
| Letter Assignment | Objective value | — | 24.923 |
| Stadium Assignment | Total popularity value | 9,441,244 | 9,561,316 |

## Data Sources

- **Nations & FIFA Points:** FIFA (2026), INSIDEFIFA (2026)
- **Stadium capacities & schedule:** FIFA (2025, 2026a)
- **Spectator Index:** Ghoniem et al. (2017); IMF World Economic Outlook
  (2025); World Bank (2026)
- **Methodology:** Ghoniem, A. et al. (2017), *Journal of the Operational
  Research Society*, 68(10), pp. 1183–1194

## Spectator Index

Nations are scored 0–100 on expected overseas supporter share. Host nations
(USA, Mexico, Canada) are fixed at 100. For nations not in Qatar 2022, the
index is estimated as:
