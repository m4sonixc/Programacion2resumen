
## 1. De PSeInt a PHP: Equivalencias y Conceptos Básicos

PHP se ejecuta en el servidor y genera respuestas para el navegador[cite: 7]. La lógica de programación previa (variables, condiciones, ciclos, operadores) se mantiene, cambiando principalmente la sintaxis y el entorno[cite: 7].

### Tabla de Equivalencias de Sintaxis

| Concepto | PSeInt | PHP |
| --- | --- | --- |
| **Variable** | `nombre <- "Ana"` | `$nombre = "Ana";`[cite: 7] |
| **Salida** | `Escribir nombre` | `echo $nombre;`[cite: 7] |
| **Condición** | `Si edad >= 18 Entonces` | `if ($edad >= 18) {`[cite: 7] |
| **Ciclo** | `Para i <- 1 Hasta 5` | `for ($i=1; $i<=5; $i++)`[cite: 7] |
| **Operador** | `Y / O / =` | `&& / || / ==`[cite: 7] |

### Tipos de Datos Básicos y Tipado Dinámico

PHP reconoce automáticamente el tipo de dato según el valor asignado[cite: 7]:

* **String:** `$nombre = "Luna";` o `$nombre = "Marcos";`[cite: 6, 7]
* **Int:** `$edad = 17;` o `$edad = 18;`[cite: 6, 7]
* **Float:** `$promedio = 8.5;`[cite: 7]
* **Boolean:** `$activo = true;`[cite: 7]

### Delimitadores y Concatenación

* Todo código PHP se delimita mediante la etiqueta `<?php ... ?>` y cada instrucción debe finalizar obligatoriamente con un punto y coma `;`[cite: 7].
* Para unir fragmentos de texto con variables se utiliza el punto `.` como operador de concatenación[cite: 3, 4, 6, 7].

```php
<?php
$nombre = "Mora";
$edad = 18;

echo "Hola " . $nombre . "<br>";
echo "Tenés " . $edad . " años";
?>

```

### Toma de Decisiones (`if / else`)

Permite bifurcar el flujo del programa según una condición matemática o lógica[cite: 6, 7].

```php
<?php
$nombre = "Marcos";
$edad = 18;

echo "Hola " . $nombre . ". ";

if ($edad >= 18) {
    echo "eres mayor de edad";
} else {
    echo "eres menor de edad";
}
?>

```

---

## 2. Entorno de Trabajo y Servidor Local (XAMPP y Visual Studio Code)

Para trabajar con aplicaciones backend web y bases de datos relacionales, se utiliza una pila de herramientas integradas[cite: 7, 8]:

* **Visual Studio Code:** Editor ligero donde se escribe el código de la aplicación[cite: 7]. Cuenta con extensiones recomendadas como *PHP Intelephense*, *Prettier* y *Material Icon Theme*[cite: 7].
* **Apache:** Servidor web encargado de recibir las peticiones HTTP del navegador[cite: 7, 8].
* **PHP:** Intérprete que procesa y ejecuta el código en el servidor[cite: 7, 8].
* **MySQL / MariaDB:** Sistema gestor de base de datos relacional para almacenar información[cite: 7, 8].
* **phpMyAdmin:** Interfaz gráfica web para administrar visualmente las bases de datos, crear tablas, ejecutar SQL e insertar o consultar información[cite: 7, 9].
* **Directorio `htdocs` y `localhost`:**
1. Los proyectos PHP deben guardarse dentro de la carpeta `htdocs` del servidor local (ejemplo: `htdocs/clase_php/`)[cite: 7].
2. Para ejecutar un archivo desde el navegador, se accede a través de la dirección de red local: `http://localhost/clase_php/`[cite: 7].



---

## 3. Relación entre HTML y PHP (Formularios y `$_POST`)

El formulario escrito en HTML permite capturar las entradas introducidas por el usuario[cite: 7, 8]. Los datos son enviados al backend mediante el protocolo HTTP[cite: 7, 8].

### 1. Formulario HTML (`index.html` / `formulario.html`)

Para enviar datos desde un formulario hacia un script de procesamiento en PHP, se utiliza el atributo `action` especificando el archivo de destino, y `method="POST"`[cite: 2, 7]. Cada campo debe poseer el atributo `name` para que PHP lo identifique[cite: 2].

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Formulario 2</title>
    <style>
        .campo {
            margin-bottom: 15px;
        }
    </style>
