# StockFolio - Portfolio Tracker

## Original Problem Statement
Build a portal through which a user can track their stock portfolio in real time.

## User Requirements
- Real-time stock tracking with Alpha Vantage API
- European stocks support (all major exchanges)
- Crypto tracking with CoinGecko API (separate section)
- Browser push notifications for price alerts
- JWT authentication

## Architecture
- **Backend**: FastAPI with MongoDB (motor async driver)
- **Frontend**: React with Tailwind CSS, Shadcn UI components
- **APIs**: Alpha Vantage (stocks), CoinGecko (crypto)
- **Notifications**: Browser Push API

## What's Been Implemented (Dec 2025)

### Core Features
- [x] User authentication (register, login, JWT tokens)
- [x] Stock holdings CRUD (add, edit, delete)
- [x] Stock watchlist management
- [x] Real-time stock quotes (Alpha Vantage)
- [x] Portfolio dashboard with summary cards
- [x] Performance chart (recharts)
- [x] **European stocks support** (London, Frankfurt, Paris, Amsterdam, Zurich, Milan, Madrid, Nordic exchanges)
- [x] Color-coded exchange badges in UI
- [x] Multi-currency support (USD, EUR, GBP, CHF, DKK, SEK, NOK)
- [x] Crypto holdings CRUD
- [x] Crypto watchlist management
- [x] Top cryptocurrencies market view (CoinGecko)
- [x] Crypto portfolio summary
- [x] Price alerts for stocks and crypto
- [x] Browser push notifications when target price hit

### Supported European Exchanges
- 🇬🇧 London Stock Exchange (.LON) - GBP
- 🇩🇪 Frankfurt/Deutsche Börse (.DEX) - EUR
- 🇫🇷 Euronext Paris (.PAR) - EUR
- 🇳🇱 Euronext Amsterdam (.AMS) - EUR
- 🇨🇭 SIX Swiss Exchange (.SWX) - CHF
- 🇮🇹 Borsa Italiana Milan (.MIL) - EUR
- 🇪🇸 Bolsa de Madrid (.MAD) - EUR
- 🇩🇰 Copenhagen (.CPH) - DKK
- 🇸🇪 Stockholm (.STO) - SEK
- 🇳🇴 Oslo (.OSL) - NOK

### UI/UX
- Dark theme "Obsidian Ledger"
- Chivo + Manrope fonts
- Responsive design
- Exchange color-coding in search & holdings
- Tabs for Crypto (Holdings, Watchlist, Market)
- Tabs for Alerts (Active, Triggered)

## API Endpoints
- Auth: /api/auth/register, /api/auth/login, /api/auth/me
- Holdings: /api/holdings (CRUD)
- Watchlist: /api/watchlist (CRUD)
- Stocks: /api/stocks/quote, /api/stocks/search (with exchange field), /api/portfolio/summary
- Crypto: /api/crypto/top, /api/crypto/holdings, /api/crypto/watchlist, /api/crypto/portfolio/summary
- Alerts: /api/alerts (CRUD), /api/alerts/check, /api/alerts/{id}/reset

## Prioritized Backlog

### P1 (High Priority)
- Email notifications for alerts (when user offline)
- Historical portfolio performance tracking
- CSV/data export

### P2 (Medium Priority)
- Multiple portfolios support
- News integration per stock/crypto
- Currency conversion for combined portfolio value
- Percentage change alerts

## Next Tasks
1. Add email notifications via SendGrid/Resend
2. Implement historical portfolio value tracking
3. Currency conversion for unified portfolio view
