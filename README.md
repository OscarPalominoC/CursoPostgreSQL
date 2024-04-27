# CursoPostgreSQL
Desarrollo del curso de PostgreSQL

## ¿Qué es PostgreSQL?
* Open Source
* Objeto-Relacional
* Usa SQL
* Desde 1986
* PostGIS
* PL/PgSQL
* Cumple ACID = 
    * Atomicity:Corresponde a que se puede separar las funciones que está desarrollando la base de datos en pequeñas tareas, y desarrollarlas como un todo. Si alguna tarea falla, se realiza un rollback, es decir, se deshacen los cambios hechos.
    * Consistency: Todo lo que se desarrollo entorno al objeto relacional en que se puede tener 2 tablas que poseen llaves primarias, llaves foráneas, y consistencia quiere decir que los datos tienen una congruencia entre sí.
    * Isolation: Puedes tener varias tareas ejecutandose al mismo tiempo en la base de datos. 
    * Durability: Puedes tener la seguridad que la información no se perderá en caso de un fallo catastrófico, ¿Por qué? PostgreSQL primero relaciona los cambios en una bitacora, y luego escribe los cambios en la base de datos.

## ¿Por qué PostgreSQL?
* Tipos de Datos
* Integridad de Datos
* Concurrencia. Rendimiento
* Fiabilidad, recuperación ante desastres
* Seguridad
* Extensibilidad
* Internacionalización, Búsqueda de texto.

https://platzi.com/blog/que-es-el-teorema-cap-y-como-elegir-la-base-de-datos-para-tu-proyecto/
https://www.postgresql.org/


### Instalación de postgres en ubuntu.
`sudo apt-get install postgresql postgresql-contrib`
### instalación de la interfaz gráfica.
`sudo apt-get install pgadmin3`

### Iniciar la base de datos
`sudo -u postgres<usuario> psql`
### Cambiar la contraseña del usuario postgres.
* Dentro de la base de datos activa:
    `alter user postgres with password '<contraseña>';`

## Comandos más frecuentes:
* `\l` -> Lista todas las bases de datos instaladas en el servidor.
* `\c <nombre BD>` -> Ingresa a la base de datos.
* `\dt` -> Lista las relaciones en la base de datos.
* `\d <nombre columna>` -> Muestra a detalle cómo se crea un dato
* `\h` -> lista los comandos de postgres para ser usados como SQL.
* `\g` -> Ejecuta la última función que se haya utilizado en postgres.
* `\timing` -> Inicializa el contador de tiempo para que la consola muestre en pantalla cuánto tiempo demoró en ejecutar un comando.

Postgres funciona con SQL estándar, eso quiere decir que todos los comandos deben terminar con ;


## Artículo - Comandos más utilizados en PostgreSQL 

### La Consola

La consola en PostgreSQL es una herramienta muy potente para crear, administrar y depurar nuestra base de datos. podemos acceder a ella después de instalar PostgreSQL y haber seleccionado la opción de instalar la consola junto a la base de datos.

PostgreSQL está más estrechamente acoplado al entorno UNIX que algunos otros sistemas de bases de datos, utiliza las cuentas de usuario nativas para determinar quién se conecta a ella (de forma predeterminada). El programa que se ejecuta en la consola y que permite ejecutar consultas y comandos se llama psql, psql es la terminal interactiva para trabajar con PostgreSQL, es la interfaz de línea de comando o consola principal, así como PgAdmin es la interfaz gráfica de usuario principal de PostgreSQL.

Después de emitir un comando PostgreSQL, recibirás comentarios del servidor indicándote el resultado de un comando o mostrándote los resultados de una solicitud de información. Por ejemplo, si deseas saber qué versión de PostgreSQL estás usando actualmente, puedes hacer lo siguiente:

`SELECT VERSION();`

### Comandos de ayuda
En consola los dos principales comandos con los que podemos revisar el todos los comandos y consultas son:
* `\?` Con el cual podemos ver la lista de todos los comandos disponibles en consola, comandos que empiezan con backslash ()
* `\h` Con este comando veremos la información de todas las consultas SQL disponibles en consola. Sirve también para buscar ayuda sobre una consulta específica, para buscar información sobre una consulta específica basta con escribir \h seguido del inicio de la consulta de la que se requiera ayuda, así: \h ALTER

De esta forma podemos ver toda la ayuda con respecto a la consulta ALTER

### Comandos de navegación y consulta de información
* `\c` Saltar entre bases de datos
* `\l` Listar base de datos disponibles
* `\dt` Listar las tablas de la base de datos
* `\d <nombre_tabla>` Describir una tabla
* `\dn` Listar los esquemas de la base de datos actual
* `\df` Listar las funciones disponibles de la base de datos actual
* `\dv` Listar las vistas de la base de datos actual
* `\du` Listar los usuarios y sus roles de la base de datos actual

