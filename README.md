# Analisis-Forense-y-Deteccion-de-Amenazas-SQL
# 🔐 Análisis Forense y Detección de Amenazas con SQL

## 📌 Descripción del proyecto

Este proyecto presenta un análisis práctico orientado a la **seguridad de la información**, utilizando consultas SQL para filtrar y analizar registros relacionados con intentos de inicio de sesión y datos de empleados.

El objetivo es aplicar consultas SQL para identificar información relevante para la investigación de posibles eventos de seguridad y para la gestión de actualizaciones de equipos dentro de una organización.

El análisis se desarrolla sobre las tablas `log_in_attempts` y `employees`, utilizando diferentes operadores y filtros SQL para obtener información específica.

---

## 🎯 Objetivos

* Identificar intentos fallidos de inicio de sesión fuera del horario de atención.
* Analizar intentos de inicio de sesión ocurridos en fechas específicas.
* Identificar intentos de inicio de sesión procedentes de países diferentes a México.
* Obtener información de empleados pertenecientes al departamento de Marketing.
* Identificar empleados pertenecientes a los departamentos de Finance o Sales.
* Identificar empleados que no pertenecen al departamento de Tecnología de la Información (TI).
* Aplicar operadores SQL para el filtrado y análisis de información relacionada con seguridad.

---

## 🛠️ Tecnologías y conceptos utilizados

| Tecnología / concepto     | Aplicación                               |
| ------------------------- | ---------------------------------------- |
| **SQL**                   | Consulta y filtrado de información       |
| **WHERE**                 | Definición de condiciones                |
| **AND**                   | Combinación de condiciones               |
| **OR**                    | Evaluación de condiciones alternativas   |
| **NOT**                   | Exclusión de determinados registros      |
| **LIKE**                  | Búsqueda mediante patrones               |
| **%**                     | Comodín para coincidencia de caracteres  |
| **Análisis de registros** | Identificación de actividades relevantes |

---

# 🔎 Análisis realizado

## 1. Recuperar intentos fallidos de inicio de sesión fuera del horario de atención

Se identificó una posible brecha de seguridad que ocurrió después del horario comercial. Por ello, se analizaron los intentos de inicio de sesión realizados después de las **18:00** que además resultaron fallidos.

### Consulta SQL

```sql
SELECT *
FROM log_in_attempts
WHERE login_time > '18:00'
AND success = FALSE;
```

### Explicación

Se utilizó la cláusula `WHERE` junto con el operador `AND` para combinar dos condiciones:

* `login_time > '18:00'`: identifica los intentos realizados después de las 18:00.
* `success = FALSE`: identifica los intentos de inicio de sesión fallidos.

### Evidencia

![Intentos fallidos de inicio de sesión fuera del horario](imagenes/01-intentos-fallidos.png)

---

## 2. Recuperar intentos de inicio de sesión en fechas específicas

Se identificó un evento sospechoso ocurrido el **09/05/2022**. Por ello, se analizaron los intentos de inicio de sesión registrados el 09/05/2022 y el día anterior, 08/05/2022.

### Consulta SQL

```sql
SELECT *
FROM log_in_attempts
WHERE login_date = '2022-05-09'
OR login_date = '2022-05-08';
```

### Explicación

Se utilizó el operador `OR` para obtener los registros correspondientes a cualquiera de las dos fechas:

* `login_date = '2022-05-09'`
* `login_date = '2022-05-08'`

### Evidencia

![Intentos de inicio de sesión en fechas específicas](imagenes/02-fechas-especificas.png)

---

## 3. Recuperar intentos de inicio de sesión fuera de México

Tras auditar los registros de acceso, se detectó una anomalía relacionada con conexiones procedentes del extranjero.

Se realizó una consulta para identificar los intentos de inicio de sesión realizados en países distintos de México.

### Consulta SQL

```sql
SELECT *
FROM log_in_attempts
WHERE NOT country LIKE 'MEX%';
```

### Explicación

Se utilizó `NOT` junto con `LIKE` para excluir los registros correspondientes a México.

El patrón `MEX%` permite coincidir con valores que comienzan con `MEX`. El símbolo `%` representa cualquier cantidad de caracteres posteriores.

### Evidencia

