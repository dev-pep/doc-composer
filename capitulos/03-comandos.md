# Comandos

En formato *JSON*, `{...}` es un mapping (diccionario key: value), y `[...]` un *array*.

`composer init` ejecuta un *wizard* que solicita información del proyecto. Autor, tipo, licencia,... Crea un `composer.json` nuevo con la información aportada.

`composer require thevendor/thepackage` descarga el paquete *thevendor/thepackage* en la carpeta `vendor`, y actualiza el `composer.json` adecuadamente con ese requisito.

`composer require --dev thevendor/thepackage` hace lo mismo que el anterior, pero en lugar de añadirlo a la *key* `"require"`, lo añade a la `"require-dev"`. Estos paquetes no se instalan en un servidor de producción, solo en uno de desarrollo.

`composer update` descarga y actualiza los paquetes instalados (y los no existentes pero requeridos) a la versión más reciente posible según requisitos y restricciones. Si hay paquetes en `vendor` que no están requeridos en `composer.json`, los elimina. Actualiza `composer.lock`, que es una instantánea que describe los paquetes instalados, indicando las versiones precisas actuales.

`composer install` instala los paquetes según la definición de `composer.lock`. Esto es útil, por ejemplo, si queremos replicar las mismas dependencias en otro equipo: solo hay que copiar `composer.lock` en el otro equipo y ejecutar `composer install` en él para tener exactamente el mismo estado de dependencias en los dos lados. En el caso de que no exista `composer.lock`, ejecuta `composer update`.

`composer remove thevendor/thepackage` desinstala (elimina) el paquete especificado de disco, y la entrada correspondiente de `composer.json`.

`composer create-project thevendor/thepackage [dir]` instala el paquete, pero en lugar de instalar en `vendor` y añadir a `composer.json`, lo descarga como proyecto a la carpeta `dir` (que si no lo especificamos, se llamará como el paquete). Esta carpeta resultante es la carpeta del nuevo proyecto.

Si tecleamos simplemente `composer create-project` en un directorio que contiene `composer.json`, instala los paquetes requeridos en el directorio actual directamente, en lugar de en `vendor` u otra carpeta. La carpeta actual es la carpeta del nuevo proyecto.

Se puede especificar una versión al crear un proyecto. Por ejemplo, para crear un proyecto *laravel 7.0*:

`composer create-project laravel/laravel myproject 7.0`

o

`composer create-project laravel/laravel:7.0 myproject`

El comando `global` se indica justo antes de install, update, require y remove, para trabajar en el directorio de configuración de *composer*, haciendo que los paquetes estén disponibles para todos los proyectos del sistema.
