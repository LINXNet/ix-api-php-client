# IX-API PHP Client

[![Latest Stable Version][packagist-image]][packagist-url]
[![Github Issues][github-issues-image]][github-issues-url]

A lightweight PHP API client for the [IX-API](https://ix-api.net).

## Installation

To install, run `composer require dant89/ixapi-client` in the root of your project or add `dant89/ix-api-client` to your composer.json.

View the tagged versions to choose between `v1` and `v2` implementations of this client.
```json
"require": {
    "dant89/ix-api-client": "^LATEST_VERSION_TAG"
}
```

## Usage

Use your provided key / secret credentials for the given implementor URL to return and then set a bearer token:

```php
use Dant89\IXAPIClient\Client;

// Create base client
$client = new Client(IXAPI_URL);

// Get a bearer token from key / secret
$response = $client->getHttpClient(HttpClientType::AUTH)
    ->postAuthToken(IXAPI_KEY, IXAPI_SECRET);

// Check for valid response status
if ($response->getStatus() === 200) {
    $client->setBearerToken($response->getContent()['access_token']);
}
```

With the bearer token set, you can return data from all endpoints that require authentication.

**Get Product Offerings:**
```php
// Query for products
$response = $client->getHttpClient(HttpClientType::PRODUCT_OFFERINGS)
    ->getProductOfferingss();

// Check for valid response and set the array of products
if ($response->getStatus() === 200) {
    $productOfferings = $response->getContent();
}
````
**Get Connections Statistical Timeseries Data:**
```php
// Query for connections timeseries data
$response = $client->getHttpClient(HttpClientType::CONNECTIONS)
    ->getStatisticTimeseries('connection-123-uuid', '30d');

// Check for valid response and set the array of products
if ($response->getStatus() === 200) {
    $timeseries = $response->getContent();
}
````

## Authentication

You will need to contact an exchange to create an API key / secret combination and find out the URL of their IX-API implementation.

## Questions

Q. The IX-API is OpenAPI 3 compliant, why don't I just create a client using a tool such as [Swagger Codegen](https://github.com/swagger-api/swagger-codegen)?

A. Please do! This client is intended to be very lightweight and something you can use to jump in, build on and experiment with. Clients generated by automated tools, such as [Swagger Codegen](https://github.com/swagger-api/swagger-codegen) can have more depth and functionality that you may find your application requires.


## Contributions

Contributions to the client are welcome, to contribute please:

1. Fork this repository
2. Create your feature branch
3. Commit your changes
4. Push to the branch
5. Create a new pull request

[packagist-image]: https://img.shields.io/packagist/vpre/dant89/ix-api-client.svg
[packagist-url]: https://packagist.org/packages/dant89/ix-api-client

[github-issues-image]: https://img.shields.io/github/issues/dant89/ix-api-php-client
[github-issues-url]: https://github.com/dant89/ix-api-php-client/issues
