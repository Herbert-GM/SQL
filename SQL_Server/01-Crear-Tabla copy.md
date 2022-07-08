# TABLA

Una tabla es una estructura de datos que organiza los datos en **columnas y filas**; cada columna es un campo (o atribujo) y cada fila, un registro. La intersección de una columna con una fila, contiene un dato específico, un solo valor.

>columna = campo

>fila = registro

>columna y fila = valor

Cada registro contiene un dato por cada  columna de la tabla.

Cada campo (columna) también debe definir el tipo de columna que almacenará


***

para ver las tablas existentes creadas por los usuarios en una base de datos usamos el procedimiento almacenado

```sql
exec sp_tables @table_owner='dbo';
```

>El parámetro `@table_owner='dbo'`  indica que solo muestre las tablas de usuarios y no las que crea el SQL Server para administración interna.

Finalizamos cada comando con un punto y coma.

---

## SINTAXIS

Al crear una tabla debemos resolver qué campos (columnas) tendrá  y qué tipo de datos almacenarán cada uno de ellos, es decir, su estructura.

La sintaxis básica y general para crear una tabla es la siguiente:

```sql
create table NOMBRETABLA(
  NOMBRECAMPO1 TIPODEDATO,
  ...
  NOMBRECAMPON TIPODEDATO
 );
```
La tabla debe ser definida con un nombre que la identifique y con el cual accederemos a ella.

Creamos una tabla llamada "usuarios" y entre paréntesis definimos los campos y sus tipos:

```sql
create table usuarios(
  nombre varchar(30),
  clave varchar(30)
 );
```
Cada campo con sutipo debe separarse con comas de los siguientes, excepto el último.

Cuando se crea una tabla debemos indicar su nombre y definir al menor un campo con su tipo de dato. En esta tabla "usuarios" definimos 2 campos:

* nombre: que contendrá una cadena de caracteres de 30 caracteres de longitud, que almacenará el nombre de usuario.
* clave: otra cadena de caracteres de 10 de longitud, que guardará la clave de cada usuario.

Cada usuario ocupará un registro de esta tabla, con su respectivo nombre y clave.

Para nombres de tablas, se puede utilizar cualquier caracter permitido para nombres de directorios, el primero debe ser un caracter alfabético y no puede contener espacio. La longitud máxima es de 128 caracteres.

Si intentamos crear una tabla con un nombre ya existente (existe otra tabla con ese nombre), mostrará un mensaje indicando que ya hay un objeto llamado 'usuarios' en la base de datos y la sentencia no se ejecutará.
***
## ESTRUCTURA

Para ver la estructura de una tabla usamos el **PROCEDIMIENTO ALMACENADO** "sp_columns" junto al nombre de la tabla:

```sql
exec sp_columns usuarios;
```
Aparece mucha información qeu no analizaremos en detalle, como el nombre de la tabla, su propietario, los campos, el tipo de dato de cada campo, la longitud, etc.:

|...COLUMN_NAME |TYPE_NAME|LENGHT|
|:-----|:----:|----:|
|nombre |varchar |30 |
|clave |varchar |30 |

***
## ELIMINAR TABLA
Para eliminar una tabla usamos **"drop table"** junto al nombre de la tabla a eliminar:

```sql
drop table NOMBRETABLA;
```

Si intentamos eliminar una tabla que no exste, aparece un mensaje de error indicando tal situación y la sentencia no se ejecuta. Para evitar este mensaje podemos agregar a la instrucción lo siguiente:

```sql
if object_id('NOMBRETABLA') is not null
    drop table NOMBRETABLA;
```
En la sentencia precedente especificamos que: Si la tabla NOMBRETABLA existe (no es null), ejecute el comando de eliminar la tabla NOMBRETABLA