### Comandos de inspección y ejecución
* `\g` Volver a ejecutar el comando ejecutando justo antes
* `\s` Ver el historial de comandos ejecutados
* `\s <nombre_archivo>` Si se quiere guardar la lista de comandos ejecutados en un archivo de texto plano
* `\i <nombre_archivo>` Ejecutar los comandos desde un archivo
* `\e` Permite abrir un editor de texto plano, escribir comandos y ejecutar en lote. \e abre el editor de texto, escribir allí todos los comandos, luego guardar los cambios y cerrar, al cerrar se ejecutarán todos los comandos guardados.
* `\ef` Equivalente al comando anterior pero permite editar también funciones en PostgreSQL

### Comandos para debug y optimización
* `\timing` Activar / Desactivar el contador de tiempo por consulta
### Comandos para cerrar la consola
* `\q` Cerrar la consola

## Ejecutando consultas en la base de datos usando la consola
De manera predeterminada PostgreSQL no crea bases de datos para usar, debemos crear nuestra base de datos para empezar a trabajar, verás que existe ya una base de datos llamada postgres pero no debe ser usada ya que hace parte del CORE de PostgreSQL y sirve para gestionar las demás bases de datos.

Para crear una base de datos debes ejecutar la consulta de creación de base de datos, es importante entender que existe una costumbre no oficial al momento de escribir consultas; consiste en poner en mayúsculas todas las palabras propias del lenguaje SQL cómo CREATE, SELECT, ALTE, etc y el resto de palabras como los nombres de las tablas, columnas, nombres de usuarios, etc en minúscula. No está claro el porqué de esta especie de “estándar” al escribir consultas SQL pero todo apunta a que en el momento que SQL nace, no existían editores de consultas que resaltaran las palabras propias del lenguaje para diferenciar fácilmente de las palabras que no son parte del lenguaje, por eso el uso de mayúsculas y minúsculas.

Las palabras reservadas de consultas SQL usualmente se escriben en mayúscula, ésto para distinguir entre nombres de objetos y lenguaje SQL propio, no es obligatorio, pero podría serte útil en la creación de Scripts SQL largos.

Vamos ahora por un ligero ejemplo desde la creación de una base de datos, la creación de una tabla, la inserción, borrado, consulta y alteración de datos de la tabla.

Primero crea la base de datos, “CREATE DATABASE transporte;” sería el primer paso.

Ahora saltar de la base de datos postgres que ha sido seleccionada de manera predeterminada a la base de datos transporte recién creada utilizando el comando \c transporte.

Ahora vamos a crear la tabla tren, el SQL correspondiente sería:

`CREATE TABLE tren ( id serial NOT NULL, modelo character varying, capacidad integer, CONSTRAINT tren_pkey PRIMARY KEY (id) );`

La columna id será un número autoincremental (cada vez que se inserta un registro se aumenta en uno), modelo se refiere a una referencia al tren, capacidad sería la cantidad de pasajeros que puede transportar y al final agregamos la llave primaria que será id.

Ahora que la tabla ha sido creada, podemos ver su definición utilizando el comando \d tren

PostgreSQL ha creado el campo id automáticamente cómo integer con una asociación predeterminada a una secuencia llamada ‘tren_id_seq’. De manera que cada vez que se inserte un valor, id tomará el siguiente valor de la secuencia, vamos a ver la definición de la secuencia. Para ello, \d tren_id_seq es suficiente:

* Vemos que la secuencia inicia en uno, así que nuestra primera inserción de datos dejará a la columna id con valor uno. `INSERT INTO tren( modelo, capacidad ) VALUES (‘Volvo 1’, 100);`
* Consultamos ahora los datos en la tabla: `SELECT * FROM tren;`
* Vamos a modificar el valor, establecer el tren con id uno que sea modelo Honda 0726. Para ello ejecutamos la consulta tipo `UPDATE tren SET modelo = 'Honda 0726' Where id = 1;`
* Verificamos la modificación `SELECT * FROM tren;`
* Ahora borramos la fila: `DELETE FROM tren WHERE id = 1;`
* Verificamos el borrado `SELECT * FROM tren;`
* El borrado ha funcionado tenemos 0 rows, es decir, no hay filas. Ahora activemos la herramienta que nos permite medir el tiempo que tarda una consulta `\timing`
* Probemos cómo funciona al medición realizando la encriptación de un texto cualquiera usando el algoritmo md5: `SELECT MD5('Vamos a encriptar un texto como el que lees.');`


## TIPOS DE DATOS EN PostgreSQL
* https://www.postgresql.org/docs/11/datatype.html
* https://todopostgresql.com/postgresql-data-types-los-tipos-de-datos-mas-utilizados/


## Artículo - Jerarquía de Bases de Datos 

### Toda jerarquía de base de datos se basa en los siguientes elementos:
    
