# M/M/1 Single-Server Queue Simulation

**IME 461 / 561 — Discrete Event Simulation**  
Bradley University · Department of Industrial & Manufacturing Engineering · Spring 2026

---

## Overview

This project verifies a Simio discrete-event simulation (DES) model of a single-server M/M/1 queuing system by comparing simulation outputs to closed-form M/M/1 queuing theory across three run lengths: **1 day**, **31 days**, and **90 days**.

The system context is a small pizza take-out store operating 24 hours a day, 7 days a week — representative of any single-attendant service point with Poisson arrivals and exponential service times.

🔗 **Portfolio page:** [View on GitHub Pages](https://your-username.github.io/mm1-queue-sim/)

---

## System Parameters

| Parameter | Value |
|-----------|-------|
| Queue model | M/M/1 / ∞ / ∞ |
| Arrival rate λ | 2 customers / min (Poisson) |
| Inter-arrival time | Exponential (mean = 0.5 min) |
| Service rate μ | 2.5 customers / min |
| Service time | Exponential (mean = 0.40 min) |
| Traffic intensity ρ | 0.80 (80%) |
| Number of servers | 1 |
| Queue discipline | FIFO |
| Queue capacity | Infinite |
| Simulation tool | Simio |

---

## M/M/1 Theoretical Benchmarks

| Metric | Formula | Value |
|--------|---------|-------|
| Utilisation U | ρ = λ/μ | **80.00%** |
| P(system empty) P₀ | 1 − ρ | **0.200** |
| Avg queue length Lq | ρ² / (1 − ρ) | **3.200 customers** |
| Avg no. in system L | Lq + ρ | **4.000 customers** |
| Avg queue wait Wq | Lq / λ | **1.600 min** |
| Avg system time W | Wq + 1/μ | **2.000 min** |

---

## Results Summary

| Metric | Theory | 1 Day | 31 Days | 90 Days |
|--------|--------|-------|---------|---------|
| Utilisation U | 80.00% | 79.87% (−0.2%) | 80.11% (+0.1%) | 79.99% (<0.1%) |
| L — avg in system | 4.000 | 3.596 (−10.1%) | 4.038 (+0.9%) | 3.940 (−1.5%) |
| Lq — avg queue length | 3.200 | 2.797 (−12.6%) | 3.237 (+1.2%) | 3.141 (−1.8%) |
| W — avg system time (min) | 2.000 | 1.810 (−9.5%) | 2.011 (+0.5%) | 1.966 (−1.7%) |
| Wq — avg queue time (min) | 1.600 | 1.407 (−12.1%) | 1.612 (+0.7%) | 1.567 (−2.1%) |
| Customers processed | — | 2,861 | 89,643 | 259,709 |

**Key finding:** The 1-day run undershoots theory by 10–13% due to warm-up transient bias (empty-start condition). Extending to 31 days reduces all errors to within 1.2% of theory. The 90-day run remains within 2.1% — residual variability is attributable to single-replication sampling noise.

---

## Repository Structure

```
mm1-queue-sim/
├── index.html                              # GitHub Pages portfolio site
├── README.md                               # This file
├── data/
│   ├── results_1day.csv                    # Simio output — 1 day run
│   ├── results_31days.xlsx                 # Simio output — 31 day run
│   └── results_90days.csv                  # Simio output — 90 day run
└── report/
    └── Single_Server_Queue_Verification_Report.docx
```

---

## How to Publish to GitHub Pages

1. Create a new repository on GitHub (e.g. `mm1-queue-sim`)
2. Push all files:
   ```bash
   git init
   git add .
   git commit -m "Initial commit — M/M/1 queue simulation"
   git branch -M main
   git remote add origin https://github.com/YOUR-USERNAME/mm1-queue-sim.git
   git push -u origin main
   ```
3. Go to **Settings → Pages → Source → Deploy from branch → main / (root)**
4. Your site will be live at `https://YOUR-USERNAME.github.io/mm1-queue-sim/`

> Update the portfolio page link in this README after your repo is live.

---

## Verification Notes

- All Simio time outputs are recorded in **hours** and converted to **minutes** (×60) for comparison with M/M/1 theory
- Little's Law check: L = λW holds for all runs (e.g. 31-day: 2.0 × 2.011 = 4.022 ≈ 4.038 ✓)
- No warm-up period was applied — future work should use Welch's method to identify and discard the transient phase
- Multiple replications with confidence intervals are recommended for more statistically rigorous estimates

---

## References

- Banks, J., Carson, J. S., Nelson, B. L., & Nicol, D. M. (2010). *Discrete-Event System Simulation* (5th ed.). Pearson.
- Gross, D. et al. (2008). *Fundamentals of Queueing Theory* (4th ed.). Wiley.
- Law, A. M. (2015). *Simulation Modeling and Analysis* (5th ed.). McGraw-Hill.
- Simio LLC. (2024). *Simio Reference Guide*. https://www.simio.com

---

*Bradley University · IME 461/561 · Spring 2026*
