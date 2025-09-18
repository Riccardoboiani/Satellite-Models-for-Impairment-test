# Econometric Analysis of Default Rates

This repository contains the interpretation of econometric results for modeling default rates using macroeconomic variables and forward-looking IFRS 9 PD estimation.

---

## Stationarity Tests (ADF)

- **Default rate**: Non-stationary in levels, stationary after first differencing → integrated of order 1, I(1).
- **GDP, Unemployment, Inflation**: Stationary in levels → integrated of order 0, I(0).

> The mixed integration order (I(0) and I(1)) makes the ARDL framework particularly appropriate, as it can handle both types of variables without requiring full differencing.

---

## OLS Regression

**Coefficient signs**:

- GDP: negative → growth reduces defaults.
- Unemployment: positive → higher unemployment increases defaults.
- Inflation: negative but not statistically significant.

**Diagnostics**:

- Low explanatory power (R² ~ 0.30)
- Residuals non-stationary and autocorrelated  
  - Durbin-Watson = 0.40  
  - Breusch-Godfrey p < 0.01
- Heteroskedasticity detected (White test p < 0.01)

**Conclusion**: OLS is a weak specification, unable to properly capture default rate dynamics.

---

## ARDL Model

**Specification**: ARDL(1,0,0)

**Advantages over OLS**:

- Residuals free from autocorrelation  
  - Durbin-Watson ~ 1.76  
  - Ljung-Box p > 0.3
- No heteroskedasticity (White test p = 0.46)
- Significant long-term equilibrium relationship confirmed by Bound Test (F-statistic >> critical values)

**Coefficient interpretation**:

- GDP: negative impact (short- and long-term)
- Unemployment: positive and significant
- Default rate autoregression: strong persistence (lag coefficient ~ 0.95)
- Error Correction Term (ECT): -0.065, significant → default rate gradually returns to long-term equilibrium after a shock

**Conclusion**: ARDL captures both short-term adjustments and long-term equilibrium relationships, making it robust for IFRS 9 forward-looking PD modeling.

---

## Granger Causality Tests

- **GDP → Default rate**: no short-term causality
- **Unemployment → Default rate**: causality at lag 3 (p < 0.05)
- **Inflation → Default rate**: no significant causality

> Interpretation: Unemployment shocks tend to anticipate changes in default rates after a delay, confirming their predictive role for credit risk.

---

## Key Takeaways

1. OLS confirms theoretical relationships but suffers from non-stationary residuals, autocorrelation, and low explanatory power.
2. ARDL resolves these issues, demonstrating cointegration and providing a valid framework for forward-looking PD estimation.
3. Unemployment is the most reliable predictor of default rates in the medium term.
4. The Error Correction Mechanism ensures consistency between short-term shocks and long-term equilibrium.
