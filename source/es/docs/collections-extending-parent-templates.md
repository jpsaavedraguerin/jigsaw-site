---
extends: _layouts.documentation
section: documentation_content
---

#### [Collections](/docs/collections)
#### [Collecciones](es/docs/collections)
## Extending Parent Templates
## Extendiendo las plantillas originaria

To display each of your collection items on their own page, you need to specify a parent template. You can do this in the `extends` key of the YAML front matter, or with the `@extends` directive in a Blade file:

Para desplegar cada uno de los items de tus colecciones en su propia página, necesitas especificar la plantilla de origen. Puedes hacerlo en el apartado `extends` de la cabecera del YAML, con la directiva `@extends` en un archivo de tipo Blade: 

> _mi-primer-post.md_

```
---
extends: _layouts.post
title: Mi Primer Post en el Blog
author: Juan P. Saavedra Guerin
date: 2020-09-22
section: content
---

This post is *profoundly* interesting.
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

### Collection items with no parent template

### Items de colección sin plantilla originaria

However, parent templates are optional for collection items. In some cases—such as for a collection of staff bios that appear on an "About Us" page—you may not need to display each of your collection items on their own pages. To do this, simply omit the `extends` key from the YAML front matter, or the `@extends` directive from a Blade file.

Las plantillas de origen son opcionales para los items de las colecciones. En algunos casos -tales como una colección de biografías del equipo que aparece en la página "Sobre nosotros"- no necesitas desplegar cada uno de los items de tu colección en su propia página. Para hacer esto, simplemente omite el apartado `extends` de la cabecera YAML, o la directiva `@extends` en el caso de los archivos de tipo Blade. 


### Collection items with multiple parent templates

### Items de colecciones con multiples plantillas originarias

Collection items can also extend _multiple_ parent templates, by specifying the templates as an array in the `extends` key in the YAML front matter. This will generate a separate URL for each template—allowing, for example, a collection item to have both `/web/item` and `/api/item` endpoints, or `/summary` and `/detail` views.

Los items también pueden extender _multiples_ plantillas originarias, al especificarlas en un ARRAY en el apartado `extends` en la cabecera YAML. Esto generará URL's separadas para cada plantilla ----, por ejemplo, un item de la colección tiene ambos `/web/item` y `/api/item`, o vistas `/summary` y `/detail`.

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


If using multiple parent templates, you can specify separate paths in `config.php` for each resulting page:

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
