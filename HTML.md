# GUÍA COMPLETA DE ESTUDIO: HTML Y FORMULARIOS WEB DE CERO A EXPERTO 🚀


---

## 📌 Tabla de Contenidos

1. Introducción y Flujo Web
2. Estructura Esqueleto de HTML5
3. Etiquetas Básicas y Semántica
4. Formularios en Profundidad: Conceptos Clave
5. Controles e Inputs de Formularios
6. Integración con Bootstrap 5
7. Simulacro de Examen: Detección de Errores (Debugging)
8. Simulacro de Examen: Escritura de Código Completo

---

## 1. Introducción y Flujo Web

Para comprender el desarrollo web, debemos situar a **HTML** dentro de la arquitectura cliente-servidor[cite: 1].

### Flujo de Datos

```text
[ USUARIO ] ---> ( Interfaz HTML / Formulario ) 
                     |
                     v  ( Petición HTTP GET / POST )
                [ SERVIDOR PHP ] 
                     |
                     v  ( Consultas SQL )
                [ BASE DE DATOS MySQL ]

```

* **HTML (HyperText Markup Language):** Es el lenguaje de marcado que define la estructura y el contenido semántico de la página web[cite: 1]. **No** realiza cálculos ni consultas a bases de datos[cite: 1].
* **PHP:** Procesa la información enviada por los formularios en el lado del servidor y realiza la lógica del negocio o CRUD[cite: 1].
* **Base de Datos:** Almacena los datos persistentes de la aplicación[cite: 1].

---

## 2. Estructura Esqueleto de HTML5

Todo documento HTML5 debe contar con la siguiente estructura básica estandarizada[cite: 1]:

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <!-- Configuración de caracteres especiales (tildes, ñ, etc.) -->
    <meta charset="UTF-8">
    <!-- Ajuste para diseño adaptable (Responsive Web Design) -->
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <!-- Título que se muestra en la pestaña del navegador -->
    <title>Mi Primera Página Web</title>
</head>
<body>
    <!-- Contenido visible para el usuario -->
    <h1>Hola Mundo</h1>
    <p>Estamos aprendiendo HTML y creación de formularios.</p>
</body>
</html>

```

### Explicación técnica de la estructura:

1. `<!DOCTYPE html>`: Declara el tipo de documento para que el navegador interprete el estándar HTML5[cite: 1].
2. `<html>`: Elemento raíz que envuelve todo el documento[cite: 1].
3. `<head>`: Contiene metadatos, títulos, scripts y enlaces a hojas de estilo (CSS)[cite: 1].
4. `<body>`: Contiene todo el cuerpo visible de la página web (encabezados, párrafos, tablas, formularios, etc.)[cite: 1].

---

## 3. Etiquetas Básicas y Semántica

Las etiquetas definen los elementos visuales y estructurales del documento[cite: 1]:

* **Encabezados:** Representan la jerarquía de títulos de la página.
```html
<h1>Título Principal (Único por página recomendado)</h1>
<h2>Subtítulo de Nivel 2</h2>
<h3>Subtítulo de Nivel 3</h3>

```


* **Párrafos y Textos:**
```html
<p>Texto descriptivo normal.</p>
<strong>Texto en negrita con énfasis semántico</strong>
<em>Texto en cursiva o itálica</em>
<br> <!-- Salto de línea sin cierre obligatorio -->

```


* **Enlaces (Hipervínculos):**
```html
<a href="https://github.com" target="_blank">Ir a GitHub</a>

```


* `href`: Especifica la URL de destino.
* `target="_blank"`: Abre la página en una pestaña nueva.


* **Imágenes:**
```html
<img src="imagen.jpg" alt="Descripción de la imagen" width="300">

```


* `src`: Ruta o dirección de la imagen.
* `alt`: Texto alternativo en caso de que la imagen no cargue o para lectores de pantalla.



---

## 4. Formularios en Profundidad: Conceptos Clave

El área de formularios es una de las más evaluadas en el examen[cite: 1]. Permite la recolección de datos que luego serán enviados a PHP para guardarse en la base de datos[cite: 1].

### Estructura general de la etiqueta `<form>`:

```html
<form action="procesar.php" method="POST" enctype="multipart/form-data">
    <!-- Elementos del formulario aquí -->
</form>

