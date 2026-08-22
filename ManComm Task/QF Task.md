# FINOVA Quant & Trading Committee: Recruitment Task

**Instrument:** RELIANCE (NSE)  
**Timeframe:** Daily (1D)  
**Period:** August 2025 - August 2026  

## Part 2 & 3: Trade Log and Summary

### Trade Log
| Trade Number | Entry Date | Entry Price | Exit Date | Exit Price | P&L (%) |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 12-Aug-2025 | 1362.00 | 28-Aug-2025 | 1345.00 | -1.25% |
| 2 | 18-Sep-2025 | 1380.00 | 15-Jan-2026 | 1450.00 | +5.07% |
| 3 | 12-Feb-2026 | 1395.00 | 25-Feb-2026 | 1378.00 | -1.22% |
| 4 | 20-Apr-2026 | 1420.00 | 14-May-2026 | 1360.00 | -4.23% |
| 5 | 22-Jul-2026 | 1305.00 | 05-Aug-2026 | 1285.00 | -1.53% |

### Summary Statistics
* **Total Trades:** 5
* **Number of Winners:** 1
* **Win Rate:** 20.0%
* **Largest Single Winner:** +5.07%
* **Largest Single Loser:** -4.23%

## Part 4: Chart References

*Note: You can view the live interactive charts for these specific events on TradingView using the 1D timeframe and applying the 20/50 EMAs.*

**1. Full 12-Month Chart (Both EMAs visible)**
* **Link:** [RELIANCE (NSE) on TradingView](https://in.tradingview.com/chart/?symbol=NSE%3ARELIANCE) (UNABLE TO UPLOAD THE SCREENSHOTS; DO APOLOGISE)

**2. Best Trade (Trade #2: +5.07%)**
* **Action:** Zoom into the period between **September 18, 2025** (Entry crossover) and **January 15, 2026** (Exit crossover).

**3. Worst Trade (Trade #4: -4.23%)**
* **Action:** Zoom into the period between **April 20, 2026** (Entry crossover) and **May 14, 2026** (Exit crossover).

## Part 5: Final Verdict

**RELIANCE | 5 Trades | 20.0% Win Rate | Reject (Do Not Trade)**

It should be clear that I would never exchange this strategy for my own money as it stands right now. The 12 month test period yielded a poor 20% win rate (1 win out of 5 trades) with a negative expected value. The first obvious flaw in this system is the fact that Exponential Moving Averages are always **lagging indicators**, meaning they react only after the price has moved. In an environment where the market was experiencing choppiness, ranges or consolidation such as in the case of Reliance for the majority of the year, the 20-day and 50-day EMAs will keep crossing over each other repeatedly. This will lead to numerous "whipsaws" (false breakouts), causing the continuous depletion of capital through small losses.

This strategy performs best in conditions of a sustained bull/bear market where the amount of lag compared to the size of the multi-month move is negligible. Yet in the case of Trade 2 (the only winner, at +5.07%), the waiting for the exit crossover led to a significant giving up of unrealized profits by the strategy until the trade was closed. To make such a moving average crossover a viable system for trading with real money, one needs additional regime filters (such as ADX), volume confirmation and dynamic stop/exit point.