* Servidor de base de datos: Computador que tiene un motor de base de datos instalado y en ejecución.
* Motor de base de datos: Software que provee un conjunto de servicios encargados de administrar una base de datos.
* Base de datos: Grupo de datos que pertenecen a un mismo contexto.
* Esquemas de base de datos en PostgreSQL: Grupo de objetos de base de datos que guarda relación entre sí (tablas, funciones, relaciones, secuencias).
* Tablas de base de datos: Estructura que organiza los datos en filas y columnas formando una matriz.

PostgreSQL es un motor de base de datos.

La estructura de la base de datos diseñada para el reto corresponde a los siguientes elementos:
```
BD: transporte -> Schema: public.
```
La base de datos se llama transporte, usaremos su esquema predeterminado public.

El esquema public contiene las siguientes tablas:
* Estación
* Pasajero
* Tren

Y las tablas de relaciones entre cada uno de los elementos anteriores son:
* Trayecto
* Viaje

El esquema relacional entre las tablas corresponde al siguiente diagrama:

![Esquema](./ESQUEMA.jpg)

### Estación
Contiene la información de las estaciones de nuestro sistema, incluye datos de nombre con tipo de dato texto y dirección con tipo de dato texto, junto con un número de identificación único por estación.
### Tren
Almacena la información de los trenes de nuestro sistema, cada tren tiene un modelo con tipo de dato texto y una capacidad con tipo de dato numérico que representa la cantidad de personas que puede llevar ese tren, también tiene un ID único por tren.
### Pasajero
Es la tabla que contiene la información de las personas que viajan en nuestro sistema de transporte masivo, sus columnas son nombre tipo de dato texto con el nombre completo de la persona, direccion_residencia con tipo de dato texto que indica dónde vive la persona, fecha_nacimiento tipo de dato texto y un ID único tipo de dato numérico para identificar a cada persona.
### Trayecto
Relaciona los trenes con las estaciones, simula ser las rutas que cada uno de los trenes pueden desarrollar entre las estaciones
### Viaje
Relaciona Trayecto con Pasajero ilustrando la dinámica entre los viajes que realizan las personas, los cuales parten de una estación y se hacen usando un tren.

## Creación de Tablas


INSERCIÓN DE INFORMACIÓN
```
    Passenger:
        INSERT INTO public.passenger(
        name, address, birthday)
        VALUES ('Passenger', 'Address', '2020-06-09');
    
    Station:
        INSERT INTO public.station(
        name, address)
        VALUES ('Name', 'Address');
    
    Train:
        INSERT INTO public.train(
        model, capacity)
        VALUES ('Model', 'Capacity');
    
    Trip:
        INSERT INTO public.trip(
        id_train, id_station)
        VALUES (1, 2);
    
    Travel:
        INSERT INTO public.trip(
        id, id_train, id_station)
        VALUES (1, 1);
```
## TABLAS PARTICIONADAS
* NO hacen uso de llaves primarias.
* Al momento de crearlas, en la pestaña general se selecciona la opción partitioned table. Esto le indicará a POSTGRES que es una tabla particionada.
* Se ingresan los datos de las columnas, y luego se dirige a 'Partitions'.
* Se selecciona el tipo de partición, rango, lista o hash. Para la clase, fue de rango.
* Se agrega una Partition Key (+).
* Se selecciona el tipo de llave, columna o expresión (columna en la clase)
* Se selecciona la columna. y Ok
* Clic derecho a la tabla particionada, Scripts, Insert Script.

Se escribe lo siguiente:
```
    INSERT INTO public.log_travel(
	id_travel, date_travel)
	VALUES (1, '2020-10-10');
        
    SELECT * FROM log_travel;
        
    CREATE TABLE log_travel202010 PARTITION OF log_travel
    FOR VALUES FROM ('2020-10-01') TO ('2020-10-31');
```
Lo que primero se debe ejecutar es la creación de la partición:
```
    CREATE TABLE log_travel202010 PARTITION OF log_travel
    FOR VALUES FROM ('2020-10-01') TO ('2020-10-31');
```
Luego, se guardan los datos.
```
    INSERT INTO public.log_travel(
	id_travel, date_travel)
	VALUES (1, '2020-10-10');
```
Por último, se verifican:
```
    SELECT * FROM log_travel;
```
Como es una tabla particionada, si intento guardar un dato más, no me dejará, porque ya fue almacenada en memoria, así que lo ideal para este tipo de tablas, es automatizarla y que se llene con los datos disponibles en la DB.


## CREACIÓN DE ROLES
### ¿Qué puede hacer un rol?
* Crear y eliminar
* Asignar atributos
* Agrupar con otros roles
* Roles predeterminados
    


Inner join: solo nos trae los datos que coinciden en ambas tablas.
```
select * from route r
innerjoin train tr
on tr.train_id = r.train_id;
```
Este es un full outer join: trae todos los datos de ambas tablas. Coincidan o no.
```
select * 
from route r
fullouterjoin train tr
on tr.train_id = r.train_id;
```

