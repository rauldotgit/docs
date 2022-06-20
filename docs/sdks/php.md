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

```php
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
$experimentId = 'button_color';//experiment id is also there


$runExperimentResult = $client->experiments()->run($userSignature, $experimentId);
$experimentId = $runExperimentResult->getExperimentId(); //form-color
$branchId = $runExperimentResult->getBranchId(); //red
echo '<button style="color: '. $branchId .'">Hello</button>';
```

You can create an experiment and get your token and id of experiment on [ABRouter](https://abrouter.com) or just read the [docs](https://abrouter.com/en/docs).

## Sending the stats

```php
use Abrouter\Client\Config\Config;
use DI\ContainerBuilder;
use Abrouter\Client\Client;

require '/app/vendor/autoload.php';

$userId = uniqid();

$containerBuilder = new ContainerBuilder();
$di = $containerBuilder->build();

/**
 * @var Client $client
 */
$client = $di->make(Abrouter\Client\Client::class); // using PHP-DI
$client->statistics()->sendEvent(new EventDTO(
        null, // temporary user id 
        $userId, // permanent user id 
        'visited_test_page'
));
```

Please note, you can use the IncrementalEventDTO (Abrouter\Client\DTO\IncrementalEventDTO) if you would like to send the increment counter statistics, and SummarizeEventDTO(same namespace) to track some sum.


## Parallel running

Parallel running is a mode which allows you to run the experiments asynchronous.
Main things to make it works are configuring KvStorage and TaskManager.
KvStorage and TaskManager are using Redis to store data and tasks.


ABRouter php client has built-in KvStorage and TaskManager, but you can make your own implementation and replace it via DI and contracts.
We're highly recommend you to use built-in solution. The implementation is completely tested and works well. Using Parallel running gives you a great growth in speed.


The config for parallel running is a bit different from the default config.


### Configuration
```php
use Abrouter\Client\Config\Config;
use DI\ContainerBuilder;
use Abrouter\Client\Client;
use Abrouter\Client\Config\RedisConfig;
use Abrouter\Client\Contracts\KvStorageContract;
use Abrouter\Client\DB\RedisConnection;
use Abrouter\Client\Services\KvStorage\KvStorage;
use Abrouter\Client\Services\TaskManager\TaskManager;
        
require '/app/vendor/autoload.php';
        
$containerBuilder = new ContainerBuilder();
$di = $containerBuilder->build();


$redisConfig = new RedisConfig(
    $_SERVER['REDIS_HOST'] ?? 'redis',
    6379,
    '',
    '',
    ''
);

$host = 'https://abrouter.com';
$token = uniqid();

$config = new Config(
    $token,
    $host,
);
$config->setRedisConfig($redisConfig);
$container->set(Config::class, $config);

$kvStorage = $container->make(KvStorage::class);
$container->make(KvStorage::class);
$container->set(
    KvStorageContract::class,
    $kvStorage
);

$config->setKvStorageConfig($kvStorage);
$container->set(Config::class, $config);
$taskManager = $container->make(TaskManager::class);

$config->setParallelRunConfig(new ParallelRunConfig(true, $taskManager));
```

### Worker

Worker is a supervisor config which running the process which handles your tasks.
Make sure supervisor is installed on your machine. The example of supervisor config is located in worker/worker.conf.
Please, configure the worker.php before running the supervisor config.
You have to put the same configuration of the client there as in your main application.
Copy supervisor config to the specific folder which specified in etc/init.d/supervisord.conf.
And, please don't forget to adjust the path of worker.php aligned to your application base directory.


## :white_check_mark: Testing
Requires docker-compose and docker installed.

``` bash
$ make up
$ make test-run
```

