# Fundamentos de Bases de Datos

[13 Reglas de Codd](./Reglas_Codd.md)

## Entidades

Una entidad es algo similar a un objeto (programación orientada a objetos) y representa algo en el mundo real, incluso algo abstracto. Tienen atributos que son las cosas que los hacen ser una entidad y por convención se ponen en plural.

![Entidad Laptop](./Pictures/Entidades_Laptop.png)

### Atributos

Son las características o propiedades que describen a la entidad (se encierra en un óvalo). Los atributos se componen de:

- Los atributos compuestos son aquellos que tienen atributos ellos mismos.

- Los atributos llave son aquellos que identifican a la entidad y no pueden ser repetidos. Existen:

  - Naturales: son inherentes al objeto como el número de serie
  - Clave artificial: no es inherente al objeto y se asigna de manera arbitraria.

### Tipos de Entidades

Entidades fuertes: son entidades que pueden sobrevivir por sí solas.

Entidades débiles: no pueden existir sin una entidad fuerte y se representan con un cuadrado con doble línea.

- Identidades débiles por identidad: no se diferencian entre sí más que por la clave de su identidad fuerte.

- Identidades débiles por existencia: se les asigna una clave propia.

### Representación

![Notacion chen](./Pictures/Notacion_Chen.png)

## Relaciones

Las relaciones nos permiten ligar o unir nuestras diferentes entidades y se representan con rombos. Por convención se definen a través de verbos.

Las relaciones tienen una propiedad llamada cardinalidad y tiene que ver con números. Cuántos de un lado pertenecen a cuántos del otro lado:

- Cardinalidad: 1 a 1
- Cardinalidad: 0 a 1
- Cardinalidad: 1 a N
- Cardinalidad: 0 a N
- Cardinalidad: N a N

![Relaciones y Cadinalidad](./Pictures/Relaciones.png)

## Tipos de Datos

|Texto  | Números | Fecha/Hora|Lógicos|
|-------|---------|-----------|----|
|CHAR (n)| INTEGER  |DATE| BOOLEAN|
|VARCHAR (n)| BIGINT | TIME||
|TEXT| DECIMAL (n,s)| DATETIME||
||NUMERIC (n,s)| TIMESTAMP||
||SMALLINT|||

## Restricciones

|Tipo de Restricción | Descripción |
|----|----------|
|NOT NULL| Se asegura que la columna no tenga valores nulos|
|UNIQUE| Se asegura que cada valor en la columna no se repita|
|PRIMARY KEY| Es una combinación de NOT NULL y UNIQUE|
|FOREIGN KEY| Identifica de manera única una tupla en otra tabla|
|CHECK| Se asegura que el valor en la columna cumpla una condición dada|
|DEFAULT| Coloca un valor por defecto cuando no hay un valor especificado|
|INDEX| Se crea por columna para permitir búsquedas más rápidas|

## Normalización

### Primera forma normal (1FN)

Formalmente, una tabla está en primera forma normal si:

- Todos los atributos son atómicos. Un atributo es atómico si los elementos del dominio son simples e indivisibles.
- No debe existir variación en el número de columnas.
- Los campos no clave deben identificarse por la clave (dependencia funcional).
- Debe existir una independencia del orden tanto de las filas como de las columnas; es decir, si los datos cambian de orden no deben cambiar sus significados.

Se traduce básicamente a que si tenemos campos compuestos como por ejemplo “nombre_completo” que en realidad contiene varios datos distintos, en este caso podría ser “nombre”, “apellido_paterno”, “apellido_materno”, etc.

También debemos asegurarnos que las columnas son las mismas para todos los registros, que no haya registros con columnas de más o de menos.

Todos los campos que no se consideran clave deben depender de manera única por el o los campos que si son clave.

Los campos deben ser tales que si reordenamos los registros o reordenamos las columnas, cada dato no pierda el significado.

![Primera forma sin normalizar](./Pictures/1NL_Sin.png)

Atributos atómicos (Sin campos repetidos)
![Primera forma normalizada](./Pictures/1NL_Normalizado.png)

### Segunda forma normal (2FN)

Formalmente, una tabla está en segunda forma normal si:

- Está en 1FN
- Sí los atributos que no forman parte de ninguna clave dependen de forma completa de la clave principal. Es decir, que no existen dependencias parciales.
- Todos los atributos que no son clave principal deben depender únicamente de la clave principal.