```

### Atributos Cruciales para el Examen:

1. **`action`**: Define la URL o script del servidor (ej. `procesar.php`) hacia donde se enviarán los datos introducidos[cite: 1]. Si se deja vacío, la petición se envía a la misma página.
2. **`method`**: Especifica el método HTTP para enviar los datos:
* **`GET`**: Envía los datos a través de la URL (visibles en la barra de direcciones). Adecuado para búsquedas o datos no sensibles.
* **`POST`**: Envía los datos ocultos dentro del cuerpo de la petición HTTP. Necesario para datos sensibles (contraseñas), textos largos o procesamiento en base de datos[cite: 1].


3. **`enctype="multipart/form-data"`**: Atributo **OBLIGATORIO** si el formulario va a subir archivos o documentos al servidor (usando `<input type="file">`).
4. **Atributo `name` vs `id**`:
* **`name`**: Nombre de la variable con la que PHP recibirá el dato (`$_POST['nombre']` o `$_GET['nombre']`). **Si un input no tiene el atributo `name`, su valor NO se enviará al servidor.**
* **`id`**: Identificador único usado por CSS, JavaScript o para enlazar la etiqueta `<label for="id">`.



---

## 5. Controles e Inputs de Formularios

A continuación se listan las principales etiquetas y tipos de entradas utilizadas en los formularios[cite: 1]:

### 1. Etiqueta `<label>` y Vincular Entradas

Vincula un texto indicativo con un elemento de entrada mediante el atributo `for`, el cual debe coincidir exactamente con el `id` del input.

```html
<label for="campo-nombre">Nombre Completo:</label>
<input type="text" id="campo-nombre" name="nombre_usuario" placeholder="Ej: Juan Pérez" required>

```

### 2. Tipos de `<input>` comunes:

* **Texto:** `<input type="text" name="usuario" placeholder="Usuario">`
* **Contraseña:** `<input type="password" name="clave" required>`
* **Correo Electrónico:** `<input type="email" name="correo" required>`
* **Número:** `<input type="number" name="edad" min="18" max="99">`
* **Fecha:** `<input type="date" name="fecha_nacimiento">`
* **Casilla de Selección (Checkbox):** Permite selección múltiple.
```html
<input type="checkbox" id="acepto" name="terminos" value="si">
<label for="acepto">Acepto términos y condiciones</label>

```


* **Botón de Opción (Radio):** Permite selección única dentro de un grupo (deben compartir el mismo `name`).
```html
<input type="radio" id="m" name="genero" value="M">
<label for="m">Masculino</label>
<input type="radio" id="f" name="genero" value="F">
<label for="f">Femenino</label>

```


* **Subida de Archivos:** `<input type="file" name="archivo_adjunto">`

### 3. Listas Desplegables (`<select>`)

```html
<label for="pais">País:</label>
<select id="pais" name="pais_origen" required>
    <option value="">-- Seleccione una opción --</option>
    <option value="AR">Argentina</option>
    <option value="MX">México</option>
    <option value="ES">España</option>
</select>

```

### 4. Áreas de Texto Multilínea (`<textarea>`)

**Nota para el examen:** A diferencia del `<input>`, la etiqueta `<textarea>` requiere cierre implícito (`</textarea>`) y **NO** utiliza el atributo `value`.

```html
<label for="comentario">Comentario:</label>
<textarea id="comentario" name="mensaje" rows="4" cols="50" placeholder="Escriba aquí..."></textarea>

```

### 5. Botones de Envío y Reinicio

```html
<button type="submit">Enviar Datos</button>
<button type="reset">Limpiar Formulario</button>

```

---

## 6. Integración con Bootstrap 5

En el examen también pueden solicitar aplicar clases de **Bootstrap** para maquetar el formulario con estilos adaptables[cite: 1].

### Inclusión por CDN en la cabecera `<head>`:

```html
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">

```

### Clases Principales de Formularios en Bootstrap 5:

* `container`: Contenedor principal que centra y limita el ancho del contenido.
* `mb-3`: Aplica un margen inferior (Margin Bottom) para distanciar campos.
* `form-label`: Aplica estilos formateados a las etiquetas `<label>`.
* `form-control`: Aplica estilos estándar a `<input>`, `<textarea>` y campos de entrada.
* `form-select`: Aplica estilos formateados a los elementos `<select>`.
* `btn btn-primary`: Estiliza botones con colores corporativos base.

---

## 7. Simulacro de Examen: Detección de Errores (Debugging)

Practica encontrando errores comunes en ejercicios típicos de evaluación:

### ❌ Ejercicio con Errores #1

Analiza el siguiente código e identifica los fallos:

```html
<!-- CÓDIGO CON ERRORES -->
<form action="guardar.php">
    <label for="usr">Usuario:</label>
    <input type="text" id="usuario" placeholder="Ingrese usuario">
    
    <label for="email">Email:</label>
    <input type="email" id="email" name="email">

    <select name="rol">
        <option value="1">Admin
        <option value="2">Usuario
    </select>

    <input type="file" id="foto">
    <input type="submit" value="Enviar">
</form>

