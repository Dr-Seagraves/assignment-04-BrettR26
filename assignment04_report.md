# Assignment 04 Interpretation Memo

**Student Name:** Brett R
**Date:** February 11, 2026
**Assignment:** REIT Annual Returns and Predictors (Simple Linear Regression)

---

## 1. Regression Overview

You estimated **three** simple OLS regressions of REIT *annual* returns on different predictors:

| Model | Y Variable | X Variable | Interpretation Focus |
|-------|------------|------------|----------------------|
| 1 | ret (annual) | div12m_me | Dividend yield |
| 2 | ret (annual) | prime_rate | Interest rate sensitivity |
| 3 | ret (annual) | ffo_at_reit | FFO to assets (fundamental performance) |

For each model, summarize the key results in the sections below.

---

## 2. Coefficient Comparison (All Three Regressions)

**Model 1: ret ~ div12m_me**
- Intercept (β₀): 0.1082 (SE: 0.006, p-value: 0.000)
- Slope (β₁): −0.0687 (SE: 0.032, p-value: 0.035)
- R²: 0.0018 | N: 2,527

**Model 2: ret ~ prime_rate**
- Intercept (β₀): 0.1998 (SE: 0.016, p-value: 0.000)
- Slope (β₁): −0.0194 (SE: 0.003, p-value: 0.000)
- R²: 0.0164 | N: 2,527

**Model 3: ret ~ ffo_at_reit**
- Intercept (β₀): 0.0973 (SE: 0.009, p-value: 0.000)
- Slope (β₁): 0.5770 (SE: 0.567, p-value: 0.309)
- R²: 0.0004 | N: 2,518

*Note: Model 3 has 9 fewer observations due to missing ffo_at_reit values; statsmodels dropped those rows.*

---

## 3. Slope Interpretation (Economic Units)

**Dividend Yield (div12m_me):**
- A 1 percentage point increase in dividend yield (12-month dividends / market equity) is associated with a −0.0687 (≈ −6.87 percentage point) change in annual return.
- REITs with higher dividend yields in the prior year earn significantly *lower* returns in the current year. This negative relationship challenges the intuition that high dividend-paying stocks should offer higher total returns. One explanation: the market may be pricing in slower growth for high-dividend REITs, or dividend yield may proxy for a market correction (high yield because price fell). We cannot conclude causality from this simple regression.

**Prime Loan Rate (prime_rate):**
- A 1 percentage point increase in the year-end prime rate is associated with a −0.0194 (≈ −1.94 percentage point) change in annual return.
- REIT returns are statistically significantly sensitive to interest rates in a negative direction. This aligns with economic theory: higher borrowing costs reduce REIT profitability and make fixed-income assets more attractive, depressing equity valuations. A 100 basis point rise in the prime rate predicts roughly a 1.94 percentage point drop in annual REIT returns.

**FFO to Assets (ffo_at_reit):**
- A 1 unit increase in FFO/Assets (fundamental performance) is associated with a 0.5770 change in annual return.
- While the slope is positive (suggesting more profitable REITs earn higher returns), this relationship is *not* statistically significant at the 5% level (p = 0.309). The lack of significance and very tight confidence interval [−0.536, 1.690] suggests FFO/Assets alone has limited predictive power. Profitability matters less than we might expect when examined in isolation.

---

## 4. Statistical Significance

For each slope, at the 5% significance level:
- **div12m_me:** Significant (p = 0.035) — Higher dividend yield is significantly associated with lower future returns.
- **prime_rate:** Significant (p < 0.001) — The prime rate has a strong, statistically significant negative relationship with REIT returns.
- **ffo_at_reit:** Not significant (p = 0.309) — Profitability (FFO/Assets) shows no statistically significant linear relationship with annual returns in this univariate model.

**Which predictor has the strongest statistical evidence of a relationship with annual returns?** The prime loan rate has the strongest evidence, with a p-value near zero and the largest t-statistic (−6.487). Interest rate risk is the most robustly significant driver of REIT returns among these three predictors.

---

## 5. Model Fit (R-squared)

Compare R² across the three models:
- **div12m_me:** R² = 0.0018 (explains 0.18% of variation)
- **prime_rate:** R² = 0.0164 (explains 1.64% of variation)  
- **ffo_at_reit:** R² = 0.0004 (explains 0.04% of variation)

The prime rate explains the most variation in returns, but even it accounts for less than 2% of the variance. All three models have very low R² values, indicating that **most of REIT annual return variation is driven by factors not captured in these univariate models**—possibly macroeconomic shocks, sector-specific performance, management quality, property location, leverage, or idiosyncratic firm events. Simple one-variable regressions are insufficient to predict REIT returns; multiple factors must be considered simultaneously.

---

## 6. Omitted Variables

By using only one predictor at a time, we might be omitting:
- **Market conditions / broad equity risk:** REIT returns move with the broader equity market, which may be correlated with interest rates. If market conditions also affect dividend yields, omitting market risk could bias the dividend yield coefficient downward (spurious negative relationship).
- **REIT leverage and balance sheet structure:** Highly leveraged REITs are more sensitive to interest rates but may differ systematically in dividend yield or profitability. Omitting leverage could confound the relationship between our X variables and returns.
- **Property sector and geographic composition:** Different REIT types (residential, industrial, retail, office) have different return profiles and different sensitivities to interest rates and fundamentals. Omitting sector indicators masks heterogeneous effects.

**Potential bias:** The prime rate coefficient (−0.0194) is likely biased in magnitude because it omits market-wide factors that co-move with rates. The dividend yield slope (−0.0687) might be biased downward if dividend yield is mechanically high after price declines (mean reversion not captured by this model).

---

## 7. Summary and Next Steps

**Key Takeaway:**
Interest rates emerge as the most significant single predictor of REIT annual returns: each 1% rise in the prime rate correlates with a ~1.94% decline in returns, and this relationship is highly statistically significant. Dividend yield also shows a significant negative relationship with forward returns, suggesting either a value-trapping effect or opportunistic pricing. Conversely, profitability (FFO/Assets) has no meaningful univariate predictive power. Overall, REIT returns are complex and driven by multiple factors; none of these simple models account for more than 2% of return variation, highlighting the importance of multivariate analysis and consideration of macroeconomic, financial, and sector-specific factors.

**What we would do next:**
- Extend to multiple regression (include two or more predictors simultaneously) to isolate effects and reduce omitted variable bias
- Test for heteroskedasticity and other OLS assumption violations (normality of residuals appears violated given skewness/kurtosis in the regression outputs)
- Examine whether relationships vary by time period, REIT sector, or leverage quartile (interaction effects and subgroup analysis)
- Add controls for market-wide returns and volatility to isolate REIT-specific effects
- Consider lag effects: do prior-year fundamentals predict current-year returns better than contemporaneous measures?

---

## Reproducibility Checklist
- [x] Script runs end-to-end without errors
- [x] Regression output saved to `Results/regression_div12m_me.txt`, `regression_prime_rate.txt`, `regression_ffo_at_reit.txt`
- [x] Scatter plots saved to `Results/scatter_div12m_me.png`, `scatter_prime_rate.png`, `scatter_ffo_at_reit.png`
- [x] Report accurately reflects regression results
- [x] All interpretations are in economic units (not just statistical jargon)
