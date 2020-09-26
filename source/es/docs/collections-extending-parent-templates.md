---
extends: _layouts.documentation
section: documentation_content
---

#### [Colecciones](es/docs/collections)
## Extendiendo las plantillas principales

Para desplegar cada uno de los items de tus colecciones en su propia página, necesitas especificar la plantilla de origen. Puedes hacerlo en el atributo `extends` de la cabecera YAML usando la directiva `@extends` en un archivo de tipo Blade: 

> _mi-primer-post.md_

```
---
extends: _layouts.post
title: Mi Primer Post en el Blog
author: Juan P. Saavedra Guerin
date: 2020-09-22
section: content
---

Este post es *profundamente* interesante.
```

> _mi-segundo-post.blade.php_

```
---
title: Mi Segundo Post en el Blog My Second Blog Post
author: Juan P. Saavedra Guerin
date: 2020-09-22 2017-03-25
section: content
---
@extends ('_layouts.post')

This is {{ $page->author }}'s second <strong>amazing</strong> post.

Este es el <strong>increible</strong> segundo post de {{ $page->author }}.
```

### Items de colección sin plantilla principal

El uso de plantillas principales para los items de las colecciones es opcional. En algunos casos -tales como una colección de biografías del equipo que aparece en la página "Sobre nosotros"- no necesitas desplegar cada uno de los items de tu colección en su propia página. Para hacer esto, simplemente omite el atributo `extends` de la cabecera YAML, o la directiva `@extends` en el caso de los archivos de tipo Blade. 

### Items de colecciones con multiples plantillas principales

Los items también pueden extender _multiples_ plantillas principales, especificandolas en un array en el atributo `extends` de la cabecera YAML. Esto generará URL's separadas para cada plantilla, permitiendo por ejemplo, a un item de la colección tener tanto `/web/item` y `/api/item` como puntos finales, o las vistas `/summary` y `/detail`.

> __people/abraham-lincoln.md_

```
---
name: Abraham Lincoln
role: President
number: 16
extends:
  web: _layouts.person
  api: _layouts.api.person
section: content
---
...
```

> __layouts.person.blade.php_

```
@extends('_layouts.master')

@section('body')
    <header>
        <h1>{{ $page->name }}</h1>
        <h2>{{ $page->role }}</h2>
    </header>

    @yield('content')
@endsection
```

> __layouts.api.person.blade.js_

```
{!! ($page->api()) !!}
```


Si usas multiples plantillas originarias, se puede especificar rutas separadas en el archivo `config.php` para cada página resultante: 

> _config.php_

```
<?php

use Illuminate\Support\Str;

return [
    'collections' => [
        'people' => [
            'path' => [
                'web' => 'people/{number}/{filename}',
                'api' => 'people/api/{number}/{filename}',
            ],
            'api' => function ($page) {
                return [
                    'slug' => Str::slug($page->getFilename()),
                    'name' => $page->name,
                    'number' => $page->number,
                    'content' => $page->getContent(),
                ];
            },
        ],
    ],
];
```
