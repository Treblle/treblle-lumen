
<img src="https://d224n10qh3hhwu.cloudfront.net/github/hero-lumen.jpg" alt="Treblle for Lumen" align="center">

# Treblle for Lumen

[![Latest Version](https://img.shields.io/packagist/v/treblle/treblle-lumen)](https://packagist.org/packages/treblle/treblle-lumen)
[![Total Downloads](https://img.shields.io/packagist/dt/treblle/treblle-lumen)](https://packagist.org/packages/treblle/treblle-lumen)
[![MIT Licence](https://img.shields.io/packagist/l/treblle/treblle-lumen)](LICENSE)

Treblle makes it super easy to understand what’s going on with your APIs and the apps that use them. Just by adding
Treblle to your API out of the box you get:

* Real-time API monitoring and logging
* Auto-generated API docs with OAS support
* API analytics
* Quality scoring
* One-click testing
* API management on the go
* and more...

## Requirements

* PHP 7.2+
* Lumen 7+

## Dependencies

* [`laravel/lumen`](https://packagist.org/packages/laravel/lumen)
* [`guzzlehttp/guzzle`](https://packagist.org/packages/guzzlehttp/guzzle)
* [`nesbot/carbon`](https://packagist.org/packages/nesbot/carbon)

## Installation

Install Treblle for Lumen via [Composer](http://getcomposer.org/) by running the following command in your console:

```bash
composer require treblle/treblle-lumen
```

## Getting started
Installing Lumen packages is a lot more complicated than Laravel packages and requires a few manual steps. If you want a completely automated process please use Laravel.

### Step 1: Publish config files
The first thing we need to do is publish the Treblle config file and make sure Lumen loads it. To do that we need to copy/paste the package config file like so:

```bash
mkdir -p config
cp vendor/treblle/treblle-lumen/config/treblle.php config/treblle.php
```
Now we can have Lumen load the config file. We do that by adding a new line in `bootstrap/app.php`, under the *Register Config Files* section, like so:

```php
$app->configure('treblle');
```

### Step 2: Register middleware
We need to register the Treblle middleware in Lumen. To do add a new line of code to `bootstrap/app.php`, under the Register Middleware section, like so:
```php
$app->routeMiddleware([
    'treblle' => Treblle\Middlewares\TreblleMiddleware::class
]);
```
### Step 3: Configure Treblle
You need an API KEY and PROJECT ID for Treblle to work. You can get those by creating a FREE account on <https://treblle.com> and your first project. You'll get the two keys which you need to add to your .ENV file like so:

```bash
TREBLLE_API_KEY=YOUR_API_KEY
TREBLLE_PROJECT_ID=YOUR_PROJECT_ID
```

## Enable Treblle on your API

Now that we've installed the package we simply need to enable it. Open **routes/web.php** and assign the **treblle** middleware to your API routes like so:

```php
$router->group(['prefix' => 'api', 'middleware' => 'treblle'], function () use ($router) {
    $router->get('users',  ['uses' => 'UserController@index']);
    $router->post('users',  ['uses' => 'TestController@store']);
});
```
**You're all set**. Next time someone makes a request to your API you will see it in real-time on your Treblle dashboard
alongside other features like: auto-generated documentation, error tracking, analytics and API quality scoring.

## Configuration options

You can configure Treblle using just .ENV variables:

```shell
TREBLLE_IGNORED_ENV=local,dev,test
```

Define which environments Treblle should NOT LOG at all. By default, Treblle will log all environments except local, dev
and test. If you want to change that you can define your own ignored environments by using a comma separated list, or
allow all environments by leaving the value empty.

### Masked fields

Treblle **masks sensitive information** from both the request and response data as well as the request headers data
**before it even leaves your server**. The following parameters are automatically masked: password, pwd, secret,
password_confirmation, cc, card_number, ccv, ssn, credit_score.

You can customize this list by editing the array  configuration file.

## Support

If you have problems of any kind feel free to reach out via <https://treblle.com> or email vedran@treblle.com, and we'll
do our best to help you out.

## License

Copyright 2022, Treblle Limited. Licensed under the MIT license:
http://www.opensource.org/licenses/mit-license.php
