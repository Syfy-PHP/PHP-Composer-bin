# composer-bin-plugin

Isolated vendor for your bin dependencies.

## Why?

As you project grows, it is possible that your bin dependencies collide with each other
or with your project dependencies. This would either force you to use a lower version of
a given package, or even worse, make your dependencies unsolvable.

## How does this plugin work?

It allows you to install your bin vendors in isolated locations, and still link them
to your [bin-dir](https://getcomposer.org/doc/06-config.md#bin-dir).

This is done by registering a `bin` command, which can be used to run Composer commands inside a namespace.

## Installation

```sh
composer global require bamarni/composer-bin-plugin:0.*@dev
```

## Usage

Let's install Behat and PHPSpec inside a `bdd` namespace :

```sh
composer bin bdd require behat:behat:^3.0 phpspec/phpspec:^2.0
```

This command creates the following directory structure :

````
├── composer.json
├── composer.lock
├── vendor
│   └── bin
│       ├── behat -> ../../vendor-bin/bdd/vendor/behat/behat/bin/behat
│       └── phpspec -> ../../vendor-bin/bdd/vendor/phpspec/phpspec/bin/phpspec
└── vendor-bin
    └── bdd
        ├── composer.json
        ├── composer.lock
        └── vendor
```

You can continue to run `./vendor/bin/phpspec` and `./vendor/bin/phpspec`,
but they'll use an isolated set of dependencies.

### Tips

#### .gitignore

Make sure to add the following line in your `.gitignore` :

    vendor-bin/*/vendor