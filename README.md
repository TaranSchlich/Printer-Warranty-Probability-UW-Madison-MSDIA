[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1XAJ6AIp02s1vX2872nOTvxOG0sc5ATfD?usp=sharing)

# Warranty Claim Probability Analysis (Personal Printers)
**Author:** Taran Schlichtmann  
**Date:** 09/21/2025  

*Discrete probability modeling using Poisson and Binomial distributions to estimate monthly warranty claim volumes and clogged nozzle incidents.*

---

## Overview
This project models expected warranty claim volumes for personal printers and estimates the frequency of clogged nozzle incidents using historical averages and event probabilities. It applies **Poisson** (events over time) and **Binomial** (successes in fixed trials) distributions to quantify risk and support service operations planning.

---

## Business Context
You work for a company that sells personal printers. Customers receive a **one-year warranty** on parts and service. When defects arise, the company pays for repairs—sometimes handled in-house, other times outsourced to a partner. Forecasting monthly claim volume and common issue types (e.g., clogged nozzles) helps plan **staffing, parts inventory, and vendor costs**.

---

## Methods
- **Poisson distribution** for monthly claim counts (e.g., probability of ≤200, ≥200, exactly 175 claims).
- **Binomial distribution** for clogged-nozzle share within a fixed set of claims (e.g., exactly 70 in 300; >80 in 300; 75–90 in 300).
- Uses **CDF** (cumulative probability) and **PMF** (exact probability) to answer operational questions.

---

## Key Results (from the notebook)
- ~97.1% chance of **200 or fewer** claims next month; ~2.9% chance of **200 or more**.
- ~3.0% chance of **exactly 175** claims next month.
- ~4.3% chance **exactly 70 of 300** claims are clogged-nozzle; ~23% chance **more than 80 of 300**; ~50.1% chance **between 75 and 90 of 300**.

> Adjust parameters to reflect your organization’s actual historical rates to tailor these probabilities.

---

## Project Structure
```
printer-warranty-probability-analysis/
├─ notebooks/
│  └─ warranty_probability.ipynb   # Colab notebook
├─ src/
│  └─ probability_models/
│     ├─ poisson_claims.py         # Poisson helpers
│     ├─ binomial_nozzles.py       # Binomial helpers
├─ tests/
│  ├─ test_poisson.py              # Unit tests
│  └─ test_binomial.py             # Unit tests
├─ requirements.txt                # Python dependencies
├─ README.md                       # Project documentation
```

---

## Quickstart
Clone the repo and install dependencies:
```bash
git clone https://github.com/TaranSchlich/printer-warranty-probability-analysis.git
cd printer-warranty-probability-analysis
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
```

Run your notebook locally or in Colab:
```bash
# Local (optional):
python -m pip install jupyterlab && jupyter lab
```

---

## Usage Example
```python
from scipy import stats

# Poisson: monthly claims (mean λ = 175)
monthly_claims = stats.poisson(175)
prob_le_200 = monthly_claims.cdf(200)        # P(X ≤ 200)
prob_ge_200 = 1 - monthly_claims.cdf(200)    # P(X ≥ 200)
prob_eq_175 = monthly_claims.pmf(175)        # P(X = 175)

# Binomial: clogged nozzles in next 300 claims (p = 0.25)
clogged = stats.binom(n=300, p=0.25)
prob_eq_70 = clogged.pmf(70)                 # exactly 70
prob_gt_80 = 1 - clogged.cdf(80)             # > 80
prob_75_to_90 = clogged.cdf(90) - clogged.cdf(74)  # include 75–90
```

---

## Requirements
- **Python:** 3.9+
- **Dependencies:**
  - `scipy` – probability distributions (stats)
  - `numpy` *(optional)* – numerical helpers
- Works in **local environment** or **Google Colab**

Example `requirements.txt`:
```txt
scipy>=1.10
numpy>=1.21
```

---

## Notes
- Parameters (λ for Poisson, p and n for Binomial) should reflect your latest operational data.
- Results demonstrate how **CDF** and **PMF** answer practical service questions.

---

## Disclaimer
This project is for **educational purposes** and **planning exploration**. Validate assumptions with your organization’s actual data before making operational decisions.

---

## License
This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.

