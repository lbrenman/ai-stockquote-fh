# Amplify Integration - Stock API

A stock quote and watch list API based on [**Finnhub**](https://finnhub.io/) created in Amplify Integration.

The project exposes two end points
* `GET /quote?symbol=AAPL`
* `GET /watchlist?symbols=AAPL,INTC,TXN,NVDA,AMZN,MSFT`

The `quote` API is basically a pass through of the Finnhub Stock quote API with a field mapped payload. It takes a single symbol as a query parameter. The `watchlist` API returns an array of stock quotes suitable for a watch list. It takes a comma separated list of symbols.

The project is intended to be a simple example of how to expose API endpoints and map and aggregate data in Amplify Integration.

An OpenAPI 3.0 doc is provided as well

## Quote

`GET /quote?symbol=AAPL`

200 response:

```json
{
  "Price": 212.49,
  "Change": -1.75,
  "ChangePercent": -0.8168,
  "DayHigh": 215.17,
  "DayLow": 211.3,
  "OpenPrice": 213.81,
  "PreviousClose": 214.24,
  "Symbol": "AAPL",
  "Name": "Apple Inc"
}
```

Should return 204 on bad sysmbol

## Watchlist

* `GET /watchlist?symbols=AAPL,INTC,TXN,NVDA,AMZN,MSFT`

200 response:

```json
[
  {
    "Change": -1.75,
    "ChangePercent": -0.8168,
    "Price": 212.49,
    "Symbol": "AAPL",
    "Name": "Apple Inc"
  },
  {
    "Change": -0.01,
    "ChangePercent": -0.0328,
    "Price": 30.45,
    "Symbol": "INTC",
    "Name": "Intel Corp"
  },
  {
    "Change": -2.38,
    "ChangePercent": -1.2126,
    "Price": 193.9,
    "Symbol": "TXN",
    "Name": "Texas Instruments Inc"
  },
  {
    "Change": 2.27,
    "ChangePercent": 1.7514,
    "Price": 131.88,
    "Symbol": "NVDA",
    "Name": "NVIDIA Corp"
  },
  {
    "Change": -0.17,
    "ChangePercent": -0.0925,
    "Price": 183.66,
    "Symbol": "AMZN",
    "Name": "Amazon.com Inc"
  },
  {
    "Change": 0.99,
    "ChangePercent": 0.2242,
    "Price": 442.57,
    "Symbol": "MSFT",
    "Name": "Microsoft Corp"
  }
]
```

Bad symbols will not be added to array response
If all symbols are bad, then you will get a 204

## Installation

* Import the `StockQuoteFH.zip` project into Amplify Integration
* Edit the Finnhub connector and enter your API Key
  * You can get an API Key [**here**](https://finnhub.io/)
* Enable your integrations
* Call your API