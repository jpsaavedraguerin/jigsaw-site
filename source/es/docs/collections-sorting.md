---
extends: _layouts.documentation
section: documentation_content
---

#### [Colecciones](/es/docs/collections)

## Ordenando


Puedes controlar el orden en que se muestran los items de tu colección. Cuando itereas sobre la colección en un loop `@foreach`, los elementos serán retornados en el orden que especifíques. 


### Orden por defecto

Por defecto, los elementos de la colección serán ordenados por su nombre de arhivo de forma ascendente. Puedes utilizar esta característica para ordenra los elementos por fecha, simplemente anteponiendo la fecha a cada nombre de archivo: 


```
2017-01-01-my-first-post.md
2017-02-14-my-second-post.md
2017-03-15-my-third-post.md
...
```

### Ordenando mediante una Variable


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
