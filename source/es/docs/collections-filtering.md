---
extends: _layouts.documentation
section: documentation_content
---

#### [Colecciones](es/docs/collections)
## Filtrando

Es posible filtrar los items de una colección agregando el atributo `filter` al array de la colección en el archivo `config.php`, y especificar una característica invocable que acepte el ítem y que retorne un booleano. Los ítems que retornan `false` para el filtro especificado no serán generados.

A common use for filtering is to mark some blog posts as `published`, using a variable in the YAML front matter of each collection item that specifies a boolean or a date. Using a filter in `config.production.php`, draft posts can be made visible in the local or staging [environments](/docs/building-and-previewing-environments), but omitted from your production build.

Un caso de uso común para el filtrado es marcar algun post como `publicado`, usando una variable en la cabecera YAML de cada item de la colección que especifique un booleano o una fecha. Usando un filtro en `config.production.php`, los borradores pueden pueden ser generados en el [entorno](/docs/building-and-previewing-environments) local o stage, pero omitidos en el entorno de producción.

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
