---
extends: _layouts.documentation
section: documentation_content
---

#### [Colecciones](es/docs/collections)
## Mapeo

Puedes mapear los elementos de tu colección al agregar el atributo `map` al array de la colección en el archivo `config.php`, y especificar una llamada que acepte el item de la colección. Cada item es una instancia de la clase `TightenCo\Jigsaw\Collection\CollectionItem`, desde donde puedes instanciar tu propia clase personalizada usando el método estático `fromItem()`. Tu clase personalizada puede incluir métodos `helper` que podrían ser demasiado complicados para almacenarlos en el array del archivo `config.php`

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
