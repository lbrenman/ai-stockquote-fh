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
    "Quote": {
        "OpenPrice": 236.18,
        "DayHigh": 236.18,
        "DayLow": 234.01,
        "Price": 235,
        "Change": 2.85,
        "ChangePercent": 1.2277,
        "Name": "Apple Inc",
        "Symbol": "AAPL"
    }
}
```

Returns 204 on bad symbol, 400 on missing query parameter and 500 on Finnhub API call error, all with the following schema:

```json
{
    "message": "Missing symbol"
}
```

## Watchlist

* `GET /watchlist?symbols=AAPL,INTC,TXN,NVDA,AMZN,MSFT`

200 response:

```json
{
    "Watchlist": [
        {
            "Price": 235,
            "Change": 2.85,
            "ChangePercent": 1.2277,
            "Symbol": "AAPL",
            "Name": "Apple Inc"
        },
        {
            "Price": 198.47,
            "Change": 0.17,
            "ChangePercent": 0.0857,
            "Symbol": "TXN",
            "Name": "Texas Instruments Inc"
        },
        {
            "Price": 22.77,
            "Change": 0.33,
            "ChangePercent": 1.4706,
            "Symbol": "INTC",
            "Name": "Intel Corp"
        }
    ]
}
```

Bad symbols will not be added to array response
Returns 204 if all symbols are bad
Returns 500 on Finnhub API call error
All with folowing schema:

```json
{
    "message": "Missing symbols"
}
```

## Installation

* Import the `StockQuoteFH2.zip` project into Amplify Integration
* Edit the Finnhub connector and enter your API Key
  * You can get an API Key [**here**](https://finnhub.io/)
* Enable your integrations
* Call your API