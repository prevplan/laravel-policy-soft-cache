# Laravel Policy Soft Cache Package

[![Latest Version on Packagist](https://img.shields.io/packagist/v/innoge/laravel-policy-soft-cache.svg?style=flat-square)](https://packagist.org/packages/innoge/laravel-policy-soft-cache)
[![GitHub Tests Action Status](https://img.shields.io/github/workflow/status/innoge/laravel-policy-soft-cache/run-tests?label=tests)](https://github.com/innoge/laravel-policy-soft-cache/actions?query=workflow%3Arun-tests+branch%3Amain)
[![GitHub Code Style Action Status](https://img.shields.io/github/workflow/status/innoge/laravel-policy-soft-cache/Fix%20PHP%20code%20style%20issues?label=code%20style)](https://github.com/innoge/laravel-policy-soft-cache/actions?query=workflow%3A"Fix+PHP+code+style+issues"+branch%3Amain)
[![Total Downloads](https://img.shields.io/packagist/dt/innoge/laravel-policy-soft-cache.svg?style=flat-square)](https://packagist.org/packages/innoge/laravel-policy-soft-cache)

This package helps prevent performance problems with frequent Policy calls within your application lifecycle. To achieve this policy-calls are soft cached after they have run initially. The cache does not cache policy calls through concurrent requests; only duplicated calls within a single request are cached.

## Beta
Laravel Policy Soft Cache is still in beta and not recommended for production applications. If you have problems, please open an issue.

## Installation

You can install the package via composer:

```bash
composer require innoge/laravel-policy-soft-cache
```

You can publish the config file with:

```bash
php artisan vendor:publish --tag="laravel-policy-soft-cache-config"
```

This is the contents of the published config file:

```php
return [
    /*
     * When enabled, the package will cache the results of all Policies in your Laravel application
     */
    'cache_all_policies' => true,
];
```

## Usage

By default, this package caches all policy calls of your entire application. You can disable this behavior by setting the ```cache_all_policies```configuration to false. Now you can specify which Policy classes should be soft cached and which not. If you want your policy to be cached, add the ```Innoge\LaravelPolicySoftCache\Contracts\SoftCacheable``` interface.

For Example:

```
use Innoge\LaravelPolicySoftCache\Contracts\SoftCacheable;

class UserPolicy implements SoftCacheable
{
    ...
}
```

## Clearing the cache
Sometimes you want to clear the policy cache after model changes. You can call the ```Innoge\LaravelPolicySoftCache::flushCache();``` method.

## Testing

```bash
composer test
```

## Changelog

Please see [CHANGELOG](CHANGELOG.md) for more information on what has changed recently.

## Contributing

Please see [CONTRIBUTING](CONTRIBUTING.md) for details.

## Security Vulnerabilities

Please review [our security policy](../../security/policy) on how to report security vulnerabilities.

## Credits

- [Tim Geisendörfer](https://github.com/geisi)
- [All Contributors](../../contributors)

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.
