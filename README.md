Ask DB allows you to use OpenAI's GPT-3 to build natural language database queries.

```php
DB::ask('How many users do we have on the "pro" plan?');
```

## Installation

You can install the package via composer:

```bash
composer require mkreftsymfonia/laravel-eloquent-ai
```

You can publish the config file with:

```bash
php artisan vendor:publish --tag="ask-database-config"
```

This is the contents of the published config file:

```php
return [
    /**
     * The database connection name to use. Depending on your
     * use case, you might want to limit the database user
     * to have read-only access to the database.
     */
    'connection' => env('ASK_DATABASE_DB_CONNECTION', 'mysql'),

    /**
     * Strict mode will throw an exception when the query
     * would perform a write/alter operation on the database.
     *
     * If you want to allow write operations - or if you are using a read-only
     * database user - you may disable strict mode.
     */
    'strict_mode' => env('ASK_DATABASE_STRICT_MODE', true),

    /**
     * The maximum number of tables to use before performing an additional
     * table name lookup call to OpenAI.
     * If you have a lot of database tables and columns, they might not fit
     * into a single request to OpenAI. In that case, we will perform a
     * lookup call to OpenAI to get the matching table names for the
     * provided question.
     */
    'max_tables_before_performing_lookup' => env('ASK_DATABASE_MAXIMUM_TABLES', 15),
];
```

## Usage

First, you need to configure your OpenAI API key in your `.env` file:

```dotenv
OPENAI_API_KEY=sk-...
```

Then, you can use the `DB::ask()` method to ask the database:

```php
$response = DB::ask('How many users are there?');
```

## Testing

```bash
composer test
```
