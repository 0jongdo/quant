# quant
developing trading bot for soaring stock

# US Momentum Stock Scanner

## Overview
A real-time scanner and analysis tool for identifying high-momentum and breakout stocks in the US equity market (NYSE/NASDAQ). Detects explosive movers using price action, volume surge, and technical signal filters.

## Key Features
- Real-time price momentum detection (intraday % gainers)
- Volume surge alerts (e.g., 3x–10x above average volume)
- Technical filters: gap-up detection, breakout from consolidation, relative strength
- Multi-timeframe screening (1m / 5m / 15m / 1D)
- Pre-market and after-hours mover tracking
- Watchlist management with custom alert thresholds

## How to Use
1. Clone the repository
```bash
   git clone https://github.com/yourname/us-momentum-scanner.git
   cd us-momentum-scanner
```
2. Install dependencies
```bash
   pip3 install -r requirements.txt
```
3. Configure your API key (Polygon.io / Alpaca / Finnhub) in `.env`
4. Run the scanner
```bash
   python3 main.py
```

## Data Sources
- [Polygon.io](https://polygon.io) — real-time & historical US equity data
- [Alpaca Markets](https://alpaca.markets) — free paper/live trading API
- [Finnhub](https://finnhub.io) — alternative free-tier option

## Requirements
- Python 3.9+
- See `requirements.txt` for full dependency list

## License
MIT License
