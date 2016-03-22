---
title: Slayer Module Request
updated: 2016-03-01 06:43
---

I am thinking of a way to call other ``module``, so I added guzzle/guzzle package for RESTful request via cURL.

now you could easily call a module by using this way, let us say we're in the **main** module, and we want to call our **admin** module.

```php
namespace App\Main\Controllers;

class SampleController extends Controller
{
    public function index()
    {
        $client = request()->module('module');

        // slayeradmin.app/user/lists?json=true
        $client->get('user/lists?json=true');
    }
}
```

That's how simple it is now to communicate to your other module, this is also helpful for Load Balancers.
