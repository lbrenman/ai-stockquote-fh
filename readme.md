# Amplify Integration - Stock API

A stock quote and watch list API based on [**Finnhub**](https://finnhub.io/) created in Amplify Integration.

The project exposes two end points
* `GET /quote?symbol=AAPL`
* `GET /watchlist?symbols=AAPL,INTC,TXN,NVDA,AMZN,MSFT`

The `quote` API is basically a pass through of the Finnhub Stock quote API with a field mapped payload. It takes a single symbol as a query parameter. The `watchlist` API returns an array of stock quotes suitable for a watch list. It takes a comma separated list of symbols.

A sample Nodejs web app that uses the API's can be found [here](https://github.com/lbrenman/Stock-Nodejs-Web-app-to-Fusion-FH-Stock-api)

The project is intended to be a simple example of how to expose API endpoints and map and aggregate data in Amplify Integration using three method:
* HTTP Server - contractless
* HTTP Server - contractless using a common service
* API Server - using OAS Doc as starting point and leveraginG same common service

The OpenAPI 3.0 doc is provided in this repository as well

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

* Import the `StockQuoteFH.zip` project into Amplify Fusion tenant
* Edit the Finnhub OpenAPI connector override in Manager and enter your API Key which you can get  [**here**](https://finnhub.io/). Other values can be found in the project Finnhub OpenAPI connector
* Enable API and get URL
* Call your APIs