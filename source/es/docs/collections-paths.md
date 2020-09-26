---
extends: _layouts.documentation
section: documentation_content
---

#### [Colecciones](/es/docs/collections)
## Rutas

### Configuración por defecto de las rutas

Por defecto, cada uno de los elementos de tu colección (si extienden una plantilla principal) serán asignados a la ruta compuesta por dos componentes, el primero corresponde al nombre de la colección, y el segundo, es el nombre del archivo convertido en una URL "slug", todo en minúsculas, separando cada palabra con un guión. Asi que, por defecto, la ruta al archivo `My First Blog Post.md` en una colección llamada `posts` será `/posts/my-first-blog-post`.

De todas formas, Jigsaw te brinda la habilidad de poder personalizar las rutas a tus colecciones, agregando el parámetro `path` al array de tu colección. 


### Rutas referenciadas

Puedes especificar la ruta de tu colección como un `string`. En estos strings, es posible referenciar el valor de cualquier variable definida en los parametros de la cabecera YAML del elemento de la colección, especificando el nombre de la variable entre corchetes `{}`. Si cada elemento de tu colección incluye una variable `title`, por ejemplo, puedes definir la ruta de la siguiente forma: 

```
'path' => 'blog/{title}'                             // 'blog/Title Of First Post'
```

Adicionalmente, las variables `filename` (que contiene el nombre del archivo sin incluir la extensión) y `collection` (conteniendo el nombre de la colección) también estan disponibles:

```
'path' => '{collection}/{filename}'                  // 'posts/my first blog post'
```

En la mayoría de los casos, cuando usas nombres de archivo (filenames) o títulos (title), podrías querer integrarlos como parte de la ruta. Para hacerlo debes anteponer el separador que desees al nombre de la variable: 

```
'path' => '{collection}/{-filename}'                 // 'posts/my-first-blog-post'
'path' => '{collection}/{_filename}'                 // 'posts/my_first_blog_post'
```

Si incluyes la fecha como variable en los elementos de tu colección (en el formato YYYY-MM-DD), puedes controlar el formato en que se muestra la fecha en la ruta agregando el carácter separador `|` y usando códigos de formato de fecha de PHP. Además, Jigsaw creará sub-directorios como sea necesario, cada vez que agregues `/` en el formato de fecha.  

```
'path' => '{collection}/{published|Y-m-d}/{-title}'  // 'posts/2017-03-27/title-of-first-post'
'path' => '{collection}/{published|Y/m}/{-title}'    // 'posts/2017/03/title-of-first-post'
'path' => 'blog-{published|F-Y}/{-title}'            // 'blog-March-2017/title-of-first-post'
```


### Closure personalizado para rutas

Así como las rutas referenciadas permiten facilmente crear los más comunes formatos de "permalink", también puedes retornar un closure desde una ruta (`path`) si requieres más control. El closure recibira el contenido del elemento actual de la colección como su primer parámetro. Por ejemplo: 


```
use Illuminate\Support\Str;

'path' => function ($page) {
    return 'posts/' . ($page->featured ? 'featured/' : '') . Str::slug($page->getFilename());
},
```
