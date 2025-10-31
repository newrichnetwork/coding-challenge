# Coding Challenge

Welcome to the NewRich Coding Challenge! This project provides a pre-configured environment with modern PHP development tools.

## Getting Started

1. Start the API server:
   ```bash
   docker-compose up -d api
   ```

2. Install dependencies:
   ```bash
   composer install
   ```

## Writing Code

1. Place your application code in the `src/` directory
2. Use the `App\` namespace (PSR-4 autoloading is configured)

Example:
```php
<?php

declare(strict_types=1);

namespace App;

class YourClass
{
    public function yourMethod(): string
    {
        return 'Hello, World!';
    }
}
```

## Writing Tests

1. Place your tests in the `tests/` directory
2. Use the Pest PHP testing framework
3. Test files should end with `Test.php`

Example:
```php
<?php

use App\YourClass;

test('it works', function () {
    $instance = new YourClass();
    expect($instance->yourMethod())->toBe('Hello, World!');
});
```

## Documentation

- [Pest PHP](https://pestphp.com/docs)
- [PHPStan](https://phpstan.org/)
- [PHP CodeSniffer](https://github.com/squizlabs/PHP_CodeSniffer)
- [PSR-12 Coding Standards](https://www.php-fig.org/psr/psr-12/)
