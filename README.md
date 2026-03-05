# Interactive BTC Liquidity Dashboard

A live, interactive trading dashboard for BTC/USDT perpetual futures that combines three key derivatives market tools in a single view.

🔗 **[Live demo →](https://YOUR_USERNAME.github.io/interactive-btc-dashboard)**
*(replace YOUR_USERNAME with your GitHub username after deploying)*

---

## What it shows

### ① Liquidation Map
Heatmap overlay on the price chart showing where leveraged positions would be force-closed. Red bands = long liquidations below price (cascade risk). Green bands = short liquidations above price (squeeze potential). These levels act as price magnets.

### ② Open Interest (OI)
Bottom panel tracking total open derivatives contracts over time. Rising OI + rising price = confirmed momentum. Divergence between OI and price direction is flagged automatically as a warning signal.

### ③ Order Book Depth
Right panel showing real-time bid/ask depth as horizontal bars. The imbalance ratio at the bottom indicates which side has more weight at any given moment.

### ④ Composite Signal
Synthesizes all three inputs into a single directional bias: **BULLISH / NEUTRAL / BEARISH**. Use it as a context filter, not a standalone trading signal.

---

## Features

- 1H / 4H timeframe selector
- Liquidation map toggle (on/off)
- Live tick simulation (updates every 2 seconds)
- Fully responsive layout
- Zero dependencies — pure React via CDN + custom SVG rendering

---

## ⚠️ Data disclaimer

**All data in this dashboard is simulated, not live.**

| Layer | Simulation method |
|---|---|
| Candles | Gaussian random walk with configurable volatility per timeframe |
| Open Interest | Sine wave with drift + noise to mimic real accumulation |
| Liquidation levels | Probabilistic distribution around current price, weighted by distance |
| Order book | Exponential decay from mid-price for realistic bid/ask tapering |
| Live tick | Last candle updated every 2 seconds |

### For production use with real data

| Data | Source | Cost |
|---|---|---|
| Candles + OI | [Binance Futures API](https://binance-docs.github.io/apidocs/futures/en/) | Free |
| Liquidation heatmap | [Coinglass API](https://coinglass.com/api) | ~$30/month (pro tier) |
| Order book depth | [Bybit L2 WebSocket](https://bybit-exchange.github.io/docs/v5/websocket/public/orderbook) | Free |

---

## Customization

All colors are defined in a single `C` object at the top of the script inside `index.html`:

```js
const C = {
  bull:  "#00e5a0",  // green — bullish candles, short liquidations
  bear:  "#ff3b5c",  // red   — bearish candles, long liquidations
  price: "#f7c948",  // yellow — current price line
  bg:    "#060a12",  // background
  panel: "#0a0e1a",  // panel background
  grid:  "#1e2535",  // grid lines
  muted: "#4a5568",  // secondary text
  text:  "#e2e8f0",  // primary text
};
```

To change the base price or candle count, edit these constants:

```js
const BASE_PRICE   = 91420;
const CANDLE_COUNT = timeframe === "1H" ? 60 : 40;
```

---

## Deploy to GitHub Pages

1. Fork or clone this repository
2. Go to **Settings → Pages**
3. Source: `Deploy from a branch` → Branch: `main` → Folder: `/ (root)`
4. Save — your dashboard will be live at `https://YOUR_USERNAME.github.io/interactive-btc-dashboard`

---

## Built with

- [React 18](https://react.dev/) via CDN (no build step required)
- [Babel Standalone](https://babeljs.io/docs/babel-standalone) for JSX in-browser
- Custom SVG rendering — no charting libraries
- [JetBrains Mono](https://www.jetbrains.com/lp/mono/) + [Space Grotesk](https://fonts.google.com/specimen/Space+Grotesk) via Google Fonts

---

*This is a prototype for educational and demonstration purposes. Not financial advice.*
