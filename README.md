# IX-API PHP API Client

[![Latest Stable Version][packagist-image]][packagist-url]
[![Github Issues][github-issues-image]][github-issues-url]

PHP API client for the [IX-API](https://ix-api.net).

## Installation

To install, run `composer require dant89/ixapi-client` in the root of your project or add `dant89/ix-api-client` to your composer.json.
```json
"require": {
    "dant89/ix-api-client": "^0.0.1"
}
```

## Usage

The following is a simple example of how you could use this client to get a list of products from an implementor of the API.

```php
<?php

require('vendor/autoload.php');

use Dant89\IXAPIClient\Client;

// Create base client
$client = new Client(IXAPI_URL);

// Declare authentication variables
$key = IXAPI_KEY;
$secret = IXAPI_SECRET;

// Get a bearer token from key / secret
$authClient = $client->getHttpClient('auth');
$authResponse = $authClient->postAuthToken($key, $secret);
$authContent = $authResponse->getContent();

// Authenticate
$client->setBearerToken($authContent['access_token']);

// Get a list of products
$productClient = $client->getHttpClient('product');
$productResponse = $productClient->getProducts();
$products = $productResponse->getContent();

foreach ($products as $product) {
    echo $product['name'] . "\n";
}

```

## Authentication

You will need to speak directly to an exchange to be provided with an API key / secret combination and the URL of their IX-API implementation.

## Contributions

Contributions to the client are welcome, to contribute please:

1. Fork this repository
2. Create your feature branch
3. Commit your changes
4. Push to the branch
5. Create a new Pull Request

[packagist-image]: https://img.shields.io/packagist/vpre/dant89/ix-api-client.svg
[packagist-url]: https://packagist.org/packages/dant89/ix-api-client

[github-issues-image]: https://img.shields.io/github/issues/dant89/ix-api-php-client
[github-issues-url]: https://github.com/dant89/ix-api-php-client/issues
