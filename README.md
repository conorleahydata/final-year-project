# Predicting Stock Prices with the Fast Fourier Transform

BSc Financial Mathematics and Actuarial Science, University College Cork (MS4090 Final Year Project, 2023). Supervisor: Dr Spyridon Dendrinos.

## What this project does
Tests whether the Fast Fourier Transform (FFT) can predict the direction (up or down) of a stock's next closing price. The method:

1. Takes the previous N daily closing prices and computes the day-to-day changes.
2. Applies the FFT to find the dominant frequencies in those changes.
3. Picks the frequency cutoff (20 candidate thresholds, mean to mean + 2 standard deviations) that minimises RMSE.
4. Rebuilds the signal from those frequencies to forecast the next day(s).
5. Scores a prediction as a success if the predicted direction matches the real one, repeated over 100 random dates.

## Data
Adjusted daily closing prices from Yahoo Finance, 1 Jan 2018 to 31 Dec 2022:
- Stocks: Apple (AAPL), Amazon (AMZN), Tesla (TSLA)
- Crypto (USD): Bitcoin, Ethereum, Litecoin

The CSV files are not included. Download them from Yahoo Finance and update the file path in the notebook.

## Results (100 random test dates, 250 days of history, 1 day ahead)
| Asset | Direction accuracy |
|---|---|
| Apple | 69% |
| Amazon | 61% |
| Tesla | 56% |
| Bitcoin | 58% |
| Ethereum | 55% |
| Litecoin | 62% |

Other findings (Apple and Litecoin):
- **History length:** accuracy fell to about 50% with only 50 days of data, and 500 days gave no improvement over 250.
- **Forecast horizon:** accuracy dropped as the horizon grew, to about 50% at 10 days and 40-44% beyond.

## Limitations
- With only 100 trials per asset, the margin of error is roughly ±5 percentage points, so the weaker results (55-58%) can't be distinguished from chance.
- Only directional accuracy was measured, not profitability, transaction costs, or magnitude of error.
- Results are in-sample experiments on a single 5-year window, not a validated trading strategy.
- The function sometimes errors with 50-100 days of data.

## Possible extensions
Walk-forward backtesting, significance testing, comparison against simple baselines, and combining the FFT with other models.

## Files
- `final_year_project_master.ipynb`: code and plots
