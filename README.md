Laravel Flash Notifications 0.1.0
===========================

Flash Notifications Helper for Laravel 4

## Install

### Install via composer

Add dependency to your `composer.json` file and run `composer update`.a

```json
require: {
    "szykra/notifications": "0.1.*
}
```

### Configure Laravel

Add ServiceProvider and Facade to your `config/app.php` file:

```php
'Szykra\Notifications\NotificationServiceProvider'
```

```php
'Flash' => 'Szykra\Notifications\Flash'
```

### Publish and include default alert view to your views directory

Package default provides bootstrap ready alert view. To publish it use `artisan`.

```
php artisan view:publish szykra/notifications
```

Now you can include alert view in your blade files:

```php
@include('packages.szykra.notifications.flash')
````

## Usage

You can push flash message ever you need by facade `Flash`. It provides 4 alert types:

* success
* error
* warning
* info

```
Flash::info('Your alert message here!')->push();
```

Method `push()` exists because you can push more than one event at the same time. __See below__.

Every alert method takes 1 or 2 arguments. If you give one parameter it will __message__. If you provide two parameters,
first will be __title__ and second will be __message__.

```php
Flash::success('User has been updated successfully.');
Flash::error('Oh snap!', 'Something went wrong. Please try again for a few seconds.');
Flash::push(); // Push all alerts
```

## Custom alert view

Package default provides bootstrap ready view for alerts. You can define own style for it. 
Just create new __blade__ template file!

```php
@if(Session::has('flash.alerts'))
    @foreach(Session::get('flash.alerts') as $alert)

        <div class='alert alert-{{ $alert['level'] }}'>
            <button class="close" type="button" data-dismiss="alert" aria-hidden="true">&times;</button>

            @if( ! empty($alert['title']))
                <div><strong>{{ $alert['title'] }}</strong></div>
            @endif

            {{ $alert['message'] }}
        </div>

    @endforeach
@endif
```

All alerts will be in `flash.alerts` session variable. Single alert looks like:

```php
[
  'title' => 'Title',
  'message' => 'Example message',
  'level' => 'success'
]
```

__Level__ for all alerts are following:

* `success` has level __success__
* `error` has level __danger__
* `warning` has level __warning__
* `info` has level __info__

## License

The MIT License. Copyright (c) 2014 Szymon Krajewski.
