
---

### 1. Libros: Mostrar todos los libros en orden alfabético

**Consulta SQL:**

```sql
SELECT * 
FROM libros 
ORDER BY titulo ASC;

```

* **¿Para qué sirve?:** Sirve para obtener la lista completa de libros almacenados y presentarlos ordenados alfabéticamente por su título.


* **¿Cómo se realiza?:**
* `SELECT *`: Selecciona todas las columnas/campos de la tabla.


* `FROM libros`: Especifica que la consulta se realiza sobre la tabla `libros`.


* `ORDER BY titulo ASC`: Ordena los resultados utilizando la columna `titulo` en sentido ascendente (A-Z). Si se omite `ASC`, SQL ordena de forma ascendente por defecto.





---

### 2. Autores: Mostrar nombre y apellido en orden descendente

**Consulta SQL:**

```sql
SELECT nombre, apellido 
FROM autores 
ORDER BY apellido DESC;

```

* **¿Para qué sirve?:** Sirve para listar únicamente la identidad de los autores (sin traer campos innecesarios como el ID) ordenados de la Z a la A.


* **¿Cómo se realiza?:**
* `SELECT nombre, apellido`: Filtra solo las columnas requeridas separadas por coma.


* `FROM autores`: Especifica la tabla `autores`.


* `ORDER BY apellido DESC`: Ordena la lista utilizando el apellido en sentido descendente (Z-A).





---

### 3. Libros: Mostrar título y año de publicación posteriores a un año determinado (ej. 2020)

**Consulta SQL:**

```sql
SELECT titulo, anio_publicacion 
FROM libros 
WHERE anio_publicacion > 2020;

```

* **¿Para qué sirve?:** Permite filtrar los libros para mostrar únicamente los más recientes lanzados después de un año específico.


* **¿Cómo se realiza?:**
* `SELECT titulo, anio_publicacion`: Selecciona únicamente las columnas de título y año.


* `FROM libros`: Indica la tabla origen.


* `WHERE anio_publicacion > 2020`: La cláusula `WHERE` aplica la condición relacional para descartar todos los libros cuyo año sea menor o igual a 2020.





---

### 4. Usuarios: Buscar usuarios que cumplan dos condiciones simultáneamente

**Consulta SQL:**

```sql
SELECT * 
FROM usuarios 
WHERE estado = 'activo' AND ciudad = 'Formosa';

```

*(Nota: Ajusta los nombres de campos como `estado` o `ciudad` según los que hayas definido en tu tabla)*.

* **¿Para qué sirve?:** Sirve para restringir la búsqueda de modo que solo devuelva los registros que cumplan estrictamente dos criterios al mismo tiempo.


* **¿Cómo se realiza?:**
* `WHERE ... AND ...`: `WHERE` inicia la condición de filtrado y el operador lógico `AND` exige que ambas condiciones (`estado = 'activo'` **Y** `ciudad = 'Formosa'`) se evalúen como verdaderas simultáneamente.





---

### 5. Autores: Buscar autores cuyo nombre o apellido comience con una letra determinada

**Consulta SQL:**

```sql
SELECT * 
FROM autores 
WHERE nombre LIKE 'G%' OR apellido LIKE 'G%';

```

* **¿Para qué sirve?:** Permite realizar búsquedas parciales de texto o patrones dentro de cadenas de caracteres (por ejemplo, buscar autores que comiencen con la letra "G").


* **¿Cómo se realiza?:**
* `WHERE ... LIKE 'G%'`: El operador `LIKE` evalúa coincidencia de patrones.


* `%` (Comodín): Representa cero, uno o cualquier número de caracteres. `'G%'` indica que debe empezar obligatoriamente con "G" y continuar con cualquier texto.


* `OR`: Permite evaluar si se cumple la condición en el nombre **O** en el apellido.





---

### 6. Libros + Autores: Mostrar el título del libro junto con el nombre y apellido del autor

**Consulta SQL:**

```sql
SELECT libros.titulo, autores.nombre, autores.apellido 
FROM libros 
INNER JOIN autores ON libros.id_autor = autores.id_autor;

```

* **¿Para qué sirve?:** Vincula dos tablas distintas para mostrar información combinada en un solo resultado (el libro junto al nombre real de quien lo escribió).


