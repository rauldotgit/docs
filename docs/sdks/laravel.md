---
sidebar_position: 2
---

# Laravel

We have a composer package for Laravel framework  - (https://packagist.org/packages/abrouter/laravel-abtest).
You can see the source code by the following URL: (https://github.com/abrouter/laravel-abtest).

If you need an example of step-by-step implementing A/B test you can see the example on [ABRouter website](https://abrouter.com/en/laravel-ab-tests)

## Short guide how to install

To get a complete guide please visit the links above.

```bash
$ composer require abrouter/laravel-abtest
```

### Setting service provider

This package provide auto discovery for service provider

If Laravel package auto-discovery is disabled, add service providers manually to /config/app.php. There are service provider you must add:

```
\Abrouter\LaravelClient\Providers\AbrouterServiceProvider::class
```

### Publish client configuration

```
php artisan vendor:publish --tag=abrouter
```

### Configure ABRouter client

Put your ABRouter token in /config/abrouter.php. You can find this token in [ABRouter dashboard](https://abrouter.com/en/board):
```javascript
<?php
return [
    'token' => '14da89de1713a74c1ed50aafaff18c24bf372a9913e67e6a7a915def3332a97c9c9ecbe2cd6d3047',
    'host' => 'https://abrouter.com',
];
```

### Configure Parallel running

Parallel running is a feature that allows you to run A/B tests asynchronously.
It requires ready-to-use Laravel cache (probably by Redis).

This feature enables caching of experiment branches to run the experiment locally, then using Laravel built-in queues to sync the data with ABRouter server.
Please make sure, your supervisor config, queues and caching storage is enabled in Laravel to use.

Parallel running allows to run your A/B tests without blocking.
Additionally, you can configure it on your own.


## :rocket: Running A/B tests

```javascript
<?php
use Abrouter\Client\Client;

class ExampleController
{
    public function __invoke(Client $client)
    {
        $buttonColor = $client->experiments()->run(uniqid(), 'D1D06000-0000-0000-00005030');
        return view('button', [
            'color' => $buttonColor->getBranchId(),
        ]);
    }
}
```

## :rocket: Running feature flags

```php
use Abrouter\Client\Client;

class ExampleController
{
    public function __invoke(Client $client)
    {
        $isEnabledButton = $client->featureFlags()->run('enabled_button_feature_flag');

        return view('featureFlags', [
            'enabledButtonFeatureFlag' => $isEnabledButton,
        ]);
    }
}
```

## :rocket: Sending the stats

```php
use Abrouter\Client\Client;

class ExampleController
{
    public function __invoke(Client $client)
    {
        //ABRouter can store more data. Please learn more in EventDTO arguments.
        $client->statistics()->sendEvent(new EventDTO(
            null,
            $userId,
            'visited_test_page'
        ));
    }
}
```

Please note, you can use the IncrementalEventDTO (Abrouter\Client\DTO\IncrementalEventDTO) if you would like to send the increment counter statistics, and SummarizeEventDTO(same namespace) to track some sum. 

### Managing UI

You can create an experiment/feature flags and set up statistics and get your token and id of experiment on [ABRouter](https://abrouter.com) or just read the [docs](https://abrouter.com/en/docs).



### Example

You can get an dockerized usage example by the following link: https://github.com/abrouter/laravel-example

