# Testing Gaussian VaR on the S&P 500

## Question
Does a 99% Gaussian Value at Risk underestimate large daily losses?

## Method
- Downloaded daily S&P 500 closing levels (2010-2025) from Yahoo Finance using yfinance
- Calculated daily returns, their mean and standard deviation
- Computed 99% VaR as 2.326 × standard deviation − mean
- Counted days with losses larger than the VaR
- Compared the returns with a normal distribution

## Results
- 99% VaR: 2.49%
- Expected breaches: about 40 of 4,023 days (1%)
- Actual breaches: 81 (2.01%)

The Gaussian VaR was breached about twice as often as expected.
The histogram also shows more extreme gains and losses than
the normal curve predicts.

## Limitations
- In-sample test: the same data was used to fit and test the model
- Volatility is assumed constant over the whole period
- Only one index, time period and confidence level were tested
- VaR does not measure how large losses are beyond the cutoff

## How to run
Install the libraries, then run `var_test.ipynb` from top to bottom:

`pip install yfinance pandas numpy matplotlib scipy ipykernel`

## Part 2: Monthly VaR
Each month's VaR used the previous month's mean and standard
deviation. Both models were compared on the same 4,005 days.

- Fixed VaR breach rate: 2.02%
- Monthly VaR breaches: 155 (3.87%)
- Target: 1%

Monthly updating did not achieve the target. The fixed model was
estimated using the full period, including future data, so this
is not an equal forecasting comparison.

## Part 3: 250-Day Rolling VaR
Each day's VaR used only the previous 250 trading days.
All three models were compared on the same 3,773 days.

| Model | Breach rate (target: 1%) |
|---|---|
| Rolling VaR | 2.65% (100 breaches) |
| Monthly VaR | 3.87% |
| Fixed VaR (uses future data) | 1.96% |

The rolling model did better than the monthly model, but none
of the three reached the target.
