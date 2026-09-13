# PHP

```bash
composer require hanshs474/kavel
```

PHP 8.1+, `ext-curl` and nothing else — no HTTP client to clash with your framework's.

```php
use Kavel\Kavel;
use Kavel\KavelException;

try {
    $img = (new Kavel())->generate('a small wooden sailboat on a calm teal lake, golden hour', '16:9');
    echo $img->url;
} catch (KavelException $e) {
    if ($e->kind === KavelException::QUOTA) { /* retry tomorrow */ }
}
```

A call blocks for a minute or more while the job queues, so run it from a queue worker or a CLI
command rather than inside a web request. Source:
[github.com/hanshs474/kavel-php](https://github.com/hanshs474/kavel-php).
