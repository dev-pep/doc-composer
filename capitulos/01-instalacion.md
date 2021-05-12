# Instalación de Composer

Se instala ejecutando el *script* que nos proporciona <https://getcomposer.org/>.

El *script* deja en el directorio actual un archivo ***composer.phar***, que se ejecuta como:

```
php composer.phar
```

En sistemas *Unix*, se puede ejecutar directamente como `composer.phar`, ya que tiene la correspondiente línea *shebang*. En este caso, deben otorgarse permisos de ejecución a este script.

Si queremos que esté disponible en todo el sistema, se debe copiar a un directorio en el ***PATH***, como por ejemplo, ***/usr/local/bin***. De lo contrario habrá que especificar la ruta del *script* (`./composer.phar` si está en el directorio actual).

También es útil renombrarlo como ***composer*** a secas.

Los paquetes que queramos instalar a nivel global, no solo en el proyecto actual, se guardan en el directorio de configuración de *composer*. En *Linux*, los archivos ejecutables de un paquete instalado **globalmente** van al directorio ***~/.config/composer/vendor/bin***.

Por ejemplo, si queremos disponer del instalador de aplicaciones *laravel*, teclearemos:

```
composer global require laravel/installer
```

Esto instalará el instalador. Para que los ejecutables de los paquetes instalados globalmente en *composer* estén disponibles en el ***PATH***, editaremos nuestro ***.bashrc***, añadiendo:

```
export PATH="$PATH:$HOME/.config/composer/vendor/bin"
```

Ahora ya podríamos usar el instalador de *laravel* desde cualquier sitio:

```
laravel new nombreApp
```

Esto crearía un directorio ***nombreApp*** con un proyecto *laravel* (con su correspondiente archivo ***index.php*** en ***nombreApp/public***, etc.).
