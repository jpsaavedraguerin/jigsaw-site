---
extends: _layouts.documentation
section: documentation_content
---

## Installation
## Instalación

### System Requirements
### Requerimientos del sistema 

To use Jigsaw, you need to have PHP (minimum version 7.2.5) and [Composer](https://getcomposer.org/) installed on your machine. You'll also optionally need Node.js and NPM installed if you want to use [Laravel Mix](https://laravel.com/docs/7.x/mix) to compile your CSS and Javascript.

Para usar Jigsaw, necesitas tener instalado PHP (versión 7.2.5 mínimo) y [Composer](https://getcomposer.org/) en tu equipo. Opcionalmente puedes necesitar tener instalado Node.js y NPM si deseas usar [Laravel Mix](https://laravel.com/docs/7.x/mix) para compilar CSS y Javascript.

---

### 1. Create the Project Directory
### 1. Crear un Directorio de Proyecto

First, create a new directory for your site:
Primero, crea un nuevo directorio para tu sitio:

```
$ mkdir my-site
```

### 2. Install Jigsaw via Composer
### 2. Instala Jigsaw via Composer

Next, navigate to your new project directory and install Jigsaw using Composer:
Luego, dirigete al directorio de tu proyecto e instala Jigsaw usando Composer: 

```
$ cd my-site
$ composer require tightenco/jigsaw
```

### 3. Initialize your Project
### 3. Inicializa tu Proyecto

Finally, from your project directory, run Jigsaw's `init` command to scaffold the default directory structure:

Finalmente, dentro del directorio de tu proyecto, ejecuta el comando `init` de Jigsaw para generar la estructura de directorios por defecto: 

```
$ ./vendor/bin/jigsaw init
```

Alternatively, get up and running quickly by using a [starter template](/docs/starter-templates), which starts you off with a fully-configured, professionally-designed site, ready for you to customize with your content. You can use one of Jigsaw's built-in templates for a blog or an open source documentation site, or [use a third-party template](/docs/starter-templates#installing-a-third-party-starter-template).

Alternativamente, puedes 

```
$ ./vendor/bin/jigsaw init blog
```

or

```
$ ./vendor/bin/jigsaw init docs
```

---

### Directory Structure

By default, Jigsaw gives you the following directory structure:

<div class="files">
    <div class="folder folder--open">source
        <div class="folder folder--open">_assets
            <div class="folder folder--open">js
                <div class="file">main.js</div>
            </div>
            <div class="folder folder--open">sass
                <div class="file">main.scss</div>
            </div>
        </div>
        <div class="folder folder--open">_layouts
            <div class="file">master.blade.php</div>
        </div>
        <div class="folder folder--open">assets
            <div class="folder folder--open">build
                <div class="folder folder--open">js
                    <div class="file">main.js</div>
                </div>
                <div class="folder folder--open">sass
                    <div class="file">main.css</div>
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
    <div class="file">bootstrap.php</div>
    <div class="file">composer.json</div>
    <div class="file">composer.lock</div>
    <div class="file">config.php</div>
    <div class="file">package.json</div>
    <div class="file">webpack.mix.js</div>
</div>

The `/source` directory contains the actual contents of your site. This is where all of your site's pages, CSS, Javascript, images, etc. will be kept.

At the root of the directory, Jigsaw provides a `config.php` file where you can specify configuration settings for your site, along with `webpack.mix.js` for settings related to compiling your assets.

Next, learn about [building and previewing your site](/docs/building-and-previewing).

---
<div class="pt-3"></div>

> Why are there two `assets` directories in `/source`, one prefixed with an underscore? Find out in the [Compiling Assets](/docs/compiling-assets) section.
