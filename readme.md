# Amplify Integration - Stock API

A stock quote and watch list API based on [**Finnhub**](https://finnhub.io/) created in Amplify Integration.

The project exposes two end points
* `GET /quote?symbol=AAPL`
* `GET /watchlist?symbols=AAPL,INTC,TXN,NVDA,AMZN,MSFT`

The `quote` API is basically a pass through of the Finnhub Stock quote API with a field mapped payload. It takes a single symbol as a query parameter. The `watchlist` API returns an array of stock quotes suitable for a watch list. It takes a comma separated list of symbols.

The project is intended to be a simple example of how to expose API endpoints and map and aggregate data in Amplify Integration.

An OpenAPI 3.0 doc is provided as well.

## Quote

`GET /quote?symbol=AAPL`

```json
{
  "Price": 212.49,
  "Change": -1.75,
  "ChangePercent": -0.8168,
  "DayHigh": 215.17,
  "DayLow": 211.3,
  "OpenPrice": 213.81,
  "PreviousClose": 214.24
}
```

## Watchlist

* `GET /watchlist?symbols=AAPL,INTC,TXN,NVDA,AMZN,MSFT`

```json
[
  {
    "Price": 212.49,
    "Change": -1.75,
    "ChangePercent": -0.8168,
    "DayHigh": 215.17,
    "DayLow": 211.3,
    "OpenPrice": 213.81,
    "PreviousClose": 214.24
  },
  {
    "Price": 30.45,
    "Change": -0.01,
    "ChangePercent": -0.0328,
    "DayHigh": 30.56,
    "DayLow": 30.23,
    "OpenPrice": 30.285,
    "PreviousClose": 30.46
  },
  {
    "Price": 193.9,
    "Change": -2.38,
    "ChangePercent": -1.2126,
    "DayHigh": 195.6275,
    "DayLow": 193.07,
    "OpenPrice": 193.84,
    "PreviousClose": 196.28
  },
  {
    "Price": 131.88,
    "Change": 2.27,
    "ChangePercent": 1.7514,
    "DayHigh": 132.835,
    "DayLow": 128.32,
    "OpenPrice": 129.94,
    "PreviousClose": 129.61
  },
  {
    "Price": 183.66,
    "Change": -0.17,
    "ChangePercent": -0.0925,
    "DayHigh": 183.72,
    "DayLow": 182.23,
    "OpenPrice": 182.99,
    "PreviousClose": 183.83
  },
  {
    "Price": 442.57,
    "Change": 0.99,
    "ChangePercent": 0.2242,
    "DayHigh": 443.1376,
    "DayLow": 436.721,
    "OpenPrice": 438.42,
    "PreviousClose": 441.58
  }
]
```

## Installation

* Import the `StockQuoteFH.zip` project into Amplify Integration
* Edit the Finnhub connector and enter your API Key
  * You can get an API Key [**here**](https://finnhub.io/)
* Enable your integrations
* Call your API