Este full outer join ahora solo nos trae los datos que no coinciden de la tabla A  con la la tabla B, tambien nos trae los datos de la tabla B que no coiniden con la  tabla A. (es como el opuesto del inner join, porque en lugar de traernos los que coinciden en ambas tablas, nos trae solo los que no coinciden en ambas tablas.)
```
select * 
from route r
fullouterjoin train tr
on tr.train_id = r.train_id
where r.train_id isnull
or tr.train_id isnull;
```

left join: nos trae todos los datos de la tabla A(izquierda) y solo los datos de la  tabla B que coincidan en la tabla A.
```
select * from route r
leftjoin train tr
on tr.train_id = r.train_id;
```
left outer join: nos devuelve todos los datos de la tabla A que no coincide con la tabla B.
```
select * from route r
leftjoin train tr
on tr.train_id = r.train_id
where tr.train_id isnull;
```
right join: nos devuelve todos los datos de la tabla B, y solo los datos de la tabla A que coincidan con la tabla B
```
select * from route r
rightjoin train tr
on tr.train_id = r.train_id;
```
right outer join: nos trae todos los datos de la tabla B que no coinciden con la tabla A

```
select * from route r
rightjoin train tr
on tr.train_id = r.train_id
where r.train_id isnull;
```
NOTA: Cuando usamos left join (Tabla A a la tabla B) estamos usando la tabla A, es decir traemos todos los datos de la tabla A y solo los datos de la tabla B que coinciden con la tabla A. si queremos usar un left outer join la llave primaria null que debemos especificar es la de la tabla B.
```
WHERE b.pkey us null;
```
lo mismo pasa cuando usamos un right outer join. Como usamos la tabla B y solo los que coinciden con la tabla A entonces la llave null que usamos es de la tabla A.
```
WHERE a.pkey us null;							
```

## FUNCIONES ESPECIALES PRINCIPALES
* `ON CONFLICT DO`: Ayuda a solucionar problemas cuando queremos insertar o modificar datos en una tabla que no podamos, y después hacemos la actualización correcta, es decir, si queremos insertar un dato sobre otro dato, ON CONFLICT DO permite caracterizar si lo que queremos es actualizar el dato.
```
INSERT INTO public.station(
id, name, address)
VALUES (1, 'Center Station', '1234 Evergreen Av.')
ON CONFLICT (id) DO UPDATE SET name = 'Center Station', address = '1234 Evergreen Av.';
```
* `RETURNING`: Permite devolver todos los cambios hechos sobre la base de datos. Devolver no significa que regrese a un estado anterior, sino que muestra de nuevo todos los datos para confirmar que todo haya quedado bien insertado y si hay un campo tipo serial, nos devuelve el valor asignado.
```
INSERT INTO public.station(
name, address)
VALUES ('Tamal Station', 'Food Av.')
RETURNING id;
```
**Regresa en pantalla el id creado para Tamal Station.**

* LIKE / ILIKE: Permite hacer búsquedas, al estilo de REGEX donde por ejemplo, podemos probar buscar nombres que empiecen por la letra O, o que terminen con la letra Z.

Postgres recibe 2 parámetros, % y underscore (_), % devuelve todos los caracteres que estén por delante o detrás de la letra a buscar, underscore muestra en pantalla el resultado siempre y cuando, la cantidad de underscore sea la misma del caracter buscado, ej:    
```
SELECT name
FROM public.station
WHERE name ILIKE 'c_____________'; -> Retornó Center Station.
SELECT name
FROM public.passenger
WHERE name ILIKE 'j%';
```
Retorna todos los pasajeros cuyo nombre empieza por la letra j, sin importar si empieza en mayúsculas o minúsculas. ILIKE no tiene en cuenta minúsculas o mayúsculas, a diferencia de LIKE.
    
* `IS` / `IS NOT`: Permite comparar 2 tipos de dato que no sean estándar, como numérico o alfanumérico, sino que sean de tipo objeto o especiales como null, con este podemos saber si un campo es nulo o no lo es.
```
SELECT *
FROM public.train
WHERE model IS NOT NULL;
```
Con esto devuelve todos los datos de la tabla tren, puesto que ninguno de los datos ingresados contiene un modelo null.
```
SELECT *
FROM public.train
WHERE model IS NULL;
```
No devuelve nada, ya que todos los datos en el modelo no es nulo.