![Intentos de inicio de sesión fuera de México](imagenes/03-fuera-de-mexico.png)

---

## 4. Recuperar empleados en Marketing

Se necesitaba obtener información de los empleados pertenecientes al departamento de **Marketing** que trabajan en el edificio **East**, con el objetivo de identificar los equipos que requieren una actualización.

### Consulta SQL

```sql
SELECT *
FROM employees
WHERE department = 'Marketing'
AND office LIKE 'East%';
```

### Explicación

Se utilizó `AND` para combinar dos condiciones:

* `department = 'Marketing'`: filtra a los empleados del departamento de Marketing.
* `office LIKE 'East%'`: identifica las oficinas pertenecientes al edificio East.

### Evidencia

![Empleados del departamento de Marketing](imagenes/04-empleados-marketing.png)

---

## 5. Recuperar empleados en Finance o Sales

También se necesitaba obtener información de los empleados pertenecientes a los departamentos de **Finance** y **Sales**, debido a que requerían una actualización de seguridad diferente.

### Consulta SQL

```sql
SELECT *
FROM employees
WHERE department = 'Finance'
OR department = 'Sales';
```

### Explicación

Se utilizó el operador `OR` porque se necesitaba obtener empleados que pertenecieran a cualquiera de los dos departamentos:

* `department = 'Finance'`
* `department = 'Sales'`

### Evidencia

![Empleados de Finance o Sales](imagenes/05-finance-sales.png)

---

## 6. Recuperar empleados que no están en TI

Finalmente, se necesitaba identificar a los empleados que **no pertenecen al departamento de Tecnología de la Información**.

### Consulta SQL

```sql
SELECT *
FROM employees
WHERE NOT department = 'Information Technology';
```

### Explicación

Se utilizó el operador `NOT` para filtrar a los empleados que no pertenecen al departamento de Tecnología de la Información.

### Evidencia

![Empleados que no pertenecen a TI](imagenes/06-no-ti.png)

---

# 📊 Resumen

Durante este proyecto se aplicaron diferentes filtros SQL para obtener información específica relacionada con los intentos de inicio de sesión y los equipos de los empleados.

Las tablas utilizadas fueron:

```text
log_in_attempts
employees
```

Los principales operadores y elementos utilizados fueron:

```text
WHERE
AND
OR
NOT
LIKE
%
```

Estas consultas permitieron analizar diferentes escenarios relacionados con:

* Intentos fallidos de inicio de sesión.
* Actividad fuera del horario de atención.
* Actividad registrada en fechas específicas.
* Conexiones procedentes de países diferentes de México.
* Empleados pertenecientes a determinados departamentos.
* Empleados que no pertenecen al área de TI.

---

# 🎓 Aprendizajes

Este proyecto permitió aplicar consultas SQL a escenarios relacionados con el **análisis de información y la seguridad**, fortaleciendo el uso de filtros, operadores lógicos y patrones de búsqueda para identificar información relevante dentro de diferentes conjuntos de datos.

Entre los principales conocimientos aplicados se encuentran:

* Construcción de consultas SQL.
* Filtrado de registros mediante condiciones.
* Uso de operadores lógicos.
* Búsqueda de patrones con `LIKE`.
* Análisis de registros de inicio de sesión.
* Identificación de información relevante para investigaciones de seguridad.
* Aplicación de SQL en escenarios relacionados con ciberseguridad.

---

# 📁 Estructura del proyecto

```text
analisis-forense-deteccion-amenazas-sql/
│
├── README.md
│
└── imagenes/
    ├── 01-intentos-fallidos.png
    ├── 02-fechas-especificas.png
    ├── 03-fuera-de-mexico.png
    ├── 04-empleados-marketing.png
    ├── 05-finance-sales.png
    └── 06-no-ti.png
```

---

## 🎓 Nota sobre el proyecto

Proyecto desarrollado con **fines educativos** como parte del curso **Google Cybersecurity**, realizado a través de **Coursera**. Las imágenes corresponden al entorno de laboratorio utilizado durante las prácticas del curso.

---

## 👤 Autor

**José Miguel Rojas Laurente**

**Áreas de interés:**
Ciberseguridad · Seguridad de la Información · SQL · Análisis de Seguridad
