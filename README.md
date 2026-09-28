# Option Pricing Models: From Binomial Trees to Stochastic Volatility

Prices the same European call option five ways, and validates each method against the others:

| Method | Validated against |
|---|---|
| Binomial tree (Cox-Ross-Rubinstein) | Converges to Black-Scholes as steps increase; put-call parity holds exactly |
| Black-Scholes | Closed-form benchmark |
| Monte Carlo under risk-neutral GBM | Black-Scholes falls inside the 95% confidence interval; antithetic variates cut the standard error |
| Heston, semi-analytic (characteristic function) | Collapses to Black-Scholes as vol-of-vol → 0 |
| Heston, Monte Carlo | Agrees with the semi-analytic price within simulation error |

Also covers Euler vs exact GBM discretization (measured against the true lognormal distribution) and shows how Heston produces the implied-volatility skew that Black-Scholes cannot.

## What makes it rigorous

- **Every numerical method is checked** against a closed form or an independent method, and the gap is reported.
- **Common random numbers:** when comparing methods, the same random draws are reused, so differences reflect the model rather than simulation noise.
- **Monte Carlo prices come with standard errors** and 95% confidence intervals.
- **Heston uses the numerically stable "little Heston trap"** characteristic function (Albrecher et al., 2007).

## Contents

- `option_pricing_models.ipynb` — the full analysis, with code, figures, tables and interpretation
- `requirements.txt` — Python packages needed

## How to run

```
pip install -r requirements.txt
jupyter notebook option_pricing_models.ipynb
```

Price data is downloaded from Yahoo Finance at run time. The ticker, sample period and risk-free rate are set in the configuration cell.

## Limitations

Heston parameters are illustrative rather than calibrated to market option prices; volatility is estimated from historical returns rather than implied volatility; European options only, with no dividends, jumps or transaction costs.

## Extensions

Calibrate Heston to a real option chain, price American options with early exercise in the tree, and add jumps (Bates model).