Lo anterior quiere decir que sí tenemos datos que pertenecen a diversas entidades, cada entidad debe tener un campo clave separado

Cumple 1FN y Cada campo de la tabla debe depender de una clave única.
![Segunda forma normalizada](./Pictures/2NL_Normalizado.png)

### Tercera forma normal (3FN)

Esta FN se traduce en que aquellos datos que no pertenecen a la entidad deben tener una independencia de las demás y debe tener un campo clave propio. Continuando con el ejemplo anterior, al aplicar la 3FN

Cumple 1FN y 2FN y los campos que NO son clave NO deben tener dependencias.
![Tercera forma normalizada](./Pictures/3NL_Normalizado.png)

### Cuarta forma normal (4FN)

Esta FN trata de eliminar registros duplicados en una entidad, es decir que cada registro tenga un contenido único y de necesitar repetir la data en los resultados se realiza a través de claves foráneas.

Cumple 1FN, 2FN y 3FN los campos multievaluados se identifican por una clave única.

![Cuarta forma normalizada](./Pictures/4NL_Normalizado.png)

## SQL hasta la sopa

Diferentes sublenguajes del lenguaje SQL
![SQL Comandos](./Pictures/SQL_Comandos.png)

### Sublenguaje DDL

Creando la infraestructura de la base de datos.

**Creación de bases de datos y tablas** (CREATE).

``` SQL
#Crear una base de datos
CREATE DATABASE test_db;
USER DATABASE test_db;

#Crear una tabla
CREATE TABLE people(
  person_id INTEGER PRIMARY KEY AUTOINCREMENT NOT NULL,
  last_name VARCHAR(255),
  first_name VARCHAR(255),
  address VARCHAR(255),
  city VARCHAR(255)
);
```

En este caso lo primero que estamos haciendo es crear la base de datos llamada test_db y seleccionándola.

Lo siguiente a realizar es crear la tabla people cuyo campo llave es *person_id* en el cual lo llamamos clave primaria que sea autoincremental es decir que vaya aumentando en cada registro y que no se permita que este campo se encentré vació.

Los siguientes campos son en su gran mayoría texto a 255 Caracteres.

**Creando una vista** (SELECT)

```SQL
# Crear View
CREATE OR REPLACE VIEW v_brasil_customers AS 
  SELECT customer_name,
  contact_name
  FROM customers
  WHERE country = "Brasil";
```

En este código empieza checando si ya existe la vista *v_brasil_customers* en caso de que no, lo crea seleccionando los campos de *[ customer_name, contact_name]* de la tabla customers donde el país de residencia sea brasil.

**Modificar una tabla** (ALTER)

```SQL
ALTER TABLE people
ADD date_of_birth DATE;

ALTER TABLE people
ALTER COLUMN date_of_birth YEAR;

ALTER TABLE people
DROP COLUMN date_of_birth;
```

Lo primero a realizar es tomar la tabla people y le añadimos el campo de *date_of_birth* el cual especificamos que sea de tipo fecha.

En la segunda modificación cambiamos el campo antes mencionado a un que solo almacene el año.

Y por ultimo eliminamos el cambio de la tabla people.

**Eliminando Datos** (DROP)

```SQL
DROP TABLE people;
DROP DATABASE test_db;
```

La secuencia drop, elimina ya sea la tabla, base de datos o la vista.

Hay que tener suficiente cuidado con este comando porque es un comando sencillo pero puede eliminar todos los datos.

### Sublenguaje DML

Modificando los datos.

Insert

```SQL
INSERT INTO people (last_name, first_name, address, city)
VALUES ('Hernandez', 'Laura', 'Calle 21', 'Monterrey')
```

Introduce los valores a la base de datos de people.

Update

```SQL
UPDATE people
SET last_name = 'Chavez', city='Merida'
WHERE person_id = 1;

UPDATE people 
SET first_name = 'Juan'
WHERE city = 'Merida'

UPDATE people
SET first_name ='Juan';
```

Actualizando los datos de la tabla people.

Delete

```SQL
DELETE FROM people
WHERE person_id = 1;

DELETE FROM people;
```

Elimina un registro de acuerdo a los parámetros que seleccionemos.

Select

```SQL
SELECT first_name, last_name
FROM people;
```

Selecciona los diferentes datos y campos relacionados.

## Consultas a una base de datos

Las consultas o queries a una base de datos son una parte fundamental ya que esto podría salvar un negocio o empresa.
Alrededor de las consultas a las bases de datos se han creado varias especialidades como ETL o transformación de datos, business intelligence e incluso machine learning.

