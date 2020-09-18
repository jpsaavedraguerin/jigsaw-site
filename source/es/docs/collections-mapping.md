---
extends: _layouts.documentation
section: documentation_content
---

#### [Collections](/docs/collections)
#### [Colecciones](es/docs/collections)
## Mapping
## Mapeo

You can map over your collection items by adding a `map` key to the collection's array in `config.php`, and specifying a callback that accepts the collection item. Each item is an instance of the `TightenCo\Jigsaw\Collection\CollectionItem` class, from which you can instantiate your own custom class using the static `fromItem()` method. Your custom class can include helper methods that might be too complex for storing in your `config.php` array.

Puedes mapear los elementos de tu colección al agregar el apartado `map` al array de la colección en el archivo `config.php`, y especificar una llamada que acepte el item de la colección. Cda item es una instancia de la clase `TightenCo\Jigsaw\Collection\CollectionItem`, desde donde puedes instanciar tu propia clase usando el método estático `fromItem()`. Tu clase personalizada puede incluir métodos `helper` que podrían ser demasiado complicados para almacenarlos en el array del archivo `config.php`

> _config.php_

```
<?php

return [
    'collections' => [
        'posts' => [
            'map' => function ($post) {
                return Post::fromItem($post);
            }
        ],
    ],
];
```

Your custom `Post` class should extend `TightenCo\Jigsaw\Collection\CollectionItem`, and could include helper functions, reference and/or modify page variables, etc.:

Tu clase personalizada `Post` debería extender `TightenCo\Jigsaw\Collection\CollectionItem`, y podría incluir funciones de tipo `helper`, referenciar y/o modificar las variables de la página, entre otras cosas: 

```
<?php

use TightenCo\Jigsaw\Collection\CollectionItem;

class Post extends CollectionItem
{
    public function getAuthorNames()
    {
        return implode(', ', $this->author);
    }
}
```
