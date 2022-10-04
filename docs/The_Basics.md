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
## Include CSS and JavaScript
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

