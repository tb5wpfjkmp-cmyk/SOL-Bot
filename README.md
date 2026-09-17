# SOL-Bot

A ready-to-run Solana market-monitoring project that fetches SOL/USD data, calculates technical indicators, produces transparent informational market signals, optionally sends SMS alerts, provides a Streamlit dashboard, and runs automatically with GitHub Actions.

> **Important:** This project is for research, education, and alerts. It does not place trades. Signals are not guarantees of future returns.

## Features

- SOL/USD market data from CoinGecko
- RSI(14), MACD(12/26/9), EMA(20/50)
- 20-day relative-volume detection
- Trend/momentum/FOMO-style analysis
- `BUY-WATCH`, `HOLD-WATCH`, and `SELL-WATCH` informational labels
- Historical directional backtest
- Optional Twilio SMS alerts
- Streamlit dashboard
- Scheduled GitHub Actions workflow
- Secrets kept out of source code

## Structure

```text
SOL-Bot/
├── src/
│   ├── __init__.py
│   ├── config.py
│   ├── market_data.py
│   ├── indicators.py
│   ├── signal.py
│   ├── backtest.py
│   ├── sms.py
│   └── main.py
├── dashboard/
│   └── app.py
├── tests/
│   └── test_indicators.py
├── .github/workflows/
│   └── sol-alert.yml
├── .env.example
├── .gitignore
├── requirements.txt
└── README.md
```

## Run locally

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
cp .env.example .env
python -m src.main
```

On Windows PowerShell, activate the environment with:

```powershell
.venv\Scripts\Activate.ps1
```

### Dashboard

```bash
streamlit run dashboard/app.py
```

### Backtest

```bash
python -m src.backtest
```

## SMS setup

The bot uses Twilio when `SEND_SMS=true`.

Configure these environment variables locally in `.env`, or as GitHub Actions repository secrets:

- `TWILIO_ACCOUNT_SID`
- `TWILIO_AUTH_TOKEN`
- `TWILIO_FROM_NUMBER`
- `TWILIO_TO_NUMBER`

Use E.164 phone-number format, such as `+15551234567`.

Test with `SEND_SMS=false` first.

## GitHub Actions

The included workflow can be launched manually or runs once per day.

In GitHub, add secrets under:

**Settings → Secrets and variables → Actions → New repository secret**

Then use:

**Actions → SOL Alert → Run workflow**

The sample cron is `0 15 * * *`. GitHub Actions cron schedules are UTC, so edit the workflow if you want a different alert time.

## Signal logic

The default engine is intentionally transparent rather than pretending to predict the market. It combines:

- EMA20 vs EMA50 trend
- MACD vs signal line
- RSI
- relative volume
- a FOMO-style momentum warning

A score of `>= 4` becomes `BUY-WATCH`; `<= -4` becomes `SELL-WATCH`; everything else is `HOLD-WATCH`.

These are research labels, not instructions to buy or sell.

## Data source

CoinGecko API is used for current and historical SOL market data. You can optionally supply a CoinGecko demo API key with `COINGECKO_API_KEY`.

## Disclaimer

This software is not financial advice. Cryptocurrency is volatile and can result in substantial losses. Backtests can overfit and historical performance does not guarantee future results.
