dwollaphp
=========

[![Build Status](https://travis-ci.org/mach-kernel/dwollaphp.svg?branch=master)](https://travis-ci.org/mach-kernel/dwollaphp)

The new and improved Dwolla library based off of the Guzzle REST client. `dwollaphp` includes support for all API endpoints, and is the new library officially supported by Dwolla. 

## Version

2.0.0

## Installation

`dwollaphp` is available on [Packagist](http://packagist.org), and therefore can be installed automagically via [Composer](http://getcomposer.org).

**The PHP JSON and CURL extensions are required for `dwollaphp` to operate.** 

*To install without adding to `composer.json`:*

```
composer install dwollaphp
```

*To add to `composer.json` and make this a permanent dependency of your package:*
```
composer require "dwolla/dwollaphp=2.*"
composer update && composer install
```

## Quickstart

`dwollaphp` makes it easy for developers to hit the ground running with our API. Before attempting the following, you should ideally create [an application key and secret](https://www.dwolla.com/applications).

* Set any variables in `_settings.php` or the `Settings` class. All fields are public.
* Instantiate `dwollaphp` with the class that contains the endpoints you require.
* Use at will!

```php
require '../lib/account.php';
$Account = new Dwolla\Account();

/**
 * Example 1: Get basic information for
 * a Dwolla user using their Dwolla ID.
 */
print_r($Account->basic('812-121-7199'));
```

---

There are 8 quickstart files which will walk you through working with `dwollaphp`'s classes/endpoint groupings. 

* `account.php`: Retrieve account information, such as balance.
* `checkouts.php`: Offsite-gateway endpoints, server-to-server checkout example.
* `contacts.php`: Retrieve/sort through user contacts.
* `fundingSources.php`: Modify and get information with regards to funding sources.
* `masspay.php`: Create and retrieve jobs/data regarding MassPay jobs. 
* `oauth.php`: Examples on retrieving OAuth access/refresh token pairs.
* `requests.php`: Create and retrieve money requests/information regarding money requests.
* `transactions.php`: Send money, get transaction info by ID, etc.

## Structure

`dwollaphp` is a conglomerate of multiple classes; each file in the `lib/` directory contains a class which contains all the endpoints for that certain category ([similar to Dwolla's developer documentation](https://developers.dwolla.com/dev/docs)). 

### Endpoint Classes / Methods

Each endpoint class extends `RestClient` located in `client.php` (e.g. `RestClient::Account()`).

* `Account()`:
 * `basic()`: Retrieves basic account information
 * `full()`: Retrieve full account information
 * `balance()`: Get user balance
 * `nearby()`: Get nearby users
 * `getAutoWithdrawal()`: Get auto-withdrawal status
 * `toggleAutoWithdrawal()`: Toggle auto-withdrawal
* `Checkouts()`:
 * `resetCart()`: Clears out item cart.
 * `addToCart()`: Adds item to cart.
 * `create()`: Creates a checkout session.
 * `get()`: Gets status of existing checkout session.
 * `complete()`: Completes a checkout session.
 * `verify()`: Verifies a checkout session.
* `Contacts()`:
 * `get()`: Retrieve a user's contacts.
 * `nearby()`: Get spots near a location.
* `FundingSources()`:
 * `info()`: Retrieve information regarding a funding source via ID.
 * `get()`: List all funding sources.
 * `add()`: Add a funding source.
 * `verify()`: Verify a funding source.
 * `withdraw()`: Withdraw from Dwolla into funding source.
 * `deposit()`: Deposit to Dwolla from funding source.
* `MassPay()`:
 * `create()`: Creates a MassPay job.
 * `getJob()`: Gets a MassPay job.
 * `getJobItems()`: Gets all items for a specific job.
 * `getItem()`: Gets an item from a specific job.
 * `listJobs()`: Lists all MassPay jobs.
* `OAuth()`:
 * `genAuthUrl()`: Generates OAuth permission link URL
 * `get()`: Retrieves OAuth + Refresh token pair from Dwolla servers.
 * `refresh()`: Retrieves OAuth + Refresh pair with refresh token.
* `Requests()`:
 * `create()`: Request money from user.
 * `get()`: Lists all pending money requests.
 * `info()`: Retrieves info for a pending money request.
 * `cancel()`: Cancels a money request.
 * `fulfill()`: Fulfills a money request.
* `Transactions()`:
 * `send()`: Sends money
 * `refund()`: Refunds money
 * `get()`: Lists transactions for user
 * `info()`: Get information for transaction by ID.
 * `stats()`: Get transaction statistics for current user.

### Internal Use

`client.php/RestClient()` is the base class for all of the aforementioned classes, `_settings.php/Settings()` does not inherit from anything and only contains configuration parameters. 

## Unit Testing

`dwollaphp` uses [PHPUnit](https://phpunit.de/) for unit testing. These tests do not test integration and will occassionally show console API errors due to 'dummy' data being used. Integration testing is planned sometime in the future. 

To run the tests, install `require\dev` from `composer.json` and run:

```
cd tests
../vendor/bin/phpunit
```

## Changelog

2.0.0
* Initial release

## Credits

This wrapper is based on [Guzzle](https://github.com/guzzle/guzzle) for REST capability and uses [PHPUnit](https://phpunit.de/) for unit testing and [Travis](https://travis-ci.org/) for automagical build verification. 

Initially written by [David Stancu](http://davidstancu.me) (david@dwolla.com).

## License

Copyright (c) 2014 Dwolla Inc, David Stancu

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
