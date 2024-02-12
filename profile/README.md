
Fignon is an ExpressJs like framework for PHP. It is designed to be simple and easy to use.

## Sample Hello in Fignon

```php
<?php
declare(strict_types=1);

include_once __DIR__ . "/../vendor/autoload.php";

use Fignon\Middlewares\BodyParser;
use Fignon\Tunnel;
use Fignon\Request\Request;
use Fignon\Response\Response;
use Fignon\Middlewares\Griot;
use Fignon\Extra\TwigEngine;

$app = new Tunnel();

// Some config
$app->set('env', 'development');
$app->set('baseUrl', 'http://localhost:8000');
$app->set('debug', true);

// View engine initialization
$app->set('views', dirname(__DIR__) . '/tests-data/templates');
$app->set('views cache', dirname(__DIR__) . '/tests-data/var/cache');
$app->set('view engine options', []); // Add options to the view engine
$app->engine('twig', new TwigEngine()); 


// Some handy middlewares
$app->use(new BodyParser());
$app->use(new Griot());


$app->get('/', function (Request $req, Response $res) {
    // You can use LaravelBlade, Plates, Twig, Smarty, vanilla Php or whatever you want as view engine which can run in php environment
    $res->status(200)->render('hello.twig.html');
})->as('get_hello');

$app->listen();
```
