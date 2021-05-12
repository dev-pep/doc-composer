# Paquetes

Para ver los paquetes disponibles, se puede navegar en <https://packagist.org>.

Los nombres de los proyectos se componen de nombre del *vendor* (desarrollador del paquete) y el nombre del paquete en sí, de la forma ***vendor/paquete***.

Todas las dependencias que definamos quedan reflejadas en el archivo ***composer.json***.

Cuando instalamos paquetes con *composer*, se crea un directorio ***vendor*** en el directorio raíz del proyecto, que es donde instalará las dependencias del proyecto.

> Si usamos *git*, es buena idea incluir el directorio ***vendor*** en ***.gitignore***.

## Paquetes de la plataforma

En *composer* pueden definirse (a través de ***composer.json***) versiones de paquetes que no son gestionados por *composer* mismo, sino por el entorno en el que se encuentra. Se trata de paquetes (*virtuales*) instalados en el sistema sobre los que *composer* no tiene ningún control.

De este modo podemos requerir una versión (o versiones) de *PHP* (***php***), una extensión de este (***ext-<nombreext>***), o una biblioteca del sistema (***lib-<nombrelib>***).
