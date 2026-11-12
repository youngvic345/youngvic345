[← Back to profile](../README.md)

# Trading research platform

**Python · FastAPI · Redis · React · TypeScript · OANDA API · MetaTrader 5 · Pine Script · KLineCharts**

A personal side project for studying ICT and Smart Money Concepts with real tooling instead of screenshots.

## Platform

- **Live data:** streams ticks for about ten forex and metal pairs, resamples to candles, and detects structure live: fair value gaps, order blocks, break of structure and change of character.
- **Event-driven architecture:** an ingestion engine, Redis publish/subscribe, an API hub, and a React UI over WebSockets.
- **Multi-strategy engine** with a broker router that switches between an internal simulator and a practice account, a high-impact-news auto-halt, and a one-click historical backtester.
- **Trading UI:** single, split and quad chart layouts with independent pairs and timeframes, a replay engine (step, scrub, speed up), session and previous-day high/low overlays, performance analytics and a CSV trade journal.
- Alerts through chat webhooks.

## Confluence chart app

A separate TypeScript app for comparing timeframes side by side:
- Several linked chart panes from monthly down to one-minute data, with shared crosshair, synced viewport and candle width.
- Optional pairing of two devices over WebSocket.
- Standalone concept explainers: concept graph, timeframe cascade, confluence story and auxiliary tools.

## Also

An MT5 expert advisor with backtests and written analysis, an Obsidian trading journal vault with risk and review templates, and Pine Script indicator work with TradingView.

All research and practice-account work.
