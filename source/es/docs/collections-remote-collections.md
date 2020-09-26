---
extends: _layouts.documentation
section: documentation_content
---

#### [Colecciones](/es/docs/collections)
## Colecciones Remotas.

Adicionalmente a Markdown o archivos Blade para los items de tu colección, puedes retornar los items de la colección directamente desde el array `collections` del archivo `config.php`. Esto te permitirá generar items de forma programada, por ejemplo, puedes [incluir elementos desde una fuente remota](#remoteItems) como una API externa o de sistemas de gestión de contenidos, como Contentful, GraphCMS, o DatoCMS.

---

### Generando items de una colección en config.php

Para cualquier colección, los items pueden ser generados al retornar un array o colección de `items` desde el array de atributos de configuración de la colección que está ubicado en `config.php`. Cada item debería ser un array, para los cuales los atributos del item serán convertidos en variables de página (tales como aquellos que aparecen típicamente en la cabecera YAML del archivo Markdown), mientras que el valor de la variable `content` será ejecutado como el contenido del ítem de la colección. Este contenido será leido como Markdown, y por lo tanto, puede contener tanto Markdown como HTML; estará disponible dentro de la plantilla Blade mediante `@yield('content')` o `{!! $page->getContent() !!}`:

>_config.php_

```php
return [
    'collections' => [
        'posts' => [
            'extends' => '_layouts.post',
            'items' => [
                [
                    'title' => 'Title of my first post',
                    'content' => '## The first post content',
                ],
                [
                    'title' => 'Title of my second post',
                    'content' => '## The second post content',
                ],
            ],
        ],
    ],
];
```

> __layouts/post.blade.php_

```php
@extends('_layouts.master')

@section('body')
    <h1>{{ $page->title }}</h1>

    @yield('content')
@endsection
```

Tras bambalinas, Jigsaw hará lo siguiente: 

1. Crear un directorio `_tmp` en el directorio de la colección (por ejemplo, . `source/_posts/_tmp`) para almacenar temporalmente los archivos Markdown para cada item de la colección  
2. Procesar los archivos temporales como si fueran archivos `*.blade.md`   
3. Eliminar los archivos temporales cuando el proceso  `jigsaw build` finalice    
Adicionalmente a `content`, cada item puede especificar un atributo `filename`, el cual será usado como el nombre temporal del archivo Markdown. Si es omitido, el valor por defecto será el nombre de la colección seguido por un índice; `post_1.blade.md`, `post_2.blade.md`, etc. La ruta del archivo 
resultante será procesada según las reglas por defecto para el manejo de colecciones. 

Alternativamente, el array de `items` puede contener simples cadenas de strings, los que serán tratados como contenido Markdown, sin variables de página: 

>_config.php_

```php
return [
    'collections' => [
        'posts' => [
            'extends' => '_layouts.post',
            'items' => [
                '## The content for post 1',
                '## The content for post 2',
                '## The content for post 3',
            ],
        ],
    ],
];
```

---

<a name="remoteItems"></a>
### Fetching collection items from a remote API

The `items` key in `config.php` can also reference a closure that returns an array or collection of items. By using a closure, collection items can be fetched from anywhere—from a remote API, from other places on the filesystem, or built up programmatically. The resulting data can then be transformed before collection items are built. For example:

>_config.php_

```php
return [
    'collections' => [
        'posts' => [
            'extends' => '_layouts.post',
            'items' => function ($config) {
                $posts = json_decode(file_get_contents('https://jsonplaceholder.typicode.com/posts'));

                return collect($posts)->map(function ($post) {
                    return [
                        'title' => $post->title,
                        'content' => $post->body,
                    ];
                });
            },
        ],
    ],
];
```

If you want the remote API to only be called when building for particular environments, you can place the `items` closure in the appropriate `config.{environment}.php` file. For example, to only access your remote API when running `build production`, create a `config.production.php` file and include your `items` closure there. This will prevent potentially long build times while running `build local` in development.

The `items` closure receives the `config` array as a parameter, so you may also reference other config values (for example, an API URL) inside the closure.


