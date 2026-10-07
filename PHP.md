

## 1. Fundamentos de PHP desde Cero

PHP es un lenguaje que se ejecuta del lado del **servidor**. Genera respuestas HTML dinámicas para el navegador y permite interactuar con bases de datos MySQL/MariaDB.

* **Sintaxis Básica:** Todo código PHP debe ir encerrado entre `<?php` y `?>`.


* **Variables:** Se declaran anteponiendo el signo `$` (ej. `$nombre = "Ana";`).


* **Impresión en pantalla:** Se utiliza la instrucción `echo` (ej. `echo $nombre;`).



### Tabla de Equivalencias (PSeInt vs. PHP)



| Concepto 
| 
| **Variable** PSEINT `nombre <- "Ana"` |       PHP `$nombre = "Ana";`<br> |
| **Salida** | PSEINT `Escribir nombre` |        PHP `echo $nombre;`<br> |
| **Condición** | PSEINT `Si edad >= 18 Entonces` |   PHP`if ($edad >= 18) {`<br> |
| **Bucle / Ciclo** | PSEINT `Para i <- 1 Hasta 5` |  PHP    `for ($i=1; $i<=5; $i++)`<br> |
| **Operadores** | PSEINT `Y / O / =` |    PHP  `&& / |

---

## 2. Integración con Bootstrap

Para estilizar la interfaz web, incorporamos la biblioteca CSS de Bootstrap dentro de la etiqueta `<head>` del documento HTML/PHP:

```html
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.8/dist/css/bootstrap.min.css" rel="stylesheet">

```

### Aplicación de clases principales de Bootstrap

:

* **Contenedores:** `<div class="container mt-4">`
* **Botones:** `<button class="btn btn-primary">Guardar</button>`

* **Formularios:** `<input class="form-control" name="nombre">`
* **Tablas:** `<table class="table table-striped">`

---

## 3. Flujo Integrado de Arquitectura Web

El flujo continuo de la aplicación desde que el usuario interactúa hasta que se persiste la información sigue este camino:

$$\text{USUARIO} \longrightarrow \text{FORMULARIO (HTML/Bootstrap)} \longrightarrow \text{POST} \longrightarrow \text{PHP (Variables)} \longrightarrow \text{PDO} \longrightarrow \text{SQL} \longrightarrow \text{MYSQL / MARIADB}$$

---

## 4. Conexión a la Base de Datos con PDO (`conexion.php`)

**PDO** (*PHP Data Objects*) nos permite conectar PHP con MySQL de forma confiable y segura. Se utiliza un bloque `try / catch` para capturar cualquier fallo sin detener bruscamente la aplicación.

```php
<?php
$host    = "localhost";
$base    = "escuela";
$usuario = "root";
$clave   = "";

try {
    $pdo = new PDO("mysql:host=$host;dbname=$base;charset=utf8", $usuario, $clave);
    // Configurar modo de errores de PDO a excepciones
    $pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
} catch (PDOException $e) {
    echo "Error de conexión: " . $e->getMessage();
    exit();
}
?>

```

---

## 5. Desarrollo Completo del CRUD mediante PDO

Para el examen, recuerda la regla de **Consultas Preparadas**:


$$\text{RECIBIR} \longrightarrow \text{PREPARAR (prepare)} \longrightarrow \text{EJECUTAR (execute)} \longrightarrow \text{CONFIRMAR / MOSTRAR}$$

Separar las instrucciones SQL de los datos mediante `prepare()` y `execute()` evita vulnerabilidades de seguridad.

---

### A. **CREATE (Insertar Datos)** — `agregar.php`

Recibe los datos del formulario mediante el método `POST` y los inserta en la base de datos.

```php
<?php
include 'conexion.php';

if ($_SERVER["REQUEST_METHOD"] == "POST") {
    // 1. RECIBIR
    $nombre = $_POST["nombre"];
    $edad   = $_POST["edad"];

    // 2. PREPARAR
    $sql = "INSERT INTO alumnos (nombre, edad) VALUES (?, ?)";
    $stmt = $pdo->prepare($sql);

    // 3. EJECUTAR
    $stmt->execute([$nombre, $edad]);

    // 4. CONFIRMAR
    header("Location: index.php");
    exit();
}
?>

```

---

### B. **READ (Leer y Listar con Bootstrap)** — `index.php`

Consulta todos los registros almacenados y los imprime dentro de una tabla formateada con Bootstrap.

```php
<?php
include 'conexion.php';

// Consulta para leer todos los registros
$stmt = $pdo->query("SELECT * FROM alumnos ORDER BY id DESC");
$alumnos = $stmt->fetchAll(PDO::FETCH_ASSOC);
?>

<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Lista de Alumnos</title>
    <!-- Conexión a Bootstrap -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.8/dist/css/bootstrap.min.css" rel="stylesheet">
