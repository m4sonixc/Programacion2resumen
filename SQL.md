

## 1. ¿Qué es SQL y una Base de Datos Relacional?

**SQL** (*Structured Query Language*) es el lenguaje utilizado para definir, manipular y consultar la información guardada en un gestor de bases de datos relacionales como **MySQL** o **MariaDB**.

* **Tabla:** Organización de datos en filas (registros) y columnas (campos).


* **Clave Primaria (Primary Key / PK):** Campo único que identifica cada registro de manera irrepetible (ej. `id_autor INT AUTO_INCREMENT PRIMARY KEY`).


* **Clave Foránea (Foreign Key / FK):** Campo que enlaza un registro con la clave primaria de otra tabla para formar una relación (ej. `id_autor` en la tabla `libros`).



---

## 2. Tipos de Datos Principales

Al crear estructuras en SQL, debes especificar el tipo de datos adecuado para cada campo:

* **`INT`**: Números enteros.


* **`VARCHAR(N)`**: Cadenas de texto de hasta $N$ caracteres.


* **`DATE`**: Fechas.


* **`DECIMAL`**: Números con decimales.



---

## 3. Sentencias de Definición y Modificación (DDL y DML)

### A. Crear Bases de Datos y Tablas (`CREATE`)



```sql
CREATE DATABASE escuela; -- Crea la base de datos[cite: 2]
USE escuela;            -- Selecciona la base de datos[cite: 2]

CREATE TABLE alumnos (
    id INT AUTO_INCREMENT PRIMARY KEY, -- Identificador único automático[cite: 1, 2]
    nombre VARCHAR(100) NOT NULL,      -- Texto de hasta 100 caracteres[cite: 2]
    edad INT NOT NULL                 -- Número entero[cite: 2]
);

```

### B. Insertar Datos (`INSERT INTO`)



```sql
INSERT INTO autores (nombre, apellido) 
VALUES ('Gabriel', 'Gómez'), ('Mariana', 'Fernández'); -- Inserta registros en la tabla[cite: 1]

```

### C. Actualizar Datos (`UPDATE`)



```sql
UPDATE alumnos 
SET edad = 20 
WHERE id = 1; -- Cambia la edad del alumno con id = 1

```

### D. Eliminar Datos (`DELETE`)



```sql
DELETE FROM alumnos 
WHERE id = 1; -- Borra el registro indicado

```

---

## 4. Consultas de Datos (`SELECT`) y Filtros Solicitados

La consulta básica para leer información tiene la siguiente estructura:

```sql
SELECT campos FROM tabla;

```

### A. `WHERE` (Filtrado condicional)



Se utiliza para filtrar registros que cumplan con una condición específica.

```sql
SELECT * FROM alumnos 
WHERE edad >= 18; -- Devuelve solo los alumnos mayores o iguales a 18 años

```

### B. `AND` (Operador Lógico "Y")

Permite combinar múltiples condiciones en una cláusula `WHERE`. **Todas** las condiciones separadas por `AND` deben cumplirse obligatoriamente para que el registro sea seleccionado.

```sql
SELECT * FROM alumnos 
WHERE edad >= 18 AND nombre = 'Juan'; 
-- Devuelve los alumnos que tienen 18 años o más Y que además se llaman 'Juan'

```

### C. `LIKE` (Búsqueda de patrones en texto)

Se combina con `WHERE` para buscar texto que coincida con un patrón específico utilizando el comodín `%` (que representa cero o más caracteres).

* **`LIKE 'A%'`**: Que empiece con "A".
* **`LIKE '%a'`**: Que termine con "a".
* **`LIKE '%mar%'`**: Que contenga "mar" en cualquier parte.

```sql
SELECT * FROM autores 
WHERE apellido LIKE 'G%'; 
-- Selecciona los autores cuyo apellido comience con la letra 'G' (ej. Gómez)[cite: 1]

```

### D. `ORDER BY` (Ordenamiento de resultados)



Ordena los registros devueltos en función de una o más columnas. Por defecto ordena de forma ascendente (`ASC`), pero se puede especificar descendente (`DESC`).

```sql
SELECT * FROM alumnos 
ORDER BY edad DESC; 
-- Devuelve todos los alumnos ordenados de mayor a menor edad

```

---

## 5. Integración de Clausulas en una sola Consulta

El orden de las cláusulas en SQL debe ser estricto. El orden correcto de escritura es:

1. `SELECT`
2. `FROM`
3. `WHERE` (con `AND` / `LIKE`)
4. `ORDER BY`

```sql
SELECT id, nombre, edad 
FROM alumnos 
WHERE edad >= 18 AND nombre LIKE '%a%' 
ORDER BY nombre ASC;

```

*Explicación:* Trae `id`, `nombre` y `edad` de la tabla `alumnos` de aquellos que tengan 18 años o más **Y** cuyo nombre contenga la letra 'a', ordenados alfabéticamente por `nombre`.

---

## 6. Errores Comunes para Identificar en el Examen

1. **Orden incorrecto de cláusulas:** Poner `ORDER BY` antes de `WHERE` causa un error de sintaxis en SQL.
2. **Uso de comodines en `LIKE`:** Olvidar comillas simples alrededor de los patrones en `LIKE` (ej. escribir `LIKE %G%` en lugar de `LIKE '%G%'`).
3. **Falta de `WHERE` en `UPDATE` o `DELETE`:** Ejecutar `UPDATE alumnos SET edad = 20;` sin `WHERE` cambiará la edad de **todos** los registros de la base de datos.
4. **Comas sobrantes:** Dejar comas al final de las definiciones de campos antes del paréntesis de cierre en un `CREATE TABLE`.
