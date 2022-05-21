---
sidebar_position: 1
---

# PHP

We have a composer package for vanilla PHP  - https://packagist.org/packages/abrouter/abrouter-php-client.

You can see the source code by the following URL: (https://github.com/abrouter/abrouter-php-client).

If you need an example of step-by-step implementing A/B test you can see the example on [ABRouter website](https://abrouter.com/en/php-how-to-launch-ab-tests-in-5-minutes)

## Short guide how to install

To get a complete guide please visit the links above.

## :package: Install
Via composer

``` bash
$ composer require abrouter/abrouter-php-client
```

## :rocket: Usage

Client is uses [PHP-DI](https://github.com/PHP-DI/PHP-DI) for DI. If you're uses own DI, you must to configure it in a such way as on example below.
If you're not uses any DI, let's move php-di from dev-dependency to dependency:
``` bash
$ composer require "php-di/php-di": "^6.0"
```

### Using with PHP-DI

```javascript
use Abrouter\Client\Config\Config;
use DI\ContainerBuilder;
use Abrouter\Client\Client;

require '/app/vendor/autoload.php';

$containerBuilder = new ContainerBuilder();
$di = $containerBuilder->build();

$token = '04890788ba2c89c4ff21668c60838a00a87b1cf42c9c6b45d6aa8e11174f0d5762b16b6c09b6b822'; //you can find your token in ABRouter dashboard

$di->set(Config::class, new Config($token, 'https://abrouter.com'));
/**
 * @var Client $client
 */
$client = $di->make(Abrouter\Client\Client::class);
$userSignature = uniqid();
$experimentId = 'B95AC000-0000-0000-00005030';//experiment id is also there


$runExperimentResult = $client->experiments()->run($userSignature, $experimentId);
$experimentId = $runExperimentResult->getExperimentId(); //form-color
$branchId = $runExperimentResult->getBranchId(); //red
echo '<button style="color: '. $branchId .'">Hello</button>';
```

You can create an experiment and get your token and id of experiment on [ABRouter](https://abrouter.com) or just read the [docs](https://abrouter.com/en/docs).

## :white_check_mark: Testing
Requires docker-compose and docker installed.

``` bash
$ make up
$ make test-run
```

