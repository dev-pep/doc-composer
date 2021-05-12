# Comandos

> En formato *JSON*, `{...}` es un mapping (diccionario key: value), y `[...]` un *array*.

`composer init` ejecuta un *wizard* que solicita información del proyecto. Autor, tipo, licencia,... Crea un `composer.json` nuevo con la información aportada.

`composer require thevendor/thepackage` descarga el paquete *thevendor/thepackage* en la carpeta `vendor`, y actualiza el `composer.json` adecuadamente con ese requisito.

`composer require --dev thevendor/thepackage` hace lo mismo que el anterior, pero en lugar de añadirlo a la *key* `"require"`, lo añade a la `"require-dev"`. Estos paquetes no se instalan en un servidor de producción, solo en uno de desarrollo.

`composer update` descarga y actualiza los paquetes instalados (y los no existentes pero requeridos) a la versión más reciente posible según requisitos y restricciones. Se encarga de instalar también todas las dependencias de todos los paquetes. Si hay paquetes en `vendor` que no están requeridos en `composer.json` y no son necesarios, los elimina. Actualiza (o crea, si no existe) `composer.lock`, que es una **instantánea** que describe los paquetes instalados, indicando las versiones que están instaladas actualmente.

Si solo deseamos actualizar un paquete determinado:

 ```
 composer update vendor/paquete
 ```

`composer install` instala los paquetes según la definición de `composer.lock`, es decir, recrea esa última instantánea. Esto es útil, por ejemplo, si queremos replicar las mismas dependencias en otro equipo: solo hay que copiar `composer.lock` en el otro equipo y ejecutar `composer install` en él para tener exactamente el mismo estado de dependencias en los dos lados. En el caso de que no exista `composer.lock`, ejecuta `composer update`.

`composer remove thevendor/thepackage` desinstala (elimina) el paquete especificado de disco, y la entrada correspondiente de `composer.json`.

`composer create-project thevendor/thepackage [dir]` instala el paquete, pero en lugar de instalar en `vendor` y añadir a `composer.json`, lo descarga como proyecto a la carpeta `dir` (que si no lo especificamos, se llamará como el paquete). Esta carpeta resultante es la carpeta del nuevo proyecto.

Si tecleamos simplemente `composer create-project` en un directorio que contiene `composer.json`, instala los paquetes requeridos en el directorio actual directamente, en lugar de en `vendor` u otra carpeta. La carpeta actual es la carpeta del nuevo proyecto.

Se puede especificar una versión al crear un proyecto. Por ejemplo, para crear un proyecto *laravel 7.0*:

`composer create-project laravel/laravel myproject 7.0`

o

`composer create-project laravel/laravel:7.0 myproject`

El comando `global` se indica justo antes de install, update, require y remove, para trabajar en el directorio de configuración de *composer*, haciendo que los paquetes estén disponibles para todos los proyectos del sistema.

## Autoloading

Para las bibliotecas que proporcionan *autoload*, *composer* crea un archivo ***vendor/autoload.php***, de tal modo que incluyendo ese archivo en algún punto de nuestro proyecto, quedarán todas esas bibliotecas autocargadas en nuestro código fuente. Aunque lo podríamos incluir con `include`, es mejor hacerlo con `require`.

Si queremos añadir elementos propios al *autoload*, podemos hacerlo en ***composer.json***:

```json
{
    "autoload": {
        "psr-4": {"Acme\\": "src/"},
        "psr-4": {"Acme\\Fuu\\": "src2/"}
    }
}
```

Tras modificar el apartado de *autoloading* manualmente, hay que ejecutar:

`composer dump-autoload`

De este modo, se añadirá este mapeo en ***vendor/autoload.php***.

### PSR-4

El ejemplo anterior añade un *autoloader PSR-4* para el *namespace* ***Acme*** (*PSR-4* define el mapeo entre los *namespaces* y los directorios, y el nombre de la clase con el nombre del archivo que la define). En este sentido, estamos definiendo nuestro propio mapeo, del directorio ***src*** (relativo al **raíz del proyecto**) al *namespace* ***Acme***.

En el ejemplo anterior, si en el código fuente aparece la clase ***Acme/Foo/Faa/myClase***, se buscará en ***src/Foo/Faa/myClase.php***. Y la clase ***Acme/Fuu/Faa/myOtraClase***, se buscará en ***src2/Faa/myOtraClase.php***.

Los *namespaces* deben terminar en barra invertida, ya que si no, `"Acme"` coincidiría con clases en *namespaces* como ***AcmeFoo***, ***AcmeBar***,...

Es posible buscar una clase en más de un directorio hasta encontrarlo:

`"psr-4": {"Acme\\": ["src/", "src2/", "src3/"]}`

También podemos definir un (o varios) directorio *fallback* para el resto de clases:

`"psr-4": {"": "src/"}`

### PSR-0

*PSR-0* es similar a *PSR-4*, pero con algunas diferencias que le dan compatibilidad con viejos estilos de mapeo. En el ejemplo anterior, en lugar de mapear ***Acme/Fuu/Faa/myOtraClase*** a ***src2/Faa/myOtraClase.php***, lo haría a ***src2/Acme/Fuu/Faa/myOtraClase.php***. Por otro lado, permite también mapear, no solo *namespaces*, sino el nombre de una clase.

### Classmap y Files

El tipo de *autoloading* `classmap` busca en los directorios y archivos especificados y **escanea** todas las clases que estén ahí definidas (en archivos *.php* y *.inc*). En los nombres se pueden usar el *wildcard* ***\****.

Si queremos excluir archivos del *classmap*, se usará `exclude-from-classmap`. Se puede usar el *wildcard* ***\****, que coincide con todos los caracteres exceptuando la barra (***/***), o ***\*****, que coincide con todos los caracteres sin excepción.

Por otro lado, se pueden requerir (`require`) explícitamente archivos usando `files`.

```json
{
    "autoload": {
        "classmap": ["src/addons/*/lib/", "3rd-party/*", "Something.php"],
        "exclude-from-classmap": ["/Tests/", "/test/", "/tests/"],
        "files": ["src/MyLibrary/functions.php"]
    }
}
```