## FUNCIONES AVANZADAS EN POSTGRESQL.
* `COALESCE`: Permite comparar 2 valores y retornar cuál de los 2 NO es nulo.
```
SELECT id, COALESCE(name, 'No aplica'), address, birthday
FROM public.passenger WHERE id = 1002;
```
Muestra la información del registro con id = 1002, que se le borró el nombre y se guardó vacío (null por defecto), al aplicar COALESCE, retorna la búsqueda, y en lugar de mostrar null, mostró la frase 'No aplica', y el nombre de la columna pasó de ser name a COALESCE.
```
SELECT id, COALESCE(name, 'No aplica') AS nombre, address, birthday
FROM public.passenger WHERE id = 1002;
```
Retorna lo mismo que la búsqueda anterior, pero con la diferencia que el AS nombre le añade un alias a la columna, es decir, en lugar de darle como nombre a la columna COALESCE, le pone "nombre".
* `NULLIF`: Compara 2 valores y regresa NULL si son iguales.
```
SELECT NULLIF (0,0) // Retorna null, debido a que son valores iguales.
```
* `GREATEST` y `LEAST`: Compara un arreglo de valores y retorna el mayor y el menor respectivamente.
```
SELECT GREATEST (0,5,4,,1,5,7,5,2,6) // Retorna 7, porque es el número mayor de la lista.
SELECT LEAST (0,5,4,,1,5,7,5,2,6) // Retorna 0, porque es el número menor de la lista.
```
* BLOQUES ANÓNIMOS: Al igual que los lenguajes de programación, permite realizar condicionales dentro de una consulta de bases de datos.
```
SELECT id, name, address, birthday,
CASE
WHEN birthday > '2002-06-13' 
THEN 'Menor de edad.'
ELSE 'Mayor de edad.'
END
FROM public.passenger;
```
Selecciona toda la información de los pasajeros e identifica mediante una nueva columna si son mayores o menores de edad, con el uso del WHEN.
```
SELECT id, name, address, birthday,
CASE
WHEN EXTRACT(YEAR FROM current_date) - EXTRACT(YEAR FROM birthday) < 18
THEN 'Menor de edad.'
ELSE 'Mayor de edad.'
END
FROM public.passenger;
```
Hace exactamente lo mismo, pero con la diferencia que es más dinámico

## RETO.
GENERAR 2 COLUMNAS CON LA LISTA DE PASAJEROS, UNA QUE INDIQUE QUÉ NOMBRES COMIENZAN CON O Y OTRA QUE INDIQUE QUÉ PERSONAS SON MAYORES Y/O MENORES DE EDAD.
```
SELECT id, name,
CASE
WHEN name ILIKE 'o%' 
    THEN 'True'
    ELSE 'False'
END AS start_with_an_O,
CASE
    WHEN EXTRACT(YEAR FROM current_date) - EXTRACT(YEAR FROM birthday) < 30
        THEN 'Menor de edad.'
        ELSE 'Mayor de edad.'
END AS older_age
FROM public.passenger
ORDER BY start_with_an_o DESC;
```

## VISTAS
Agarra una consulta que se realice muchas veces y colocarla bajo un solo nombre.

Centraliza muchos esfuerzos en una sola función.
* Vista volátil: Siempre que se haga la consulta en la vista, la BD hace la ejecución de la consulta en la BD, por lo que siempre se va a tener información reciente.
* Vista materializada: Hace la consulta una sola vez, y la información queda almacenada en memoria, la siguiente vez que se consulte, trae el dato almacenado, eso es bueno y malo a la vez, bueno porque la velocidad con la que se entrega la información es rápida, malo porque la información no es actualizada. Es ideal utilizar este tipo de vista en procesos que utilice días anteriores, porque el día de ayer, ya pasó y no hay razón para actualizarlo.
Para crear una vista volátil en postgres, damos click derecho a views, create, view, le damos un nombre, y en la pestaña code escribimos o pegamos el código de la consulta que queremos guardar, la guardamos y para usar la vista usamos:
```
SELECT * FROM <nombre_vista>; y listo.
```
Para crear una vista materializada, primero creamos la consulta, y definimos si los datos nos interesan o no, luego, vamos a la opción materialized views, click derecho, create, materialized view. Se abre la ventana, le damos un nombre, termina con _mview, y en la pestaña Definition escribimos la consulta que necesitamos guardar. Guardamos.

Al probarla en este momento nos lanza un error, ¿por qué? porque no tiene datos almacenados. Para almacenar datos usamos:
```
REFRESH MATERIALIZED VIEW <nombre vista>;
```

Y ahora si podemos consultarla:
```
SELECT * FROM <nombre_vista_mview>;
```


