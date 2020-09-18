---
extends: _layouts.documentation
section: documentation_content
---

## Building & Previewing

## Construyendo y Previsualizando

When you'd like to generate your site, run the `build` command from within your project root:

Cuando quieras generar tu sitio, ejecuta el comando `build` desde dentro de tu directorio raíz:

`$ ./vendor/bin/jigsaw build`

Jigsaw will generate your static HTML and place it in the `/build_local` directory by default.

Jigsaw generará tu HTML estático y lo colocará en el directorio `/build_local`
por defecto.

Using the default site structure, `/build_local` will look like this:

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

### Previewing with PHP

### Previsualizando con PHP

To quickly preview your site, use the `serve` command:

Para previsualizar tu sitio rapidamente, usa el comando `serve`:

`$ ./vendor/bin/jigsaw serve`

You can now view your site at `http://localhost:8000` in your browser.

Ahora podrás ver tu sitio en la dirección `http://localhost:8000` en tu explorador.

You can also optionally specify the environment and port to serve like so:

Opcionalmente puedes especificar el ambiente y el puerto desde donde servir, de la siguiente forma:

`$ ./vendor/bin/jigsaw serve production --port=8080`

This will serve your `/build_production` directory at `http://localhost:8080`.

Esto generará tu sitio en el directorio `/build_production` desde la dirección 
`http://localhost:8080`.

### Previewing with Browsersync

### Previsualizando con Browsersync

If you are [using Laravel Mix to compile your assets](/docs/compiling-assets) (which is included in the default Jigsaw setup), you can preview your site with Browsersync by simply running:

Si estás [usando Laravel Mix para compilar tus assets](es/doc/compiling-assets)(el cual está incluido por defecto en la configuración de Jigsaw), puedes previsualizar tu sitio con Browsersync, simplemente ejecuta:

```
$ npm run watch
```

_(If you haven't already, you'll need to run `npm install` before running `npm run watch`.)_

_(Si no lo has hecho, necesitarás ejecutar `npm install` antes de ejecutar  `npm run watch`.)_

Browsersync will automatically open a new browser tab and reload the page every time you make a change. Very helpful for previewing your changes quickly!

Browsersync abrirá automáticamente una nueva pestaña en tu explorador y refrescará la página cada vez que hagas cambios. Es una forma muy útil para previsualizar tus cambios rápidamente!
