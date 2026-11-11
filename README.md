# Who leaves, and when? Retention among HR professionals

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/adinuansah/time-to-attrition/blob/main/01_time_to_attrition.ipynb)

**Methods:** Kaplan-Meier survival curves, log-rank tests, Cox proportional hazards model, time-split analysis
**Tools:** Python, pandas, lifelines, matplotlib, Google Colab

## The question

Most attrition reports tell you *who* left. I wanted to know *when* people leave, because that decides when a manager should step in. So instead of a yes/no prediction model, I used survival analysis, which looks at how risk changes over someone's time at a company.

## The data

1,116 employees, mostly HR professionals across 16 industries. 560 of them left during the observation period. It's a public dataset by Edward Babushkin, available on [Kaggle](https://www.kaggle.com/datasets/aman2114/turnover-survival-analysis) under a CC0 license.

Before analyzing anything, I made a few cleaning calls:
- I removed 13 rows that were exact duplicates on all 16 fields, including five personality scores. Two different people matching on everything is very unlikely, so I treated them as double entries.
- The tenure column (`stag`) isn't labeled with a unit. The longest tenure is 179, which only makes sense as months (about 15 years), so I treated it as months.
- I fixed a few label errors (a stray space, a broken character in "Finance") and grouped industries with fewer than 30 people into "Other", so tiny groups wouldn't produce unreliable estimates.

## What I found

**Most people who leave do it in months 6 to 24.** 94% are still there at six months, 70% at two years, and 61% at three. After year two, the pace of exits slows noticeably.

**Partly undeclared ("grey") pay is the clearest warning sign.** People paid that way had 65% higher risk of leaving, even after accounting for industry, role, age and the rest. Most of that extra risk shows up in the first two years.

**People hired through friends were less than half as likely to leave in their first two years.** I expected that. What I didn't expect was how completely it wore off: by year three they looked like everyone else. Referral hires showed the same pattern.

**People the employer approached through job sites went the other way.** They looked fairly average early on, then left about 50% faster after year two. My guess is that someone who was approached once tends to get approached again, but this data can't confirm that.

**Coaching didn't make a difference here,** whether it came from a manager or a dedicated coach. That doesn't mean coaching is useless. The people who got a dedicated coach may have been the ones already seen as risky, which would hide any benefit. Testing that properly needs a different design, which is my next project.

## What I'd recommend

1. Put retention effort into months 6 to 24, not just onboarding. That's where most of the exits happen.
2. Keep hiring through referrals, but don't count on the effect lasting. Around months 18 to 24 is a good time for a real career conversation.
3. For people you sourced directly, plan a check-in before the two-year mark, when their risk starts climbing.
4. Don't expand coaching just to improve retention. Test whether it works first.

## What I can't say

I can't say grey pay *causes* people to leave. Companies that pay partly off the books are probably different in other ways too: smaller, less stable, maybe worse managed. What I can say is that it's the clearest warning sign in this data.

A few other limits worth knowing:
- Two out of three people in this data work in HR, so I wouldn't assume the same patterns hold for engineers or sales teams.
- I tested 32 factors, so one or two "significant" results could be chance. I've leaned on the large, consistent effects and treated the borderline ones as things to watch.
- Two recruitment channel codes (`rabrecNErab`, `recNErab`) aren't explained in the source, so I haven't interpreted them.

## Files

| File | What's in it |
|---|---|
| `01_time_to_attrition.ipynb` | The full analysis, from data checks to the final model |
| `turnover.csv` | The source data |

To run it, click the "Open in Colab" badge, then Runtime → Run all.
