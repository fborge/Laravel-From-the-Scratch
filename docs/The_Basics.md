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

