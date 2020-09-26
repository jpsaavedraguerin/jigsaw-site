---
extends: _layouts.documentation
section: documentation_content
---

## Creando y Previsualizando

Cuando quieras generar tu sitio, ejecuta el comando `build` desde dentro del directorio raíz de tu proyecto:

`$ ./vendor/bin/jigsaw build`

Jigsaw generará el HTML estático del sitio y lo colocará en el directorio `/build_local` por defecto.

Usando la estructura por defecto del sitio, `/build_local` se verá así:

<div class="files">
    <div class="folder folder--open focus">build_local
        <div class="folder folder--open">assets
            <div class="folder folder--open">build
                <div class="folder folder--open">css
                    <div class="file">main.css</div>
                </div>
                <div class="folder folder--open">js
                    <div class="file">main.js</div>
                </div>
                <div class="file">mix-manifest.json</div>
            </div>
            <div class="folder folder--open">images
                <div class="file">jigsaw.png</div>
            </div>
        </div>
        <div class="file">index.html</div>
    </div>
    <div class="folder">source</div>
    <div class="folder">tasks</div>
    <div class="folder">vendor</div>
    <div class="ellipsis">...</div>
</div>

### Previsualizando con PHP

Para previsualizar tu sitio rápidamente, usa el comando `serve`:

`$ ./vendor/bin/jigsaw serve`

Ahora podrás ver tu sitio en la dirección `http://localhost:8000` desde tu navegador.

Opcionalmente puedes especificar el entorno y el puerto desde donde servir tu sitio, de la siguiente forma:

`$ ./vendor/bin/jigsaw serve production --port=8080`

Esto generará tu sitio en el directorio `/build_production` y será accesible desde la dirección `http://localhost:8080`

### Previsualizando con Browsersync

Si estás [usando Laravel Mix para compilar tus assets](es/doc/compiling-assets)(el cual está incluido por defecto en la configuración de Jigsaw), puedes previsualizar tu sitio con Browsersync, simplemente ejecuta:

```
$ npm run watch
```

_(Si no lo has hecho, necesitarás ejecutar `npm install` antes de ejecutar  `npm run watch`.)_

Browsersync abrirá automáticamente una nueva pestaña en tu navegador y refrescará la página cada vez que hagas cambios. Es una forma muy útil para previsualizar tus cambios rápidamente!
