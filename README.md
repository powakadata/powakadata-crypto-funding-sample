# Crypto Perpetual Funding Rate + Open Interest (Free Sample)

Historical **funding rates**, **mark price**, and **open interest** for the 8 largest
Binance USDT perpetual futures — full funding history back to **2019**.

Most free crypto datasets only give you OHLCV. Funding rate + open interest history per
perpetual is rare and hard to find for free — and it's exactly what you need for
**funding-carry research, basis trades, and realistic perpetual-futures backtests**.

This is a free 8-symbol sample from [PowakaData](https://powakadata.com). The full product
covers **900+ perpetual contracts** (Binance + OKX) with all timeframes (1m → 1d), order
book depth, mark price OHLC, and premium index.

> Also on Kaggle: [Crypto Perpetual Funding Rates & Open Interest](https://www.kaggle.com/datasets/powakadata/crypto-perpetual-funding-rates-and-open-interest)

## Symbols

`BTCUSDT` · `ETHUSDT` · `SOLUSDT` · `BNBUSDT` · `XRPUSDT` · `DOGEUSDT` · `ADAUSDT` · `AVAXUSDT`

One CSV per symbol: `{SYMBOL}_funding_oi.csv`

## Columns

| Column | Description |
|--------|-------------|
| `symbol` | Perpetual contract, e.g. `BTCUSDT` |
| `datetime_utc` | Funding timestamp (UTC), 8-hour interval (00:00 / 08:00 / 16:00) |
| `funding_rate` | Funding rate applied at that timestamp |
| `mark_price` | Mark price at the funding moment |
| `open_interest` | Open interest (contracts), aligned to the funding timestamp |
| `open_interest_value` | Open interest notional value (USDT) |

Funding + mark price cover full history; open interest history is shorter (exchange
limitation), so older rows have empty OI fields.

## Quick start

```python
import pandas as pd

df = pd.read_csv("BTCUSDT_funding_oi.csv", parse_dates=["datetime_utc"])

# Average funding by year
print(df.set_index("datetime_utc")["funding_rate"].resample("YE").mean())

# Cumulative funding paid by a perpetual long (rough carry proxy)
df["cum_funding"] = df["funding_rate"].cumsum()
```

Or load every symbol at once with the included `load_funding_data.py`:

```python
from load_funding_data import load_all
df = load_all()          # all 8 symbols in one DataFrame
```

## What this is good for

- Funding-rate carry / basis-trade research
- Backtesting perpetual-futures strategies with realistic funding costs
- Studying open-interest dynamics around price moves
- Cross-exchange funding comparison (full set includes OKX)

## Full dataset

900+ perpetuals across Binance and OKX, all timeframes, order book depth, mark price OHLC,
and premium index — **[powakadata.com](https://powakadata.com)**

## License

Free sample provided for research and evaluation. See [powakadata.com](https://powakadata.com)
for terms on the full dataset.
