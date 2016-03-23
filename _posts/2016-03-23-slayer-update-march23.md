---
title: Slayer Updates March 23
updated: 2016-03-23 10:20
---

## Here's the current update in the development branch:

#### The ``di()`` function handles now a ``string`` and an ``array`` on its argument

```php
<?php
// it acts like di()->get('application')
di('application');
```

and

```php
<?php
// it acts like di()->set(<alias>, <callback>, <singleton = false>)
di(
    [
        'myAlias',
        function () {},
        $shared = true,
    ]
);
```

#### The ``config()`` function handles now an ``array`` too on its argument

Let's assume we have the default config extracted using ``config()->toArray()``

```php
<?php

[
    'env' => 'production',
    'app' => [
        'services' => [
            0 => 'Namespace\Of\MyServiceProvider',
        ],
    ]
    //...
];
```

the ``config(<array>, <merge = true>)`` shows the ability to update the current config structure, if we will will use the **merge** process

```php
<?php

config([
    'app' => [
        'services' => [
            'New\Namespace\MyNewServiceProvider',
        ],
    ],
]);
```

the code above will automatically **merge** your passed-in config, so when extracting using ``config()->toArray()``, you should be able to have the same config below

```php
<?php

[
    'app' => [
        'services' => [
            0 => 'Namespace\Of\MyServiceProvider',
            1 => 'New\Namespace\MyNewServiceProvider',
        ],
    ],
];
```

how about having the option to recursively change things to override a non-associative index in config. You have the ***second argument*** to pass-in ``false`` value to apply ``array_replace_recursive()```

```php
<?php

config([
    'app' => [
        'services' => [
            'New\Namespace\MyNewServiceProvider',
        ],
    ],
], false);
```

Now extracting the config:

```php
<?php

[
    'app' => [
        'services' => [
            0 => 'New\Namespace\MyNewServiceProvider',
        ],
    ],
];
```

So the ``Namespace\Of\MyServiceProvider:class`` is already replaced.

#### Version

Right now it is currently under development in the ``dev`` branch which points to the ``1.4.x`` development along the ``framework`` repository.