* **¿Cómo se realiza?:**
* `SELECT libros.titulo, autores.nombre, ...`: Se especifica `tabla.columna` para evitar ambigüedades sobre de qué tabla proviene cada dato.


* `FROM libros INNER JOIN autores`: `INNER JOIN` cruza las filas de la tabla `libros` con la tabla `autores`.


* `ON libros.id_autor = autores.id_autor`: La cláusula `ON` establece el vínculo relacional igualando la clave foránea (`FK` en `libros`) con la clave primaria (`PK` en `autores`).





---

### 7. Libros + Categorías: Mostrar el título de cada libro junto con el nombre de su categoría

**Consulta SQL:**

```sql
SELECT libros.titulo, categorias.nombre_categoria 
FROM libros 
INNER JOIN categorias ON libros.id_categoria = categorias.id_categoria;

```

* **¿Para qué sirve?:** Permite conocer la clasificación o género asignado a cada libro vinculando ambas tablas.


* **¿Cómo se realiza?:**
* `FROM libros INNER JOIN categorias`: Combina la tabla de libros con la tabla de categorías.


* `ON libros.id_categoria = categorias.id_categoria`: Define la relación matching entre la clave foránea de la categoría guardada en el libro y la clave primaria de la tabla categorías.





---

### 8. Usuarios + Préstamos: Mostrar préstamos con los datos del usuario aplicándole una condición de fecha

**Consulta SQL:**

```sql
SELECT prestamos.id_prestamo, prestamos.fecha_prestamo, usuarios.nombre, usuarios.apellido 
FROM prestamos 
INNER JOIN usuarios ON prestamos.id_usuario = usuarios.id_usuario 
WHERE prestamos.fecha_prestamo > '2026-01-01';

```

* **¿Para qué sirve?:** Muestra el historial de transacciones de préstamos identificando al usuario responsable, filtrando solo los préstamos recientes efectuados después de cierta fecha.


* **¿Cómo se realiza?:**
* `FROM prestamos INNER JOIN usuarios ON ...`: Relaciona la tabla de préstamos con la tabla de usuarios a través de la clave `id_usuario`.


* `WHERE prestamos.fecha_prestamo > '2026-01-01'`: Filtra el resultado combinado para incluir únicamente aquellas transacciones ocurridas con posterioridad a la fecha especificada.





---

### 9. Usuarios + Préstamos + Detalle de préstamos + Libros: Relacionar las 4 tablas

**Consulta SQL:**

```sql
SELECT 
    usuarios.nombre, 
    usuarios.apellido, 
    prestamos.fecha_prestamo, 
    libros.titulo 
FROM prestamos 
INNER JOIN usuarios ON prestamos.id_usuario = usuarios.id_usuario 
INNER JOIN detalle_prestamos ON prestamos.id_prestamo = detalle_prestamos.id_prestamo 
INNER JOIN libros ON detalle_prestamos.id_libro = libros.id_libro;

```

* **¿Para qué sirve?:** Resuelve la consulta integradora para conocer exactamente **quién** hizo un préstamo, **cuándo** lo hizo y **qué libro(s)** específicos se llevó.


* **¿Cómo se realiza?:**
* Se van encadenando múltiples sentencias `INNER JOIN` siguiendo el mapa de relaciones de la base de datos:


1. Se une `prestamos` con `usuarios` mediante `id_usuario`.


2. Se une `prestamos` con la tabla intermedia `detalle_prestamos` mediante `id_prestamo`.


3. Se une `detalle_prestamos` con `libros` mediante `id_libro`.




* De esta forma, la tabla `detalle_prestamos` actúa como puente entre el encabezado del préstamo y los libros contenidos en él.





---

### 💡 Resumen rápido de componentes utilizados para repasar:

* **`SELECT`**: Indica qué columnas queremos visualizar en el resultado.


* **`FROM`**: Especifica la tabla principal sobre la que se consulta.


* **`WHERE`**: Permite establecer filtros o condiciones lógicas.


* **`AND` / `OR**`: Operadores lógicos para combinar dos o más condiciones.


* **`LIKE '%...'`**: Operador para búsquedas de patrones en campos de texto.


* **`ORDER BY ... ASC|DESC`**: Cláusula para ordenar los resultados de forma ascendente o descendente.


* **`INNER JOIN ... ON`**: Combina filas de dos o más tablas relacionando sus Claves Primarias (`PK`) y Foráneas (`FK`).
