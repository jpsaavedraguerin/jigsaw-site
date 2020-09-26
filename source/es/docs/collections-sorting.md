---
extends: _layouts.documentation
section: documentation_content
---

#### [Collections](/docs/collections)
#### [Colecciones](/es/docs/collections)
## Sorting
## Ordenando

You can control the order in which your collection items are sorted. When iterating over your collection in a `@foreach` loop, the items will be returned in the order you specify.

Puedes controlar el orden en que se muestran los items de tu colección. Cuando itereas sobre la colección en un loop `@foreach`, los elementos serán retornados en el orden que especifíques. 


### Default Sort
### Orden por defecto

By default, collection items will be sorted by their filenames in ascending order. This can be a handy way to order items by date, for instance, by prepending the date to each filename:

Por defecto, los elementos de la colección serán ordenados por su nombre de arhivo de forma ascendente. Puedes utilizar esta característica para ordenra los elementos por fecha, simplemente anteponiendo la fecha a cada nombre de archivo: 


```
2017-01-01-my-first-post.md
2017-02-14-my-second-post.md
2017-03-15-my-third-post.md
...
```

### Sorting by a Variable
### Ordenando mediante una Variable

You can also sort your collection by the values of variables defined in the YAML front matter of each collection item. Add a `sort` key to the collection's array in `config.php`, and specify the name of the field to sort by:

También puedes ordenar la colección por los valores de una variable definida en la cabecera YALM de cada elemento de la colección. Agrega `sort` al array de la colección en el archivo `config.php`, y especifíca el nombre del campo por el cual ordenar: 

> _config.php_

```
<?php

return [
    'collections' => [
        'posts' => [
            'sort' => 'sort_order',
        ],
    ],
];
```

To sort by multiple variables (for a hierarchical sort), specify an array of variables:

Para ordenar usando multiples variables (para un ordenamiento jerárquico), especifíca un array de variables: 

> _config.php_

```
<?php

return [
    'collections' => [
        'posts' => [
            'sort' => ['featured', 'date'],
        ],
    ],
];
```

To sort in descending order, prepend a `-` to the variable name:

Para ordenar en orden descendente, antecede el nombre de la variable con un `-`:

> _config.php_

```
<?php

return [
    'collections' => [
        'posts' => [
            'sort' => ['featured', '-date'],
        ],
    ],
];
```
