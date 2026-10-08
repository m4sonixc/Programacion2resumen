Para aprobar este tipo de examen, necesitas dos cosas: **entender la sintaxis básica** y **desarrollar ojo crítico** para detectar los errores típicos que los profesores suelen poner en el código (sintaxis, lógica y tipos de datos).

---

## 1. Reglas de oro y sintaxis básica

1. **Etiquetas de apertura y cierre:** Todo código PHP debe ir dentro de `<?php ... ?>`. Si el archivo contiene solo PHP, la etiqueta de cierre `?>` se suele omitir, pero en exámenes con PHP integrado en HTML, siempre va.
2. **Sensibilidad a mayúsculas:** Las variables son **sensibles** a mayúsculas/minúsculas (`$suma` no es lo mismo que `$Suma`). Sin embargo, las funciones del lenguaje (`ECHO`, `echo`, `If`, `if`) **no** son sensibles a mayúsculas.
3. **Comentarios:**
* `//` o `#` para una sola línea.
* `/* ... */` para múltiples líneas.



---

## 2. Variables, Imprimir en pantalla y Tipos de datos

En PHP, todas las variables empiezan estrictamente con el signo peso `$`.

* `echo`: Muestra datos en pantalla. Puede imprimir varios textos separados por comas.
* `print`: Similar a `echo`, pero solo acepta un argumento y siempre retorna `1`.
* `var_dump($var)`: **Fundamental para exámenes**. Muestra el tipo de dato y su valor.

```php
<?php
$nombre = "Marcos";  // String (Texto)
$edad = 22;          // Integer (Entero)
$precio = 150.50;    // Float / Double (Decimal)
$esEstudiante = true; // Boolean (Verdadero/Falso)

echo "Hola " . $nombre; // El punto (.) sirve para concatenar (unir) texto
?>

```

---

## 3. Trampas típicas en los exámenes (¿Está bien o mal?)

### Caso A: El punto de concatenación vs. El signo más

En PHP, el operador `+` **solo realiza sumas matemáticas**. Para unir texto se usa el punto `.`.

```php
// ¿BIEN O MAL?
$texto = "Hola " + "Mundo"; 
// MAL: En versiones modernas de PHP esto da error (Fatal Error / TypeError). 
// CORRECTO: $texto = "Hola " . "Mundo";

$numero = "10" + 5; 
// BIEN (con advertencia): PHP convierte "10" a entero y da 15.

```

### Caso B: Comillas dobles vs. Comillas simples

* **Comillas dobles (`" "`):** Evalúan (reemplazan) las variables que tienen adentro.
* **Comillas simples (`' '`):** Tratan todo como texto literal.

```php
$curso = "PHP";

echo "Estudio $curso"; // Imprime: Estudio PHP (BIEN)
echo 'Estudio $curso'; // Imprime: Estudio $curso (Cuidado en el examen)

```

### Caso C: Olvidar el signo `$` o el punto y coma `;`

```php
// ¿BIEN O MAL?
$x = 10
y = 20;
// MAL: Falta ';' en la primera línea y falta '$' en la 'y'.

```

---

## 4. Estructuras de Control (Condicionales y Bucles)

### Condicionales (`if`, `else`, `elseif`)

Ojo con la diferencia entre `=` (asignación) y `==` / `===` (comparación).

* `==` compara valor (ej: `"5" == 5` es `true`).
* `===` compara valor **y** tipo de dato (ej: `"5" === 5` es `false`).

```php
$nota = 7;

if ($nota >= 8) {
    echo "Promocionado";
} elseif ($nota >= 4) {
    echo "Aprobado";
} else {
    echo "Desaprobado";
}

```

> **Trampa común de examen:**
> ```php
> if ($x = 10) { ... } // MAL: Esto asigna 10 a $x, convirtiendo la condición en verdadera.
> if ($x == 10) { ... } // BIEN: Esto compara si $x es igual a 10.
> 
> ```
> 
> 

---

### Bucles: `for`, `while`, `foreach`

El bucle `foreach` es exclusivo para recorrer **arreglos (arrays)** y aparece casi siempre en los parciales.

```php
$frutas = ["Manzana", "Banana", "Naranja"];

// Recorrer valores
foreach ($frutas as $fruta) {
    echo $fruta . "<br>";
}

// Recorrer clave y valor
foreach ($frutas as $posicion => $fruta) {
    echo "Índice $posicion: $fruta <br>";
}

```

---

## 5. Arreglos (Arrays)

En PHP existen dos tipos principales de arreglos:

### Arreglos Indexados (Numéricos)

Los índices empiezan siempre en `0`.

```php
$numeros = [10, 20, 30];
echo $numeros[0]; // Imprime 10

// ¿BIEN O MAL?
echo $numeros[3]; 
// MAL: El último índice es 2. Dará un error de "Undefined array key 3".

```

### Arreglos Asociativos (Clave => Valor)

En lugar de números, usas nombres como clave.

```php
$persona = [
    "nombre" => "Juan",
    "edad" => 25,
    "carrera" => "Sistemas"
];

echo $persona["nombre"]; // Imprime Juan

```

---

## 6. Funciones y Alcance de Variables (Scope)

Las funciones encapsulan lógica. **Ojo:** Las variables creadas fuera de la función **no** están accesibles dentro de ella a menos que se usen palabras clave como `global` o se pasen por parámetro.

```php
$mensaje = "Hola";

function saludar() {
    // ¿BIEN O MAL?
    echo $mensaje; 
    // MAL: $mensaje no existe dentro del ámbito local de la función (Warning/Notice).
}

// FORMA CORRECTA:
function saludarCorrecto($texto) {
    echo $texto;
}
saludarCorrecto($mensaje); // Imprime "Hola"

```

---

## Ejercicios de Práctica Tipo Examen

Analiza los siguientes 3 casos para ver si identificas el comportamiento:

### Ejercicio 1

```php
<?php
$a = "5";
$b = 5;

if ($a === $b) {
    echo "Iguales";
} else {
    echo "Diferentes";
}
?>

```

* **Respuesta:** Imprime `Diferentes`. Aunque ambos valen 5, `$a` es de tipo `string` y `$b` es `integer`. El operador `===` exige que coincida el tipo.

---

### Ejercicio 2

```php
<?php
$i = 0;
while ($i < 3) {
    echo $i;
}
?>

```

* **Respuesta:** **CÓDIGO INCORRECTO / BUCLE INFINITO**. Falta incrementar `$i` (`$i++`) dentro del cuerpo del `while`.

---

### Ejercicio 3

```php
<?php
$precios = [100, 200, 300];
$total = 0;

foreach ($precios as $p) {
    $total += $p;
}

echo "Total: $total";
?>

```

* **Respuesta:** **CÓDIGO CORRECTO**. Declara la variable `$total` en 0, suma correctamente cada elemento del array y muestra `Total: 600`.
