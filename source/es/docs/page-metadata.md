---
extends: _layouts.documentation
section: documentation_content
---

## Page Metadata
## Metadata de página

For each page, Jigsaw provides you with certain metadata values through `get` functions accessed on the `$page` object:
Para cada página, Jigsaw nos provee de ciertos valores de metadata a traves de la función `get` accesible en el objeto `$page`:


`$page->getPath()` returns the path to the current page, relative to the site root

`$page->getRelativePath()` returns the relative path (i.e. parent directories) of the current page, relative to the site root

`$page->getUrl()` returns the full URL to the item, if `baseUrl` was defined in `config.php`

`$page->getFilename()` returns the filename of the page, without extension (e.g. `my-first-page`)

`$page->getExtension()` returns the file extension (e.g. `md`)

`$page->getModifiedTime()` returns the last modified time of the file, as a Unix timestamp

`$page->getPath()` retorna la ruta a la página actual, relativa a la raiz del sitio

`$page->getRelativePath()` retorna la ruta relativa de la página actual, relativa a la raíz del sitio

`$page->getUrl()` retorna la URL completa del elemento, si se definió `baseUrl` en `config.php`

`$page->getFilename()` retorna el nombre de archivo de la págin, sin la extensión. Por ejemplo, `my-frist-page`.

`$page->getExtension()` retorna la extensión del archivo. Por ejemplo, `md`

`$page->getModifiedTime()` retorna la ultima fecha de la modifcación del archivo como un timestamp Unix