## Satellite Model for IFRS 9 Impairment
In the dataset, "Tasso Default" means "Default Rate". Apologies for the legacy; I should have updated all the code, otherwise it wouldn’t work properly. The dafault rate was obtained from the Bank of Italy dataset regarding the No financial firms.

### Context and Motivation

The purpose of this project is to provide a methodological framework for the development of a **satellite model** designed to estimate the **Probability of Default (PD)** under a **forward-looking approach**, in line with the requirements of the **IFRS 9 accounting standard**.

IFRS 9 explicitly requires financial institutions to incorporate expectations about future macroeconomic conditions into credit risk parameters. This implies that models cannot rely solely on historical default rates but must also integrate **macroeconomic forecasts** to ensure that estimates of **lifetime PD** remain consistent with the expected evolution of the economic environment.

### Why a Satellite Model?

Credit risk is significantly influenced by the dynamics of the broader economy. Key macroeconomic drivers such as:

* **Gross Domestic Product (GDP)** – negatively correlated with default rates.
* **Unemployment rate** – positively correlated with default rates.
* **Inflation rate** – potentially non-linear effects, depending on the economic context.

These relationships are well documented in the academic and regulatory literature. A satellite model allows us to explicitly capture these dependencies and translate macroeconomic scenarios into credit risk parameters. To fully meet the regulatory requirements mentioned above, the analysis presented is based on macroeconomic data expressed as quarter-over-quarter percentage changes. This methodological choice allows for greater informational granularity while maintaining a reasonably limited time horizon. This ensures, on one hand, the robustness of the estimates and, on the other, alignment with market best practices.


### Choice of Econometric Framework

A traditional static regression (e.g., Ordinary Least Squares, OLS) provides a first insight into the relationship between default rates and macroeconomic variables. However, such approaches are limited:

* They explain only a small portion of the variability in default rates.
* They cannot capture the **dynamic interactions** and **lagged effects** of macroeconomic shocks.

To overcome these limitations, the model relies on an **AutoRegressive Distributed Lag (ARDL)** framework.

#### Why ARDL?

The ARDL methodology offers several advantages:

* It distinguishes **short-term dynamics** from **long-term equilibrium relationships**.
* It is applicable even when time series are not fully stationary, as long as they are integrated of order zero or one (I(0) or I(1)).
* It allows for the presence of **autoregressive components** (past default rates) and **distributed lags** (past values of macroeconomic variables).
* It supports the detection of **cointegration relationships**, ensuring that the model reflects an economically meaningful long-term equilibrium.

This makes ARDL particularly well suited for credit risk modeling under IFRS 9, where both short-term volatility and long-term structural dependencies must be taken into account.

### Key Features of the Model

* Integration of **macroeconomic forecasts** (GDP, unemployment, inflation).
* Robust econometric framework that balances explanatory power with interpretability.
* Compliance with **IFRS 9 forward-looking requirements**.
* Ability to translate **macroeconomic scenarios** into **lifetime PD estimates**.

### Intended Use

This model is not intended to produce point predictions of default rates, but rather to serve as a **framework** for scenario analysis and impairment testing. It can be adapted and extended to specific portfolios, asset classes, or jurisdictions by calibrating the macroeconomic variables and default data accordingly.
