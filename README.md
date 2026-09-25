# Short-Term Price and Volume Signals in Cross-Sectional Equity Markets

An independent quantitative research study investigating short-term price-reversal and price-volume signals in cross-sectional equity markets.

## Overview

This project investigates whether short-term price and trading-volume information can be used to construct systematic cross-sectional equity signals.

Two signal families are studied:

1. **Short-Term Price Reversal**
2. **Price-Volume Interaction**

Each signal is evaluated using 3-day, 5-day, and 10-day lookback periods to examine sensitivity to the chosen time horizon.

The research was conducted using the WorldQuant BRAIN simulation environment.

## Research Questions

The study investigates the following questions:

- Can recent price changes provide information about subsequent cross-sectional equity performance?
- Does incorporating trading-volume information change the characteristics of a price-based signal?
- How sensitive are the signals to the chosen lookback period?
- How consistent are the results across different calendar years?
- What limitations arise when interpreting historical quantitative simulations?

## Methodology

The simulations use the following configuration:

| Parameter | Setting |
|---|---|
| Region | USA |
| Instrument Type | Equity |
| Universe | TOP3000 |
| Delay | 1 |
| Neutralization | Subindustry |
| Decay | 6 |
| Truncation | 0.08 |
| Pasteurization | On |
| Unit Handling | Verify |
| NaN Handling | Off |
| Test Period | 1 year |
| Lookback | 256 |
| Language | Fast Expression |

## Alpha 1 — Short-Term Price Reversal

The first signal is defined as:

\[
\alpha_1(n) =
-\operatorname{rank}\left(\Delta P_n\right)
\]

where \(P\) represents closing price and \(n\) represents the lookback period.

### 3-day

```text
-rank(ts_delta(close, 3))

-rank(ts_delta(close, 5))

-rank(ts_delta(close, 10))

## Alpha 2 — Price-Volume Interaction

The second signal incorporates both price and trading volume:

$$ \alpha_2(n) = -\operatorname{rank}\left(\Delta P_n\right) \times \operatorname{rank}\left(\Delta V_n\right) $$

where \(P\) represents closing price and \(V\) represents trading volume.

3-day
-rank(ts_delta(close, 3)) * rank(ts_delta(volume, 3))
5-day
-rank(ts_delta(close, 5)) * rank(ts_delta(volume, 5))
10-day
-rank(ts_delta(close, 10)) * rank(ts_delta(volume, 10))
Results
Price-Reversal Signal
Lookback	Sharpe	Returns	Turnover	Drawdown
3 days	2.10	12.24%	44.79%	4.16%
5 days	1.60	9.22%	34.79%	4.51%
10 days	1.50	8.32%	22.17%	3.58%
Price-Volume Signal
Lookback	Sharpe	Returns	Turnover	Drawdown
3 days	1.93	9.43%	63.66%	2.28%
5 days	2.47	11.94%	51.12%	2.18%
10 days	2.11	9.86%	40.75%	2.20%
Key Observations

The experiments show positive aggregate simulated performance across the tested specifications, while performance varies across lookback periods and calendar years.

The price-reversal signal exhibited a relationship between shorter lookback periods and higher turnover.

The price-volume signal produced its highest aggregate Sharpe ratio using the 5-day specification, while the 10-day specification produced lower turnover.

Annual results also varied substantially, demonstrating the importance of evaluating quantitative signals across different market environments rather than relying only on aggregate statistics.

Limitations

This project is based on historical simulation and does not represent live investment performance.

Important limitations include:

Historical performance does not guarantee future performance.
Parameter selection can introduce research bias.
Simulated results may differ from live implementation.
Transaction costs and market impact can affect realized performance.
The analysis is limited to the specified USA equity universe and simulation configuration.
Further out-of-sample testing is required to assess robustness.
Research Paper

The complete research report is available in the paper/ directory.

Project Status

Independent research project — September 2026.

Disclaimer

This repository is for educational and research purposes only. It does not constitute investment advice or a recommendation to buy or sell any security.

The results presented are historical simulations and should not be interpreted as guaranteed future performance.

Author

Shraddha Sharma

Independent Researcher


---

## Your `alpha/` files

### `alpha/price_reversal.txt`

```text
# Short-Term Price Reversal

# 3-day
-rank(ts_delta(close, 3))

# 5-day
-rank(ts_delta(close, 5))

# 10-day
-rank(ts_delta(close, 10))
alpha/price_volume.txt
# Price-Volume Interaction

# 3-day
-rank(ts_delta(close, 3)) * rank(ts_delta(volume, 3))

# 5-day
-rank(ts_delta(close, 5)) * rank(ts_delta(volume, 5))

# 10-day
-rank(ts_delta(close, 10)) * rank(ts_delta(volume, 10))