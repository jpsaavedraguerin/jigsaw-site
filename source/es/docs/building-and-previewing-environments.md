---
extends: _layouts.documentation
section: documentation_content
---

#### [Building & Previewing](es/docs/building-and-previewing)
## Environments

Often you might want to use different site variables in your development and production environments. For example, in production you might want to render your Google Analytics tracking snippet, but not include it in development so you don't skew your results.

Es posible que quieras utilizar variables distintas para tu sitio, en desarrollo y en producción. Por ejemplo. en producción tal vez quieres render tu Google Analytics tracking snippet, pero no incluirlo en desarrollo para no skew tus resultados. 

Jigsaw makes this simple by allowing you to create additional `config.php` files for your different environments.

Jigsaw simplifica esta tarea permitiendote crear archivos `config.php` distintos para cada caso. 

Say your base `config.php` file looks like this:

Digamos que tu archivo `config.php` base es mas o menos así:

```php
<?php

return [
    'staging' => true,
    'company' => 'Tighten',
];
```

You can override the `staging` variable in your production environment by creating a new file called `config.production.php`:

Puedes sobreescribir el `staging` variable en tu ambiente de producción al crear un nuevo archivo llamado `config.production.php`

```php
<?php

return [
    'staging' => false,
];
```

This file is _merged_ on top of `config.php`, so you only need to specify the variables that you are changing.

Este archivo es _fusionado_ sobre `config.php`, de tal forma que sólo necesitas especificar las variables que estás modificando. 

### Building files for a specific environment

### Creando archivos para un ambiente específico. 

To build files for a specific environment, just pass the environment name as an argument when running the `build` command:

Para crear archvios para un ambiente específico, sólo indica el nombre del ambiente como argumento cuando ejecutas el comando `build`:

```
$ ./vendor/bin/jigsaw build production
```

Alternatively, if you are [using Laravel Mix to compile your assets](/docs/compiling-assets), you can run the `production` script found in `package.json`:

Alternativamente, si estás [usando Laravel Mix para compilar tus assets]((/docs/compiling-assets), puedes ejecutar el script `production` que se encuentra en `package.json`:

```
$ npm run production
```

This will generate your site into a new folder called `build_production`, leaving your `build_local` folder untouched.

Esto generará tu sitio en una nueva carpeta llamada `build_production`, 
dejando tu carpeta `build_local` intacta.
