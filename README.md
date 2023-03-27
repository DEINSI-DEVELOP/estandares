# Estándares

# [Commits Convencionales](https://www.conventionalcommits.org/es/v1.0.0/)

La especificación de Commits Convencionales es una convención ligera sobre los mensajes de commits. Proporciona un conjunto sencillo de reglas para crear un historial de commits explícito; lo que hace más fácil escribir herramientas automatizadas encima del historial. Esta convención encaja con **[SemVer](http://semver.org/lang/es/)**, al describir en los mensajes de los commits las funcionalidades, arreglos, y cambios de ruptura hechos.

## **¿Qué es Semantic Versioning o SemVer?**

A modo resumen, SemVer es la convención más extendida para establecer un versionado a librerías, paquetes, dependencias, y a la vida en general.

El versionado se divide en tres bloques:

```jsx
// MAJOR.MINOR.PATCH

2.12.7
// 2 -> MAJOR
// 12 -> MINOR
// 7 -> PATCH
```

- **MAJOR**: número de versión que se incrementa cuando se rompe la compatibilidad de versiones anteriores.
- **MINOR**: número de versión que se incrementa cuando se añade funcionalidad y esta es compatible en la versión MAJOR actual.
- **PATCH**: número de versión que se incrementa cuando se arreglan errores en la versión MAJOR.MINOR actual.

Adicionalmente está permitido (y es muy común) añadir al bloque PATCH información adicional indicando si son versiones previas a un nuevo lanzamiento (alpha, beta, next, rc, ...) y el número de la compilación. Esta información adicional debe ir en el bloque PATCH precedido por un guión `-`.

Ejemplo:

```jsx
12.2.0-alpha.0

// Aquí "alpha" indica el estado de la compilación y ".0" indica el número de compilación
```

## Tipos

El primer elemento es el tipo de commit refiriéndose al contenido del commit. Basados en la [convención establecida por Angular](https://github.com/angular/angular/blob/22b96b9/CONTRIBUTING.md#-commit-message-guidelines) son los siguientes:

- **feat**: cuando se añade una nueva funcionalidad.
- **fix**: cuando se arregla un error.
- **chore**: tareas rutinarias que no sean específicas de una feature o un error como por ejemplo añadir contenido al fichero `.gitignore` o instalar una dependencia.
- **test**: si añadimos o arreglamos tests.
- **docs**: cuando solo se modifica documentación.
- **build**: cuando el cambio afecta al compilado del proyecto.
- **ci**: el cambio afecta a ficheros de configuración y scripts relacionados con la integración continua.
- **style**: cambios de legibilidad o formateo de código que no afecta a funcionalidad.
- **refactor**: cambio de código que no corrige errores ni añade funcionalidad, pero mejora el código.
- **perf**: usado para mejoras de rendimiento.
- **revert**: si el commit revierte un commit anterior. Debería indicarse el hash del commit que se revierte.

### Ámbito

El campo ámbito es opcional y sirve para dar información contextual como por ejemplo indicar el nombre de la feature a la que afecta el commit.

### Descripción

Breve descripción del cambio cumpliendo lo siguiente:

- usa imperativos, en tiempo presente: “añade” mejor que “añadido” o “añadidos”
- la primera letra siempre irá en minúscula
- no escribir un punto al final

### Cuerpo

Es opcional y debería añadir aportar más información que la descripción. Debería usar el mismo tono imperativo que esta.

### Nota al pie

Es opcional. Siempre se utiliza para indicar cambios que rompan la compatibilidad de la versión actual (Breaking Changes) aunque también están permitidos otros formatos que sigan la convención de [git trailer format](https://git-scm.com/docs/git-interpret-trailers).

El mensaje del commit debe ser estructurado de la siguiente manera:

```php
<tipo>[ámbito opcional]: <descripción>

[cuerpo opcional]

[nota(s) al pie opcional(es)]
```

El commit contiene los siguientes elementos estructurales, para comunicar la intención a los consumidores de tu librería:

1. **fix:** un commit de *tipo* `fix` corrige un error en la base del código (se correlaciona con **`[PATCH](http://semver.org/#summary)`** en el Versionado Semántico).
2. **feat:** un commit de *tipo* `feat` introduce una nueva funcionalidad en la base del código (se correlaciona con **`[MINOR](http://semver.org/#summary)`** en el Versionado Semántico).
3. **BREAKING CHANGE:** un commit que contiene la nota al pie `BREAKING CHANGE:`, o que agrega un `!` después del tipo/ámbito, introduce un cambio de ruptura de API (se correlaciona con **`[MAJOR](http://semver.org/#summary)`** en el Versionado Semántico). Un BREAKING CHANGE puede ser parte de commits de cualquier *tipo*.
4. *tipos* distintos a `fix:` y `feat:` están permitidos, por ejemplo **[@commitlint/config-conventional](https://github.com/conventional-changelog/commitlint/tree/master/%40commitlint/config-conventional)** (basados en **[la convención de Angular](https://github.com/angular/angular/blob/22b96b9/CONTRIBUTING.md#-commit-message-guidelines)**) que recomienda `build:`, `chore:`, `ci:`, `docs:`, `style:`, `refactor:`, `perf:`, `test:`, y otros.
5. *notas al pie* distintas de `BREAKING CHANGE: <descripción>` pueden ser añadidas y siguen una convención similar al **[formato git trailer](https://git-scm.com/docs/git-interpret-trailers)**.

Tipos adicionales no son obligatorios en la especificación de Commits Convencionales, y no tienen un efecto implícito en el Versionado Semántico (al menos que incluyan un BREAKING CHANGE). Un ámbito puede ser añadido al tipo de un commit, para proveer información adicional contextual y debe ser contenido entre paréntesis, ej., `feat(parser): add ability to parse arrays`.

## Ejemplos:

<aside>
<img src="https://www.notion.so/icons/command-line_blue.svg" alt="https://www.notion.so/icons/command-line_blue.svg" width="40px" /> ****Mensaje de commit con descripción y cambio de ruptura en la nota al pie****

</aside>

```bash
feat: allow provided config object to extend other configs

BREAKING CHANGE: `extends` key in config file is now used for extending other config files
```

<aside>
<img src="https://www.notion.so/icons/command-line_blue.svg" alt="https://www.notion.so/icons/command-line_blue.svg" width="40px" /> ****Mensaje de commit con `!` para llamar la atención al cambio de ruptura**

</aside>

```bash
refactor!: drop support for Node 6
```

<aside>
<img src="https://www.notion.so/icons/command-line_blue.svg" alt="https://www.notion.so/icons/command-line_blue.svg" width="40px" /> ****Mensaje de commit con ambos `!` y BREAKING CHANGE en la nota al pie**

</aside>

```bash
refactor!: drop support for Node 6

BREAKING CHANGE: refactor to use JavaScript features not available in Node 6.
```

<aside>
<img src="https://www.notion.so/icons/command-line_blue.svg" alt="https://www.notion.so/icons/command-line_blue.svg" width="40px" /> ****Mensaje de commit sin cuerpo****

</aside>

```bash
docs: correct spelling of CHANGELOG
```

<aside>
<img src="https://www.notion.so/icons/command-line_blue.svg" alt="https://www.notion.so/icons/command-line_blue.svg" width="40px" /> ****Mensaje de commit con ámbito****

</aside>

```bash
feat(lang): added polish language
```

<aside>
<img src="https://www.notion.so/icons/command-line_blue.svg" alt="https://www.notion.so/icons/command-line_blue.svg" width="40px" /> ****Mensaje de commit con cuerpo multi-párrafo y múltiples notas al pie****

</aside>

```bash
fix: correct minor typos in code

see the issue for details

on typos fixed.

Reviewed-by: Z
Refs #133
```

## ****Especificación****

Las palabras clave “DEBE” (“MUST”), “NO DEBE” (“MUST NOT”), “REQUERIDO” (“REQUIRED”), “DEBERÁ” (“SHALL”), “NO DEBERÁ” (“SHALL NOT”), “DEBERÍA” (“SHOULD”), “NO DEBERÍA” (“SHOULD NOT”), “RECOMIENDA” (“RECOMMENDS”), “PUEDE” (“MAY”) y “OPCIONAL” (“OPTIONAL”) en este documento se deben interpretar como se describe en **[RFC 2119](https://www.ietf.org/rfc/rfc2119.txt)**.

1. Los commits DEBEN iniciarse con un prefijo de tipo que consiste en un sustantivo, `feat`, `fix`, etc., seguido del ámbito OPCIONAL, `!`OPCIONAL, y dos puntos y un espacio REQUERIDO.
2. El tipo `feat` DEBE ser usado cuando un commit agrega una nueva funcionalidad a la aplicación o librería.
3. El tipo `fix` DEBE ser usado cuando el commit representa una corrección a un error en el código de la aplicación (bug).
4. Un ámbito PUEDE ser añadido después de un tipo. Un ámbito DEBE consistir en un sustantivo que describa una sección de la base del código encerrado entre paréntesis, ej., `fix(parser):`.
5. Una descripción DEBE ir inmediatamente después de los dos puntos y el espacio del prefijo de tipo/ámbito. La descripción es resúmen corto de los cambios realizados en el código, ej., *fix: array parsing issue when multiple spaces were contained in string.*.
6. Un cuerpo de commit más extenso PUEDE agregarse después de la descripción corta, dando información contextual adicional acerca de los cambios en el código. El cuerpo DEBE iniciar después de una línea en blanco después de la descripción.
7. Un cuerpo de commit es de forma-libre y PUEDE consistir de cualquier número de párrafos separados por una nueva línea.
8. Una o más notas al pie PUEDEN ser añadidas una línea en blanco después del cuerpo. Cada nota al pie DEBE consistir de una palabra clave, seguida ya sea por un separador `:<espacio>` o `<espacio>#`, seguido por un valor cadena (string) (esto está inspirado por la **[convención git trailer](https://git-scm.com/docs/git-interpret-trailers)**).
9. Una palabra clave de una nota al pie DEBE usar `` en lugar de caracteres de espacios en blanco, ej., `Acked-by` (esto ayuda a diferenciar la sección de la nota al pie de un cuerpo multi párrafo). Se hace una excepción para `BREAKING CHANGE`, que también PUEDE ser usada como palabra clave.
10. Una nota al pie PUEDE contener espacios y líneas en blanco, y el parseo DEBE terminar cuando se observe el siguiente separador/clave.
11. Los cambios de ruptura DEBEN ser indicados en el prefijo de tipo/ámbito de un commit, o como una entrada en la nota al pie.
12. Si se incluye como una nota al pie, un cambio de ruptura DEBE consistir del texto en mayúsculas BREAKING CHANGE, seguido de dos puntos, y una descripción, ej., *BREAKING CHANGE: environment variables now take precedence over config files*.
13. Si se incluye en el prefijo de tipo/ámbito, cambios de ruptura DEBEN ser indicados por un `!` inmediatamente después de `:`. Si `!` es usado, `BREAKING CHANGE:` PUEDE ser omitido de la sección de la nota al pie, y la descripción del commit DEBERÁ ser usada para describir el cambio de ruptura.
14. Tipos diferentes a `feat` y `fix` PUEDEN ser usados en los mensajes de commit, ej., *docs: updated ref docs.*.
15. Las unidades de información que componen Commits Convencionales NO DEBEN ser tratados como implementadores sensitivos de caso, con la excepción de BREAKING CHANGE que DEBE ir en mayúsculas.
16. BREAKING-CHANGE DEBE ser sinónimo de BREAKING CHANGE, cuando se usa en una nota al pie.

# [Estándares PSR](https://www.php-fig.org/psr/psr-12/)

## PSR-12

Esta especificación amplía, expande y sustituye a PSR-2, la guía de estilo de codificación, y exige el cumplimiento de PSR-1, la norma básica de codificación.

Al igual que PSR-2, la intención de esta especificación es reducir la fricción cognitiva al escanear código de diferentes autores. Lo hace enumerando un conjunto compartido de reglas y expectativas sobre cómo formatear el código PHP. Esta PSR busca proporcionar un conjunto de formas que las herramientas de estilo de codificación puedan implementar, los proyectos puedan declarar su adhesión y los desarrolladores puedan relacionar fácilmente entre diferentes proyectos. Cuando varios autores colaboran a través de múltiples proyectos, ayuda tener un conjunto de directrices para ser usadas entre todos esos proyectos.

La PSR-2 fue aceptada en 2012 y, desde entonces, se han introducido una serie de cambios en PHP que repercuten en las directrices de estilo de codificación. Mientras que la PSR-2 es muy completa en cuanto a la funcionalidad de PHP que existía en el momento de su redacción, la nueva funcionalidad está muy abierta a la interpretación. Esta PSR, por lo tanto, pretende aclarar el contenido de la PSR-2 en un contexto más moderno con la nueva funcionalidad disponible, y hacer que la fe de erratas de la PSR-2 sea vinculante.

Ejemplo
Este ejemplo engloba algunas de las reglas que figuran a continuación a modo de resumen rápido:

```php
<?php

declare(strict_types=1);

namespace Vendor\Package;

use Vendor\Package\{ClassA as A, ClassB, ClassC as C};
use Vendor\Package\SomeNamespace\ClassD as D;

use function Vendor\Package\{functionA, functionB, functionC};

use const Vendor\Package\{ConstantA, ConstantB, ConstantC};

class Foo extends Bar implements FooInterface
{
    public function sampleFunction(int $a, int $b = null): array
    {
        if ($a === $b) {
            bar();
        } elseif ($a > $b) {
            $foo->bar($arg1);
        } else {
            BazClass::bar($arg2, $arg3);
        }
    }

    final public static function bar()
    {
        // method body
    }
}
```

> 2.1 Norma básica de codificación
> 

El código DEBE seguir todas las reglas descritas en PSR-1.

El término 'StudlyCaps' en PSR-1 DEBE interpretarse como PascalCase donde la primera letra de cada palabra se escribe en mayúscula, incluyendo la primera letra.

> 2.2 Archivos
> 

Todos los archivos PHP DEBEN usar únicamente el final de línea Unix LF (salto de línea).

Todos los archivos PHP DEBEN terminar con una línea que no esté en blanco, terminada con una sola LF.

La etiqueta de cierre ?> DEBE ser omitida en archivos que contengan únicamente PHP.

> 2.3 Líneas
> 

NO DEBE haber un límite duro en la longitud de las líneas.

El límite blando de longitud de línea DEBE ser de 120 caracteres.

Las líneas NO DEBEN ser más largas de 80 caracteres; las líneas más largas DEBEN ser divididas en múltiples líneas subsecuentes de no más de 80 caracteres cada una.

NO DEBE haber espacios en blanco al final de las líneas.

Pueden añadirse líneas en blanco para mejorar la legibilidad y para indicar bloques de código relacionados, excepto cuando esté explícitamente prohibido.

NO DEBE haber más de una sentencia por línea.

> 2.4 Sangría
> 

El código DEBE usar una sangría de 4 espacios por cada nivel de sangría, y NO DEBE usar tabuladores para sangrar.

2.5 Palabras clave y tipos

Todas las palabras clave y tipos reservados de PHP [1][2] DEBEN estar en minúsculas.

Cualquier nuevo tipo y palabra clave añadida a futuras versiones de PHP DEBE estar en minúsculas.

Se DEBE usar la forma corta de las palabras clave de tipo, p.e. bool en lugar de boolean, int en lugar de integer, etc.

> 3. Declaraciones Declare, Namespace y Declaraciones Import
> 

El encabezado de un archivo PHP puede consistir en un número de bloques diferentes. Si está presente, cada uno de los bloques a continuación DEBE estar separado por una sola línea en blanco, y NO DEBE contener una línea en blanco. Cada bloque DEBE estar en el orden listado a continuación, aunque los bloques que no sean relevantes pueden ser omitidos.

Etiqueta Bloque de documento a nivel de archivo.

Una o más declaraciones declare.

La declaración del espacio de nombres del archivo.

Una o más declaraciones use import basadas en clases.

Una o más sentencias import basadas en funciones.

Una o más sentencias import de uso basado en constantes.

El resto del código del archivo.

Cuando un archivo contiene una mezcla de HTML y PHP, cualquiera de las secciones anteriores puede ser utilizada. Si es así, DEBEN estar presentes en la parte superior del archivo, incluso si el resto del código consiste en una etiqueta PHP de cierre y luego una mezcla de HTML y PHP.

Cuando la etiqueta de apertura

Las declaraciones de importación nunca DEBEN comenzar con una barra invertida inicial, ya que siempre deben estar completamente calificadas.

El siguiente ejemplo ilustra una lista completa de todos los bloques:

```php
<?php

/**
 * This file contains an example of coding styles.
 */

declare(strict_types=1);

namespace Vendor\Package;

use Vendor\Package\{ClassA as A, ClassB, ClassC as C};
use Vendor\Package\SomeNamespace\ClassD as D;
use Vendor\Package\AnotherNamespace\ClassE as E;

use function Vendor\Package\{functionA, functionB, functionC};
use function Another\Vendor\functionD;

use const Vendor\Package\{CONSTANT_A, CONSTANT_B, CONSTANT_C};
use const Another\Vendor\CONSTANT_D;

/**
 * FooBar is an example class.
 */
class FooBar
{
    // ... additional PHP code ...
}
```

NO DEBEN utilizarse espacios de nombres compuestos con una profundidad superior a dos. Por lo tanto, a continuación se indica la profundidad máxima de composición permitida:

```php
<?php

use Vendor\Package\SomeNamespace\{
    SubnamespaceOne\ClassA,
    SubnamespaceOne\ClassB,
    SubnamespaceTwo\ClassY,
    ClassZ,
};
```

Y lo siguiente no estaría permitido:

```php
<?php

use Vendor\Package\SomeNamespace\{
    SubnamespaceOne\AnotherNamespace\ClassA,
    SubnamespaceOne\ClassB,
    ClassZ,
};
```

Cuando desee declarar tipos estrictos en archivos que contengan marcado fuera de las etiquetas de apertura y cierre de PHP, la declaración DEBE estar en la primera línea del archivo e incluir una etiqueta de apertura de PHP, la declaración de tipos estrictos y la etiqueta de cierre.

Por ejemplo:

```php
<?php declare(strict_types=1) ?>
<html>
<body>
    <?php
        // ... additional PHP code ...
    ?>
</body>
</html>
```

Las declaraciones no DEBEN contener espacios y DEBEN ser exactamente declare(strict_types=1) (con un punto y coma opcional).

Las declaraciones en bloque están permitidas y DEBEN tener el formato que se indica a continuación. Observe la posición de las llaves y el espaciado:

```php
declare(ticks=1) {
    // some code
}
```

> 4. Clases, propiedades y métodos
El término "clase" se refiere a todas las clases, interfaces y rasgos.
> 

Cualquier llave de cierre NO DEBE ir seguida de ningún comentario o declaración en la misma línea.

Al instanciar una nueva clase, los paréntesis DEBEN estar siempre presentes aunque no se pasen argumentos al constructor.

```php
new Foo();
```

> 4.1 Extensiones e implementos
> 

Las palabras clave extends e implements DEBEN declararse en la misma línea que el nombre de la clase.

La llave de apertura de la clase DEBE ir en su propia línea; la llave de cierre de la clase DEBE ir en la siguiente línea después del cuerpo.

Las llaves de apertura DEBEN ir en su propia línea y NO DEBEN ir precedidas ni seguidas de una línea en blanco.

Las llaves de cierre DEBEN ir en su propia línea y NO DEBEN ir precedidas de una línea en blanco.

```php
<?php

namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class ClassName extends ParentClass implements \ArrayAccess, \Countable
{
    // constants, properties, methods
}
```

Las listas de implementos y, en el caso de las interfaces, de extensiones PUEDEN dividirse en varias líneas, en las que cada línea subsiguiente tiene una sangría. Al hacerlo, el primer elemento de la lista DEBE estar en la línea siguiente, y sólo DEBE haber una interfaz por línea.

> 4.2 Propiedades y constantes
> 

La visibilidad DEBE ser declarada en todas las propiedades.

La visibilidad DEBE ser declarada en todas las constantes si la versión mínima de PHP de su proyecto soporta visibilidades constantes (PHP 7.1 o posterior).

La palabra clave var NO DEBE ser usada para declarar una propiedad.

NO DEBE haber más de una propiedad declarada por sentencia.

Los nombres de propiedades NO DEBEN ir precedidos de un guión bajo para indicar visibilidad protegida o privada. Es decir, un prefijo de guión bajo explícitamente no tiene ningún significado.

DEBE haber un espacio entre la declaración del tipo y el nombre de la propiedad.

Una declaración de propiedad tiene el siguiente aspecto:

```php
<?php

namespace Vendor\Package;

class ClassName
{
    public $foo = null;
    public static int $bar = 0;
}
```

4.3 Métodos y funciones

La visibilidad DEBE declararse en todos los métodos.

Los nombres de los métodos NO DEBEN ir precedidos de un guión bajo para indicar visibilidad protegida o privada. Es decir, un prefijo de guión bajo carece explícitamente de significado.

Los nombres de métodos y funciones NO DEBEN declararse con un espacio después del nombre del método. La llave de apertura DEBE ir en su propia línea, y la llave de cierre DEBE ir en la línea siguiente al cuerpo. NO DEBE haber un espacio después del paréntesis de apertura, y NO DEBE haber un espacio antes del paréntesis de cierre.

Una declaración de método tiene el siguiente aspecto. Observe la colocación de los paréntesis, comas, espacios y llaves:

```php
<?php

namespace Vendor\Package;

class ClassName
{
    public function fooBarBaz($arg1, &$arg2, $arg3 = [])
    {
        // method body
    }
}
```

Una declaración de función tiene el siguiente aspecto. Observe la colocación de paréntesis, comas, espacios y llaves:

```php
<?php

function fooBarBaz($arg1, &$arg2, $arg3 = [])
{
    // function body
}
```

> ****4.4 Method and Function Arguments****
> 

En la lista de argumentos, NO DEBE haber un espacio antes de cada coma, y DEBE haber un espacio después de cada coma.

Los argumentos de métodos y funciones con valores por defecto DEBEN ir al final de la lista de argumentos.

```php
<?php

namespace Vendor\Package;

class ClassName
{
    public function foo(int $arg1, &$arg2, $arg3 = [])
    {
        // method body
    }
}
```

Las listas de argumentos PUEDEN dividirse en varias líneas, cada una de ellas con una sangría. Al hacerlo, el primer elemento de la lista DEBE estar en la línea siguiente, y sólo DEBE haber un argumento por línea.

Cuando la lista de argumentos se divide en varias líneas, el paréntesis de cierre y el corchete de apertura DEBEN colocarse juntos en su propia línea con un espacio entre ellos.

```php
<?php

namespace Vendor\Package;

class ClassName
{
    public function aVeryLongMethodName(
        ClassTypeHint $arg1,
        &$arg2,
        array $arg3 = []
    ) {
        // method body
    }
}
```

Cuando haya una declaración de tipo de retorno presente, DEBE haber un espacio después de los dos puntos seguido de la declaración de tipo. Los dos puntos y la declaración DEBEN estar en la misma línea que el paréntesis de cierre de la lista de argumentos, sin espacios entre los dos caracteres.

```php
<?php

declare(strict_types=1);

namespace Vendor\Package;

class ReturnTypeVariations
{
    public function functionName(int $arg1, $arg2): string
    {
        return 'foo';
    }

    public function anotherFunction(
        string $foo,
        string $bar,
        int $baz
    ): string {
        return 'foo';
    }
}
```

En las declaraciones de tipo anulable, NO DEBE haber un espacio entre el signo de interrogación y el tipo.

```php
<?php

declare(strict_types=1);

namespace Vendor\Package;

class ReturnTypeVariations
{
    public function functionName(?string $arg1, ?int &$arg2): ?string
    {
        return 'foo';
    }
}
```

Cuando se utiliza el operador de referencia & delante de un argumento, NO DEBE haber un espacio después, como en el ejemplo anterior.

NO DEBE haber un espacio entre el operador variádico de tres puntos y el nombre del argumento:

```php
public function process(string $algorithm, ...$parts)
{
    // processing
}
```

Al combinar el operador de referencia y el operador variádico de tres puntos, NO DEBE haber ningún espacio entre ambos:

```php
public function process(string $algorithm, &...$parts)
{
    // processing
}
```

> 5. Cierres
> 

Los cierres DEBEN declararse con un espacio después de la palabra clave function, y un espacio antes y después de la palabra clave use.

El paréntesis de apertura DEBE ir en la misma línea, y el paréntesis de cierre DEBE ir en la línea siguiente al cuerpo.

NO DEBE haber un espacio después del paréntesis de apertura de la lista de argumentos o de la lista de variables, y NO DEBE haber un espacio antes del paréntesis de cierre de la lista de argumentos o de la lista de variables.

En la lista de argumentos y la lista de variables, NO DEBE haber un espacio antes de cada coma, y DEBE haber un espacio después de cada coma.

Los argumentos de cierre con valores por defecto DEBEN ir al final de la lista de argumentos.

Si está presente un tipo de retorno, DEBE seguir las mismas reglas que con las funciones y métodos normales; si está presente la palabra clave use, los dos puntos DEBEN seguir a los paréntesis de cierre de la lista use sin espacios entre los dos caracteres.

Una declaración de cierre tiene el siguiente aspecto. Observe la colocación de paréntesis, comas, espacios y llaves:

```php
<?php

$closureWithArgs = function ($arg1, $arg2) {
    // body
};

$closureWithArgsAndVars = function ($arg1, $arg2) use ($var1, $var2) {
    // body
};

$closureWithArgsVarsAndReturn = function ($arg1, $arg2) use ($var1, $var2): bool {
    // body
};
```

Las listas de argumentos y variables PUEDEN dividirse en varias líneas, cada una de ellas con una sangría. Al hacerlo, el primer elemento de la lista DEBE estar en la línea siguiente, y sólo DEBE haber un argumento o variable por línea.

Cuando la lista final (ya sea de argumentos o variables) se divide en varias líneas, el paréntesis de cierre y la llave de apertura DEBEN colocarse juntos en su propia línea con un espacio entre ellos.

A continuación se muestran ejemplos de cierres con y sin listas de argumentos y listas de variables divididas en varias líneas.

```php
<?php

$longArgs_noVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) {
   // body
};

$noArgs_longVars = function () use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
   // body
};

$longArgs_longVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
   // body
};

$longArgs_shortVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) use ($var1) {
   // body
};

$shortArgs_longVars = function ($arg) use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
   // body
};
```

Tenga en cuenta que las reglas de formato también se aplican cuando el cierre se utiliza directamente como argumento en una llamada a una función o método.

```php
<?php

$foo->bar(
    $arg1,
    function ($arg2) use ($var1) {
        // body
    },
    $arg3
);
```

> 6. Clases anónimas
> 

Las Clases Anónimas DEBEN seguir las mismas directrices y principios que los cierres de la sección anterior.

```php
<?php

$instance = new class {};
```

El corchete de apertura PUEDE estar en la misma línea que la palabra clave class siempre que la lista de interfaces implementadas no se envuelva. Si la lista de interfaces se envuelve, el corchete DEBE colocarse en la línea inmediatamente posterior a la última interfaz.

```php
<?php

// Brace on the same line
$instance = new class extends \Foo implements \HandleableInterface {
    // Class content
};

// Brace on the next line
$instance = new class extends \Foo implements
    \ArrayAccess,
    \Countable,
    \Serializable
{
    // Class content
};
```

# [Estándares de nombramiento en Laravel](https://www.mindtwo.de/guidelines/coding/laravel#site)

| Clases | Convención | Ejemplo |
| --- | --- | --- |
| Controller | singular | ArticleController |
| Route | plural | articles/1 |
| Named route | snake_case with dot notation | users.show_active |
| Model | singular | User |
| hasOne or belongsTo relationship | singular | articleComment |
| All other relationships | plural | articleComments |
| Table | plural | article_comments |
| Pivot table | singular model names in alphabetical order | article_user |
| Table column | snake_case without model name | meta_title |
| Foreign key | singular model name with _id suffix | article_id |
| Primary key | - | id |
| Migration | - | 2017_01_01_000000_create_articles_table |
| Method | camelCase | getAll |
| Function | snake_case | abort_if |
| Method in resource controller | more infos: table | store |
| Method in test class | camelCase | testGuestCannotSeeArticle |
| Model property | snake_case | $model->model_property |
| Variable | camelCase | $anyOtherVariable |
| Collection | descriptive, plural | $activeUsers = User::active()->get() |
| Object | descriptive, singular | $activeUser = User::active()->first() |
| Config and language files index | snake_case | articles_enabled |
| View | kebab-case | show-filtered.blade.php |
| Config | kebab-case | google-calendar.php |
| Contract (interface) | adjective or noun | Authenticatable |
| Trait | adjective | Notifiable |

# Siempre que sea posible, utilice una sintaxis más corta y legible.

| Sintáxis Común | Sintaxis más corta y legible |
| --- | --- |
| Session::get('cart') | session('cart') |
| $request->session()->get('cart') | session('cart') |
| Session::put('cart', $data) | session(['cart' => $data]) |
| $request->input('name'), Request::get('name') | $request->name, request('name') |
| return Redirect::back() | return back() |
| is_null($object->relation) ? $object->relation->id :                             null                             } | optional($object->relation)->id |
| return view('index')->with('title', $title)->with('client',                             $client) | return view('index', compact('title', 'client')) |
| $request->has('value') ? $request->value :                             'default'; | $request->get('value', 'default') |
| Carbon::now(), Carbon::today() | now(), today() |
| App::make('Class') | app('Class') |
| ->where('column', '=', 1) | ->where('column', 1) |
| ->orderBy('created_at', 'desc') | ->latest() |
| ->orderBy('age', 'desc') | ->latest('age') |
| ->orderBy('created_at', 'asc') | ->oldest() |
| ->select('id', 'name')->get() | ->get(['id', 'name']) |
| ->first()->name | ->value('name') |

# Principio de responsabilidad única

Principio de responsabilidad única es un principio de programación que indica que una clase y un método deben tener una sola responsabilidad. Esto significa que cada clase y método debe tener una única tarea o responsabilidad y no debe tener más de una razón para cambiar.

Este principio se aplica en Laravel a través de la separación de responsabilidades en las diferentes capas de la arquitectura del framework. Por ejemplo, los modelos son responsables de interactuar con la base de datos, los controladores son responsables de manejar las solicitudes HTTP y las vistas son responsables de mostrar la información al usuario final.

Siguiendo el principio de responsabilidad única, es más fácil mantener y escalar una aplicación ya que cada componente es responsable de una única tarea y no tiene dependencias innecesarias. Esto también facilita la reutilización del código ya que las clases y métodos se pueden utilizar en diferentes partes de la aplicación sin tener que modificarlos.

## Una clase y un método deben tener una sola responsabilidad.

### Ejemplo `INCORRECTO`

```php
public function getFullNameAttribute()
    {
        if (auth()->user() && auth()->user()->hasRole('client') && auth()->user()->isVerified()) {
            return 'Mr. ' . $this->first_name . ' ' . $this->middle_name . ' ' . $this->last_name;
        } else {
            return $this->first_name[0] . '. ' . $this->last_name;
        }
    }
```

### Ejemplo `CORRECTO`

```php
public function getFullNameAttribute()
    {
        return $this->isVerifiedClient() ? $this->getFullNameLong() : $this->getFullNameShort();
    }

    public function isVerifiedClient()
    {
        return auth()->user() && auth()->user()->hasRole('client') && auth()->user()->isVerified();
    }

    public function getFullNameLong()
    {
        return 'Mr. ' . $this->first_name . ' ' . $this->middle_name . ' ' . $this->last_name;
    }

    public function getFullNameShort()
    {
        return $this->first_name[0] . '. ' . $this->last_name;
    }
```

# Modelos robustos, controladores débiles

Pon toda la lógica relacionada con la BD en modelos Eloquent o en clases Repositorio si estás usando Query Builder o consultas SQL sin procesar.

### Ejemplo `INCORRECTO`

```php
public function index()
    {
        $clients = Client::verified()
            ->with(['orders' => function ($q) {
                $q->where('created_at', '>', Carbon::today()->subWeek());
            }])
            ->get();

        return view('index', ['clients' => $clients]);
    }
```

### Ejemplo `CORRECTO`

```php
public function index()
    {
        return view('index', ['clients' => $this->client->getWithNewOrders()]);
    }

    class Client extends Model
    {
        public function getWithNewOrders()
        {
            return $this->verified()
                ->with(['orders' => function ($q) {
                    $q->where('created_at', '>', Carbon::today()->subWeek());
                }])
                ->get();
        }
    }
```

# Validación

Trasladar la validación de los controladores a las clases Request.

### Ejemplo `INCORRECTO`

```php
public function store(Request $request)
    {
        $request->validate([
            'title' => 'required|unique:posts|max:255',
            'body' => 'required',
            'publish_at' => 'nullable|date',
        ]);

        ....
    }
```

### Ejemplo `CORRECTO`

```php
public function store(PostRequest $request)
    {
        ....
    }

    class PostRequest extends Request
    {
        public function rules()
        {
            return [
                'title' => 'required|unique:posts|max:255',
                'body' => 'required',
                'publish_at' => 'nullable|date',
            ];
        }
    }
```

# La lógica empresarial debe estar en la clase de servicio

Un controlador debe tener una sola responsabilidad, así que mueve la lógica de negocio de los controladores a las clases de servicio.

### Ejemplo `INCORRECTO`

```php
public function store(Request $request)
    {
        if ($request->hasFile('image')) {
            $request->file('image')->move(public_path('images') . 'temp');
        }

        ....
    }
```

### Ejemplo `CORRECTO`

```php
public function store(Request $request)
    {
        $this->articleService->handleUploadedImage($request->file('image'));

        ....
    }

    class ArticleService
    {
        public function handleUploadedImage($image)
        {
            if (!is_null($image)) {
                $image->move(public_path('images') . 'temp');
            }
        }
    }
```

# No repetir código

Reutiliza el código siempre que puedas. SRP te ayuda a evitar la duplicación. Además, reutiliza las plantillas de Blade, usa los ámbitos de Eloquent, etc.

### Ejemplo `INCORRECTO`

```php
public function getActive()
    {
        return $this->where('verified', 1)->whereNotNull('deleted_at')->get();
    }

    public function getArticles()
    {
        return $this->whereHas('user', function ($q) {
                $q->where('verified', 1)->whereNotNull('deleted_at');
            })->get();
    }
```

### Ejemplo `CORRECTO`

```php
public function scopeActive($q)
    {
        return $q->where('verified', 1)->whereNotNull('deleted_at');
    }

    public function getActive()
    {
        return $this->active()->get();
    }

    public function getArticles()
    {
        return $this->whereHas('user', function ($q) {
                $q->active();
            })->get();
    }
```

# Utilizar Eloquent en lugar de Query Builder y consultas SQL sin procesar. Usar primero las colecciones a las matrices

Eloquent permite escribir código legible y fácil de mantener. Además, Eloquent tiene grandes herramientas integradas como soft deletes, events, scopes etc.

### Ejemplo `INCORRECTO`

```sql
SELECT *
    FROM `articles`
    WHERE EXISTS (SELECT *
                  FROM `users`
                  WHERE `articles`.`user_id` = `users`.`id`
                  AND EXISTS (SELECT *
                              FROM `profiles`
                              WHERE `profiles`.`user_id` = `users`.`id`)
                  AND `users`.`deleted_at` IS NULL)
    AND `verified` = '1'
    AND `active` = '1'
    ORDER BY `created_at` DESC
```

### Ejemplo `CORRECTO`

```php
Article::has('user.profile')->verified()->latest()->get();
```

# Asignación masiva

### Ejemplo `INCORRECTO`

```php
$article = new Article;
$article->title = $request->title;
$article->content = $request->content;
$article->verified = $request->verified;
// Add category to article
$article->category_id = $category->id;
$article->save();
```

### Ejemplo `CORRECTO`

```php
$category->article()->create($request->all());
```

# No ejecutar consultas en plantillas Blade y utilizar eager loading (problema N + 1)

### `INCORRECTO`(para 100 usuarios, se ejecutarán 101 consultas a la base de datos):

```php
@foreach (User::all() as $user)

    @endforeach
```

### `CORRECTO` (para 100 usuarios, se ejecutarán 2 consultas a la base de datos):

```php
$users = User::with('profile')->get();

    ...

    @foreach ($users as $user)

    @endforeach
```

# El código se comenta usando nombres descriptivos de métodos y variables a los comentarios.

### `INCORRECTO`

```php
if (count((array) $builder->getQuery()->joins) > 0)
```

### `ACEPTABLE`

```php
// Determine if there are any joins.
    if (count((array) $builder->getQuery()->joins) > 0)
```

### `CORRECTO`

```php
if ($this->hasJoins())
```

# No poner código JS y CSS en las plantillas Blade y no ponga HTML en las clases PHP.

### `INCORRECTO`

```jsx
let article = ``;
```

### `ACEPTABLE`

```html
<input id="article" type="hidden" value="">

    Or

    <button class="js-fav-article" data-article=""><button>
```

### `CORRECTO`

```jsx
let article = $('#article').val();
```

La mejor manera es utilizar el paquete especializado PHP a JS para transferir los datos.

# `(Debería)`Utilizar archivos de configuración y de idioma, constantes en lugar de texto en el código.

### `INCORRECTO`

```php
public function isNormal()
    {
        return $article->type === 'normal';
    }

    return back()->with('message', 'Your article has been added!');
```

### `CORRECTO`

```php
public function isNormal()
    {
        return $article->type === Article::TYPE_NORMAL;
    }

    return back()->with('message', __('app.article_added'));
```

# Utilizar herramientas Laravel estándar aceptadas por la comunidad

| Tarea | Herramientas estandar | Herramientas de terceros |
| --- | --- | --- |
| Authorization | Policies | Entrust, Sentinel and other packages |
| Compiling assets | Laravel Mix | Grunt, Gulp, 3rd party packages |
| Development Environment | Homestead | Docker |
| Deployment | Laravel Forge | Deployer and other solutions |
| Unit testing | PHPUnit, Mockery | Phpspec |
| Browser testing | Laravel Dusk | Codeception |
| DB | Eloquent | SQL, Doctrine |
| Templates | Blade | Twig |
| Working with data | Laravel collections | Arrays |
| Form validation | Request classes | 3rd party packages, validation in controller |
| Authentication | Built-in | 3rd party packages, your own solution |
| API authentication | Laravel Passport | 3rd party JWT and OAuth packages |
| Creating API | Built-in | Dingo API and similar packages |
| Working with DB structure | Migrations | Working with DB structure directly |
| Localization | Built-in | 3rd party packages |
| Realtime user interfaces | Laravel Echo, Pusher | 3rd party packages and working with WebSockets directly |
| Generating testing data | Seeder classes, Model Factories, Faker | Creating testing data manually |
| Task scheduling | Laravel Task Scheduler | Scripts and 3rd party packages |
| DB | MySQL, PostgreSQL, SQLite, SQL Server | MongoDB |

# No obtener directamente los datos del archivo ".env

Pasar los datos a los archivos de configuración en su lugar y luego utilizar la función de ayuda config() para utilizar los datos en una aplicación.

### `INCORRECTO`

```php
$apiKey = env('API_KEY');
```

### `CORRECTO`

```php
// config/api.php
    'key' => env('API_KEY'),

    // Use the data
    $apiKey = config('api.key');
```