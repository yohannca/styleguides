# PHP

## General PHP Rules

Code style follows [PSR-1](https://www.php-fig.org/psr/psr-1/),
[PSR-2](https://www.php-fig.org/psr/psr-2/), and [PSR-4](https://www.php-fig.org/psr/psr-4/)
autoloading standard.

## PHPDoc

Below is an example of a valid documentation block. Note that the `@param` attribute
is followed by two spaces, the argument type, two more spaces, and finally the
variable name:

```php
/**
 * Register a binding with the container.
 *
 * @param  string|array  $abstract
 * @param  \Closure|string|null  $concrete
 * @param  bool  $shared
 * @return void
 *
 * @throws \Exception
 */
public function bind($abstract, $concrete = null, $shared = false)
{
    //
}
```

## Comments

Comments should be avoided as much as possible by writting expressive code.
If you do need to use a comment, format it like this:

```php
// Should be a space before a single line comment.

/*
 * If you need to explain a lot about the code you can use
 * a comment block like this with a single * on the first
 * line unlike our typical docblocks.
 */
```

## If statements

Always use curly braces.

```php
// Good
if (true) {
    ...
}

// Bad
if (true) ...
```

They should have some breathing room. It is also a matter of what looks best in
its context.

```php
// Good
public function infinityGauntlet($gemColour)
{
    $gem = Gem::whereColor($gemColour)->first();

    if (! $gem) {
        return null;
    }

    if ($gem->colour === 'green') {
        return 'Time';
    }

    return 'Space';
}

// Bad
public function infinityGauntlet($gemColour)
{
    $gem = Gem::whereColour($gemColour)->first();
    if (! $gem) {
        return null;
    }
    if ($gem->colour === 'green') {
        return 'Time';
    }
    return 'Space';
}

// Don't add extra empty lines between curly brackets.
if (! $gem) {

    return null;

}
```

## Ternary operators

Each portion should be on its own line unless it's a really short expression.

```php
// Good
$infinityWar = Gauntlet::whereUser($thanos)->hasAllStones()
    ? $thanos->snapFingers()
    : $thanos->run();

$infinityWar = $thanos->stones() ? 'fingers' : 'run';
```

## Configuration

Configuration file must use **kebab-case** and keys must use **snake_case**.

```
config/infinity-war.php
```

```php
<?php

return [
    'infinity_war' => env('INFINITY_WAR'),
];
```

Do not use `env()` outside of a configuration file.

## Artisan Commands

Artisan commands should be in kebab case and should always give feedbacks through
the handle method.

```
// Good
php artisan clear-audit

// Bad
php artisan clearAudit
```

## Routing

URLs must use kebab case.

```
https://yohann.io/blog/must-be-kebab-case
```

Route names must use kebab case.

```php
Route::get('my-blog', 'BlogController@index')->name('my-blog');
```

```html
<a href="{{ route('my-blog') }}">My Blog</a>
```

Route parameters should use camel case.

```php
Route::get('blog/{blogId}', 'BlogController@show');
```

## Views

View files must be in kebab case.

```
resources/views/sidebar-first.blade.php
```

Blade templates must start with a docblock listing available variables and
variable names must be in camel case.

```PHP
<?php
/**
 * Template for showing the password reset confirmation page.
 *
 * Available variables:
 * - $agent: The user agent from \Jenssegers\Agent\Agent.
 * - $app_name: The name of the application from the configuration.
 */
 ?>
 @extends('layouts.app')
```

### Blade templates

Indent using four spaces and don't add space after statements.

```php
@if ($condition)
    Show something
@endif
```

## Naming classes

### Controllers

Generally controllers are named by the plural form of their corresponding resources
and a `Controller` suffix.

e.g. `UsersController`

When writing non-resourceful controllers you might come across invokable controllers
that perform a single action. These can be named by the action they perform again
suffixed by `Controller`.

e.g. `PerformCleanupController`

### Jobs

Jobs should describe an action.

E.g. `CreateUser` or `PerformDatabaseBackup`

### Events

Events will often be fired before or after the actual event. This should be
very clear by the tense used in their name.

E.g. `ApprovingLoan` before the action is completed and `LoanApproved` after
the action is completed.

### Listeners

Listeners will perform an action based on an incoming event. Their name should
reflect that action with a Listener suffix. This might seem strange at first
but will avoid naming collisions with jobs.

E.g. `SendInvitationMailListener`

### Mailable

Again to avoid naming collisions we'll suffix mailables with Mail, as they're
often used to convey an event, action or question.

e.g. `AccountActivatedMail` or `NewEventMail`
