# PHP code quality

## Installation

It can be installed through composer.

    composer require --dev horlivak/php-cq


## Toolchain

### PHPUnit
[PHPUnit](https://phpunit.de/) is a programmer-oriented testing framework for PHP. The unit tests should be in the
`tests` directory.

Create the PHPUnit configuration in the project's root folder

    cp vendor/horlivak/php-cq/phpunit.xml.dist phpunit.xml

### PHPStan
[PHPStan](https://github.com/phpstan/phpstan) is a static code analysis tool.

Create the PHPStan configuration to the project root folder

    cp vendor/horlivak/php-cq/phpstan.neon.dist phpstan.neon

### ECS (Easy Coding Standard)
[ECS](https://github.com/easy-coding-standard/easy-coding-standard) tool fixes your code to follow standards.

Create the ECS configuration in the project root folder

    cp vendor/horlivak/php-cq/ecs.php.dist ecs.php

### Rector
[Rector](https://github.com/rectorphp/rector) is a tool for instant upgrades and automated refactoring of PHP code.

Create the Rector configuration in the project root folder

    cp vendor/horlivak/php-cq/rector.php.dist rector.php

### Codeception (optional)
[Codeception](http://codeception.com/) is a BDD style testing framework for PHP. It can be used for unit, functional
and integration tests.

Codeception isn't included by default. It can be installed through composer.

## Usage

### Composer scripts
Add these scripts to your `composer.json` to run quality checks and tests:

    "scripts": {
        "ecs": "./vendor/bin/ecs check --config ecs.php --fix",
        "ecs-show": "./vendor/bin/ecs check --config ecs.php",
        "rector": "./vendor/bin/rector process src tests migrations",
        "rector-show": "./vendor/bin/rector process src tests migrations --dry-run",
        "phpstan": "./vendor/bin/phpstan analyse --configuration phpstan.neon --error-format=raw",
        "test": [
          "phpunit",
          "@ecs-show",
          "@rector-show",
          "@phpstan"
        ],
        "fix": [
          "@ecs",
          "@rector"
        ],
        "checks": [
          "@ecs-show",
          "@rector-show",
          "@phpstan",
          "@composer dump-autoload",
          "@composer validate"
        ]
    },
    "scripts-descriptions": {
        "checks": "Run all quality checks and show them",
        "fix": "Run all quality checks and fix them",
        "test": "Run all tests"
    }

### Running commands

To run all quality checks:

    composer checks

To run automated fixes:

    composer fix

To run all tests:

    composer test
