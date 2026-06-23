# Multi-Asset Trend Following — Mulan

**Bitget AI Hackathon S1 — Studio Native Submission**
Strategy type: Trend-following | Assets: BTCUSDT · ETHUSDT · SOLUSDT Perpetuals | Built with: GetAgent Studio

---

## Why I Built It

Single-asset strategies are exposed to asset-specific noise. When BTC consolidates, ETH or SOL may be trending cleanly — and a strategy locked to one pair misses that entirely. I wanted to build a system that hunts for trend setups across all three major crypto perpetuals simultaneously, allocating to whichever asset is actually moving while keeping risk consistent across every trade.

The secondary goal was discipline. Most multi-asset systems either over-trade (too many signals, too much noise) or under-trade (filters so strict nothing ever fires). Mulan is built to find the middle — frequent enough to generate a meaningful sample of trades, selective enough that each entry has a genuine edge.

---

## Core Logic

The strategy is built on one thesis: once crypto markets establish a sustained directional move, price tends to continue with periodic pullbacks that offer continuation opportunities. Mulan captures the middle of established trends — not the initial breakout, not the exhaustion top.

**Trend detection — triple EMA alignment**
Structure is confirmed when all three EMAs stack in sequence: EMA(20) > EMA(50) > EMA(200) for longs, reversed for shorts. This eliminates entries in choppy, mean-reverting conditions where a single EMA crossover would generate false signals.

**Entry conditions (long — all must be true)**
- EMA 20 > EMA 50 > EMA 200 (bullish alignment)
- Price making higher highs and higher lows
- Pullback to EMA 20 or EMA 50 zone
- Bullish reversal candle at moving average support
- Volume increasing on upward continuation

Short entries mirror these conditions on the bearish side.

**Exit logic — three layers**
- Take profit at previous swing highs/lows and ATR-based targets (4.0× ATR from entry)
- Hard stop beyond last structural swing point (2.0× ATR from entry)
- ATR-based trailing stop activates once the trade moves in favour

**Risk management**
- Risk per trade: 1% of account equity ($100 per trade on $10,000)
- Position size calculated from stop distance — not fixed lot
- Leverage: 5×
- Margin budget: $10,000
- Applies identically across BTC, ETH, and SOL

**Signals used:** Technical only — triple EMA alignment, swing structure (HH/HL or LH/LL), volume confirmation, ATR-based stops and targets. No on-chain, macro, or sentiment inputs.

**Timeframe:** 1H candles

---

## Results (Backtest + Paper Trading — May–Jun 2026)

| Metric | Value |
|---|---|
| Total return | +3.5% |
| Max drawdown | −1.5% |
| Win rate | 64% |
| Profit factor | 2.17× |
| Avg round trip | +0.45% |
| Round trips | 14 |
| Avg hold time | 6h 30m |

Paper trading live since Jun 22, 2026.

**Standout trade:** Short ETHUSDT Jun 2 04:00 PM → Jun 3 04:00 AM · +$180.52 · +4.25% in 12 hours

---

## Development Challenges

**Challenge 1: Short bias in a bull market**
The backtest window (May–Jun 2026) captured a BTC correction phase, naturally favouring short setups. All 14 completed trades were shorts. In BTC's subsequent rally above $84K the triple EMA alignment has not yet confirmed a long — the EMA(200) lags significantly. Next step is adding a higher-timeframe bias filter (4H or daily) to reduce lag on trend direction changes.

**Challenge 2: Small per-trade returns**
With 1% risk per trade and a 2× ATR stop, individual trade returns are modest (+0.45% avg). This is by design for capital preservation but limits headline return figures. Increasing ATR TP multiplier from 4.0 to 5.0 or 6.0 would extend winners without changing the risk per entry.

**Challenge 3: Multi-asset signal conflicts**
Running three assets simultaneously occasionally produces overlapping signals that compete for margin. Added margin budget cap at $10,000 across all open positions to prevent over-allocation in correlated moves.

---

## What's Complete / What's Next

**Complete**
- Triple EMA trend filter across BTC, ETH, SOL
- Swing structure confirmation (HH/HL, LH/LL)
- ATR-based stop, take profit, and trailing stop
- 1% per-trade risk with dynamic position sizing
- Backtest and paper trading live on GetAgent Studio

**Missing / Next steps**
- Higher-timeframe bias filter (4H EMA alignment as pre-condition)
- Long-side trade execution — strategy has only fired shorts so far
- Extend backtest beyond 6-month window
- Add XRPUSDT or BNBUSDT as fourth tradable symbol
- Increase ATR TP multiplier to improve reward-to-risk ratio

---

## Tools & Frameworks

| Tool | Usage |
|---|---|
| GetAgent Studio (Playbook) | Strategy authoring, backtesting, paper trading |
| Bitget Perpetuals | BTCUSDT, ETHUSDT, SOLUSDT |
| EMA (20/50/200) | Triple trend filter |
| ATR (14) | Stop loss, take profit, trailing stop, position sizing |

**Bitget tools used:** GetAgent Studio — Playbook

---

## Experience with Bitget AI Tools

GetAgent Studio made it possible to go from strategy concept to live paper trading in a single session. The multi-asset support is particularly strong — being able to run BTC, ETH, and SOL under one playbook with shared risk parameters is exactly what a systematic trader needs.

The main gap is backtest depth. A 6-month window captures one market phase. A 2-year window would let you stress-test across bull, bear, and sideways regimes — which is the minimum bar for trusting a trend-following system. A regime overlay (trending / ranging / volatile) built into the Studio chart would also help builders diagnose where their strategy leaks.

The future of agentic trading is systems that don't just execute signals but adapt their parameters based on detected regime. Mulan is a step toward that — the next version will read market regime before deciding whether to apply trend-following or switch to a mean-reversion mode.

---

## Links

GitHub: https://github.com/amosanthony005-oss/Multi-Asset-Trend-Following-Mulan

GetAgent Studio: https://getagent.studio/strategy/bdb127c7-15ea-41ce-abf4-f2ccfc72bf1d

Project post: https://x.com/i/status/2069407937911488826

Campaign repost: https://x.com/i/status/2068599931099619833

Assets: BTCUSDT · ETHUSDT · SOLUSDT

Bitget tools used: GetAgent Studio — Playbook

Paper trading: Live since Jun 22 · 14 trades · 64% win rate · 2.17× profit factor · +3.5% return

---

Ready for the trading log CSV and Twitter thread next?
