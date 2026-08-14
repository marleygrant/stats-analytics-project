# Decision Log

## Assignment 2: Dataset (2026-07-19)
- Dataset: E-commerce sales dataset from Kaggle
- Main variable of interest: **Revenue**, because it's a natural outcome that most of the
  dataset's categorical and continuous fields (product category, discount, delivery rating,
  etc.) could plausibly explain — giving us a wide range of angles to explore rather than a
  dataset that would run out of interesting questions quickly.
- Key decision: chose e-commerce over teammates' initial interests (healthcare, sports) because
  it best matched the assignment's requirement for a mix of categorical and continuous variables.

> *(Project note: starting with Assignment 3, the project switched to the EPL/Serie A player
> statistics dataset — see README for details. Entries below reflect that dataset.)*

## Assignment 3: Descriptive Stats (2026-07-26)
- Cleaning done: merged two source tables (standard stats + playing-time) on player ID and
  squad, keeping only players present in **both** — an inner join by design. That dropped the
  raw pool from 1,160 to **1,074 complete records**, so no missing-value imputation was needed
  in the final dataset.
- Outliers/messy data: flagged (not removed) two variables with extreme shape early —
  **plus/minus per 90** spans a 120-point range (-30 to +90) despite a near-zero mean, and
  **Red Cards** is almost entirely zeros (mean 0.10, max 2). Both were kept in the dataset as
  legitimate values (not data errors), but flagged for careful handling in the distribution
  work in Assignment 4.
- Most surprising pattern: Red Cards' near-total concentration at zero foreshadowed exactly
  the kind of non-normal shape that would matter for Assignment 4.

## Assignment 4: Probability (2026-07-26)
- Normal vs. empirical, and why: skewness/kurtosis diagnostics showed Minutes, % of Squad
  Minutes Played, and Yellow/Red Cards are all right-skewed. We tested this directly by
  comparing empirical (count-based) probabilities against `NORM.DIST`-based theoretical ones:
  - For **Minutes** (Pr(X > 1200)), the normal approximation (0.4814) matched the empirical
    count (517/1074 = 0.4814) almost exactly — normal assumption held.
  - For **Goals + Assists per 90** (Pr(X > 0.50)), empirical probability was **0.104** vs. a
    normal-distribution estimate of **0.735** — a 7x overestimate. We used the **empirical**
    approach for this variable instead of the theoretical one, since the normal assumption
    clearly didn't hold for a mostly-zero, right-skewed metric.

## Assignment 5: Inference (2026-08-09)
- What we tested, alpha, conclusion: ran one-sample right-tailed t-tests at **α = 0.05** on two
  variables.
  - Team Points Per Match: H₀: μ ≤ 1.25 vs. Hₐ: μ > 1.25 → t = 2.055, p = 0.0201 → rejected H₀.
  - % of Squad Minutes Played: H₀: μ ≤ 35 vs. Hₐ: μ > 35 → t = 2.485, p = 0.0066 → rejected H₀.
  - The 95% CI for Team Points Per Match, [1.252, 1.325], excludes 1.25 entirely — consistent
    with the test result.

## Assignment 6: Regression (2026-08-12)
- First predictor removed and why: **Minutes**, removed first — not for a high p-value, but
  because a correlation matrix showed Minutes and % of Squad Minutes Played were correlated at
  **0.9999995**, essentially the same variable measured two ways.
- Multicollinearity handling: kept % of Squad Minutes Played (already normalized across squads)
  and dropped Minutes to resolve the collinearity, then continued backward elimination on
  p-value alone: England (p = 0.579) → Pos_D (p = 0.399) → Yellow Cards (p = 0.228) →
  Pos_F (p = 0.200) → Goals + Assists per 90 (p = 0.060).
- Final model: % of Squad Minutes Played, plus/minus per90, Red Cards, and European — all
  significant at p < 0.05. R² = 0.126, Adjusted R² = 0.123 (essentially unchanged from the
  10-variable model's 0.125), confirming the removed variables were adding noise, not
  explanatory power. Strongest predictor: plus/minus per90 (t = 10.19, p < 0.001).
