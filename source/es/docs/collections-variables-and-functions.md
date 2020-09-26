---
extends: _layouts.documentation
section: documentation_content
---

#### [Collections](/docs/collections)
#### [Colecciones](/es/docs/collections)
## Variables & Helper Functions
## Variables y funciones Helper

Each collection can have its own set of variables and helper methods defined in the collection array in `config.php`. These follow the same format as the site-wide [variables](/docs/site-variables) and [helper methods](/docs/helper-methods) that are defined at the top level of the `config.php` array.

Cada colección puede tener su propio set de variable y métodos helper definidos en un array en `config.php`. Estos siguen el mismo formato que las [variables](/es/docs/site-variables) y los [métodos helper](/es/docs/helper-methods) de todo el sitio que están definidas en el nivel superior del array de `config.php`.

### Variables
### Variables

Just as with site-wide variables, collection variables defined in `config.php` can act as defaults, which can be overridden by variables of the same name specified in the YAML front matter of a collection item. In fact, top-level variables in `config.php` will be overridden by variables of the same name in a collection's array, which will be further overridden by references in the YAML header of any individual page, allowing you to set up a cascade of variable defaults. For example:

Tal como en las variables de todo el sitio, las variables de colección definidas en `comfig.php` pueden actuar como variables por defecto, las que pueden ser sobreescritas por variables del mismo nombre especificadas en la directiva YAML del elemento de la colección. De hecho, las variables del nivel superior en `config.php` serán sobreescritas por las variables del mismo nombre en el array de la colección, las cuales serán luego sobreescritas por la cabecera YAML propia de cada página, permitiendote establecer una cascada de variables por defecto. Por ejemplo: 

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

For this collection item, author will be *Keith Damiani*, the value from the YAML header.

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

For this collection item, author will be *Default Blog Author*, the value from the `posts` array in `config.php`.

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

For this regular (non-collection) page, author will be *Default Site Author*, the value from the top level of `config.php.`

Para esta página (no perteneciente a una colección), el autor será *Default Site Author*, el valor en el nivel superior de `config.php`


### Helper Functions
### Funciones Helper

Helper functions can be included in the collection settings array in `config.php`, and will be available to all of that collection's items. The same cascading rules that apply to variables also apply to functions, i.e. functions defined for a collection will override a function of the same name defined at the top level. For example:

Las funciones helper pueden ser incluidas en el array de configuración de la colección en `config.php` y estarán disponibles para todos los elementos de la colección. Las mismas reglas de cascada que aplican para las variables, aplican también para las funciones. En otras palabras, las funciones definidas para una colección serán sobreescritas por las funciones del mismo nombre definidas en el nivel superior. Por ejemplo: 

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
