---
extends: _layouts.documentation
section: documentation_content
---

#### [Creando y Previsualizando](es/docs/building-and-previewing)
## Entornos

Es posible que quieras utilizar variables para tu sitio distintas en tus entornos de desarrollo y de producción. Por ejemplo, en producción tal vez quieras integrar Google Analytics, pero no incluirlo en tu entorno de desarrollo, para no dañar tus resultados.

Jigsaw simplifica esta tarea permitiendote crear archivos `config.php` distintos para cada caso. 

Digamos que tu archivo `config.php` base es mas o menos así:

```php
<?php

return [
    'staging' => true,
    'company' => 'Tighten',
];
```

Puedes sobreescribir la variable `staging` en tu entorno de producción al crear un nuevo archivo llamado `config.production.php`

```php
<?php

return [
    'staging' => false,
];
```

Este archivo es _fusionado_ integrado sobre `config.php`, de tal forma que sólo necesitas especificar aquellas variables que estás modificando. 

### Creando archivos para un entorno específico. 

Para crear archvios para un entorno específico, sólo indica el nombre del entorno como argumento cuando ejecutas el comando `build`:

```
$ ./vendor/bin/jigsaw build production
```

Alternativamente, si estás [usando Laravel Mix para compilar tus assets](es/docs/compiling-assets), puedes ejecutar el script `production` que se encuentra en `package.json`:

```
$ npm run production
```

Esto generará tu sitio en una nueva carpeta llamada `build_production`, 
dejando tu carpeta `build_local` intacta.