* PL/PgSQL (Procedural Language / PostgreSQL Structured Query Language)
* Ayuda a desarrollar código directamente sobre la base de datos.
* Se componen de nombres de funciones, declaraciones y bloques de código.
Estructura Básica.
```
[ <label> ]
[ DECLARE
    declarations]
BEGIN
    Statements
END [label];

DO $$
BEGIN
    RAISE NOTICE 'Algo está pasando';
END
$$
```
* DECLARE
rec record := ; // Se escribe el nombre de la variable y luego el tipo de dato que retorna, para darle un valor inicial utilizamos := ¿por qué? porque el igual solo está reservado para las consultas.
```
DO $$
DECLARE
rec record; // Record almacena datos.
counter integer := 0; // Entero
BEGIN
	FOR rec IN SELECT * FROM passenger LOOP // rec almacenará todos los datos de la tabla passenger
		RAISE NOTICE 'Un pasajero se llama %', rec.name; // El % será reemplazado por la variable que vamos a mostrar. Para acceder al nombre usamos rec.name
		counter := counter + 1;
	END LOOP;
	RAISE NOTICE 'La cantidad de pasajeros es: %', counter;
END
$$
```
Postgres usando algunas librerías puede soportar otros lenguajes de programación, como python, c++, sql básico entre otros. Por ello, cuando hagamos una función debemos indicar qué lenguaje de programación estamos utilizando.
```
CREATE FUNCTION testPL() 
  RETURNS void // No regresa nada.
AS $$
DECLARE
rec record;
counter integer := 0;
BEGIN
	FOR rec IN SELECT * FROM passenger LOOP
		RAISE NOTICE 'Un pasajero se llama %', rec.name;
		counter := counter + 1;
	END LOOP;
	RAISE NOTICE 'La cantidad de pasajeros es: %', counter;
END
$$
LANGUAGE PLPGSQL;

SELECT testPL();
```
En las tablas no mostrará ningún valor, pero si se mira desde la pestaña de mensajes, se podrán ver el mensaje de los pasajeros y cuántos hay.
Para actualizar una función se utiliza CREATE OR REPLACE FUNCTION <nombreFunción>(). Sin embargo, si queremos actualizar el tipo de dato que retorna será imposible hacer dicha actualización, porque el tipo de dato no es actualizable, para ello, debemos borrar la función con DROP FUNCTION <nombreFunción>(); y luego volver a crear la función.
```
DROP FUNCTION testPL(); // Borramos la función anterior, para poder actualizar el tipo de dato que retorna
CREATE OR REPLACE FUNCTION testPL() 
  RETURNS integer 
AS $$
DECLARE
rec record;
counter integer := 0;
BEGIN
	FOR rec IN SELECT * FROM passenger LOOP
		RAISE NOTICE 'Un pasajero se llama %', rec.name;
		counter := counter + 1;
	END LOOP;
	RAISE NOTICE 'La cantidad de pasajeros es: %', counter;
	RETURN counter;
END
$$
LANGUAGE PLPGSQL;

SELECT testPL(); // Nos muestra en una celda la cantidad de pasajeros que hay en nuestra tabla, adicionalmente, en la pestaña mensajes muestra las consultas al nombre de estos pasajeros y al final cuántos hay.
```

## CREANDO PL USANDO FUNCIONES DE PGADMIN.

En el menú desplegable de la izquierda vamos a functions, click derecho, CREATE, le damos el nombre, en Definition se le tiene que asignar un tipo de retorno, en Code pegamos el bloque de código que queremos insertar, en este caso es:
```
DECLARE
rec record;
counter integer := 0;
BEGIN
	FOR rec IN SELECT * FROM passenger LOOP
		RAISE NOTICE 'Un pasajero se llama %', rec.name;
		counter := counter + 1;
	END LOOP;
	RAISE NOTICE 'La cantidad de pasajeros es: %', counter;
	RETURN counter;
END
```
Las configuraciones por defecto nos funcionan bien cómo están, así que no moveremos nada por ahora, depende de los requerimientos de la base de datos y de los proyectos en los que trabajemos requeriremos estas funciones, pero por ahora, la configuración por defecto es óptima.
En la pestaña SQL nos muestra el código que se va a ejecutar, podemos ver que postgres coloca sus propios signos pesos, razón por la cual no es necesario que peguemos en la pestaña código dichos signos.
Guardamos y vemos que la función ha sido creada.


## TRIGGERS
También conocidos como disparadores. Permiten ejecutar funciones dependiendo de acciones que se ejecuten dentro de una DB.
* Insert.
* Update.
* Delete.
Primero validamos la función, y que podamos guardar datos en una nueva tabla que hemos creado, para este caso se llamará 'passenger_counter'. Seleccionamos en el menú desplegable las funciones, la función que vamos a editar, en este caso es testPL, y añadimos la función para añadir la cantidad de pasajeros.
```
CREATE OR REPLACE FUNCTION public."testPL"(
	)
    RETURNS integer
    LANGUAGE 'plpgsql'

    COST 100
    VOLATILE 
    
AS $BODY$DECLARE
rec record;
counter integer := 0;
BEGIN
	FOR rec IN SELECT * FROM passenger LOOP
		RAISE NOTICE 'Un pasajero se llama %', rec.name;
		counter := counter + 1;
	END LOOP;
	INSERT INTO passenger_counter (total, time)
	VALUES (counter, now());
	RETURN counter;
END$BODY$;

ALTER FUNCTION public."testPL"()
    OWNER TO postgres;
```
Ya que funciona, ahora la función no puede devolver un tipo de dato integer, sino un tipo de dato trigger. Elíminamos el RETURN porque al ser un trigger no returna ningún tipo de dato.
```
CREATE OR REPLACE FUNCTION public."testPL"(
	)
    RETURNS TRIGGER
    LANGUAGE 'plpgsql'
AS $BODY$DECLARE
rec record;
counter integer := 0;
BEGIN
	FOR rec IN SELECT * FROM passenger LOOP
		counter := counter + 1;
	END LOOP;
	INSERT INTO passenger_counter (total, time)
	VALUES (counter, now());
END$BODY$;
```
Borramos la función anterior con DROP FUNCTION y volvemos a crear la nueva función con el retorno de dato de tipo trigger.