</head>
<body>
    <h1>Bienvenido al Segundo Formulario</h1>
    
    <form action="procesa.php" method="POST">
        <div class="campo">
            <label>Introduce tu Nombre:</label>
            <input name="nombre" type="text">
        </div> 
        <div class="campo">
            <label>Ingresa tu Apellido:</label>
            <input name="apellido" type="text">
        </div>
        <div class="campo">
            <label>Ingresa tu edad:</label>
            <input name="edad" type="number">
        </div>
        <button type="submit">Enviar</button>
    </form>
</body>
</html>

```

### 2. Procesamiento de Entrada en PHP (`procesa.php`)

PHP recibe los datos del formulario a través de la variable superglobal `$_POST`, mapeando las llaves asociativas directamente con el atributo `name` de las etiquetas `<input>`[cite: 2, 3, 4].

```php
<?php
$nombre = $_POST["nombre"];
$edad = $_POST["edad"];
$apellido = $_POST["apellido"];

echo "Hola " . $nombre . " " . $apellido . ", Tu edad es: " . $edad;
?>

```

---

## 4. Estructura de la Base de Datos en MySQL / MariaDB

Las sentencias SQL definen la base de datos relacional y las tablas requeridas para el sistema[cite: 7, 8].

### Creación de Base de Datos y Tablas

A través del lenguaje SQL o desde phpMyAdmin se ejecutan los comandos para la tabla `alumnos` o tablas asociadas (como `autores`)[cite: 7, 9]:

```sql
CREATE DATABASE escuela;
USE escuela;

CREATE TABLE alumnos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    edad INT NOT NULL
);

```

* **`id`:** Clave primaria única generada de forma automática por el gestor mediante `AUTO_INCREMENT`[cite: 7].
* **`NOT NULL`:** Especifica que los campos son obligatorios y no pueden almacenarse vacíos.

---

## 5. Conexión a la Base de Datos con PDO

**PDO (PHP Data Objects)** es el objeto utilizado para conectar PHP con la base de datos MySQL de forma segura[cite: 5, 7, 8].

### Estructura de Conexión (`conexion.php`)

La conexión se envuelve dentro de una estructura de control de excepciones `try-catch` para capturar cualquier fallo de la red o credenciales sin interrumpir abruptamente el sistema[cite: 5, 7].

```php
<?php
$host = "localhost";
$base = "sistema_biblioteca"; // O "escuela"
$usuario = "root";
$clave = "";

try {
    $pdo = new PDO(
        "mysql:host=$host;dbname=$base",
        $usuario, 
        $clave
    );
    echo "Conexion exitosa";
} catch (PDOException $e) {
    echo "error de conexion";
}
?>

```

---

## 6. Operaciones CRUD Completas en PHP

El ciclo **CRUD** contempla las cuatro operaciones esenciales sobre una base de datos relacional: Crear, Leer, Modificar y Eliminar[cite: 1, 8].

---

### C - Create (Insertar Registro / Guardar)

Captura los datos enviados desde un formulario mediante un método `POST` e inserta el nuevo registro en la base de datos[cite: 1, 7].

#### Archivo: `nuevo.php` / `guardar.php`

```php
<?php
require_once "conexion.php";

if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $nombre = $_POST["nombre"];
    $edad = $_POST["edad"];

    // Sentencia SQL parametrizada con marcadores ?
    $sql = "INSERT INTO alumnos (nombre, edad) VALUES (?, ?)";
    
    // Preparación e inserción mediante PDO
    $stmt = $pdo->prepare($sql);
    $stmt->execute([$nombre, $edad]);

    // Redirección
    header("Location: listar.php");
    exit();
}
?>

<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Nuevo Registro</title>
</head>
<body>
    <h2>Agregar Alumno</h2>
    <form action="guardar.php" method="POST">
        <div>
            <label>Nombre:</label>
            <input type="text" name="nombre" required>
        </div>
        <div>
            <label>Edad:</label>
            <input type="number" name="edad" required>
        </div>
        <button type="submit">Guardar</button>
    </form>
</body>
</html>

```

---

### R - Read (Leer / Mostrar Registros)

Consulta los datos persistentes usando una instrucción `SELECT` y los recorre dinámicamente mediante estructuras repetitivas en una tabla HTML[cite: 1, 8].

#### Archivo: `listar.php`

```php
<?php
require_once "conexion.php";