</head>
<body class="bg-light">
<div class="container mt-5">
    <h2 class="mb-4">Registro de Alumnos</h2>
    
    <!-- Formulario estilizado para Crear / Insertar -->
    <form action="agregar.php" method="POST" class="row g-3 mb-4">
        <div class="col-md-5">
            <input type="text" name="nombre" class="form-control" placeholder="Nombre completo" required>
        </div>
        <div class="col-md-4">
            <input type="number" name="edad" class="form-control" placeholder="Edad" required>
        </div>
        <div class="col-md-3">
            <button type="submit" class="btn btn-primary w-100">Guardar Alumno</button>
        </div>
    </form>

    <!-- Tabla de Lectura de Datos -->
    <table class="table table-bordered table-striped">
        <thead class="table-dark">
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
                <td><?= htmlspecialchars($alumno['nombre']) ?></td>
                <td><?= $alumno['edad'] ?></td>
                <td>
                    <a href="editar.php?id=<?= $alumno['id'] ?>" class="btn btn-warning btn-sm">Editar</a>
                    <a href="eliminar.php?id=<?= $alumno['id'] ?>" class="btn btn-danger btn-sm" onclick="return confirm('¿Desea eliminar este registro?')">Eliminar</a>
                </td>
            </tr>
            <?php endforeach; ?>
        </tbody>
    </table>
</div>
</body>
</html>

```

---

### C. **UPDATE (Actualizar Datos)** — `editar.php`

Permite cargar la información existente de un registro mediante su `id` enviado por `GET`, para luego guardar los cambios enviados por `POST`.

```php
<?php
include 'conexion.php';

$id = $_GET['id'] ?? null;

if (!$id) {
    header("Location: index.php");
    exit();
}

// Si se envía el formulario de edición
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $nombre = $_POST["nombre"];
    $edad   = $_POST["edad"];

    $sql = "UPDATE alumnos SET nombre = ?, edad = ? WHERE id = ?";
    $stmt = $pdo->prepare($sql);
    $stmt->execute([$nombre, $edad, $id]);

    header("Location: index.php");
    exit();
}

// Obtener los datos actuales del alumno
$stmt = $pdo->prepare("SELECT * FROM alumnos WHERE id = ?");
$stmt->execute([$id]);
$alumno = $stmt->fetch(PDO::FETCH_ASSOC);
?>

<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Editar Alumno</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.8/dist/css/bootstrap.min.css" rel="stylesheet">
</head>
<body>
<div class="container mt-5">
    <h2>Editar Alumno #<?= $alumno['id'] ?></h2>
    <form method="POST" class="mt-3">
        <div class="mb-3">
            <label class="form-label">Nombre</label>
            <input type="text" name="nombre" value="<?= htmlspecialchars($alumno['nombre']) ?>" class="form-control" required>
        </div>
        <div class="mb-3">
            <label class="form-label">Edad</label>
            <input type="number" name="edad" value="<?= $alumno['edad'] ?>" class="form-control" required>
        </div>
        <button type="submit" class="btn btn-success">Actualizar</button>
        <a href="index.php" class="btn btn-secondary">Cancelar</a>
    </form>
</div>
</body>
</html>

```

---

### D. **DELETE (Eliminar Datos)** — `eliminar.php`

Recibe el `id` por la URL mediante el método `GET` y remueve el registro correspondiente de la base de datos.

```php
<?php
include 'conexion.php';

$id = $_GET['id'] ?? null;

if ($id) {
    // Preparar y ejecutar la eliminación
    $sql = "DELETE FROM alumnos WHERE id = ?";
    $stmt = $pdo->prepare($sql);
    $stmt->execute([$id]);
}

// Redireccionar al listado principal
header("Location: index.php");
exit();
?>

```

---

## 6. Errores Frecuentes en Exámenes de PHP + PDO

1. **Olvidar el signo `$` en variables:** Escribir `nombre = $_POST['nombre'];` genera un error de sintaxis en PHP.
2. **Confundir la sintaxis de PDO:** Usar `$pdo->execute()` directamente en lugar de `$stmt = $pdo->prepare($sql)` seguido de `$stmt->execute(...)`.


3. **No pasar parámetros en un array al ejecutar:** Escribir `$stmt->execute($nombre, $edad);` es incorrecto. Los parámetros deben ir dentro de corchetes: `$stmt->execute([$nombre, $edad]);`.


4. **Olvidar concatenar o incluir la conexión:** Intentar hacer `$pdo->prepare(...)` en `agregar.php` o `eliminar.php` sin haber hecho previamente `include 'conexion.php';` o `require 'conexion.php';`.
5. **Mezclar `$_POST` y `$_GET`:** Intentar leer un campo de formulario que usa `method="POST"` leyendo con `$_GET["campo"]`.
