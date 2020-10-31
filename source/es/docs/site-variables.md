---
extends: _layouts.documentation
section: documentation_content
---

## Site Variables
## Variables de sitio

Anything you add to the array in `config.php` will be made available in all of your templates, as a property of the `$page` object.

Todo lo que agreguemos al array en `config.php` estará disponible en todos las plantillas, como propiedad del objeto `$page`.

For example, if your `config.php` looks like this:
Por ejemplo, si tu archivo `config.php` se ve como sigue: 

```php
<?php

return [
    'contact_email' => 'support@example.com',
];
```

...you can use that variable in any of your templates like so:
...puedes usar esa variable en cualquier de tus plantilas, así:

```
@extends('_layouts.master')

@section('content')
    <p>Contact us at {{ $page->contact_email }}</p>
@stop
```

If you prefer, site variables can also be accessed as arrays:
Si lo prefieres, puedes acceder a las variables de sitio como array:

```
<p>Contact us at {{ $page['contact_email'] }}</p>
```

Jigsaw also supports environment-specific site variables, which you can learn more about [here](/docs/environments/).
Jigsaw también sporta varibles de sitio para entornos específicos, de lo cual puedes aprender más [aquí](/docs/environments/).

