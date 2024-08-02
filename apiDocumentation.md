# Integration API Standards

## Endpoints

1. [Market Data Overview](#market-data-overview)
   - **URL**: `https://spotapi.foruspf.com/v1/spot/summary`
   - **Description**: Overview of market data for all tickers and all markets.

2. [Crypto Assets Details](#crypto-assets-details)
   - **URL**: `https://walletapi.foruspf.com/v1/wallet/assets`
   - **Description**: In-depth details on cryptocurrencies available on the exchange.

3. [24-Hour Price Change Statistics](#24-hour-price-change-statistics)
   - **URL**: `https://spotapi.foruspf.com/v1/spot/ticker`
   - **Description**: 24-hour rolling window price change statistics for all markets.

4. [Market Depth](#market-depth)
   - **URL**: `https://spotapi.foruspf.com/v1/spot/orderbook`
   - **Description**: Market depth of a trading pair. Contains lists of ask and bid prices.

5. [Recent Trades](#recent-trades)
   - **URL**: `https://spotapi.foruspf.com/v1/spot/trades`
   - **Description**: Recently completed trades for a given market. 24-hour historical full trades available as a minimum requirement.

## Endpoint Details

### Market Data Overview

**Endpoint**: `v1/spot/summary`

**Method**: GET

**Example Response**:
```json
[
   {
       "trading_pairs": "BNB_USDT",
       "last_price": 788881688.241272,
       "base_volume": 285160.136,
       "quote_volume": 61610811.4505,
       "highest_price_24h": 218.8,
       "lowest_price_24h": 213.6,
       "price_change_percent_24h": 0.603,
       "lowest_ask": 860337790.041287,
       "highest_bid": 750636034.388173
   }
]