```

#### 🔍 Diagnóstico de Errores y Corrección:

1. **Falta el método de envío (`method="POST"`):** Por defecto toma `GET`, lo cual expone datos en la URL[cite: 1].
2. **El atributo `for="usr"` no coincide con el `id="usuario"`:** La etiqueta no estará vinculada.
3. **El campo de usuario no tiene el atributo `name`:** PHP no recibirá la variable `usuario`.
4. **Subida de archivo sin `enctype`:** El campo `<input type="file">` requiere que el formulario contenga `enctype="multipart/form-data"`.
5. **Etiquetas `<option>` no cerradas correctamente:** Falta `</option>`.

---

### ✅ Código Corregido #1

```html
<!-- CÓDIGO CORREGIDO -->
<form action="guardar.php" method="POST" enctype="multipart/form-data">
    <label for="usuario">Usuario:</label>
    <input type="text" id="usuario" name="usuario" placeholder="Ingrese usuario" required>
    
    <label for="email">Email:</label>
    <input type="email" id="email" name="email" required>

    <label for="rol">Rol:</label>
    <select id="rol" name="rol">
        <option value="1">Admin</option>
        <option value="2">Usuario</option>
    </select>

    <label for="foto">Foto de Perfil:</label>
    <input type="file" id="foto" name="foto">

    <button type="submit">Enviar</button>
</form>

```

---

## 8. Simulacro de Examen: Escritura de Código Completo

A continuación se presenta un ejemplo completo que reúne todos los conceptos: HTML5, semántica, estructura de formulario avanzada y estilos mediante Bootstrap 5[cite: 1].

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Examen - Formulario Completo de Registro</title>
    <!-- CDN Bootstrap 5 -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
</head>
<body class="bg-light">

    <main class="container my-5">
        <div class="row justify-content-center">
            <div class="col-md-8">
                <div class="card shadow-sm">
                    <div class="card-header bg-primary text-white">
                        <h2 class="h4 mb-0">Formulario de Registro de Usuario</h2>
                    </div>
                    <div class="card-body">
                        
                        <!-- Inicio del Formulario -->
                        <form action="registro.php" method="POST" enctype="multipart/form-data">
                            
                            <!-- Campo Nombre -->
                            <div class="mb-3">
                                <label for="nombre" class="form-label">Nombre Completo:</label>
                                <input type="text" class="form-control" id="nombre" name="nombre" placeholder="Ej: Maria Lopez" required>
                            </div>

                            <!-- Campo Correo -->
                            <div class="mb-3">
                                <label for="correo" class="form-label">Correo Electrónico:</label>
                                <input type="email" class="form-control" id="correo" name="correo" placeholder="correo@ejemplo.com" required>
                            </div>

                            <!-- Campo Clave -->
                            <div class="mb-3">
                                <label for="password" class="form-label">Contraseña:</label>
                                <input type="password" class="form-control" id="password" name="password" required>
                            </div>

                            <!-- Selección de Perfil -->
                            <div class="mb-3">
                                <label for="perfil" class="form-label">Perfil de Usuario:</label>
                                <select class="form-select" id="perfil" name="perfil" required>
                                    <option value="" selected disabled>-- Seleccionar --</option>
                                    <option value="estudiante">Estudiante</option>
                                    <option value="docente">Docente</option>
                                    <option value="administrador">Administrador</option>
                                </select>
                            </div>

                            <!-- Opciones Radio: Turno -->
                            <div class="mb-3">
                                <label class="form-label d-block">Turno de Cursada:</label>
                                <div class="form-check form-check-inline">
                                    <input class="form-check-input" type="radio" name="turno" id="turno-manana" value="manana" checked>
                                    <label class="form-check-label" for="turno-manana">Mañana</label>
                                </div>
                                <div class="form-check form-check-inline">
                                    <input class="form-check-input" type="radio" name="turno" id="turno-noche" value="noche">
                                    <label class="form-check-label" for="turno-noche">Noche</label>
                                </div>
                            </div>

                            <!-- Subida de Archivo -->
                            <div class="mb-3">
                                <label for="documento" class="form-label">Adjuntar Documento de Identidad (PDF/Imagen):</label>
                                <input type="file" class="form-control" id="documento" name="documento">
                            </div>

                            <!-- Campo Comentarios -->
                            <div class="mb-3">
                                <label for="observaciones" class="form-label">Observaciones:</label>
                                <textarea class="form-control" id="observaciones" name="observaciones" rows="3"></textarea>
                            </div>

                            <!-- Casilla de Verificación -->
                            <div class="mb-3 form-check">
                                <input type="checkbox" class="form-check-input" id="terminos" name="terminos" value="1" required>
                                <label class="form-check-label" for="terminos">Acepto los términos y condiciones del servicio</label>
                            </div>

                            <!-- Botones de Acción -->
                            <div class="d-grid gap-2 d-md-flex justify-content-md-end">
                                <button type="reset" class="btn btn-secondary me-md-2">Limpiar</button>
                                <button type="submit" class="btn btn-primary">Registrar Datos</button>
                            </div>

                        </form>
                        <!-- Fin del Formulario -->

                    </div>
                </div>
            </div>
        </div>
    </main>

</body>
</html>

```

