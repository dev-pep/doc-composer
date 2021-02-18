# Paquetes

Para ver los paquetes disponibles, se puede navegar en <https://packagist.org>.

Cuando instalamos paquetes con *composer*, se crea un directorio `vendor` en el directorio raíz del proyecto, que es donde instalará las dependencias del proyecto.

Se creará un archivo `vendor/autoload.php` dentro del proyecto, de tal modo que incluyendo ese archivo quedarán todas las dependencias incluidas.

Aunque lo podríamos incluir con `include`, es mejor hacerlo con `require`.
