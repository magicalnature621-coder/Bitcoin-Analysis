# Bitcoin-Analysis

PROBLEM STATEMENT :

Assignment Overview

You will have to work with two primary datasets:
1. Bitcoin Market Sentiment Dataset
o Columns: Date, Classification (Fear/Greed
2. Historical Trader Data from Hyperliquid
o Columns include: account, symbol, execution price, size, side, time, 
start position, event, closedPnL, leverage, etc.
Your objective is to explore the relationship between trader performance and market 
sentiment, uncover hidden patterns, and deliver insights that can drive smarter trading 
strategies.

Link to dataset
Historical Data 

https://drive.google.com/file/d/1IAfLZwu6rJzyWKgBToqwSmmVYU6VbjVs/view?usp=sharing


Fear Greed Index link:

https://drive.google.com/file/d/1PgQC0tO8XN-wqkNyghWc_-mnrYv_nhSf/view?usp=sharing



Exploring the relationship between the Bitcoin Fear & Greed Index and real trader behaviour on Hyperliquid — uncovering hidden patterns to drive smarter Web3 trading strategies.

Datasets

| Dataset | Rows | Description |
| `fear_greed_index.csv` | 2,644 | Daily Bitcoin Fear & Greed Index with numeric value (0–100) and classification |
| `historical_data.csv` | 211,224 | Trade-level records from 32 Hyperliquid traders across 246 coins |

fear_greed_index.csv — Columns
| Column | Description |
| `timestamp` | Unix timestamp |
| `value` | Index value (0 = Extreme Fear, 100 = Extreme Greed) |
| `classification` | Extreme Fear / Fear / Neutral / Greed / Extreme Greed |
| `date` | Calendar date (YYYY-MM-DD) |

historical_data.csv — Key Columns
| Column | Description |
|--------|-------------|
| `Account` | Trader wallet address |
| `Coin` | Traded asset (BTC, ETH, HYPE, SOL, etc.) |
| `Execution Price` | Fill price |
| `Size USD` | Notional trade value in USD |
| `Side` | BUY / SELL |
| `Direction` | Open Long / Close Long / Open Short / Close Short / Spot |
| `Closed PnL` | Realised profit or loss (0 for open trades) |
| `Crossed` | True = cross-margin (higher risk), False = isolated margin |
| `Timestamp IST` | Trade timestamp in Indian Standard Time |

 Setup & Usage

Requirements :
pandas
numpy
matplotlib
seaborn
scipy

Running the Notebook
```bash
jupyter notebook bitcoin_sentiment_analysis.ipynb
```


Place both CSV files in the **same directory** as the notebook before running. Run all cells top to bottom — each section builds on the previous.


## 📓 Notebook Structure

| Section | Description |
|---------|-------------|
| 1 | Data loading & cleaning — timestamp parsing, type validation, ordinal encoding of sentiment |
| 2 | EDA — sentiment distribution, F&G trend over time, PnL histogram, top coins, direction breakdown |
| 3 | Merging datasets — trades joined to F&G index by calendar date |
| 4 | Performance by sentiment zone — win rate, avg PnL, total PnL, box plots |
| 5 | Correlation analysis — Pearson r and Spearman ρ between F&G value and daily avg PnL |
| 6 | Long vs Short breakdown — how direction interacts with sentiment |
| 7 | Trader-level analysis — top 10 traders, consistency score, trade count vs PnL scatter |
| 8 | Coin-wise performance — top 6 coins analysed across all 5 sentiment zones |
| 9 | Time-of-day analysis — hourly avg PnL and volume, sentiment × hour heatmap |
| 10 | Volume vs sentiment over time — dual-axis chart |
| 11 | Margin type & position sizing — cross-margin vs isolated margin by sentiment zone |
| 12 | Trader behavioural classification — Contrarian vs Momentum traders, style map scatter |
| 13 | Key insights & strategy recommendations |

---

 Key Findings

### Sentiment & Win Rate
- **Extreme Greed** has the highest win rate at **89.2%**, followed by Fear at **87.3%**
- Plain Greed (76.9%) underperforms Fear (87.3%) on win rate — counter to naive intuition
- **Neutral sentiment is the worst zone** to trade in for both win rate and average PnL

### Average PnL per Trade
- Extreme Greed: **~$130/trade** (highest)
- Fear: **~$113/trade**
- Neutral & Extreme Fear: **~$71/trade** (lowest)
- A clear U-shape — extreme sentiment in either direction creates tradeable volatility

### Long vs Short by Sentiment
- **Closing shorts during Fear** produces significantly higher avg PnL than closing longs
- During Extreme Greed, some traders successfully fade the top with short positions

### Correlation
- Pearson r ≈ **0.001** between numeric F&G value and daily avg PnL
- The signal lives in the **category labels**, not the raw number

### Margin Type (Leverage Proxy)
- **Isolated margin traders consistently outperform cross-margin traders** in avg PnL
- The gap is largest during Fear — disciplined risk management matters most when volatility is high
- Traders deploy **largest average positions during Fear** — classic "buy the fear" sizing

### Trader Behavioural Types
| Type | Count | Avg Total PnL | Avg Win Rate |
|------|-------|---------------|--------------|
| Momentum | 21 | $305K | 87% |
| Contrarian | 10 | $383K | 81% |

- **Contrarian traders average higher PnL** despite fewer trades — suggesting "buy the fear" is a genuine alpha source on Hyperliquid

### Time of Day (IST)
- **12:00 IST** and **07:00 IST** are the most profitable hours
- Extreme Greed + midday is the highest avg PnL combination in the heatmap


 Figures Generated

| Figure | Description |
|--------|-------------|
| fig1 | Sentiment distribution bar chart + monthly F&G trend line |
| fig2 | PnL distribution histogram + top 10 traded coins |
| fig3 | Trade direction breakdown |
| fig4 | Win rate, avg PnL, and total PnL by sentiment zone |
| fig5 | PnL box plots per sentiment zone |
| fig6 | Correlation scatter: F&G value vs daily avg PnL |
| fig7 | Long vs short: avg PnL and win rate by sentiment |
| fig8 | Top 10 traders — avg PnL across sentiment zones |
| fig9 | Trade count vs total PnL scatter (coloured by win rate) |
| fig10 | Coin-wise avg PnL across sentiment zones (6-panel) |
| fig11 | Hourly avg PnL and trade volume |
| fig12 | Heatmap: hour of day × sentiment zone avg PnL |
| fig13 | Daily trade volume vs F&G index (dual-axis) |
| fig14 | Cross-margin vs isolated: avg PnL and win rate by sentiment |
| fig15 | Position size (mean & median) by sentiment zone |
| fig16 | Contrarian vs Momentum traders: count, PnL, win rate |
| fig17 | Trader style map: fear-zone PnL vs greed-zone PnL scatter |

Strategy Recommendations

1. **Fear zones = short opportunity** — closing shorts during Fear/Extreme Fear delivers the strongest risk-adjusted returns
2. **Avoid Neutral sentiment** — weakest environment across all metrics
3. **Use isolated margin** — especially during high-volatility sentiment periods
4. **Size up in Fear** — top traders deploy larger positions when others are fearful
5. **Trade the 12:00–13:00 IST window** — historically the highest avg PnL per trade
6. **BTC/ETH for consistency, meme coins during Extreme Greed only** — speculative assets spike in greed but crash in fear

 Limitations & Notes

- The Hyperliquid dataset covers **May 2023 – May 2025** (only 32 unique traders) — findings may not generalise to the broader platform
- `Closed PnL = 0` rows are **open/partial trades** and are excluded from all PnL analysis
- The Fear & Greed Index is Bitcoin-specific; altcoin trades may respond differently to sentiment
- "Leverage" is proxied via the `Crossed` (margin type) column — explicit leverage multipliers are not in the dataset
- Contrarian/Momentum classification requires a trader to have trades in **both** fear and greed zones

