# Who leaves, and when? Retention among HR professionals

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/adinuansah/time-to-attrition/blob/main/01_time_to_attrition.ipynb)

**Methods:** Kaplan-Meier survival curves, log-rank tests, Cox proportional hazards model, time-split analysis
**Tools:** Python, pandas, lifelines, matplotlib, Google Colab

## Question

Which hiring and employment factors predict when employees leave, and when should retention efforts happen?

## Data

1,116 employees, mostly HR professionals across 16 industries, with 560 observed exits. Public dataset by Edward Babushkin, from [Kaggle](https://www.kaggle.com/datasets/aman2114/turnover-survival-analysis) (CC0 license).

Cleaning decisions:
- Removed 13 exact duplicate rows (identical on all 16 fields), treated as double-entered records.
- Tenure (`stag`) is in months: the maximum is 179, which is about 15 years.
- Fixed label errors (leading spaces, an encoding error) and grouped industries with fewer than 30 people into "Other".

## Key findings

1. **The risk window is months 6–24.** Retention is 94% at 6 months, 70% at 24 months, and 61% at 36. Half of those who leave are gone by about 51 months.
2. **Partly undeclared ("grey") pay is the strongest warning sign.** It carries 65% higher risk of leaving after controlling for other factors, concentrated in the first two years.
3. **Hires through friends and referrals stay longer, but only early on.** Their risk in the first 24 months is less than half the baseline, and the advantage disappears after year two.
4. **Employer-sourced hires become riskier over time:** about 50% higher risk after year two.
5. **Coaching type showed no measurable effect on retention.**

## Recommendations

1. Focus retention effort on months 6–24, not only onboarding.
2. Use referral hiring for early retention, and plan structured career conversations around months 18–24, when that advantage fades.
3. Add a retention check-in at 18–24 months for employer-sourced hires.
4. Don't expand coaching on retention grounds alone. Evaluate it with a proper comparison design first.

## Confidence and limitations

- These are associations, not proven causes. Grey pay may reflect wider employer instability.
- The sample is mostly HR professionals, so results may not generalize to other roles.
- With 32 factors tested, borderline results should be treated as signals to monitor.
- Two recruitment channel codes (`rabrecNErab`, `recNErab`) are not fully documented in the source.

## Repository

| File | Contents |
|---|---|
| `01_time_to_attrition.ipynb` | Full analysis, from data checks to the final model |
| `turnover.csv` | Source data |

To run: click the "Open in Colab" badge, then Runtime → Run all.
