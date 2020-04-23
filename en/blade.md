# Blade template

The Attla framework uses the laravel blade template engine. So you can create a view with the extension `.blade.php` and take advantage of almost all standard directives.

So if you are not familiar with the blade read the [official documentation](https://laravel.com/docs/7.x/blade#introduction).

## Directives removed

Some directives have been removed as they are exclusive to laravel, thus making them useless in the framework.

- @each
- @inject
- @can
- @elsecan
- @endcan
- @cannot
- @elsecannot
- @endcannot
- @canany
- @elsecanany
- @endcanany
- @error
- @enderror
- @env
- @elseenv
- @endenv
- @unlessenv

## Exclusive policies

There are some directives exclusive to the Attla framework that can help you. See below:

### @header

This directive includes the `header` file, whether with the extension `.php` or `.blade.php`.

```php
<!-- includes header -->

@header('page title')

<!-- if the header is in a directory inside the public ex public/admin/ folder -->
<!-- you can pass the third parameter being the path of the directory -->

@header('page title', 'page description', '/admin')
```

In the `header` file it is possible to access the title and description by the variables `$title` and `$description` respectively.

### @footer

Includes the file `footer` with the extension `.php` or `.blade.php`.

```php
<!-- includes footer-->

@footer()

<!-- if the footer is in a directory inside the public ex public/admin/ folder -->
<!-- you can pass the directory path -->

@footer('/admin')
```

### @assets

Returns the absolute path to the file.

It is recommended that all image files, css, js and the like stay inside the folder `public/assets/`.

```php
@assets('/css/style.css')

<!-- alias -->

@asset('/js/main.js')
```

### @url

Returns the application URL.

```php
@url()

<!-- you can pass a file path or route as a parameter -->

@url('/login')

<!-- alias -->

@uri('/dashboard')
```

### @set_global

Defines one or more variables as global within the application, being possible to recover the value in any view.

```php
<!-- define a variable globally -->
@set_global('user', [
	'id' => 42,
	'name' => 'Lucas Nicolau'
])

<!-- you can also define several variables at the same time -->

@set_globals([
	'user' => [
		'id' => 42,
		'name' => 'Lucas Nicolau'
	],
	'is_logged' => true
])
```

### @import

Includes a file, either with the extension `.php` or `.blade.php`, with access to all global variables.

```php
@import('file')

@import('admin/dashboard_sidebar')
```
