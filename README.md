# PHP code quality

## Installation

It can be installed through composer.

    composer require --dev horlivak/php-cq


## Toolchain

### PHPUnit
[PHPUnit](https://phpunit.de/) is a programmer-oriented testing framework for PHP. The unit tests should be in the
`tests` directory.

Create the PHPUnit configuration into the projects root folder

### PHPStan
[PHPStan](https://github.com/phpstan/phpstan) is a static code analysis tool.

Create the PHPStan configuration to the project root folder

    cp vendor/horlivak/php-cq/phpstan.neon.dist phpstan.neon

### PHP-CS-Fixer
[PHP-CS-Fixer](https://github.com/FriendsOfPHP/PHP-CS-Fixer) tool fixes your code to follow standards.

Create the PHP-CS-Fixer configuration to the project root folder

    cp vendor/horlivak/php-cq/.php_cs.dist .php_cs.dist

### Codeception (suggested)
[Codeception](http://codeception.com/) is a BDD style testing frameworks for PHP. It can be used for unit, functional
and integration tests.

Codeception isn't installed by default. It can be installed through composer.

### Composer scripts
Composer can be configured to run all tests

    "scripts": {
        "test": [
          "phpunit",
          "phpstan analyse --configuration phpstan.neon --error-format=raw"
        ],
        "fixer": "php-cs-fixer --verbose fix"
    },
    "scripts-descriptions": {
        "test": "Run all tests and quality checks",
        "fixer": "Run php fixer"
    }

To run all tests do

    composer run-script test
    
To run php fixer

    composer run-script fixer
