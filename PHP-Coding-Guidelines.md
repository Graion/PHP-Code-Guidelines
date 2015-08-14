PHP Coding Guidelines
=====================

Este documento está basado sobre los
[Standards PSR aceptados](https://github.com/php-fig/fig-standards/tree/master/accepted).
Detallamos solo los casos particulares o que PSR no cubra.

Las palabras clave "DEBE", "NO (SE) DEBE", "REQUERIDO", "PUEDE", "PUEDE NO",
"DEBERÍA", "NO (SE) DEBERÍA", "RECOMENDADO", "PODRÍA" y "OPCIONAL" en este documento
se deben interpretar cómo su equivalente en Inglés ("MUST", "MUST NOT",
"REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY",
and "OPTIONAL") tal como son descritas en [RFC 2119](http://www.ietf.org/rfc/rfc2119.txt).

Proyectos y Archivos nuevos
---------------------------

Esta sección detalla el inicio de un proyecto y la creación de los archivos PHP.

### Todos los proyectos DEBEN estár libres de `Warnings` y `Notices`.

Al empezar un proyecto es importante que el código a escribir esté bien pensado
y no haya comportamiento inesperado, con este fin todas las computadoras de
desarrollo DEBEN configurar error reporing a `E_ALL`. `Notices` y `Warnings` son
una indicación de que el código no está optimizado y pueden depender de los
caprichos del lenguaje PHP.

### Todos los archivos DEBEN empezar con `<?php`

Todos los archivos PHP DEBEN comenzar con la etiqueta PHP apertura `<?php`.
NO DEBEN utilizar la forma abreviada `<?` ni la forma de `echo` corta `<?="algo"?>`.

### Los archivos PHP NO DEBEN tener tag de cierre de PHP `?>`

Los archivos PHP son sintácticamente correctos cierren la etiqueta PHP al final
o no. Si un desarrollador introdujera un espacio después de la etiqueta de
cierre, causaría el famoso error `"Cannot modify header information – headers
already sent"`. Con el fin de impedir que esto suceda se DEBE omitir la
etiqueta PHP de cierre `?>`.

Cuestiónes Básicas
------------------

### NO SE DEBERÍA usar el operador de la supresión de error `@`

**A REVISAR**

Este operador puede parecer útil por las razones equivocadas.
Si se necesita suprimir un error, con toda probabilidad, hay un problema con el
código que debe ser abordado. Además, el operador de la supresión de error no le
impide a PHP invocar funciones de manejo de errores, que causa más sobrecarga por
primero deshabilitar el `error_reporting`, después de lo cual provoca que el
`error handler` se invoque. Entonces, el operador hace que el informe de errores
se restablezca a su valor original.
