# Monte Carlo Portfolio Optimizer

This project tries to answer a simple question: **'if you had ₹10,00,000 to invest across 8 Indian stocks, what mix of them gives you the best return for the risk you're taking?'**

## Key finding: 
Using 10,000 random portfolio simulations, I found optimal weights that gave a Sharpe Ratio of **1.03** on historical data (2021–2024). But when I tested those exact same weights on newer, unseen data (2024–2026), the Sharpe Ratio dropped to **-0.14** — showing that optimization on past data doesn't guarantee future performance. This is a well-known limitation in real portfolio management, and catching it was the most important part of this project.

## What stocks are in it?
PERSISTENT, BAJAJ-AUTO, AXISBANK, LUPIN, MARICO, SRF, SIEMENS, BAJFINANCE (all NSE-listed, 5 years of daily price data from 2021 to 2026)

## How it works
1. Pulled 5 years of daily stock prices using `yfinance`
2. Calculated daily returns and checked how the stocks move together (correlation heatmap, pairplot)
3. Randomly generated 10,000 different portfolio weight combinations (just random guessing, not with deep or fancy mathematics)
4. For each combination, calculated expected annual return, volatility (risk), and Sharpe Ratio (using ~6.67% as the risk-free rate)
5. Plotted all 10,000 combinations on a scatter plot (the Efficient Frontier) and picked the one with the highest Sharpe Ratio

## Checking if it actually works: Train/Test Split
Picking the "best" portfolio using data you already fully know isn't good proof — it's like predicting yesterday that actually happened. So I split the 5 years:
- **Train period** (2021–2024): found the best weights using only this data
- **Test period** (2024–2026): applied those exact same frozen weights to unseen data

During the train period, the optimized portfolio achieved a Sharpe Ratio of **1.03**, with an expected annual return of **24.5%** and volatility of **17.2%**. On the test period, the Sharpe Ratio dropped to **-0.14**, with expected return falling to **4.08%** while volatility stayed similar at **18.23%**.

## What I'd improve next
- Try real optimization (`scipy.optimize`) instead of random guessing
- Add constraints (e.g., no more than 30% in one stock)
- Test on a longer or different time period

## Tools used
Python, pandas, numpy, yfinance, plotly, matplotlib, seaborn

## About me
I'm 18 yo, currently preparing for retaking CFA Level 1 and building projects like this to understand Portfolio Theory and Quant Research for growing knowledge in mathematics and research.
