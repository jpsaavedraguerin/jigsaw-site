---
extends: _layouts.documentation
section: documentation_content
---

## Compiling Assets with Laravel Mix
## Compilando tus Assets

Jigsaw sites are configured with support for [Laravel Mix](https://laravel.com/docs/7.x/mix) out of the box. If you've ever used Mix in a Laravel project, you already know how to use Mix with Jigsaw.

Los sitios generados con Jigsaw soportan [Laravel Mix](https://laravel.com/docs/7.x/mix) por defecto. Si alguna vez has usado Mix en proyectos con Laravel, entonces ya sabes cómo utilizar Mix con Jigsaw.

---

### Setup
### Configuración

To get started, first make sure you have Node.js and NPM installed in your environment.
Para comenzar, asegurate de que cuentas con Node.js y NPM en tu entorno de desarrollo.

Once you have Node.js and NPM installed, pull in the dependencies needed to compile your assets:
Una vez que instales Node.js y NPM, solicita las dependencias necesarias para compilar tus assets: 

```
$ npm install
```

For more detailed installation instructions, check out the [full Laravel Mix documentation](https://laravel.com/docs/7.x/mix).
Para más instrucciones detalladas sobre la instalación, revisa la [ documentación de Laravel Mix](https://laravel.com/docs/7.x/mix).

### Organizing your assets
### Organizando tus assets

By default, any assets you want to process with Mix should live in `/source/_assets`:
Por fefecto, los assets que desees procesar con Mix deberían vivir en `/source/_assets`:

<div class="files">
    <div class="folder folder--open">source
        <div class="folder folder--open focus">_assets
            <div class="folder folder--open">js
                <div class="file">app.js</div>
            </div>
            <div class="folder folder--open">sass
                <div class="file">main.scss</div>
            </div>
        </div>
        <div class="folder folder--open">_layouts
            <div class="file">master.blade.php</div>
        </div>
        <div class="folder folder--open">assets
            <div class="folder">build</div>
            <div class="folder folder--open">images
                <div class="file">jigsaw.png</div>
            </div>
        </div>
        <div class="file">index.blade.php</div>
    </div>
    <div class="folder">tasks</div>
    <div class="folder">vendor</div>
    <div class="ellipsis">...</div>
</div>

Mix looks for each asset type _(like Sass, Less, or Coffeescript)_ in a subdirectory named after that asset type. We recommend following this convention to avoid additional configuration.

By default, once Webpack compiles your assets, they will be placed in their corresponding subdirectories in `/source/assets/build`:

<div class="files">
    <div class="folder folder--open">source
        <div class="folder folder--open">_assets
            <div class="folder folder--open">js
                <div class="file">app.js</div>
            </div>
            <div class="folder folder--open">sass
                <div class="file">main.scss</div>
            </div>
        </div>
        <div class="folder folder--open">_layouts
            <div class="file">master.blade.php</div>
        </div>
        <div class="folder folder--open focus">assets
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
        <div class="file">index.blade.php</div>
    </div>
    <div class="folder">tasks</div>
    <div class="folder">vendor</div>
    <div class="ellipsis">...</div>
</div>

Then, when Jigsaw builds your site, the entire `/source/assets` directory containing your `build` files (and any other directories containing static assets, such as `images` or `fonts`, that you choose to store there) will be copied to `/build_local` or `/build_production`.

Luego, cuando Jigsaw construya el sitio, todo el directorio `/source/assets` ´conteniendo tus archivos `build` (y cualquier otro directorio conteniendo assets estáticos, como `images` o `fonts`, que decidas guardar allí) serán copiados a `/build_local` o `/build_production`

In your templates, you can reference these assets using the `mix` Blade directive. If you are using the default setup, your compiled assets will be copied to your site's `/assets/build` directory, which should be specified as the 2nd parameter of the `mix` directive:

En tus plantillas, puedes referenciar estos assets usando la directiva `mix` de Blade. Si estás usando la configuración por defecto, tus assets compilados serán copiados al directorio `/assets/build` del sitio, el cual debería ser especificado como el segundo parámetro de la directiva `mix`:

```php
<link rel="stylesheet" href="{{ mix('css/main.css', 'assets/build') }}">
```

### Compiling your assets
### Compilando tus assets

To compile your assets, run:
Para compilar tus assets, ejecuta: 

```
$ npm run dev
```

First, Webpack will compile your assets and store them in the `/source/assets/build` directory. Then, Jigsaw's `build` command will be run automatically to build your site (including your compiled assets) to `/build_local`. You can then preview your changes in the browser.

Primero, Webpack compilará tus assets y los guardará en el directorio `/source/assets/build`. Luego, el comando `build` de Jigsaw será ejecutado automáticamente para generar tu sitio (incluyendo los assets compilados) en `/build_local`. Puedes entonces previsualizar tus cambios en el navegador.

### Watching for changes
### Visualizando los cambios

Manually running `npm run dev` every time you make a change gets old pretty fast.
Ejecuta manualmente `npm run dev` cada vez que haces un cambio se vuelve tedioso rápidamente. 

Instead, you can run the following command to watch your project for changes:
En cambio, puedes ejecutar el siguiente comando para visualizar automáticamente los cambios en tu proyecto: 

```
$ npm run watch
```

Any time any file changes in your project, Webpack will recompile your assets, and Jigsaw will regenerate your static HTML pages to `/build_local`.
Cada vez que algun archivo cambie en tu proyecto, Webpack recompilará tus assets, y Jigsaw regenerará las páginas HTML estáticas en `/build_local`.

Using `npm run watch` also enables [Browsersync](https://www.browsersync.io/), so your browser will automatically reload any time you make a change. It also manages serving your site locally for you, so you don't need to start your own local PHP server.

Usar `npm run watch` también habilita [Browsersync](https://www.browsersync.io/), por lo tanto, tu navegador automáticamente refrescará cada vez que hagas un cambio. Al mismo tiempo, se encarga de servir tu sitio localmente, así que no tienes necesidad de inicializar el servidor PHP local. 

You can also watch a specific environment by running `npm run local`, `npm run staging`, or `npm run production`.

También puedes visualizar los cambios automáticamente en un entorno específico al ejecutar `npm run local`, `npm run staging`, o `npm run production`

---

### Changing asset locations
### Cambiando la ubicación de los assets

If you'd like to change the source and destination directories for your assets, edit the following lines in `webpack.mix.js`:

Si deseas cambiar los directorios de origen y destin de tus assets, debes editar las siguientes líneas en `webpack.mix.js`:

```js
mix.setPublicPath('source/assets/build');

mix.js('source/_assets/js/main.js', 'js/')
    .sass('source/_assets/sass/main.scss', 'css')
    .options({
        processCssUrls: false,
    }).version();
```

---

### Enabling different preprocessors
### Habilitando diferentes preprocesadores

Jigsaw ships with the following `webpack.mix.js` and is configured to use Sass out of the box:

Jigsaw viene con el siguiente `webpack.mix.js` y es configurado para usarse con Sass sin necesidad de configuración adicional: 

```js
let mix = require('laravel-mix');
let build = require('./tasks/build.js');

mix.disableSuccessNotifications();
mix.setPublicPath('source/assets/build');
mix.webpackConfig({
    plugins: [
        build.jigsaw,
        build.browserSync(),
        build.watch(['source/**/*.md', 'source/**/*.php', 'source/**/*.scss', '!source/**/_tmp/*']),
    ]
});

mix.js('source/_assets/js/main.js', 'js')
    .sass('source/_assets/sass/main.scss', 'css')
    .options({
        processCssUrls: false,
    }).version();
```

If you'd like to switch to Less, use Coffeescript, or take advantage of any other Mix features, feel free to edit this file to your heart's content. Here's an example of what it might look like to use Less and React:

Si deseas cambiar a Less, usar Coffeescript, o aprovechar las ventajas de cualquier otra caracteristica de Mix, puedes editar este archivo a tu conveniencia. Aquí hay un ejemplo de cómo se vería usar Less y React: 

```js
mix.react('source/_assets/js/main.js', 'js')
    .less('source/_assets/sass/main.less', 'css')
    .version();
```

---

### Inlining your assets
### Incluyendo tus assets

You may choose to inline your CSS or JavaScript assets into the `<style>` or `<script>` tags in your page `<head>`, to save a network request and to avoid blocking the rest of the page from loading. The `inline` helper function will accomplish this:

Tal vez prefieras incluir CSS o Javascript en los tags `<style>` o `<script>` en el `<head>` de tu sitio, para ahorrar una solicitud a la red y evitar que se evite cargar el resto de la página. La función helper `inline` logrará este objetivo: 

```
{{ inline(mix('css/main.css', 'assets/build')) }}
```

---

### Note for Sass users
### Nota para usuarios de Sass

To prevent URLs in your `.scss` files—such as background images and fonts—from being processed and modified by Mix, set the `processCssUrls` option to `false` in your `webpack.mix.js` file.

Para evitar URLs en tus archivos `.scss` como imágnes de fondo o fuentes tipográficas de ser procesadas y modificadas por Mix, establece la opción `processCssUrls` como `false` en tu archivo `webpack.mix.js`

