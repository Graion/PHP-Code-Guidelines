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



### Sentencias que abarquen multiples lineas DEBEN ser identadas y empezar con un operador

Cuando una sentencia es demasiado larga para ser legible en una linea, deberia
ser cortada. Cuando cortas una sentencia, es mejor que la siguientes lineas
esten identadas y empiecen con un operador, identificando facilmente que
pertenecen a la linea anterior. Por ejemplo;
	$someVar = 'this is a very long line of text that wraps '
		. 'onto the next line';
	y
		if (($a > 4 && stristr($text, 'sentence'))
			|| $a <= 4
		) {
			…
		}

### Quoting strings

PHP permite el uso de comillas simples (') y dobles (") cuando usamos strings.
Es recomendado usar comillas simples en la mayoria, pero no en todos, los casos.
Mientras que las comillas dobles son convenientes porque permiten la
substitucion de variables, las comillas simples son mejores para la legibilidad.

Usando el siguiente ejemplo:
	$b = 'sentence';
	$text = 'this is a ' . $b;
es preferible sobre:
	$b = 'sentence';
	$text = "this is a $b";
Aunque no debe ser siempre asi.
Es, sin embargo, mas conveniente usar comillas simples si el string contiene
comillas dobles.

### Definiendo arrays

Cuando se define un array el corchete de inicio NO DEBE tener un espacio antes.
Es RECOMENDADO que sea seguido por una linea nueva, aunque los arrays pequeños
PODRIAN ser definidos con multiples valores en una linea. Tambien es RECOMENDADO
que el corchete de cierre este en una nueva linea. Ejemplos:

$user = [
	'name' => 'John',
	'address' => '123 Main St.'
];
Lo anterior es preferible, aunque lo siguiente esta permitido ya que es la
definicion de un pequeño array:

$user = ['name' => 'John', 'address' => '123 Main St.'];

De ser posible utilizar la sintaxis corta [] para definir arrays en lugar de
array().

### Comentarios
Comentarios de linea-simple C (//) y multi-linea C (/* */) estan permitidos.
Comentarios Perl (#) no lo estan.

### Variables

Los nombres de variables DEBERIAN ser descriptivos y no contener abreviaturas.
Las variables que representan valores escalares DEBERIAN ser en minusculas y con
las palabras separadas por guiones bajos. Las variables que representen objetos
DEBERIAN ser camel-case con la primer letra de cada palabra (excepto la primera)
en mayuscula. Ejemplo:
	$minimum_bid = 5;
	$sectionBundle = new SectionBundle();
Las propiedades de los objetos, sin embargo, DEBERIAN siempre ser camel-case
independientemente del valor.

### Global State
La creacion de variables globales es altamente desalentado y DEBERIA ser evitado.
Igual que los Singletons, que DEBERIAN ser evitados a cualquier costo. ಠ_ಠ

### Constantes
Las contstantes DEBERIAN estar en mayuscula, los guiones bajos DEBEN ser usador
para separar palabras (ej. INLUDE_PATH). Las constantes NO DEBEN empezar o
terminar con guion bajo.

### Estructuras de control
Switch
El switch DEBERIA incluir el default case y DEBE estar ubicado en el final.

Funciones, Metodos y Closures
------------------------------
Esta seccion esbozará las mejores practicas cuando llamamos y definimos
funciones, metodos y closures.

### Return
Los "returns" NO DEBEN tener rodeado el valor devuelto con parentesis. Los
valores devueltos DEBEN ser consistentes; una funcion que devuelve un array de
objetos DEBERIA deolver un array aunque este contenga solo u objeto. Una funcion
DEBERIA lanzar una excepción si se produce un error irrecuperable.

### Nomenclatura
Solo los metodos magicos PODRIAN empezar con uno o mas guiones bajos.
Para mejorar la visibilidad de quien no esté utilizando un IDE sugerimos: solo
las funciones protected y privadas PODRIAN empezar con guion bajo.

Buenas Prácticas
----------------

### Usar Composer!

### Documentar el código

Programar es una actividad de grupo y es importante que nos comuniquemos bien,
tanto fuera como dentro del código. La mejor manera de lograr una buena
comunicación dentro del código de un proyecto es documentar los métodos y de ser
necesario, la funcionalidad interna si esta no fuera evidente solo con el código
escrito.

Igual de importante es no repetir en comentario lo que el código expresa bién
por sí solo. Be DRY (Don't Repeat Yourself)!

### Leverage the community

La comunidad de PHP crece y se perfecciona cada día, si existe una herramienta
que hace lo que necesitamos, usémosla! No re-inventemos la rueda a menos que sea
muy necesario.

### Seguir los principios SOLID

Siguiendo estos principios nos aseguramos que nuestro código sea lo más limpio y
flexíble posible.

#### Single responsibility

Cada clase tiene que tenér un único propósito.

#### Open-Closed

Una clase tiene que estár abierta (Open) para extensión y cerrada (Closed) para
modificación.

Si una clase depende de un `switch` o `if`s tener en cuenta distintos casos,
quiere decir que si el día de mañana necesitamos tener en cuenta un caso extra,
tenemos que modificar la clase, efectivamente rompiendo este principio.

Para lograr resolver esto, es mejor dar vuelta las responsabilidades y usar
interfases para ocultar implementaciones particulares.

Este ejemplo rompe con este principio, ya que si necesitaramos poder renderizar
a HTML o más formatos, tendríamos que modificar esta clase.

```php
<?php
class Output
{
    private $data;

    public function getData()
    {
        return $this->data;
    }

    public function setData(array $data)
    {
        $this->data = $data;
    }

    public function render($format = 'xml')
    {
        $out = '';
        $data = $this->getData();

        switch ($format)
        {
            case 'json':
                $out = json_encode($data);
                break;

            case 'xml':
                $out = '<data>';

                foreach ($data as $value)
                {
                    $out .= '<value>' . $value . '</value>';
                }

                $out .= '</data>';
                break;

            default:
                throw new Exception("Unexpected format [$format]");
        }

        return $out;
    }
}
?>
```

En este caso es preferible delegar la responsabilida del render a otra clase y
dejar que Output se encargue simplemente de usarla:

```php
<?php

interface Renderer
{
    public function render(array $data);
}

class JsonRenderer implements Renderer
{
    public function render(array $data)
    {
        return json_encode($data);
    }
}

class XmlRenderer implements Renderer
{
    public function render(array $data)
    {
        $out = '<data>';

        foreach ($data as $value)
        {
            $out .= '<value>' . $value . '</value>';
        }

        $out .= '</data>';

        return $out;
    }
}

class Output
{
    // ...

    public function render(Renderer $renderer)
    {
        return $renderer->render($this->getData());
    }
}

?>
```

Si estuvieron atentos, se habrán dado cuenta de que éste no es el único
principio que estában siendo trasgredido. En general, al caer uno, cae el resto.

Al solucionarlo de esta manera, Output ya no tiene la responsabilidad extra de
resolver el renderizado de su data, efectivamente resolviendo también una
violación al Single Responsability.

#### Liskov Substitution

A subclass' preconditions should be at least as weak and its postconditions
should be at least as strong as its parent.

#### Interface Segregation

Una clase no debería depender de otra clase con un grán número de métodos de los
cuales solo usa algunos.

Es mejor separar esas estos métodos

#### Dependency Inversion

A that defines an abstract or high-level functionality should never depend on
any class or method that defines a concrete or low-level functionality.

### Dividir métodos largos en varios métodos más chicos

### Composición sobre herencia

