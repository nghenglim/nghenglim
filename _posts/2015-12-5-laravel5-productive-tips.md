---
layout: post
title: Laravel5 Productive Tips
tags: [PHP]
---

![Laravel]({{ site.baseurl }}/images/2015112800.jpg "Laravel")

### Laravel 5
Laravel currently is the most popular PHP framework.

With the news that [PHP 7 had been released on December the 3th](https://twitter.com/official_php/status/672511111896432640), I'll expect a spike in usage of laravel usage. PHP 7 is definitely the best tool for developing web application quickly.

### Some Productive tips

- Create migration scripts directly from database, at the time I'm writing, the composer default supporting laravel-4. With this settings, we can easily generate migration script with `php artisan migrate:generate flights`

```
"require-dev": {
    "fzaninotto/faker": "~1.4",
    "mockery/mockery": "0.9.*",
    "phpunit/phpunit": "~4.0",
    "phpspec/phpspec": "~2.1",
    "xethron/migrations-generator": "dev-l5",
    "way/generators": "dev-feature/laravel-five-stable"
},
"repositories": [
    {
        "type": "git",
        "url": "https://github.com/jamisonvalenta/Laravel-4-Generators.git"
    }
],

# config/app.php
'Way\Generators\GeneratorsServiceProvider',
'Xethron\MigrationsGenerator\MigrationsGeneratorServiceProvider',
```

- Reinstall Form + Html helper, [from laravel collective](https://laravelcollective.com/docs/5.1/html)

```
#composer.json
"require": {
    "laravelcollective/html": "5.1.*"
}

#config/app.php
'providers' => [
  // ...
  Collective\Html\HtmlServiceProvider::class,
  // ...
],

#config/app.php
'aliases' => [
  // ...
    'Form' => Collective\Html\FormFacade::class,
    'Html' => Collective\Html\HtmlFacade::class,
  // ...
],
```

- Get a good open source IDE: [Atom](https://atom.io/)
  - no more sublime prompt when saving (ignore if you have never used sublime text)
