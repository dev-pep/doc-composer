# Restricción de versiones

Las restricciones se pueden editar en el `composer.json` o especificarse con el comando `composer require`, como por ejemplo:

`composer require "vendor/packa:2.*" "vendor/packb:~2.1"`

## Formato de las restricciones

- `1.5` - versión única.
- `>=1.0` indica mayor o igual a 1.0.
- `>=1.0 <2.0` indica mayor o igual a 1.0 **y** menor a 2.0. Cuando hay varias condiciones, un espacio o una coma actúa como ***AND***. Si indicamos `||`, se entenderá ***OR***.
- `>=1.0 <1.1 || >=1.2` indica mayor o igual a 1.0 y menor a 2.0, o también mayor o igual a 1.2.
- `1.0.*` equivale a `>=1.0 <1.1`.
- `1.*` equivale a `>=1.0 <2.0`.
- `1.0-2.0` equivale a `>=1.0.0 <2.1.0`. Decir `<2.1` es lo mismo que decir `<2.1.0`.
- `1.0.0-2.1.0` equivale a `>=1.0.0 <=2.1.0`.
- `~1.2` equivale a `>=1.2 <2.0`.
- `~1.2.3` equivale a `>=1.2.3 <1.3.0`.

El operador `~` permite versiones en las que **únicamente el último** número especificado puede ser tan grande como se desee:
- `^1.2` equivale a `>=1.2 <2.0`.
- `^1.2.3` equivale a `>=1.2.3 <2.0`.
- El operador `^` permite versiones hasta la *siguiente versión mayor* (no incluida), para evitar que se rompa la posible compatibilidad. Como excepción, en las versiones *pre-1.0*, se considera el segundo número como versión mayor:
- `^0.3` equivale a `>=0.3 <0.4`.

Hay otras indicaciones de tipo `dev-master`, `alpha`, etc.
