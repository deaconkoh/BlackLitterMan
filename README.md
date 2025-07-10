# Sentiment-Driven Asset Allocation using the Black-Litterman Model

This project explores how **news sentiment** can be integrated into portfolio allocation through the **Black-Litterman model**, a popular quantitative finance framework. By combining investor views derived from **FinBERT sentiment analysis** and historical price data, the model dynamically adjusts portfolio weights on a **monthly basis**.

## Project Highlights

- **Objective**: Evaluate the effectiveness of a sentiment-driven investor views on portfolio allocation.
- **Methodology**:
  - Fetched financial news using the NewsAPI.
  - Performed sentiment scoring on headlines using `FinBERT`.
  - Estimated the relationship between sentiment and future returns using **Bayesian regression**.
  - Integrated sentiment views into the Black-Litterman framework.
  - Backtest the strategy by rebalancing the portfolio **monthly** from **May 2024 to May 2025**.
- **Evaluation**: Portfolio performance is evaluated using **cumulative returns** and **Sharpe Ratio**, including a **rolling Sharpe Ratio** to observe short-term performance changes.

## Key Components

| Module                      | Description                                                                 |
|----------------------------|-----------------------------------------------------------------------------|
| `analyze_sentiment()`      | Uses FinBERT to compute sentiment score from financial news headlines       |
| `estimate_alpha()`         | Uses Bayesian linear regression to estimate return sensitivity to sentiment |
| `construct_view_matrices()`| Constructs Q, P, Ω matrices for Black-Litterman using sentiment scores       |
| `run_black_litterman()`    | Calculates posterior returns and optimal weights                            |
| `backtest loop`            | Rebalances portfolio monthly and computes performance metrics               |

## Example Output

| Sector                             | Allocation |
|------------------------------------|------------|
| Technology                         | 23.49%     |
| Financial                          | 8.53%      |
| Energy                             | 15.77%     |
| Gold                               | 16.46%     |
| Long-Term Treasury Bonds           | 4.62%      |
| Inflation-Protected Treasury Bonds | 31.13%     |

## Analysing Results

This section showcases the outcome of applying a **sentiment-integrated Black-Litterman model** with monthly rebalancing. The visuals below provide a comprehensive overview of how portfolio weights and performance metrics evolved from **May 2024 to May 2025**.

### 1. Portfolio Allocation Over Time by Sector  
![Sector Allocation](./screenshots/Sector%20Allocation.png)

This chart illustrates monthly sector weightings from May 2024 to May 2025. While allocations shifted slightly, the changes were minimal. The starting weights were:

- **Gold** (~31%)  
- **Technology** (~23%)  
- **Long-Term Treasury Bonds & Financials** (~16% each)  
- **Energy** (~9%)  
- **TIPS** (~4%)

Despite monthly rebalancing, the portfolio maintained a stable structure — an outcome of both the **limited variation in sentiment scores** and the **model’s conservative weighting on investor views (low `tau`)**. Still, the initial allocations were meaningfully influenced by sentiment, giving the strategy an informed base that contributed to its cumulative gains.

### 2. Cumulative Portfolio Returns  
![Cumulative Returns](./screenshots/Cumulative%20Returns.png)

The portfolio’s cumulative return from May 2024 to May 2025 shows a steady, though occasionally volatile, upward trend. Despite the minimal changes in portfolio weights across the months, it’s important to note that the initial allocation itself was derived from sentiment analysis using FinBERT. This sentiment-informed starting point helped shape the portfolio’s overall structure, which delivered a positive return over time.

### 3. Rolling Sharpe Ratio (21-Day Window)  
![Rolling Sharpe Ratio](./screenshots/Rolling%20Sharpe%20Ratio.png)

This plot tracks the 21-day rolling Sharpe ratio, showing how the portfolio’s risk-adjusted performance evolved over time. The frequent shifts — from above 6 to below -4 — highlight the volatile nature of financial returns, even though portfolio weights remained relatively constant. This suggests that the Sharpe Ratio variability is more reflective of market turbulence than of dynamic sentiment adaptation.

## Reflection
This project demonstrated the potential of combining **sentiment analysis** and **quantitative finance** using the **Black-Litterman model**. While the overall strategy yielded a **positive return**, the relatively **minimal month-to-month changes in sector allocation** highlighted a few key reflections:

### What Went Well
- **Seamless integration of FinBERT sentiment scores** into the Black-Litterman model via custom view matrices.
- The initial portfolio allocation was meaningfully influenced by sentiment data, which set a strong baseline for returns.
- Modular and reusable code structure, making it easy to expand or adapt for new tickers or news sources.
- Successful application of **Bayesian regression** to learn sentiment-return relationships from real forward returns.

### Limitations
- **Limited sentiment variation across months** led to minor rebalancing adjustments, reducing the model's responsiveness.
- **Short backtest duration** (1 year) may not fully capture cyclical trends or stress test the model’s robustness.
- FinBERT only analyzes **headline tone** without context on news significance or impact magnitude.
- Real-world trading frictions like **slippage, transaction costs**, and **execution delay** were not modeled.

### Future Enhancements
- Extend backtest over **multiple years** to better assess performance across different market cycles.
- Include **alternative data sources** (e.g., Reddit, Twitter sentiment, macro indicators).
- Rather than using a fixed τ (tau), dynamically adjust it based on volatility or news intensity to better reflect investor uncertainty across time.
- Incorporate **constraints** or **risk parity** considerations to enhance portfolio robustness.

## Conclusion
This project demonstrated how sentiment analysis can be integrated into a quantitative portfolio allocation strategy using the Black-Litterman model. While the monthly portfolio adjustments showed only modest variation, the strategy still achieved positive cumulative returns and a stable risk-adjusted profile. This highlights the potential of using sentiment as a supplementary signal, even when changes appear small.

🔗 Check it out on Google Colab: [Open in Colab](https://colab.research.google.com/drive/1Rszhyl3JsYnEoyRxauRe5BqmKC51NrAb?usp=sharing)
