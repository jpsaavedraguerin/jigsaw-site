---
extends: _layouts.documentation
section: documentation_content
---

## Collections
## Colecciones

Jigsaw provides powerful features for working with groups of related pages, or _collections_. Collections give you the ability to access your content at an aggregate level, enabling you to easily add near-dynamic features like menus, pagination, categories, and tags to your static site.

Jigsaw provee caracteristicas poderosas para trabajar con grupos de páginas relaiconadas, o _collections_. Las colecciones permiten acceder al contenido de un nivel agregado, permitiendo facilmente características casi dinámicas como menús, paginación, categorías, y tags al sitio estático. 

Collections can be used to generate pages of related content—for example, blog posts or articles that are sorted by date, with an index page displaying summaries of the five most recent posts—or for embedding related blocks of content _within_ a page, for content like staff bios, product descriptions, or a portfolio of projects.

Las colecciones pueden ser usadas para generar paginas de contenido relacionado, por ejemplo, post o articulos que son ordenados por fecha, con un indice que muestre resumenes de los cinco post mas recientes, o para incrustar bloques de contenido dentro de una página, para contenido como biografía del staff, descripciones de productos, o portafolio de proyectos.

### Defining a Collection
### Definiendo una colección

To define a collection, add an array named `collections` to `config.php`. Each collection should be indicated by the name of the collection (typically, plural), followed by an array of settings. For example:

Para definir una colección, agrega un array de nombre `collections` al archivo `config.php`. Cada colección debería ser indicada por su nombre (tipicamente, plural), seguido de un array con la configuración. Por ejemplo:  

> _config.php_

```
<?php

return [
    'company' => 'Tighten',
    'contact_email' => 'support@tighten.co',
    'collections' => [
        'people' => [
            'path' => 'people',
            'sort' => 'last_name',
        ],
        'posts' => [
            'path' => 'blog/{date|Y-m-d}/{filename}',
            'author' => 'Tighten',
        ],
    ],
];
```

Jigsaw will look for collection items in a directory with the same name as your collection, preceded by an underscore: in this example, `_people` and `_posts`. Collection items can be Markdown or Blade files, or even [Blade/Markdown hybrid](/docs/content-other-file-types) files.

Jigsaw buscara los elementos de lacolección en un directorio con el mismo nombre del de tu colección, precedido por un guión bajo: en este ejemplo, `_people` y `_posts`. Los elementos de la colección pueden ser archivos Markdown o Blade, o incluso [hibridos Blade/Markdown](/es/docs/content-other-file-types).

<div class="files">
    <div class="folder folder--open">source
        <div class="folder">_assets</div>
        <div class="folder folder--open">_layouts
            <div class="file">master.blade.php</div>
            <div class="file">post.blade.php</div>
        </div>
        <div class="folder folder--open">_people
            <div class="file">george-michael-bluth.blade.php</div>
            <div class="file">j-walter-weatherman.blade.php</div>
            <div class="file">steve-holt.blade.php</div>
        </div>
        <div class="folder folder--open focus">_posts
            <div class="file">1-my-first-post.md</div>
            <div class="file">2-my-second-post.md</div>
            <div class="file">3-my-third-post.md</div>
        </div>
        <div class="folder">assets</div>
        <div class="file">about-us.blade.php</div>
        <div class="file">blog.blade.php</div>
        <div class="file">index.blade.php</div>
    </div>
    <div class="folder">tasks</div>
    <div class="folder">vendor</div>
    <div class="file">bootstrap.php</div>
    <div class="file">composer.json</div>
    <div class="file">composer.lock</div>
    <div class="file">config.php</div>
    <div class="file">package.json</div>
    <div class="file">webpack.mix.js</div>
</div>

In `config.php`, the array where you define your collection can contain [path](/docs/collections-paths) and [sort](/docs/collections-sorting) settings for the collection, as well as [variables and helper functions](/docs/collections-variables-and-functions/). None of these elements are required, however; if omitted, default path and sort settings will be used. In fact, for the simplest configuration using default settings and no variables or functions, you can define a collection with simply its name:

En el array donde se define la colección, en el archivo `config.php`, es posible incluir parametros tanto para [rutas](/es/docs/collections-paths) como [tipo de ordenamiento](/es/docs/collections-sorting), así como también [variables y funciones helper](/es/docs/collections-variables-and-functions/)

> _config.php_

```
<?php

return [
    'collections' => [ 'posts' ],
];
```

### Generating Collection Pages
### Páginas individuales para elementos de la colección

