---
sidebar_position: 3
---

# Symfony

We have a composer package for Symfony PHP  - https://packagist.org/packages/abrouter/symfony-abtest.

You can see the source code by the following URL: https://github.com/abrouter/symfony-abtest.

If you need an example of step-by-step implementing A/B test you can see the example on [ABRouter website](https://abrouter.com/en/symfony-ab-tests)

## :package: Install
Via composer

``` bash
$ composer require abrouter/symfony-abtest
```

## Register the bundle
Register bundle

```
// config/bundles.php
return [
    // [...]
    Abrouter\SymfonyClient\AbrouterClientBundle::class => ['all' => true],
];
```

### Configure ABRouter client:

Put your ABRouter token in /config/packages/abrouter_client.yaml. You can find this token in [ABRouter dashboard](https://abrouter.com/en/board).

```yaml
abrouter_client:
  token:                'YOUR_TOKEN'
  host:                 'https://abrouter.com'
```


## :rocket: Usage

```js
use Abrouter\Client\Client;

class ExampleController
{
    public function __invoke(Client $client)
    {
        $buttonColorExperimentId = 'D1D06000-0000-0000-00005030';
        return new Response(json_encode([
            'button_color' => $client
                ->experiments()
                ->run('USER_ID', $buttonColorExperimentId),
        ]));
    }
}
```

You can create an experiment and get your token and id of experiment on [ABRouter](https://abrouter.com) or just read the [docs](https://abrouter.com/en/docs).


## Example
You can get an dockerized usage example by the following link: (https://github.com/abrouter/symfony-abtest-example)

