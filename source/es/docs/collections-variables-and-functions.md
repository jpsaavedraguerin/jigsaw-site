---
extends: _layouts.documentation
section: documentation_content
---

#### [Colecciones](/es/docs/collections)
## Variables y funciones Helper

Cada colección puede tener su propio set de variable y métodos helper definidos en un array en `config.php`. Estos siguen el mismo formato que las [variables](/es/docs/site-variables) y los [métodos helper](/es/docs/helper-methods) de todo el sitio, que están definidas en el nivel superior del array de `config.php`.

### Variables

Tal como en las variables de todo el sitio, las variables definidas para una colección en `config.php` actuan como variables por defecto, estas variables pueden ser sobreescritas por variables del mismo nombre especificadas en la directiva YAML de cada elemento de la colección. De hecho, las variables del nivel superior en `config.php` serán sobreescritas por las variables del mismo nombre en el array de la colección, las cuales serán luego sobreescritas por la cabecera YAML propia de cada página, permitiendote establecer una jerarquía de variables por defecto. Por ejemplo: 

> _config.php_

```
<?php

return [
    'author' => 'Default Site Author',
    'collections' => [
        'posts' => [
            'author' => 'Default Blog Author',
        ],
    ],
];
```

> __posts/blog-post-1.blade.php_

```
---
extends: _layouts.post
title: My First Post
author: Keith Damiani
---
@section ('content')

<h1>{{ $page->title }}</h1>
<p>By {{ $page->author }}</p>

@endsection
```

Para estos elementos de la colección, el autor será *Keith Damiani*, el valor en la cabecera YAML.

---

> __posts/blog-post-2.blade.php_

```
---
extends: _layouts.post
title: My Second Post
---
@section ('content')

<h1>{{ $page->title }}</h1>
<p>By {{ $page->author }}</p>

@endsection
```

Para este elemento de la colección, el autor será *Default Blog Author*, el valor en el array `posts` en `config.php`.

---

> _about-us.blade.php_

```
---
extends: _layouts.about
title: About our company
---
@section ('content')

<h1>{{ $page->title }}</h1>
<p>By {{ $page->author }}</p>

@endsection
```

Para esta página (no perteneciente a una colección), el autor será *Default Site Author*, el valor en el nivel superior, en `config.php`


### Funciones Helper

Las funciones helper pueden ser incluidas en el array de configuración de la colección en `config.php` y estarán disponibles para todos los elementos de la colección. Las mismas reglas de jerarquía que aplican para las variables, aplican también para las funciones. En otras palabras, las funciones definidas para una colección serán sobreescritas por las funciones del mismo nombre definidas en el nivel superior. Por ejemplo: 

> _config.php_

```
<?php

return [
    'excerpt' => function ($page, $characters = 100) {
        return substr($page->getContent(), 0, $characters);
    },
    'collections' => [
        'posts' => [
            'excerpt' => function ($page, $characters = 50) {
                return substr(strip_tags($page->getContent()), 0, $characters);
            },
        ],
    ],
];
```
