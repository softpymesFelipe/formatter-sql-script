# Formatter SQL Script

Paquete de ayuda, para formatear el texto resultado de una consulta a formato sql.

> Este paquete, aún se encuentra en desarrollo.

## Estructura de la información

Se debe tener en cuenta lo siguiente:

- data (str) = La información o values a formatear
- table (str) = Nombre de la tabla
- fields (str) = Los campos donde se insertarán los values

Para que se pueda utilizar el paquete correctamente, la información debe tener una estructura  similar a la de una tabla,
entre columnas y filas, ejemplo:
```
1   prueba  testing null
2   prueba  testing null   
``` 
Esta estructura de texto se consigue al copiar los datos de una tabla de un programa como excel.

Para el tema de fields, se debe manejar el mismo orden de los datos para que sea preciso el resultado.

## Como funciona

Veamos un ejemplo práctico:

si queremos formatear a un script insert debemos enviar la información de la siguiente manera:

> Los espacios de separación son tabulaciones \t

```
data="""1   prueba  testing 1
2   prueba  testing 0"""   

fields="""id    nombre  descripcion estado"""

table='ejemplo'

from formatter-sql-script import generar_script

print(generar_script(data=data, table=table, fields=fields))
```