If you'd like to generate an individual page for each of your collection items—for example, a page for each blog post—specify a [parent template](/docs/collections-extending-parent-templates) file in the `extends` key of the YAML front matter, or with the `@extends` directive in a Blade file, just as you would with a regular Jigsaw page. For example:

Si quieres generar una página específica para cada elemento de la colección, por ejemplo, una página para cada post del blog, especifíca una [plantilla principal](/es/docs/collections-extending-parent-templates) en el apartado `extends` de la cabecera YAML, o con la directiva `@extends` en un archivo de tipo Blade, tal como lo harías con una página Jigsaw regular. Por ejemplo: 

> _my-first-post.md_

```
---
extends: _layouts.post
title: My First Blog Post
author: Keith Damiani
date: 2017-03-23
section: content
---

This post is *profoundly* interesting.
```

> __layouts/post.blade.php_

```
@extends('_layouts.master')

@section('body')
    <h1>{{ $page->title }}</h1>
    <p>By {{ $page->author }} • {{ date('F j, Y', $page->date) }}</p>

    @yield('content')
@endsection
```

### Accessing Collection Items
### Accediendo a los elementos de una colección

In any Blade template, you have access to each of your collections using a variable with the collection's name. This variable references an object that contains all the elements in your collection, and can be iterated over to
access individual collection items. The collection variable also behaves as if it were an [Illuminate Collection](https://laravel.com/docs/7.x/collections) in Laravel, meaning you have access to all of Laravel's standard collection methods like `count()`, `filter()`, and `where()`.

En cualquier plantilla Blade, tienes acceso a cada una de tus colecciones usando una variable con el nombre de la colección. Esta variable hace referencia a un objeto que contiene todos los elementos de la colección, y puede ser iterado para acceder a los elementos de la misma. La variable de la colección también se comporta como un [Illuminate Collection](https://laravel.com/docs/7.x/collections) de Laravel, por lo tanto, tienes acceso a todos los metodos standard de Laravel, como: `count()`, `filter()`, y `where()`. 

For example, to create a list of the titles for all your blog posts, you can iterate over the `$posts` object in a Blade `@foreach` loop, and display the `title` property that you defined in the YAML front matter of each post:

Por ejemplo, para crear una lista de títulos para todos tus posts del blog, puedes iterar sobre el objeto `$posts` en un loop `@foreach`, y mostrar la propiedad `title` que se ha definido en la cabecera YAML de cada post: 

> _posts.blade.php_

```
<p>Total of {{ $posts->count() }} posts</p>

<ul>
@foreach ($posts as $post)
    <li>{{ $post->title }}</li>
@endforeach
</ul>
```

For example, assuming that all posts have on their YAML front matter the property `author`, to filter all posts from a particular author, you can filter the collection of `$posts` and generate a new collection:

Por ejemplo, asumiendo que todos los posts tienen en su cabecera YAML la propiedad `author`, para filtrar todos los post escritos por un autor en particular, puedes filtrar la colección de `$posts` y generar una nueva colección. 

> _author\_posts.blade.php_

```
<?php
$authorPosts = $posts->filter(function ($value, $key) use ($page) {
    return $value->author == $page->author;
}); ?>
@if ($authorPosts->count() > 0)
<ul>
@foreach ($authorPosts as $post)
    <li>{{ $post->title }}</li>
@endforeach
</ul>
@endif
```

### Collection Metadata
### Metadata de una Coleección

In addition to the [metadata](/docs/page-metadata/) available for every page, such as `getPath()`, `getUrl()`, and `getFilename()`, collection items have access to a few additional functions:

Adicionalmente al [metadata](/es/docs/page-metadata/) disponible para cada página, como `getPath()`, `getUrl()`, y `getFilename()`, los elementos de la colección tienen acceso a funciones adicionales: 

- `getContent()` retorna el contenido principal del elemento de la colección, es decir, el cuerpo del archivo Markdown (por el momento, `getContent()` está disponible sólo para archivos de tipo Markdown)
- `getCollection()` retorna el nombre de la colección
- `getPrevious()` y `getNext()` retorna los elementos adyacentes en la colección, basado en el [orden](/es/docs/collections-sorting) por defecto de la colección. 
- `getFirst()` retorna el primer elemento de la colección (como hace el método `first()` de Laravel)
- `getLast()` retorna el último elemento de la colección (como hace el método  `last()` de Laravel)

> __layouts/post.blade.php_

```
@extends('_layouts.master')

@section('body')
    <h1>{{ $page->title }}</h1>

    @yield('content')

    @if ($page->getNext())
        <p>Read my next post:
            <a href="{{ $page->getNext()->getPath() }}">{{ $page->getNext()->title }}</a>
        </p>
    @endif
@endsection
```
