## **4.4.3 The Function wildcard**
  
La expansión del comodín ocurre automáticamente en las reglas. Pero la expansión de comodines normalmente no tiene lugar cuando se establece una variable, o dentro de los argumentos de una función. Si quieres hacer una expansión de comodines en tales lugares, necesitas usar la función de comodín, como esta;

`$(wildcard pattern…)`  

Esta cadena, utilizada en cualquier parte de un archivo MAKE, se reemplaza por una lista de nombres de archivos existentes separados por espacios que coinciden con uno de los patrones de nombre de archivo dados. Si ningún nombre de archivo existente coincide con un patrón, ese patrón se omite de la salida de la función de comodín. Tenga en cuenta que esto es diferente de cómo los comodines no coincidentes se comportan en las reglas, donde se usan literalmente en lugar de ignorarse (ver Caída de comodín).

Un uso de la función comodín es obtener una lista de todos los archivos fuente C en un directorio, como este:  

`$(wildcard *.c)`    

Podemos cambiar la lista de archivos fuente C en una lista de archivos objeto reemplazando el sufijo '.c' con '.o' en el resultado, como este:  

`$(patsubst %.c,%.o,$(wildcard *.c))`   

(Aquí hemos utilizado otra función, patsubst. Ver Funciones para la Sustitución de cadenas y Análisis).

Por lo tanto, un archivo MAKE para compilar todos los archivos fuente C en el directorio y luego vincularlos se podría escribir de la siguiente manera:  
`objects := $(patsubst %.c,%.o,$(wildcard *.c))`   
`foo : $(objects)`  
       ` cc -o foo $(objects)`  
