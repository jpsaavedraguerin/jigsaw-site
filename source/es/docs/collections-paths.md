---
extends: _layouts.documentation
section: documentation_content
---

#### [Collections](/docs/collections)
#### [Colecciones](/es/docs/collections)
## Paths
## Rutas

### Default Path Setting
### Configuración por defecto de las rutas

By default, each of your collection items (if they `extend` a parent template) will be assigned a path where the first segment is the name of the collection, and the second segment is the filename converted to a URL "slug"—all lowercase, with words separated by dashes. So the default path for a file named `My First Blog Post.md` in a collection named `posts` would be `/posts/my-first-blog-post`.

Por defecto, cada uno de los elementos de tu colección (si extienden una plantilla principal) serán asignados a la ruta dodne el primer coomponente es el nombte de la colección, y el segundo es el nombre del archivo convertido en una URL "slug", todo en minúsculas, separando cada palabra con un guión. Asi que, por defecto, la ruta al archivo `My First Blog Post.md` en una colección llamada `posts` será `/posts/my-first-blog-post`.

Jigsaw gives you the ability to customize your collection paths, however, by adding a `path` key to your collection array.

De todas formas, Jigsaw te brinda la habilidad de poder personalizar las rutas a tus colecciones, agregando el parámetro `path` al array de tu colección. 


### Custom Path Shorthand
### 

You can specify your collection path as a string. In this string, you can reference the values of any variables that are defined within the YAML front matter of the collection item, by specifying the variable name enclosed in `{}` brackets. If your collection items each include a `title` variable, for example, you could define your path as:

Puedes especificar la ruta de tu colección como un `string`. En estos strings, es posible referenciar el valor de cualquier variable definida en los parametros de la cabecera YAML del elemento de la colección, especificando el nombre de la variable entre corchetes `{}`. Si cada elemento de tu colección incluye una variable `title`, por ejemplo, puedes definir la ruta de la siguiente forma: 

```
'path' => 'blog/{title}'                             // 'blog/Title Of First Post'
```

In addition, the variables `filename` (containing the filename without extension) and `collection` (containing the collection name) are available:

Adicionalmente, las variables `filename` (que contiene el nombde del archivo sin incluir la extensión) y `collection` (conteniendo el nombre de la colección) también estan disponibles:

```
'path' => '{collection}/{filename}'                  // 'posts/my first blog post'
```

In most cases, when using filenames or titles, you will want to "slugify" them when used as part of a path. To do so, prepend a separator to the variable name:

En la mayoría de los casos, cuando usas nombres de archivo (filenames) o títulos (title), podrías querer integrarlos como parte de la ruta. Para hacerlo debes anteponer el separador que desees al nombre de la variable: 

```
'path' => '{collection}/{-filename}'                 // 'posts/my-first-blog-post'
'path' => '{collection}/{_filename}'                 // 'posts/my_first_blog_post'
```

If you included a date as a variable in your collection items (in YYYY-MM-DD format), you can control the formatting of that date in your path by following the variable name with a pipe and using PHP date formatting codes. For any `/`s in your date formatting code, Jigsaw will create subdirectories as needed:

Si incluyes la fecha como variable en los elementos de tu colección (en el formato YYYY-MM-DD), puedes controlar el formato en que se muestra la fecha en la ruta agregando el carácter separador `|` y usando códigos de formato de fecha de PHP. Además, Jigsaw creará sub-directorios como sea necesario, cada vez que agregues `/` en el formato de fecha.  

```
'path' => '{collection}/{published|Y-m-d}/{-title}'  // 'posts/2017-03-27/title-of-first-post'
'path' => '{collection}/{published|Y/m}/{-title}'    // 'posts/2017/03/title-of-first-post'
'path' => 'blog-{published|F-Y}/{-title}'            // 'blog-March-2017/title-of-first-post'
```


### Custom Path Closure
### Clausuras de rutas personalizadas https://es.wikipedia.org/wiki/Clausura_(inform%C3%A1tica)

Though the path shorthand allows you to easily create the most common permalink formats, you can also return a closure from `path` if you require more control. The closure will receive the contents of the current collection item as its first parameter. For example:

Así como el PATH SHORTHAND permite facilmente crear los más comunes formatos de "permalink", también puedes retornar un closure desde una ruta (`path`) si requieres más control. El closure recibira el contenido del elemento actual de la colección como su primer parámetro. Por ejemplo: 


```
use Illuminate\Support\Str;

'path' => function ($page) {
    return 'posts/' . ($page->featured ? 'featured/' : '') . Str::slug($page->getFilename());
},
```
