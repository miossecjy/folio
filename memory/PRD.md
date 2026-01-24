# StockFolio - Portfolio Tracker

## Original Problem Statement
Build a portal through which a user can track their stock portfolio in real time.

## User Requirements
- Real-time stock tracking with Alpha Vantage API
- European stocks support (all major exchanges)
- Crypto tracking with CoinGecko API (separate section)
- Browser push notifications for price alerts
- Currency conversion for unified portfolio value
- JWT authentication

## Architecture
- **Backend**: FastAPI with MongoDB (motor async driver)
- **Frontend**: React with Tailwind CSS, Shadcn UI components
- **APIs**: Alpha Vantage (stocks), CoinGecko (crypto), Frankfurter (exchange rates)
- **Notifications**: Browser Push API

## What's Been Implemented (Dec 2025)

### Core Features
- [x] User authentication (register, login, JWT tokens)
- [x] Stock holdings CRUD (add, edit, delete)
- [x] Stock watchlist management
- [x] Real-time stock quotes (Alpha Vantage)
- [x] Portfolio dashboard with summary cards
- [x] Performance chart (recharts)
- [x] **European stocks support** (London, Frankfurt, Paris, Amsterdam, Zurich, Milan, Madrid, Nordic)
- [x] **Currency conversion** (USD, EUR, GBP, CHF, DKK, SEK, NOK)
- [x] Live exchange rates from Frankfurter API
- [x] Currency selector with preference persistence
- [x] Crypto holdings CRUD
- [x] Crypto watchlist management
- [x] Top cryptocurrencies market view (CoinGecko)
- [x] Crypto portfolio summary
- [x] Price alerts for stocks and crypto
- [x] Browser push notifications when target price hit

### Supported Currencies
- $ USD (US Dollar)
- € EUR (Euro)
- £ GBP (British Pound)
- CHF (Swiss Franc)
- kr DKK (Danish Krone)
- kr SEK (Swedish Krona)
- kr NOK (Norwegian Krone)

### Supported European Exchanges
- 🇬🇧 London (.LON) - GBP
- 🇩🇪 Frankfurt (.DEX) - EUR
- 🇫🇷 Paris (.PAR) - EUR
- 🇳🇱 Amsterdam (.AMS) - EUR
- 🇨🇭 Zurich (.SWX) - CHF
- 🇮🇹 Milan (.MIL) - EUR
- 🇪🇸 Madrid (.MAD) - EUR
- 🇩🇰 Copenhagen (.CPH) - DKK
- 🇸🇪 Stockholm (.STO) - SEK
- 🇳🇴 Oslo (.OSL) - NOK

### UI/UX
- Dark theme "Obsidian Ledger"
- Chivo + Manrope fonts
- Responsive design
- Currency selector in dashboard header
- Exchange color-coding in search & holdings

## API Endpoints
- Auth: /api/auth/register, /api/auth/login, /api/auth/me
- Holdings: /api/holdings (CRUD)
- Watchlist: /api/watchlist (CRUD)
- Stocks: /api/stocks/quote, /api/stocks/search
- Currency: /api/currencies, /api/exchange-rates
- Portfolio: /api/portfolio/summary?display_currency={code}
- Crypto: /api/crypto/top, /api/crypto/holdings, /api/crypto/watchlist
- Alerts: /api/alerts (CRUD), /api/alerts/check

## Prioritized Backlog

### P1 (High Priority)
- Email notifications for alerts
- Historical portfolio performance tracking
- CSV/data export

### P2 (Medium Priority)
- Multiple portfolios support
- News integration per stock/crypto
- Percentage change alerts

## Next Tasks
1. Add email notifications via SendGrid/Resend
2. Implement historical portfolio value tracking with charts
3. Add CSV export for holdings and transactions
