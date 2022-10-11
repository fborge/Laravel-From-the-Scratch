# The Basics

## Route Loads a View.
Dentro del directorio routes, en el recurso web.php se definira cada ruta
a utilizarse en la aplicación.
Estas rutas pueden ser simples como lo siguiente:
```php
Route::get('/', function () {
    return view('welcome');
});
```
O más elaboradas dependiendo de las posibles vistas de la aplicación.
```php
Route::get('/users/hello', function () {
    return view('welcome');
});
```
De igual forma se puede retornar lo que se desee en la vista por ejemplo un vista en formato JSON.
```php
Route::get('/users/hello', function () {
    return ['foo'=>'bar'];
});
```
## Include CSS and JavaScript.
Se modificará el recurso de la página de bienvenida ubicado en `../views/welcome.blade.php`. 
Se desplegara un simple "Hello World". 

```html
<!doctype html>

<title> My Laravel Blog </title>

<body>
    <h1> Hello World!!</h1>
</body>
```
Posteriormente para aplicar estilos creamos un recurso CSS en el directorio public `../public/app.css` que contiene estilos para el body de la página de bienvenida.

```css
body {
    background:olive;
    color: white;
}
```
Finalmente para aplicar dicho estilo a la vista se referencia en la página de bienvenida quedando el bloque
de código de la siguiente forma:

```html
<!doctype html>

<title> My Laravel Blog </title>
<link rel="stylesheet" href="/app.css">

<body>
    <h1> Hello World!!</h1>
</body>

```
## Make a route and link to it.
Desde el proyecto ubicandose en lfts.isw811.xyz/routes, editar el archivo web.php y modificar el nombre de la vista a la que se refiere.

```php
Route::get('/', function () {
    return view('welcome');
});
```
Cambiar para que refiera a una vista llamada `posts`.

```php
Route::get('/', function () {
    return view('posts');
});
```
Este modificacion lanzará un error al cargar el sitio, ya que no encuentra la vista a la que se refiere.

![Select users](../images/error-posts.png)

Así que desde el recurso ubincandose en lfts.isw811.xyz/resources/views, editar el nombre del archivo welcome.blade.php a posts.blade.php
y se podra cargar el sitio de manera normal.

Seguidamente editar el archivo `posts.blade.php` con lo siguiente, para simular el post de un articulo.

```html
<!doctype html>

<title> My Laravel Blog </title>
<link rel="stylesheet" href="/app.css">

<body>
    <article>
        <h1> My first Post</h1>
        <p>
            Lorem ipsum dolor sit amet consectetur, adipisicing elit. Minus id magni harum molestiae officia explicabo ipsam libero in fuga, velit magnam nam cupiditate mollitia tempora architecto modi ad laudantium repellendus.
        </p>
    </article>

     <article>
        <h1> My Second Post</h1>
        <p>
            Lorem ipsum dolor sit amet consectetur, adipisicing elit. Minus id magni harum molestiae officia explicabo ipsam libero in fuga, velit magnam nam cupiditate mollitia tempora architecto modi ad laudantium repellendus.
        </p>
    </article>

    <article>
        <h1> My Third Post</h1>
        <p>
            Lorem ipsum dolor sit amet consectetur, adipisicing elit. Minus id magni harum molestiae officia explicabo ipsam libero in fuga, velit magnam nam cupiditate mollitia tempora architecto modi ad laudantium repellendus.
        </p>
    </article>
    
</body>
```
Ahora teniendo estos post se implementa el uso de rutas para ser llevado a otra página por medio de links.

Ubicandose en lfts.isw811.xyz/routes, editar el archivo web.php y agregar una nueva ruta de método `post` quedando de la siguiente forma:

```php
Route::get('/', function () {
    return view('posts');
});


Route::get('post', function () {
    return view('post');
});
```
Ubincandose en lfts.isw811.xyz/resources/views, editar el archivo posts.blade.php, se agregara a los articulos referencia a la nueva ruta creada.

```html
<!doctype html>

<title> My Laravel Blog </title>
<link rel="stylesheet" href="/app.css">

<body>
    <article>
        <h1><a href="/post"> My First Post</a></h1>
        <p>
            Lorem ipsum dolor sit amet consectetur, adipisicing elit. Minus id magni harum molestiae officia explicabo ipsam libero in fuga, velit magnam nam cupiditate mollitia tempora architecto modi ad laudantium repellendus.
        </p>
    </article>

    <article>
        <h1><a href="/post"> My Second Post</a></h1>
        <p>
            Lorem ipsum dolor sit amet consectetur, adipisicing elit. Minus id magni harum molestiae officia explicabo ipsam libero in fuga, velit magnam nam cupiditate mollitia tempora architecto modi ad laudantium repellendus.
        </p>
    </article>
    
    <article>
        <h1><a href="/post"> My Third Post</a></h1>
        <p>
            Lorem ipsum dolor sit amet consectetur, adipisicing elit. Minus id magni harum molestiae officia explicabo ipsam libero in fuga, velit magnam nam cupiditate mollitia tempora architecto modi ad laudantium repellendus.
        </p>
    </article>
</body>
```
Al realizar la referencia se obtendra un error ya que la vista de Post aun no esta creada, para eso ubicarse en lfts.isw811.xyz/resources/views y crear una nueva vista llamada post.blade.php que contiene:

```html
<!doctype html>

<title> My Laravel Blog </title>
<link rel="stylesheet" href="/app.css">

<body>
    <article>
        <h1><a href="/post"> My first Post</a></h1>
        <p>
            Lorem ipsum dolor sit amet consectetur, adipisicing elit. Minus id magni harum molestiae officia explicabo ipsam libero in fuga, velit magnam nam cupiditate mollitia tempora architecto modi ad laudantium repellendus.
        </p>
    </article>
    <a href="/">Go back..</a>
</body>
```
## Store Blog Posts as HTML Files.

Para que el recurso sea más dinámico, crear una variable `$post`, que redijirá y contendrá la información de los post del blog, para ello ubicarse en lfts.isw811.xyz/resources/views y modificar el archivo post.blade.php quedando de la siguente forma:

```html
<!doctype html>

<title> My Laravel Blog </title>
<link rel="stylesheet" href="/app.css">

<body>
    <article>
        <?= $post; ?>
    </article>
    <a href="/">Go back..</a>
</body>
```
Asi mismo ubicarse en lfts.isw811.xyz/resources y crear un nuevo directorio llamado posts, donde se crearan las vistas de los posts, el directorio se verá así:

![Select users](../images/posts-view.png)

El siguiente paso es tener una variable `$post` en el archivo de rutas para que apunte a sus respectiva vista, quedando así:

```php
Route::get('posts/{post}', function ($slug) {
    $path = __DIR__ . "/../resources/posts/{$slug}.html";
    if (! file_exists($path)) {
        return redirect('/');
    }
    $post = file_get_contents($path);
    return view('post', [
        'post'=> $post
    ]);
});
```
Para finalizar ya teniendo la página inicial de la siguiente forma:

![Select users](../images/post-init.png)

Se podrá acceder a la información individal de cada post en una página única e independiente, entrando en cada uno de los links.
