---
extends: _layouts.documentation
section: documentation_content
---

## Helper Methods
## Metodos helper

In addition to storing variables in `config.php`, you can also define helper methods by adding a key with the name of the function and returning a closure. Helper methods are called by referencing the method name from the `$page` object in any Blade template.
Adicionalmente a almacenar variables en `config.php`, puedes definir metodos helper al agregar un key con el nomnbre de la función y retornar un closure. Los métodos helper son invocados a partir de la referenciarlos por su nombre desde el objeto `$page` en cualquier plantilla Blade

The method's closure automatically receives the current `$page` as its first parameter. Additional parameters can be specified as well, and passed to the method when it is called in your template.
El closure del método automáticamente recibe el `$page` actual como primer parámetro.  Se pueden especificar parámetros adicionales también, y pasarlos al método cuando sea llamado en la plantilla. 

For instance, you can add a method that identifies if the current page belongs to a particular section, for highlighting the current section in a menu template:
Por ejemplo, puedes agregar un método que identifique si la página actual pertenece a una sección en particular, para destacar la sección actual en un menú: 


> _config.php_

```
<?php

use Illuminate\Support\Str;

return [
    'company' => 'Tighten',
    'selected' => function ($page, $section) {
        return Str::contains($page->getPath(), $section) ? 'selected' : '';
    },
];
```

This method is accessible by calling `$page->selected()` from any page.
El método es accesible al llamar `$page->selected()` desde cualquier página. 

Now, we can build a menu partial that highlights the current menu item for each page:
Ahora, podemos construir un menú en el que se destaque la sección actual para cada página: 

> __menu.blade.php_

```
<a class="{{ $page->selected('about') }}" href="{{ $page->baseUrl }}/about">About Us</a>
<a class="{{ $page->selected('projects') }}" href="{{ $page->baseUrl }}/projects">Projects</a>
<a class="{{ $page->selected('posts') }}" href="{{ $page->baseUrl }}/posts">Blog</a>
```

Alternatively, global helper methods can be stored in a separate `helpers.php` file, located at the root level of your project. This file should return an array, and will be merged into `config.php` automatically if present.
Alternativamente, los métodos helper globales pueden ser almacenados en un archvio `helpers.php` separado, ubicado en la raíz de tu proyecto. Este archivo debería retornar un array, y será fusionado en `config.php` automáticamente si está presente. 
