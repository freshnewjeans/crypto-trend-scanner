# Crypto Trend Scanner

A browser-only HTX crypto perpetual trend screener that scans the available crypto USDT-margined perpetuals, surfaces only **very strong uptrends** and **very strong downtrends**, and hides ranging/sideways coins by default. It carries over the full signal and entry model from the previous HTX Signal Terminal.

**Designed & Created by Kevin Lim Fung Yen**

> Reference tool only — this app marks trends, setups, entries, stops and targets. It never places orders and is not financial advice.

## What it does

- Scans HTX **crypto perpetuals only** across 1H, 4H, 1D and 1W.
- Tokenized stocks, ETFs, indices, commodities and FX tokens are excluded from the scan.
- Ranging/weak coins are hidden in the default view and available for review under the **Ranging** tab.
- Cards are sorted by trend strength and show ADX, RSI, DI, swing structure, the latest trend-aligned candlestick pattern and a price sparkline.
- Click **Chart** for the detail view: main candlestick chart, EMA overlays, signal markers, Entry/SL/TP lines, four-timeframe mini charts, bias panel, latest setup, EMA status, strategy settings and a filterable signal log.

## Strategy engine carried over from the previous terminal

- **EMAs:** fast 9, mid 21, slow 50; golden cross (9 × 21) and death cross detection.
- **Bias:** price position versus EMA 21, with fast versus mid EMA alignment.
- **Candlestick patterns:** Hammer, Shooting Star, Doji, Bullish Engulfing, Bearish Engulfing, Piercing Line, Dark Cloud Cover, Morning Star, Evening Star, Three White Soldiers, Three Black Crows.
- **Entry model:** confirm the direction, wait for a pullback to the configured Fibonacci retrace (default 50%), then enter only on a rejection — pin bar or engulfing — at that level. If a nearby support/resistance level exists, the plan is break out, retest, then reject.
- **Stop loss:** swing extreme ± ATR(14) buffer (default multiplier 1.0).
- **Target:** configurable risk-to-reward multiple (default 2R).
- **Minimum entry timeframe:** rejection entries are only accepted on the configured timeframe or above (default 4H).

## Trend classifier

Each candidate is scored separately for long and short strength using:

- EMA 9 / 21 / 50 / 200 stack alignment
- Wilder RSI(14)
- Wilder ADX(14) with +DI and −DI
- MACD(12, 26, 9) histogram
- ATR(14)
- 50-bar linear-regression slope normalized by ATR
- Swing structure: HH + HL versus LL + LH
- EMA whipsaw count over the last 30 bars

A contract is marked **RANGE** when ADX is weak, the EMA stack is mixed, the 50-bar drift is flat, or there are frequent whipsaws. The desktop strength slider filters candidates at the chosen score threshold (default 65).

## Scanner controls

- Direction tabs: **Both**, **Strong Up**, **Strong Down**, **Ranging**.
- Timeframes: **1H**, **4H**, **1D**, **1W**.
- Search box for symbol filtering.
- Strength threshold slider: 40–100.
- 24H turnover floor: off, $1M, $10M, $50M.
- Auto refresh every 60 seconds, switchable on or off.

## Files

- `Crypto-Trend-Scanner.html` — the complete single-file application.
- `index.html` — GitHub Pages redirect to the application file.
- `README.md` — this file.

## Data sources

- Kline and ticker data are fetched live from HTX public market endpoints.
- The HTX contract-list endpoint does not send CORS headers that browsers accept, so the list cannot be fetched client-side. The application embeds a categorized snapshot taken on **2026-10-26**: crypto perpetuals are scanned; stock, ETF, index, commodity and FX tokens are listed only to mark them excluded.
- If HTX adds or delists perpetuals, refresh the embedded crypto snapshot.

## Run locally

Open `Crypto-Trend-Scanner.html` directly in Chrome, or serve the folder:

```bash
python -m http.server 8000
# then open http://localhost:8000/Crypto-Trend-Scanner.html
```

## Deploy on GitHub Pages

1. Push this folder to a public repository on the `main` branch.
2. In **Settings → Pages**, set the source to the `main` branch and root (`/`).
3. The redirect `index.html` opens `Crypto-Trend-Scanner.html` automatically.

Typical Pages URL:

```text
https://<your-username>.github.io/crypto-trend-scanner/
```

## Disclaimer

This software is a personal research and reference tool. It does not execute trades, connect to a wallet, or guarantee signals. Past patterns do not predict future results. Use your own judgment and manage risk manually.
