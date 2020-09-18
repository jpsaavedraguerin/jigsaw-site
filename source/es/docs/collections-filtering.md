---
extends: _layouts.documentation
section: documentation_content
---

#### [Collections](/docs/collections)
#### [Colecciones](es/docs/collections)
## Filtering
## Filtrando

You can filter collection items by adding a `filter` key to the collection's array in `config.php`, and specifying a callable that accepts the collection item and returns a boolean. Items that return `false` from the filter will not be built.

Puedes filtrar los items de una colección añadiendo un criterio de filtrado al array correspondiente ene el archivo `config.php`, y especificar una característica invocable que sea aceptada por el ítem y que retorne un booleano. Los ítems que retornan `false` para el filtro especificado no aparecerán en el sitio.

A common use for filtering is to mark some blog posts as `published`, using a variable in the YAML front matter of each collection item that specifies a boolean or a date. Using a filter in `config.production.php`, draft posts can be made visible in the local or staging [environments](/docs/building-and-previewing-environments), but omitted from your production build.

Un caso de uso común para el filtrado es marcar algun post como `publicado` 

> _config.php_

```
<?php

return [
    'collections' => [
        'posts' => [
            'filter' => function ($item) {
                return $item->published;
            }
        ],
    ],
];
```
