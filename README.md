# Membrane-Laravel

Integrates [Membrane-core](https://github.com/membrane-php/membrane-core) with [Laravel](https://laravel.com/).

## About

Middleware that validates the raw user input from incoming HTTP requests against your OpenAPI spec.  
Extends the `Illuminate\Http\Request` and `Illuminate\Http\Response` with a `Membrane\Result\Result` object containing
the cleaned up data and additional details in the case of invalid requests.

## Setup

### Installation

Require the `membrane/laravel` package in your composer.json and update your dependencies:

```text
composer require membrane/laravel
```

### Configuration

The defaults are set in `config/membrane.php`.  
To publish a copy to your own config, use the following:

```text
php artisan vendor:publish --tag="membrane"
```

#### API Spec File

Set this as the **absolute path** to your OpenAPI Specification.

#### Validation Error Response Code

Set this to the integer value of the HTTP Status Code you want to return for invalid results.

#### Validation Error Response Type

Set this to the url that should return with the error.

### Usage

#### Request Validation

The `RequestValidation` middleware will validate or invalidate incoming requests and let you decide how to react.
You can follow it with your own custom middleware or with one of the following built-in options to produce an error response:

#### Nested Json Response

The `ResponseJsonNested` MUST follow the `RequestValidation` middleware
as it relies on the container containing the result.
It will check whether the request has passed or failed validation.
Invalid requests will return a response detailing the reasons the request was invalid.

#### Flat Json Response

The `ResponseJsonFlat` MUST follow the `RequestValidation` middleware
as it relies on the container containing the result.
It will check whether the request has passed or failed validation.
Invalid requests will return a response detailing the reasons the request was invalid.

### Global Usage

```php
protected $middleware = [
  \Membrane\Laravel\RequestValidation::class,
    // ...
];
```
