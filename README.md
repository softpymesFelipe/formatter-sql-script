# Formatter SQL Script

Paquete de ayuda, para formatear en lenguaje SQL los datos de una tabla en excel, basta solamente con copiar y pegar la información de la tabla en el formato requerido.

> !Importante: El nombre de las columnas de la tabla deben ser los mismos que se tienen en la base de datos, para que el script resultante sea lo más exacto posible. 

> Este paquete, aún se encuentra en desarrollo.

## Estructura de la información

Se debe tener en cuenta lo siguiente:

La clase ```GenerateScript``` requiere 3 parametros y 2 opcionales:

- data (str) = La información o values a formatear
- table (str) = Nombre de la tabla
- fields (str) = Los campos donde se insertarán los values
- _type (int) = Tipo de operación permitida (0 = Insert / 1 = Update) por defecto es 0
- where (str) = Condicional del script -> UPDATE

### Como funciona

Para que se pueda utilizar el paquete correctamente, la información debe tener una estructura  similar a la de una tabla, entre columnas y filas, veamos un ejemplo del formato: 

```text
1   prueba  testing null
2   prueba  testing null   
``` 

Esta estructura de texto se consigue al copiar los datos en un libro del programa excel.

Para el tema de fields (campos / columnas), se debe manejar el mismo orden que tienen los datos para que sea preciso el resultado.

## Ejemplo de uso

Veamos algunos ejemplos prácticos:

si queremos formatear a un script insert debemos enviar la información de la siguiente manera:

> Los espacios de separación son tabulaciones \t

```py
# importación del paquete
from formatter_sql_script import GenerateScript

# asignamos la data copiada de nuestra tabla en una variable entre """ (3) comillas dobles para conservar el formato  
data = """1   prueba  testing 1
2   prueba2  testing2 0"""   

# Copiar y pegar los titulos de las columnas de la tabla de excel de la misma forma que se hizo con los datos
fields = """id    nombre  descripcion estado"""

# Asigno el nombre de mi tabla en la base de datos
table = 'ejemplo'

# Tipo de procesamiento (0=Insert / 1=Update)
_type = 0

# Instanciamos la clase y hacemos uso del método generate_script
resp = (GenerateScript(table=table, 
                      fields=fields,
                      data=data, 
                      _type=_type)
        .generate_script())

# Imprimimos en consola el resultado
print(resp)
```
para el ejemplo anterior, el resultado sería el siguiente:

```sql
insert into ejemplo 
(id, nombre, descripcion, estado)
values
(1, 'prueba', 'testing', 1),
(2, 'prueba2', 'testing2', 0):
```

Ahora si realizamos una prueba para un update

```py
# asignamos la data copiada de nuestra tabla en una variable entre """ (3) comillas dobles para conservar el formato  
data = """Testing  Una prueba de update 0"""   

# Copiar y pegar los titulos de las columnas de la tabla de excel de la misma forma que se hizo con los datos
fields = """nombre  descripcion estado"""

# Asigno el nombre de mi tabla en la base de datos
table = 'ejemplo'

# Tipo de procesamiento (0=Insert / 1=Update)
_type = 1

# Instanciamos la clase y hacemos uso del método generate_script
resp = (GenerateScript(table=table, 
                       fields=fields, 
                       data=data, 
                       _type=_type, 
                       where='id = 1')
        .generate_script())

# Imprimimos en consola el resultado
print(resp)
```

para el ejemplo anterior, el resultado sería el siguiente:

```sql
UPDATE ejemplo 
SET nombre = 'Testing', 
descripcion = 'Una prueba de update', 
estado = 0
WHERE id = 1;
```

## Desarrollado por

* 👨‍💻 Felipe Medel
* 📧 luispipemedel@gmail.com