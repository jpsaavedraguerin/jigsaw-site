---
extends: _layouts.documentation
section: documentation_content
---

#### [Collections](/docs/collections)
#### [Colecciones](/es/docs/collections)
## Pagination

You can create a Blade template that displays your collection items in a paginated format by including a `pagination` key in the template's YAML front matter. The pagination header should include the `collection` name and the `perPage` count:

Es posible crear plantillas Blade para desplegar los elementos de tu colección en un formato paginado al incluir la llave `pagination` en el YAML de la cabecera de la plantilla. Además debes indicar el nombre de la colección en `collection` y el numero de elementos por página en `perPage`:


> _posts.blade.php_

```
---
pagination:
  collection: posts
  perPage: 5
---
@extends('_layouts.master')
...
```

> If you don't provide a `perPage` value, the default value will be 10. The default value can also be set globally by adding a `perPage` key to `config.php`.

> Si no indicas un valor para `perPage`, el número por defecto de elementos a mostrar será 10. El valor por defecto puede ser indicado de forma global agregando la `perPage` al archivo de configuración `config.php`.

Once the `pagination` has been defined in the header, the template will have access to a special `$pagination` variable, which has several attributes:

Una vez que se ha definido un valor para `pagination`, podrás acceder a la variable especial `$pagination`, la cual tiene varios atributos: 

- `$pagination->items` contains an array of collection items for the current page
- `$pagination->currentPage` contains the page number of the current page
- `$pagination->totalPages` contains the total number of pages
- `$pagination->pages` contains an array of paths to each page
> Note that the `pages` are indexed by their page number, i.e. they are 1-based. So you can refer to the paths of a page by the page number, i.e. `$pagination->page[1]` will return the path to the first page.

- `$pagination->first` contains the path to the first page (the same as `$pagination->path[1]`)
- `$pagination->last` contains the path to the last page
- `$pagination->next` contains the path to the next page
- `$pagination->previous` contains the path to the previous page

- `$pagination->items` contiene un array con los elementos de la colección de la pagina actual
- `$pagination->currentPage` contiene el numero de página de la página actual 
- `$pagination->totalPages` contiene el numero total de páginas
- `$pagination->pages` contiene un array con la ruta hacia cada página
> Nota que los elementos `pages` están indexados por su número de página, por lo que puedes referenciar la ruta de la página por su número de página. Por ejemplo, `$pagination->page[1]` retornara la ruta a la primera página.

- `$pagination->first` contiene la ruta a la primera página (al igual que `$pagination->path[1]`)
- `$pagination->last` contiene la ruta a la última página
- `$pagination->next` contiene la ruta a la siguiente página
- `$pagination->previous` contiene la ruta a la página anterior




Using these `$pagination` attributes, you can build a set of pagination buttons and links:

Usando los atributos de la variable especial `$pagination`, puedes crear varios botones de páginación y links: 

```
@if ($previous = $pagination->previous)
    <a href="{{ $page->baseUrl }}{{ $pagination->first }}">&lt;&lt;</a>
    <a href="{{ $page->baseUrl }}{{ $previous }}">&lt;</a>
@else
    &lt;&lt; &lt;
@endif

@foreach ($pagination->pages as $pageNumber => $path)
    <a href="{{ $page->baseUrl }}{{ $path }}"
        class="{{ $pagination->currentPage == $pageNumber ? 'selected' : '' }}">
        {{ $pageNumber }}
    </a>
@endforeach

@if ($next = $pagination->next)
    <a href="{{ $page->baseUrl }}{{ $next }}">&gt;</a>
    <a href="{{ $page->baseUrl }}{{ $pagination->last }}">&gt;&gt;</a>
@else
    &gt; &gt;&gt;
@endif
```



To display the items on each page, iterate over the `$pagination->items` collection:

Para mostrar los elementos en cada página, itera sobre la colección `$pagination->items`:

```
@foreach ($pagination->items as $post)
    <h3><a href="{{ $post->getUrl() }}">{{ $post->title }}</a></h3>
    <p class="text-sm">by {{ $post->author }} • {{ date('F j, Y', $post->date) }}</p>
    <div>{!! $post->getContent() !!}</div>
@endforeach
```
