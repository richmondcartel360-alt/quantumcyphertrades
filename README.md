# Deriv Trading Bot - Quantum Cypher Tardes

A self-hosted, visual trading-bot builder on the Deriv WebSocket API. Drag-and-drop
strategy building with Blockly, an interactive SmartCharts chart, automated strategy
execution, and dashboard/tutorials.

> **Note:** Unlike the other templates in this repo (Rise/Fall, Accumulators, Digits)
> which are **Next.js** apps, the bot is a **[Rsbuild](https://rsbuild.dev) + React
> Router** single-page app. The commands, build output, and environment variables
> below differ accordingly.

## Analysis Tools for Advanced Digits Trading

Advanced analysis tools to enhance your digits trading strategy:

### Features
- **Real-time Digit Pattern Recognition** — Analyze historical digit sequences and identify recurring patterns
- **Volatility Index (VIX) Integration** — Monitor market volatility for optimal entry/exit timing
- **Probability Calculator** — Calculate win probabilities based on historical data and current market conditions
- **Heat Map Analysis** — Visual representation of digit frequency distribution across timeframes
- **Trend Analyzer** — Detect uptrends, downtrends, and consolidation phases in digit movements
- **Risk Assessment Dashboard** — Real-time risk metrics and exposure management
- **Backtesting Engine** — Test strategies against historical data with detailed performance metrics
- **Signal Generation** — AI-powered trading signals based on multi-factor analysis

### Quick Start with Analysis Tools
1. Access the **Analysis Tools** panel from the main dashboard
2. Select your desired analysis type (Pattern, Volatility, Probability, etc.)
3. Configure timeframe and lookback period
4. View insights and integrate signals into your trading strategy
5. Export analysis reports for further review

**Live Site:** [https://quantumcyphertrades.netlify.app](https://quantumcyphertrades.netlify.app)

---

## Prerequisites

- Node.js 18.18 or later

## Application Setup

This application is already registered with Deriv. Your App ID and OAuth credentials are configured in the environment variables below.

## Environment Configuration

Copy `.env.example` to `.env` and fill in your Deriv credentials:

```bash
cp .env.example .env
```

```env
# Required: Deriv app id — drives OAuth login/sign-up and WebSocket connections.
# Currently registered as: Quantum Cypher Tardes
NEXT_PUBLIC_DERIV_APP_ID=your_registered_deriv_app_id

# Environment: production for live Deriv, staging/preview for test environment
NEXT_PUBLIC_DERIV_ENV=production

# Optional: Affiliate/referral tracking
NEXT_PUBLIC_DERIV_REFERRAL_LINK=your_referral_link_here

# Optional: Google Drive integration for saving/loading strategies
GD_CLIENT_ID=your_google_drive_client_id
GD_APP_ID=your_google_drive_app_id
GD_API_KEY=your_google_drive_api_key
```

| Variable | Description |
|---|---|
| `NEXT_PUBLIC_DERIV_APP_ID` | Your registered Deriv app ID. Drives OAuth login/sign-up and WebSocket connections. |
| `NEXT_PUBLIC_DERIV_ENV` | `production` for live trading; `staging` or `preview` for test environment. |
| `NEXT_PUBLIC_DERIV_REFERRAL_LINK` | Affiliate referral link for attribution (optional). |
| `GD_CLIENT_ID` | Google Drive OAuth 2.0 Client ID (optional). |
| `GD_APP_ID` | Google Drive project number (optional). |
| `GD_API_KEY` | Google Drive API key (optional). |

> These variables are injected at **build time** via Rsbuild's `source.define`
> (see `rsbuild.config.ts`), so re-build after changing them.

## Local Development

```bash
npm install
npm run dev
```

The app is available at `http://localhost:4003`. (`npm install` and `npm run dev`
also regenerate brand CSS — see Branding below.)

## Build for Production

```bash
npm run build
```

This produces a static build in the `dist/` directory (Rsbuild output — there is no
`.next`/`out`). Serve the contents of `dist/` from any web server or static host.
SmartCharts engine assets are copied into `dist/js/smartcharts/` during the build.

## Google Drive Integration (Optional)

Saving/loading strategies to Google Drive stays disabled unless `GD_CLIENT_ID`,
`GD_APP_ID`, and `GD_API_KEY` are all set. **If it's not set up in your host
environment yet:**

1. **Get the credentials** — follow Google's [Picker set-up guide](https://developers.google.com/workspace/drive/picker/guides/web-picker#set-up-environment):
   enable the **Google Picker API** + **Drive API**, then create an **OAuth 2.0
   Client ID** (Web application) and an **API key**. Use the project number as `GD_APP_ID`.
2. **Authorize your domain** — add your deployed URL (e.g. `https://quantumcyphertrades.netlify.app`)
   to the OAuth client's **Authorized JavaScript origins** (exact origin; no wildcards).
3. **Set them in your host env** — add the three vars to your host environment
   (Netlify → Site Settings → Build & Deploy → Environment).
   Don't commit them to the repo.
4. **Rebuild** — they're baked in at build time (`source.define`), so trigger a new build/deploy.

## Branding & White-labeling

Branding (logo, primary color, fonts, app name) is driven by **`brand.config.json`**,
not Next.js config:

- **Colors / fonts / app name** — edit `brand.config.json`, then run
  `npm run generate:brand-css` to bake the values into the theme CSS variables. This
  runs automatically on `npm install`, `npm run dev`, and `npm run build`.
- **Logo** — drop a `public/logo.<png|jpg|jpeg|webp>` to set the header logo; it is also
  used as the favicon. Without it, a letter badge (the app name's first letter) is shown.
- **Theme** — a light/dark toggle lives in the header; the chart re-themes with it.