Para crear un trigger tenemos 3 tipos de disparadores
* BEFORE: Antes de que se hagan los cambios.
* AFTER: Después que se hagan los cambios.
* INSTEAD OF: En vez de hacer los cambios.
Y ahora creamos el trigger de la siguiente manera:
```
CREATE TRIGGER my_trigger // Creamos el trigger y le ponemos el nombre my_trigger
AFTER INSERT // Después de insertar
ON passenger // En la tabla pasajero
FOR EACH ROW // Para cada fila
EXECUTE PROCEDURE "testPL"(); // Ejecutar el procedimiento/función "testPL"()
```
Ahora, al momento de crear una fila nos arrojará un error, ¿por qué? porque el trigger tiene que retornarnos que se ha creado un dato.
Primero hay que eliminar los triggers y las funciones, como la función es un trigger, se encuentra en el menú desplegable "trigger functions".
Vuelve y se crea la función, y el trigger con el siguiente código.
```
DROP FUNCTION public."testPL"();

CREATE FUNCTION public."testPL"()
    RETURNS trigger
    LANGUAGE 'plpgsql'
    COST 100
    VOLATILE NOT LEAKPROOF
AS $BODY$DECLARE
rec record;
counter integer := 0;
BEGIN
	FOR rec IN SELECT * FROM passenger LOOP
		counter := counter + 1;
	END LOOP;
	INSERT INTO passenger_counter (total, time)
	VALUES (counter, now());
	RETURN NEW; // NEW es para retornar los datos nuevos que se están ingresando, OLD retorna los valores antiguos. Como estamos insertando valores, se necesita retornar los datos que estamos ingresando
END$BODY$;

ALTER FUNCTION public."testPL"()
    OWNER TO postgres;

CREATE TRIGGER my_trigger
    AFTER INSERT
    ON public.passenger
    FOR EACH ROW
    EXECUTE PROCEDURE public."testPL"();
```

## RETO CREAR UN TRIGGER PARA CUANDO SE BORRE UN DATO DE LA TABLA.
```
CREATE TRIGGER delete_trigger
    AFTER DELETE
    ON public.passenger
    FOR EACH ROW
    EXECUTE PROCEDURE public."testPL"();
```
No necesitamos crear una función de más, simplemente usamos la función anterior para que cuente los registros, y que se ejecute después que se borre un registro. 


## SIMULANDO UNA CONEXIÓN A DB REMOTAS.
Primero creamos la extensión dblink del gestor de extensiones de postgres. `CREATE EXTENSION dblink;`
Luego generamos la consulta desde nuestra base de datos local de transporte:
```
SELECT * FROM passenger
JOIN 
dblink ('dbname=remote 
	   port=5432 
	   host=127.0.0.1 
	   user=usuario_consulta 
	   password=123', 
	  'SELECT id, "date" FROM vip')
	  AS remote_data (id integer, "date" date)
USING (id)
```

## RETO CONSULTANDO DESDE LA BASE DE DATOS REMOTA A LA BASE DE DATOS LOCAL
```
SELECT * FROM vip
JOIN 
dblink ('dbname=transporte 
	   port=5432 
	   host=127.0.0.1 
	   user=usuario_consulta 
	   password=123', 
	  'SELECT * FROM public.passenger')
	  AS remote_data (id integer, name character varying, address character varying, birthday date)
USING (id)
```


## TRANSACCIONES
### Estructura básica.
```
BEGIN
<consultas>
COMMIT | ROLLBACK
```
* BEGIN: Inicia el motor de DB diciéndole que ejecute la consulta en una sola transacción.
* COMMIT: Le dice a la DB que si todo fue exitoso, guarde los cambios.
* ROLLBACK: Le dice a la DB que si hubo un error, deshaga todos los cambios.

Si hay varias consultas en una declaración, una de ellas falla y después de ellas hay un commit, nada se guardará, puesto que al estar en una sola transacción, postgres lo tomará como una falla total y no guardará ningún cambio.


OTRAS EXTENSIONES REMOTAS. https://www.postgresql.org/docs/12/contrib.html
```
CREATE EXTENSION fuzzystrmatch;

SELECT levenshtein('Oscar', 'Omar'); // 2

SELECT difference('Beard', 'Bird'); // 4
```