// Consulta para recuperar todos los registros
$stmt = $pdo->query("SELECT * FROM alumnos");
$alumnos = $stmt->fetchAll(PDO::FETCH_ASSOC);
?>

<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Listado de Alumnos</title>
</head>
<body>
    <h2>Lista de Alumnos</h2>
    <a href="nuevo.php">Agregar Nuevo Alumno</a>
    <br><br>

    <table border="1" cellpadding="5" cellspacing="0">
        <thead>
            <tr>
                <th>ID</th>
                <th>Nombre</th>
                <th>Edad</th>
                <th>Acciones</th>
            </tr>
        </thead>
        <tbody>
            <?php foreach ($alumnos as $alumno): ?>
                <tr>
                    <td><?= $alumno['id'] ?></td>
                    <td><?= $alumno['nombre'] ?></td>
                    <td><?= $alumno['edad'] ?></td>
                    <td>
                        <a href="editar.php?id=<?= $alumno['id'] ?>">Editar</a>
                        <a href="eliminar.php?id=<?= $alumno['id'] ?>">Eliminar</a>
                    </td>
                </tr>
            <?php endforeach; ?>
        </tbody>
    </table>
</body>
</html>

```

---

### U - Update (Modificar / Editar Registro)

Permite seleccionar un registro mediante su identificador único pasándolo por la URL (`$_GET['id']`), cargar sus datos vigentes en un formulario y procesar la modificación con la sentencia `UPDATE`[cite: 1, 8].

#### Archivo: `editar.php` / `modificar.php`

```php
<?php
require_once "conexion.php";

// 1. Obtener los datos del registro a editar
$id = $_GET['id'];
$stmt = $pdo->prepare("SELECT * FROM alumnos WHERE id = ?");
$stmt->execute([$id]);
$alumno = $stmt->fetch(PDO::FETCH_ASSOC);

// 2. Procesar la actualización al enviar el formulario
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $nombre = $_POST["nombre"];
    $edad = $_POST["edad"];

    $sql = "UPDATE alumnos SET nombre = ?, edad = ? WHERE id = ?";
    $stmt = $pdo->prepare($sql);
    $stmt->execute([$nombre, $edad, $id]);

    header("Location: listar.php");
    exit();
}
?>

<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Editar Registro</title>
</head>
<body>
    <h2>Modificar Alumno</h2>
    <form action="editar.php?id=<?= $id ?>" method="POST">
        <div>
            <label>Nombre:</label>
            <input type="text" name="nombre" value="<?= $alumno['nombre'] ?>" required>
        </div>
        <div>
            <label>Edad:</label>
            <input type="number" name="edad" value="<?= $alumno['edad'] ?>" required>
        </div>
        <button type="submit">Actualizar</button>
    </form>
</body>
</html>

```

---

### D - Delete (Eliminar Registro)

Toma el parámetro identificador pasado en la URL (`$_GET['id']`) y borra el registro seleccionado mediante la consulta parametrizada `DELETE`[cite: 1, 8].

#### Archivo: `eliminar.php`

```php
<?php
require_once "conexion.php";

if (isset($_GET['id'])) {
    $id = $_GET['id'];

    $stmt = $pdo->prepare("DELETE FROM alumnos WHERE id = ?");
    $stmt->execute([$id]);
}

header("Location: listar.php");
exit();
?>

```

---

## 7. Puntos Clave Explicativos para el Examen

1. **Lectura de Formularios:** PHP lee los campos enviados mediante el método `POST` consultando el arreglo asociativo `$_POST["nombre_del_input"]` según lo definido en el atributo `name` de la etiqueta HTML[cite: 2, 3, 4].
2. **Método `POST` vs `GET`:**
* `POST`: Transporta los datos de los formularios en el cuerpo de la petición sin exponerlos en la URL de navegación[cite: 2, 7, 8].
* `GET`: Pasa parámetros directamente agregados a la URL (utilizado para referencias de actualización o eliminación como `editar.php?id=1`)[cite: 1, 8].


3. **Uso de PDO y Sentencias Preparadas:**
* La instancia `$pdo = new PDO(...)` realiza el enlace de conexión entre el servidor web y MySQL / MariaDB[cite: 5, 7, 8].
* Se utiliza `$pdo->prepare()` junto con `$stmt->execute()` pasando marcadores de posición `?` para realizar consultas parametrizadas de forma segura[cite: 1, 8].
