# Multi-Asset Trend Following Strategy
> Bitget AI Hackathon S1 — Trading Agent Track  
> by [@amosanthony005](https://getagent.bitget.com)

---

## Overview

A pure trend-following strategy for Bitget USDT-margined perpetual futures on **BTC, ETH, and SOL**. The core thesis is that once a sustained directional move begins in crypto markets, price tends to continue along that trajectory — with periodic pullbacks offering high-probability continuation entries.

Live on Bitget GetAgent Studio (Playbook) since **June 22, 2026**.

---

## Performance Summary

| Metric | Value |
|---|---|
| Total Return | +3.5% |
| Max Drawdown | −1.5% |
| Win Rate | 64% |
| Profit Factor | 2.17× |
| Avg Round Trip Return | +0.45% |
| Round Trips | 14 |
| Avg Hold Time | 6h 30m |
| Backtest Period | May 2026 – Jun 2026 |

---

## Strategy Logic

### Entry Conditions

**Long (Bullish)**
- EMA 20 > EMA 50 > EMA 200 (bullish alignment)
- Price making higher highs and higher lows
- Pullback to EMA 20 or EMA 50 zone
- Bullish reversal candle at moving average support
- Volume increases on upward continuation

**Short (Bearish)**
- EMA 20 < EMA 50 < EMA 200 (bearish alignment)
- Price making lower highs and lower lows
- Pullback rally rejected at EMA 20 or EMA 50
- Bearish reversal candle at moving average resistance
- Volume expands on downward continuation

### Exit Conditions

| Exit Type | Logic |
|---|---|
| Take Profit | Previous swing highs/lows + ATR × 4.0 from entry |
| Stop Loss | ATR × 2.0 beyond last structural swing point |
| Trailing Stop | ATR-based, activates once trade moves favorably |

---

## Risk Management

- **Starting Capital:** 10,000 USDT
- **Risk Per Trade:** 1% of account equity
- **Leverage:** 5×
- **Position Sizing:** Dynamically adjusted based on stop-loss distance for consistent risk exposure

### When the Strategy Underperforms
- Sideways/choppy markets with no clear trend direction
- Low liquidity periods outside London/New York sessions
- High-impact news events causing sudden reversals

---

## Parameters

```
ema_fast_period     = 20
ema_mid_period      = 50
ema_slow_period     = 200
risk_per_trade_pct  = 1.0
leverage            = 5
margin_budget       = 10000
atr_period          = 14
atr_sl_multiplier   = 2.0
atr_tp_multiplier   = 4.0
```

---

## Assets Traded

- `BTCUSDT` — Bitcoin Perpetual Futures
- `ETHUSDT` — Ethereum Perpetual Futures
- `SOLUSDT` — Solana Perpetual Futures

---

## Execution Log (Sample)

| Date | Symbol | Side | Entry | Exit | P&L | Return | Hold |
|---|---|---|---|---|---|---|---|
| Jun 19 | BTCUSDT | Short | 63056.70 | 63077.80 | −$11.30 | −0.03% | 5h |
| Jun 10 | BTCUSDT | Short | 61902.10 | 61730.10 | +$8.38 | +0.28% | 5h |
| Jun 9 | BTCUSDT | Short | 61309.50 | 62178.40 | −$86.67 | −1.42% | 22h |
| Jun 2 | ETHUSDT | Short | 1919.85 | 1838.19 | +$180.52 | +4.25% | 12h |
| Jun 1 | SOLUSDT | Short | 80.643 | 80.842 | −$19.89 | −0.25% | 7h |
| Jun 1 | ETHUSDT | Short | 1964.02 | 1986.68 | −$80.39 | −1.15% | 1h |
| Jun 1 | SOLUSDT | Short | 81.991 | 81.791 | +$8.96 | +0.24% | 4h |
| Jun 1 | BTCUSDT | Short | 73785.70 | 73457.80 | +$44.60 | +0.44% | 5h |
| May 27 | SOLUSDT | Short | 82.436 | 80.665 | +$113.73 | +2.15% | 6h |

---

## Tools & Platform

- **Platform:** Bitget GetAgent Studio (Playbook)
- **Market:** USDT-margined Perpetual Futures
- **Mode:** Paper Trading (live since Jun 22, 2026)

---

## Submission Links

- 🔗 [GetAgent Studio Strategy](#) *(add your public Playbook link)*
- 📊 [Backtest Report](#) *(add GitHub link if uploading)*
- 🎥 [Demo Video](#) *(add YouTube/X link if applicable)*

---

## Hackathon

**Bitget AI Hackathon S1** — Trading Agent Track  
Submitted: June 24, 2026