## BACKUPS Y RESTAURACIÓN
* pg_dumps: Realiza backup a la base de datos.
* pg_restore: Restaura la DB.

Clic derecho a la base de datos y le damos click a la opción "Backup".

http://127.0.0.1:56898/help/help/backup_dialog.html -> Para más información de las funcionalidades del backup.


## MANTENIMIENTO
Postgres maneja una serie de funciones que trabajan en segundo plano mientras que trabajamos directamente en la base de datos, y esto es a lo que le llamamos mantenimiento.

El nombre más común de esto es Vaccum, ya que esto quita todas las filas y columnas e items del disco duro que no están funcionando, ya que postgres al percatarse de esto, las marca como "para borrar después".

Tiene 2 niveles de limpieza.
* Liviano, se ejecuta todo el tiempo en la DB en segundo plano.
* Full o completo, que es capaz de bloquear las tablas para hacer la limpieza y luego la desbloquea.

Full es importante porque puede que una tabla tenga problemas de indexación y se demore mucho en hacer las consultas.

Hacer mantenimiento en DB no es lo mismo que hacerlo directamente en las tablas.

Para ejecutar el mantenimiento se da clic derecho sobre la DB o la tabla, y luego a la opción "Maintenance".

En tablas, aparecen 3 opciones 
* full: Revisa toda la información de la tabla, si hay información que no es aplicable limpiará/eliminará la fila con la información del índice y demás. Activar o desactivar full puede tumbar totalmente la DB.
* freeze: durante el proceso se va a congelar. Ningún usuario va a tener acceso a esta tabla hasta que no termine el proceso de limpieza.
* analyze: El más suave, el programa ejecutará una revisión y mostrará qué tan bien o mal está la tabla.

Es importante siempre hacer el mantenimiento en el horario en donde menos es utilizada la DB, ¿por qué? porque si hay menos tráfico los usuarios no van a sentir tanto la ausencia del servicio. Igualmente, en la medida de las posibilidades se puede usar una DB de respaldo para que el servicio no se vea ofuscado durante el mantenimiento, luego, una vez hecho el mantenimiento se puede actualizar la DB con los datos generados en la DB de respaldo.


## REPLICAS.

Son mecánismos que permiten evitar problemas de entrada y salida en los SO.

"Existen 2 tipos de personas, los que ya usan réplicas y los que las van a usar..." - Piensa siempre en modo réplica.

A medida que la DB crece encontraremos limitaciones físicas y de electrónica, si la DB aumenta tanto su tamaño, las limitaciones serán de procesamiento, RAM, almacenamiento.

Hemos visto que las consultas en local son muy rápidas, sin embargo, cuando la aplicación ha sido desplegada pueden ocurrir multiples peticiones de lectura y escritura. Todos los motores de DB pueden hacer una ejecución a la vez, por lo que recibir tantas peticiones de consulta al mismo tiempo puede hacer que regresar una consulta se demore demasiado y eso puede ser catastrófico, pero las réplicas son la solución a este tipo de problemas.

¿Cuál es la estrategia? Tener una base de datos principal donde se realizan todas las modificaciones, y una base de datos secundaria dónde se realiza las lecturas. Separar las tareas es altamente beneficioso en cuanto al rendimiento de la aplicación, así, cuando se modifica una DB automáticamente se lleva el cambio a la DB de lectura. Todo lo que hay que hacer es configurar 2 servidores de postgres, uno como maestro y otro como esclavo. Se debe modificar la aplicación para que todas las modificaciones se hagan sobre el maestro y la lectura sobre la replica, o la DB en caliente. Es imposible realizar cambios en la DB de réplica.

IOPS = In Operation Per Second.

## IMPLEMENTACIÓN DE RÉPLICAS EN POSTGRES.

https://app.cloudjiffy.co/ -> Para crear servidores de DB en postgres.

## CONFIGURADOS Y CONECTADOS LAS DB.

Vamos a Master y editamos `postgresql.conf`, 
```
buscamos wal_level = hot_standby
max_wal_senders = 2 // o 3 depende de cómo vamos a crecer.
archive_mode = on
archive_command = 'cp %p /tmp/%f'
```
Luego en el archivo `pg_hba.conf` agregamos lo siguiente: `host    replication     all     <dir ip>/32    trust =>32` para que identifique que no es un rango de ip sino una ip común.

Abrimos la Replica y abrimos `postgresql.conf`, primero abrimos la consola y ejecutamos sudo service postgresql stop. No podemos copiar los archivos si la DB está en ejecución.

Borramos los datos guardados en la réplica con `rm -rf /var/lib/pgsql/data/*` -> Es una ruta estandar en linux.

Consola: 
```
pg_basebackup -U webadmin -R -D /var/lib/pgsql/data/ --host=<ip servidor master> port=5432
postgresql.conf:
    hot_standby = on
En la terminal: sudo postgresql start
```