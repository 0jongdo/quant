# 🚀 US Momentum Bot

> **AI-powered breakout stock scanner and trading bot for the US equity market.**  
> Built by an independent quant developer learning in the open.

[![Python](https://img.shields.io/badge/Python-3.9%2B-blue?logo=python)](https://python.org)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Status](https://img.shields.io/badge/Status-Active%20Development-orange)]()
[![Data](https://img.shields.io/badge/Data-Polygon.io%20%7C%20Alpaca-lightgrey)]()

---

## What This Is

Most momentum scanners are either locked behind expensive SaaS subscriptions or too simplistic to be useful. **US Momentum Bot** is an open-source attempt to close that gap — combining real-time market data with multi-model machine learning to surface high-probability breakout setups on NYSE and NASDAQ.

It's not a black box. Every signal comes with a score, a rationale, and the raw data behind it.

---

## How It Works

```
Real-time price & volume data (Polygon.io / Alpaca)
        │
        ▼
Feature Engineering
  ├── Volume surge ratio (vs. 20-day avg)
  ├── Gap-up % from prior close
  ├── Multi-timeframe momentum (1m / 5m / 15m / 1D)
  ├── Relative strength vs. SPY
  └── Candle pattern detection
        │
        ▼
ML Signal Scoring
  ├── LightGBM  ──┐
  ├── XGBoost   ──┼──► Voting Ensemble ──► BUY / SKIP / WATCH
  └── CatBoost  ──┘
        │
        ▼
Risk Management Layer
  ├── Position sizing (% of capital)
  ├── Stop-loss & trailing stop
  └── Max daily drawdown limit
        │
        ▼
  Alert / Execute / Log
```

---

## Key Features

- **Real-time scanner** — sub-second REST polling across NYSE/NASDAQ universe
- **Volume surge detection** — flags stocks trading 3x–10x above 20-day average volume
- **Gap-up screening** — catches pre-market and open-drive momentum before the crowd
- **Multi-model ML ensemble** — LightGBM, XGBoost, CatBoost with Voting Ensemble
- **Signal scoring** — ranked by Return, Sharpe Ratio, Max Drawdown, Accuracy, F1
- **Pre/after-hours monitoring** — catches extended-hours movers early
- **Risk management built-in** — position sizing, stop-loss, max drawdown rules
- **Paper trading mode** — test strategies without real capital via Alpaca sandbox
- **Human-readable signal log** — every decision is explainable, not just a prediction

---

## Quickstart

```bash
# 1. Clone
git clone https://github.com/0jongdo/us-momentum-bot.git
cd us-momentum-bot

# 2. Install dependencies
pip3 install -r requirements.txt

# 3. Set up environment variables
cp .env.example .env
# → Add your Polygon.io and/or Alpaca API keys

# 4. Run the scanner (paper mode by default)
python3 main.py --mode paper
```

---

## Configuration

```yaml
# config.yaml

scanner:
  universe: "nasdaq100"        # nasdaq100 | sp500 | all
  timeframes: [1m, 5m, 15m, 1D]
  volume_surge_threshold: 3.0  # x above 20-day avg
  gap_up_min_pct: 2.0          # minimum gap % to qualify

model:
  ensemble: true
  models: [lightgbm, xgboost, catboost]
  scoring: [return, sharpe, mdd, accuracy, f1]

risk:
  max_position_pct: 5.0        # % of total capital per trade
  stop_loss_pct: 2.0
  max_daily_drawdown_pct: 5.0

execution:
  mode: paper                  # paper | live
  broker: alpaca
```

---

## Signal Output Example

```
[09:32:14] 🔥 SIGNAL DETECTED
  Ticker     : NVDA
  Setup      : Gap-up + Volume Surge (4.8x avg)
  Timeframe  : 5m breakout above pre-market high
  ML Score   : 0.83 (Ensemble)
  Sharpe Est : 1.94 | MDD: -1.2% | Accuracy: 71%
  Action     : WATCH → BUY on confirmation candle
  Risk       : $200 stop / $600 target (1:3 R/R)
```

---

## Tech Stack

| Layer | Tool |
|---|---|
| Language | Python 3.9+ |
| ML Models | LightGBM, XGBoost, CatBoost, scikit-learn |
| Market Data | Polygon.io, Alpaca Markets |
| Scheduling | APScheduler |
| Storage | SQLite (signals log) |
| Config | YAML + python-dotenv |

---

## Project Status

This project is in **active early development**. It's being built by an independent developer learning quantitative trading hands-on — in the open, iteratively, and with full transparency about what works and what doesn't.

Current progress:
- [x] Real-time data pipeline (Polygon.io + Alpaca)
- [x] Feature engineering (volume, gap, momentum)
- [x] Multi-model ML scoring (LightGBM, XGBoost, CatBoost)
- [x] Voting Ensemble
- [ ] Live paper trading loop
- [ ] Backtesting framework
- [ ] Web dashboard (signal feed UI)
- [ ] Telegram / Slack alert integration

---

## Why Open Source?

Institutional traders have Bloomberg terminals, quant teams, and proprietary data feeds. Independent developers have none of that. This project exists to build the kind of tool that serious retail quant traders need — and to do it in the open so others can learn from it, contribute to it, and use it.

If you're learning quant finance and want to build something real alongside me, contributions and feedback are welcome.

---

## Data Sources

- [Polygon.io](https://polygon.io) — real-time & historical US equity data (recommended)
- [Alpaca Markets](https://alpaca.markets) — free paper/live trading API
- [Finnhub](https://finnhub.io) — alternative free-tier option

---

## Disclaimer

This software is for **educational and research purposes only**. It is not financial advice. Trading involves substantial risk of loss. Always do your own research before making any investment decisions.

---

## License

MIT License — free to use, modify, and distribute.

---

*Built with curiosity, caffeine, and a lot of market hours.*