```SQL
SELECT city, count (*) AS total
FROM people
WHERE active = true
GROUP BY city
ORDER BY total DESC
HAVING total >=2 ;
```

### Estructura de una query

Los queries son la forma en la que estructuramos las preguntas que se harán a la base de datos. Transforma preguntas en sintaxis.

El query tiene básicamente 2 partes: SELECT y FROM y puede aparecer una tercera como WHERE.

La estrellita o asterisco (*) quiere decir que vamos a seleccionar todo sin filtrar campos.

**Estructura Select**
SELECT se encarga de proyectar o mostrar datos.

El nombre de las columnas o campos que estamos consultando puede ser cambiado utilizando AS después del nombre del campo y poniendo el nuevo que queremos tener:

```SQL
SELECT titulo AS encabezado
FROM post;
```

Existe una función de SELECT para poder contar la cantidad de registros. Esa información (un número) será el resultado del query:

```SQL
SELECT COUNT(*)
FROM post;
```

**FROM y SQL JOIN'S**
FROM indica de dónde se deben traer los datos y puede ayudar a hacer sentencias y filtros complejos cuando se quieren unir tablas. La sentencia compañera que nos ayuda con este proceso es JOIN.

Los diagramas de Venn son círculos que se tocan en algún punto para ver dónde está la intersección de conjuntos. Ayudan mucho para poder formular la sentencia JOIN de la manera adecuada dependiendo del query que se quiere hacer.

![Tipos de Join](./Pictures/Tipos_Join.png)

**WHERE**
WHERE es la sentencia que nos ayuda a filtrar tuplas o registros dependiendo de las características que elegimos.

- La propiedad LIKE nos ayuda a traer registros de los cuales conocemos sólo una parte de la información.
- La propiedad BETWEEN nos sirve para arrojar registros que estén en el medio de dos. Por ejemplo los registros con id entre 20 y 30.

```SQL
SELECT * 
FROM post 
WHERE fecha_publicacion > "2025-01-01";
```

Filtra todos los registros de la tabla post que cumplan la condición que sean mayor a la fecha del 01/01/2025.

```SQL 
SELECT * 
FROM post 
WHERE titulo LIKE '%escandalo%';
```

Filtra los datos de la tabla post que en el titulo contenga la palabra escándalo.

```SQL
SELECT * 
FROM post 
WHERE fecha_publicacion BETWEEN '2023-01-01' AND '2025-01-01';
```

Devuelve todos los datos que se encuentren entre el 01/01/2023 al 01/01/2025

Where con nulo y no nulo
El valor nulo en una tabla generalmente es su valor por defecto cuando nadie le asignó algo diferente. La sintaxis para hacer búsquedas de datos nulos es IS NULL. La sintaxis para buscar datos que no son nulos es IS NOT NULL

```SQL
SELECT * 
FROM post 
WHERE usuario IS NOT NULL;
```

Devuelve todos los post que cuenten con un usuario

```SQL
SELECT * 
FROM post 
WHERE usuario IS NOT NULL 
  AND estatus ='activo'
  AND id <50
  AND categoria_id =2
  ;
```

Filtra los post que cuenten con usuario y el usuario este activo donde el post debe tener un id menor a 50 y la categoría debe ser igual a 2.

**GROUP BY**
GROUP BY tiene que ver con agrupación. Indica a la base de datos qué criterios debe tener en cuenta para agrupar.

```SQL
SELECT estatus MONTH NAME(fecha_publicacion) AS post_month, COUNT(*) AS post_quantity
FROM posts
GROUP BY estatus, post_month;
```

Agrupa los datos por estatus y mes del mes en el que fueron publicados

**ORDER BY y HAVING**
La sentencia ORDER BY tiene que ver con el ordenamiento de los datos dependiendo de los criterios que quieras usar.

- ASC sirve para ordenar de forma ascendente.
- DESC sirve para ordenar de forma descendente.
- LIMIT se usa para limitar la cantidad de resultados que arroja el query.

HAVING tiene una similitud muy grande con WHERE, sin embargo el uso de ellos depende del orden. Cuando se quiere seleccionar tuplas agrupadas únicamente se puede hacer con HAVING.

```SQL
SELECT *
FROM posts
ORDER BY fecha_publicacion ASC;
```

```SQL
SELECT *
FROM posts
ORDER BY fecha_publicacion ASC
LIMIT 5;
```
