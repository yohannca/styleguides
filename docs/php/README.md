# PHP

## General PHP Rules

Code style follows [PSR-1](https://www.php-fig.org/psr/psr-1/),
[PSR-2](https://www.php-fig.org/psr/psr-2/), and [PSR-4](https://www.php-fig.org/psr/psr-4/)
autoloading standard.

## PHPDoc

Below is an example of a valid documentation block. Note that the `@param` attribute
is followed by two spaces, the argument type, two more spaces, and finally the
variable name:

```
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

```
// Should be a space before a single line comment.

/*
 * If you need to explain a lot about the code you can use
 * a comment block like this with a single * on the first
 * line unlike our typical docblocks.
 */
```

## If statements

Always use curly braces.

```
// Good
if (true) {
    ...
}

// Bad
if (true) ...
```

They should have some breathing room. It is also a matter of what looks best in
its context.

```
// Good
public function infinityGauntlet($gemColour)
{
    $name = Gem::whereColor($gemColour)->first();

    if (! $name) {
        return null;
    }

    if ($name === 'green') {
        return 'Time';
    }

    return 'Space';
}

// Bad
public function infinityGauntlet($gemColour)
{
    $name = Gem::whereColour($gemColour)->first();
    if (! $name) {
        return null;
    }
    if ($name === 'green') {
        return 'Time';
    }
    return 'Space';
}
```
