# Solana Token Scanner & Trading Signals

Automated Solana token discovery and analysis system with AI-powered trading signal generation.

## Overview

This system scans the Solana blockchain for emerging tokens, analyzes their trading patterns using AI, and generates actionable trading signals with dynamic parameters based on market conditions.

## Features

### Token Discovery
- Real-time monitoring of Solana token activity
- Advanced filtering based on transaction volume, holder count, and pool age
- Integration with GeckoTerminal API for comprehensive market data

### AI-Powered Analysis
- Local LLM integration for token evaluation
- Dynamic trading parameter generation based on:
  - Buy/sell pressure and momentum
  - Volume and liquidity metrics
  - Price volatility patterns
  - Trade flow analysis

### Trading Signals
- **BUY**: Strong buy pressure with favorable momentum
- **WATCH**: Moderate interest worth monitoring
- **SKIP**: Insufficient metrics or unfavorable conditions

### Dynamic Trading Parameters
Each signal includes customized parameters:
- **Limit Order**: Entry price based on volatility (0% to -10%)
- **Take Profit**: Target exit based on volume (+5% to +40%)
- **Stop Loss**: Risk management based on volatility (-5% to -25%)
- **Time Frame**: Recommended holding period (30min to 1day)

### Paper Trading System
- Automated position tracking with stop loss and take profit execution
- Performance metrics including peak gains and maximum drawdown
- Historical tracking of all trades with outcome analysis

## Latest Orderbook

The `orderbook.json` file in this repository contains the most recent trading signals from the scanner. It updates automatically after each scan cycle.

### Orderbook Structure
```json
{
  "timestamp": "ISO datetime",
  "total_tokens": "number of signals",
  "buy_signals": "count of BUY signals",
  "watch_signals": "count of WATCH signals",
  "tokens": [
    {
      "name": "Token Name",
      "mint": "Token Address",
      "chart_url": "GeckoTerminal chart link",
      "decision": "BUY/WATCH/SKIP",
      "current_price": "USD price",
      "volume": "24h volume",
      "buys": "buy transaction count",
      "sells": "sell transaction count",
      "price_change": "percentage change",
      "ai_reasoning": "AI analysis explanation",
      "trading_params": {
        "limit_order_price": "suggested entry",
        "take_profit_price": "profit target",
        "stop_loss_price": "stop loss level",
        "time_frame": "recommended duration"
      }
    }
  ]
}
```

## System Architecture

### Token Scanner (app.py)
- Queries database for recent token activity
- Fetches market data from GeckoTerminal
- AI filtering and evaluation
- Signal generation and notification delivery
- Trade recording to database

### Position Monitor (scanner.py)
- Independent monitoring of open positions
- Price tracking via Jupiter and Birdeye APIs
- Automatic position closing on TP/SL/expiration
- Performance metrics calculation

### Database Integration
- SQL Server backend for persistent storage
- Trade history with full metrics
- Position tracking and outcome analysis

## Signal Distribution

Signals are delivered via:
- **Telegram**: Real-time notifications to configured channel
- **GitHub**: Automated orderbook updates (top 3 signals)
- **Local Storage**: Complete orderbook with all analyzed tokens

## AI Analysis Methodology

The system uses a multi-stage analysis approach:

1. **Initial Filtering**: Volume, transaction count, holder metrics
2. **AI Selection**: LLM reviews all candidates and selects promising tokens
3. **Deep Analysis**: Fetches recent trade history for selected tokens
4. **Parameter Generation**: AI creates dynamic trading parameters based on:
   - Recent vs historical buy pressure
   - Trade flow momentum (accelerating/decelerating/stable)
   - Volume and liquidity conditions
   - Price volatility patterns

## Performance Tracking

All trades are tracked with comprehensive metrics:
- Entry and exit prices
- Time to completion
- Final P&L percentage
- Peak profit reached (highest price)
- Maximum drawdown (lowest price)
- Number of price checks performed

## Disclaimer

This system is for educational and research purposes. All trading signals are generated algorithmically and should not be considered financial advice. Cryptocurrency trading carries significant risk. Always conduct your own research and never invest more than you can afford to lose.

## Technical Stack

- Python 3.8+
- aiohttp for async HTTP requests
- aioodbc for database connectivity
- Local LLM (Ollama) for AI analysis
- GeckoTerminal API for market data
- Jupiter & Birdeye APIs for price feeds
- Telegram Bot API for notifications

---

**Last Updated**: Auto-generated after each scan cycle
**Scan Frequency**: Configurable (default: 5 minutes)
**Data Sources**: GeckoTerminal, Jupiter, Birdeye
