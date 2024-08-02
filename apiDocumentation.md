Here is the markdown file for GitHub with the table sections formatted as code:

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
```

**Description**:

```
| Name                    | Type    | Description                                                                                       |
|-------------------------|---------|---------------------------------------------------------------------------------------------------|
| `trading_pairs`         | string  | Identifier of a ticker with delimiter to separate base/quote, eg. BTC-USD (Price of BTC in USD)    |
| `last_price`            | decimal | Last transacted price of base currency based on given quote currency                              |
| `lowest_ask`            | decimal | Lowest Ask price of base currency based on given quote currency                                   |
| `highest_bid`           | decimal | Highest bid price of base currency based on given quote currency                                  |
| `base_volume`           | decimal | 24-hr volume of market pair denoted in BASE currency                                              |
| `quote_volume`          | decimal | 24-hr volume of market pair denoted in QUOTE currency                                             |
| `price_change_percent_24h` | decimal | 24-hr % price change of market pair                                                              |
| `highest_price_24h`     | decimal | Highest price of base currency based on given quote currency in the last 24-hrs                   |
| `lowest_price_24h`      | decimal | Lowest price of base currency based on given quote currency in the last 24-hrs                    |

### Crypto Assets Details

**Endpoint**: `v1/wallet/assets`

**Method**: GET

**Example Response**:
{
   "USDT": {
       "name": "tether",
       "unified_cryptoasset_id": "64e83245bd73775ff9e42b3b",
       "can_withdraw": true,
       "can_deposit": true,
       "min_withdraw": 10,
       "max_withdraw": 1000,
       "contractAddress": "0x6d630CAA9bed9bB32F04e97e393E2C254ea95E17, 0x04BE679b492Ffa75f8436a9bc6f98642417f4B63, 0x04BE679b492Ffa75f8436a9bc6f98642417f4B63"
   },
   "BUSD": {
       "name": "BUSD",
       "unified_cryptoasset_id": "64f2fdad8708a5a45baf7372",
       "can_withdraw": true,
       "can_deposit": true,
       "min_withdraw": 10.003,
       "max_withdraw": 1000,
       "contractAddress": "0x3a3Ba980b92E63F9faFd27E821E461115140B84F"
   }
}


**Description**:


| Name                | Type    | Description                                                        |
|---------------------|---------|--------------------------------------------------------------------|
| `name`              | string  | Full name of cryptocurrency                                        |
| `unified_cryptoasset_id` | integer | Unique ID of cryptocurrency assigned                              |
| `can_withdraw`      | boolean | Identifies whether withdrawals are enabled or disabled             |
| `can_deposit`       | boolean | Identifies whether deposits are enabled or disabled                |
| `contractAddress`   | string  | Contract address of the asset on each chain                        |
| `min_withdraw`      | decimal | Single minimum withdrawal amount of a cryptocurrency               |
| `max_withdraw`      | decimal | Single maximum withdrawal amount of a cryptocurrency               |


### 24-Hour Price Change Statistics

**Endpoint**: `v1/spot/ticker`

**Method**: GET

**Example Response**:
```json
{
   "BNB_USDT": {
       "last_price": 2318714509.752429,
       "quote_volume": 285160.136,
       "base_volume": 61610811.4505
   },
   "BTC_USDT": {
       "last_price": 28207.51,
       "quote_volume": 73848.12186,
       "base_volume": 2092325338.516788
   },
   "BNB_BTC": {
       "last_price": 0.00755,
       "quote_volume": 31222.052,
       "base_volume": 235.41468856
   }
}


**Description**:


| Name           | Type    | Description                                                |
|----------------|---------|------------------------------------------------------------|
| `last_price`   | decimal | Last transacted price of base currency based on quote currency |
| `base_volume`  | decimal | 24-hour trading volume denoted in BASE currency            |
| `quote_volume` | decimal | 24-hour trading volume denoted in QUOTE currency           |


### Market Depth

**Endpoint**: `v1/spot/orderbook`

**Method**: GET

**Example Query**: `v1/spot/orderbook?pair=BTCUSDT`

**Example Response**:

{
   "timestamp": 1697519512669,
   "bids": [
       [30441.1716, 0.2]
   ],
   "asks": [
       [25931.9848, 8.67]
   ]
}


**Description**:


| Name       | Type    | Description                                                      |
|------------|---------|------------------------------------------------------------------|
| `timestamp`| integer | Unix timestamp in milliseconds for when the last update occurred |
| `bids`     | decimal | Array containing 2 elements: offer price and quantity for each bid order |
| `asks`     | decimal | Array containing 2 elements: ask price and quantity for each ask order |


### Recent Trades

**Endpoint**: `v1/spot/trades`

**Method**: GET

**Example Query**: `v1/spot/trades?pair=BTCUSDT`

**Example Response**:

[
   {
       "timestamp": 1697095081.201,
       "trade_id": "65279da9ad2261e56b2713ba",
       "price": 49.118105,
       "type": "sell",
       "base_volume": 10.227074,
       "quote_volume": 502.33449457477
   }
]


**Description**:


| Name          | Type    | Description                                                        |
|---------------|---------|--------------------------------------------------------------------|
| `trade_id`    | integer | Unique ID associated with the trade for the currency pair transaction |
| `price`       | decimal | Last transacted price of base currency based on quote currency      |
| `base_volume` | decimal | Transaction amount in BASE currency                                 |
| `quote_volume`| decimal | Transaction amount in QUOTE currency                                |
| `timestamp`   | integer | Unix timestamp in milliseconds for when the transaction occurred    |
| `type`        | string  | Indicates whether the transaction originated as a buy or sell       |
