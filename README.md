# API Driver for Laravel 8.0

An Eloquent model and query builder with support for Restful Api Server using the original Laravel API. This library extends the original Laravel classes, so it uses exactly the same methods. Supports relationships to other models with methods like hasMany, belongsTo, etc.

Works great with other Laravel instances.

### Installation
---------------
Installation using composer:
```bash
composer require netbuild/apidriver
```

And add the service provider in `config/app.php`:
```php
Netbuild\Apidriver\ApiDbServiceProvider::class
```

### Configuration
----------------
Change your default database connection name in `config/database.php`:

```php
'default' => 'api'
```

And add a new api server connection:

```php
'api' => [
        'driver' => 'api',
]
```

### Usage
--------

Create new Model extend Api Eloquent Model:

```php
use Netbuild\Apidriver\Eloquent\Model;

class User extends Model
{
	protected $url 			= 'https://api.your_restful.url';
	protected $api_token		= 'YOUR_API_TOKEN';
	protected $table 		= 'REMOTE_MODEL';
}
```

Using the original Eloquent API:

```php
$users = User::where('id', '<', 100)->take(3)->get();
```

or

```php
$users = User::where('column_1', '=', 'your_term_1')->orWhere('column_1', '=', 'your_term_2')->take(3)->get();
```

or

```php
$user = User::find(3);
```

or

```php
$user->delete();
```

### Relationships
-------------

Model User

```php
<?php

namespace App\Models\API;

use Netbuild\Apidriver\Eloquent\Model;

class User extends Model
{
    protected $connection   		= 'api';
    protected $url 			= 'https://api.your_restful.url';
    protected $api_token		= 'YOUR_API_TOKEN';
    protected $table 			= 'REMOTE_MODEL';
    public    $timestamps   		= true;

}
```

Model Database

```php
<?php

namespace App\Models\API;

use Netbuild\Apidriver\Eloquent\Model;

class Database extends Model
{
    protected $connection   		= 'api';
    protected $url 			= 'https://api.your_restful.url';
    protected $api_token		= 'YOUR_API_TOKEN';
    protected $table 			= 'REMOTE_MODEL';
    public    $timestamps   		= true;

    public function user()
    {
        return $this->belongsTo(User::class);
    }

}
```
