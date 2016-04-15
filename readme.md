* Forked at first from Laracasts/Flash to use multiple message

# Easy Flash Messages

## Installation

First, pull in the package through Composer.

Run `composer require mdupaul/flash`

And then, if using Laravel 5, include the service provider within `config/app.php`.

```php
'providers' => [
    'Mdupaul\Flash\FlashServiceProvider'
];
```

And, for convenience, add a facade alias to this same file at the bottom:

```php
'aliases' => [
    'Flash' => 'Mdupaul\Flash\Flash'
];
```

## Usage

Within your controllers, before you perform a redirect...

```php
public function store()
{
    Flash::message('Welcome Aboard!');

    return Redirect::home();
}
```

You may also do:

- `Flash::info('Message')`
- `Flash::success('Message')`
- `Flash::error('Message')`
- `Flash::warning('Message')`
- `Flash::overlay('Modal Message', 'Modal Title')`

Again, if using Laravel, this will set a few keys in the session:

- 'flash_notification.message' - The message you're flashing
- 'flash_notification.level' - A string that represents the type of notification (good for applying HTML class names)

Alternatively, again, if you're using Laravel, you may reference the `flash()` helper function, instead of the facade. Here's an example:

```php
/**
 * Destroy the user's session (logout).
 *
 * @return Response
 */
public function destroy()
{
    Auth::logout();

    flash()->success('You have been logged out.');

    return home();
}
```

Or, for a general information flash, just do: `flash('Some message');`.

With this message flashed to the session, you may now display it in your view(s). Maybe something like:

```html
@if (Session::has('flash_notification.message'))
    <div class="alert alert-{{ Session::get('flash_notification.level') }}">
        <button type="button" class="close" data-dismiss="alert" aria-hidden="true">&times;</button>

        {{ Session::get('flash_notification.message') }}
    </div>
@endif
```

> Note that this package is optimized for use with Twitter Bootstrap.

Because flash messages and overlays are so common, if you want, you may use (or modify) the views that are included with this package. Simply append to your layout view:

```html
@include('flash::message')
```



