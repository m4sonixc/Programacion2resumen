

## 1. Estructura General de un Documento HTML

Todo documento HTML debe mantener un orden estricto de etiquetas jerárquicas:

* **`<html>`**: Etiqueta raíz que contiene todo el documento.


* **`<head>`**: Contiene la configuración e información no visible de la página (título de la pestaña, codificación, enlaces a CSS, etc.).


* **`<body>`**: Contiene todo el contenido visible para el usuario.



```html
<!DOCTYPE html>
<html>
  <head>
    <title>Título de la Pestaña</title>
  </head>
  <body>
    <!-- El contenido visible va aquí -->
  </body>
</html>

```

---

## 2. Anatomía de una Etiqueta HTML

Tomando de referencia la sintaxis `<input type="text" name="nombre">`:

* **Etiqueta (Tag):** Define qué elemento estamos creando (ej. `input`, `p`, `h1`).


* **Atributo:** Configura el elemento (ej. `type`, `name`, `href`).


* **Valor:** Es la asignación dada al atributo entre comillas (ej. `"text"`, `"nombre"`).



### Etiquetas Básicas de Texto y Enlaces



* `<h1>` al `<h6>`: Títulos y subtítulos principales.


* `<p>`: Párrafos de texto.


* `<strong>`: Texto destacado o en negrita.


* `<a href="URL">`: Hipervínculos o enlaces.



---

## 3. Formularios en HTML (`<form>`)

Un formulario permite enviar datos ingresados por el usuario. El atributo clave para procesar datos es:

* **`name`**: Identifica la variable/dato que recibirá el servidor (por ejemplo, PHP).



### Componentes y Entradas Principales



| Elemento / Atributo | Ejemplo / Uso | Descripción |
| --- | --- | --- |
| **Campos de texto** | `<input type="text" name="usuario">` | Campo de entrada de una sola línea de texto.

 |
| **Casilla de verificación** | `<input type="checkbox" name="acepta">` | Activa o desactiva una opción independiente.

 |
| **Lista desplegable** | `<select name="provincia">` <br>

<br> `<option value="1">Formosa</option>` <br>

<br> `</select>` | Presenta una lista desplegable con múltiples `<option>`.

 |
| **Área de texto** | `<label>Obs:</label>` <br>

<br> `<textarea name="observaciones"></textarea>` | Campo para ingresar textos largos de varias líneas.

 |

---

## 4. Ejemplo Práctico Integrador

Un código representativo de formulario que abarca las etiquetas vistas:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Registro</title>
  </head>
  <body>
    <h1>Formulario de Registro</h1>
    <form action="procesar.php" method="POST">
      
      <p>
        <label>Nombre:</label>
        <input type="text" name="nombre">
      </p>

      <p>
        <label>Provincia:</label>
        <select name="provincia">
          <option value="">Seleccionar...</option>
          <option value="1">Formosa</option>
          <option value="2">Chaco</option>
          <option value="3">Corrientes</option>
        </select>
      </p>

      <p>
        <label>Observaciones:</label><br>
        <textarea name="observaciones"></textarea>
      </p>

      <p>
        <input type="checkbox" name="acepta"> Acepto los términos
      </p>

      <button type="submit">Enviar</button>
    </form>
  </body>
</html>

```

---

## 5. Puntos Clave para la Detección de Errores en Exámenes

1. **Cierre de etiquetas:** Verificar que etiquetas como `<select>`, `<textarea>`, `<p>`, `<h1>` tengan su correspondiente etiqueta de cierre (ej. `</textarea>`). Note que etiquetas como `<input>` no llevan cierre.


2. **Uso de `<textarea>`:** Es un error muy común escribir `<input type="textarea">`. La forma correcta es la etiqueta dedicada `<textarea name="..."></textarea>`.


3. **Estructura jerárquica:** Recordar que `<head>` y `<body>` van dentro de `<html>` y nunca entrelazados.


4. **Atributo `name`:** Verificar que todos los controles de datos tengan asignado su atributo `name`, fundamental para enviar los valores al backend.


5. **Estructura del `<select>`:** Las opciones dentro de `<select>` deben ir envueltas obligatoriamente en etiquetas `<option value="...">`.
