scheb/yahoo-finance-api
=======================

This is a PHP client for Yahoo Finance API.

Since YQL APIs have been discontinued in November 2017, this client is using non-official API endpoints for quotes, search and historical data.

**WARNING:** These non-official APIs cannot be assumed stable and might break any time. Also, you might violate Yahoo's terms of service. So use them at your own risk.

[![Build Status](https://travis-ci.org/scheb/yahoo-finance-api.svg?branch=master)](https://travis-ci.org/scheb/yahoo-finance-api)
[![PHP 7 ready](http://php7ready.timesplinter.ch/scheb/yahoo-finance-api/badge.svg)](https://travis-ci.org/scheb/yahoo-finance-api)
[![Coverage Status](https://coveralls.io/repos/scheb/yahoo-finance-api/badge.svg?branch=master&service=github)](https://coveralls.io/github/scheb/yahoo-finance-api?branch=master)
[![Latest Stable Version](https://poser.pugx.org/scheb/yahoo-finance-api/v/stable.svg)](https://packagist.org/packages/scheb/yahoo-finance-api)
[![License](https://poser.pugx.org/scheb/yahoo-finance-api/license.svg)](https://packagist.org/packages/scheb/yahoo-finance-api)

## Installation

Download via Composer:

```bash
php composer.phar require scheb/yahoo-finance-api
```

Alternatively you can also add the bundle directly to composer.json:

```json
{
    "require": {
        "scheb/yahoo-finance-api": "^3.0"
    }
}
```

and then tell Composer to install the bundle:

```bash
php composer.phar update scheb/yahoo-finance-api
```

## Usage

```php
use Scheb\YahooFinanceApi\ApiClient;
use Scheb\YahooFinanceApi\ApiClientFactory;
use GuzzleHttp\Client;

// Create a new client from the factory
$client = ApiClientFactory::createApiClient();

// Or use your own Guzzle client and pass it in
$options = [/*...*/];
$guzzleClient = new Client($options);
$client = ApiClientFactory::createApiClient($guzzleClient);

// Returns an array of Scheb\YahooFinanceApi\Results\SearchResult
$searchResult = $client->search("Apple");

// Returns an array of Scheb\YahooFinanceApi\Results\HistoricalData
$historicalData = $client->getHistoricalData("AAPL", ApiClient::INTERVAL_1_DAY, new \DateTime("-14 days"), new \DateTime("today"));

// Returns Scheb\YahooFinanceApi\Results\Quote
$exchangeRate = $client->getExchangeRate("USD", "EUR");

// Returns an array of Scheb\YahooFinanceApi\Results\Quote
$exchangeRates = $client->getExchangeRates([
    ["USD", "EUR"],
    ["EUR", "USD"],
]);

// Returns Scheb\YahooFinanceApi\Results\Quote
$quote = $client->getQuote("AAPL");

// Returns an array of Scheb\YahooFinanceApi\Results\Quote
$quotes = $client->getQuotes(["AAPL", "GOOG"]);
```
