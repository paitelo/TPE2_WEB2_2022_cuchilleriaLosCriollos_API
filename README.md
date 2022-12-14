# Documentacion API - Los Criollos || Cuchillería Artesanal

###  DESCRIPCION
Esta es una API RESTful vinculada a la base de datos de nuestra cuchillería tandilense, detallando todos los productos que tenemos disponibles. Esta herramienta es útil para acceder a nuestro catálogo actualizado en todo momento.    

### BASE DE DATOS
Importar la base de datos desde el archivo cuchilleria_los_criollos.sql ubicado en la carpeta sql del repositorio.

###  URI
Accesible mediante la dirección web http://localhost/WEB2/TPE2-REST/api/

- Debe especificarse de manera obligatoria un recurso en formato:
http://localhost/WEB2/TPE2-REST/api/recurso  
_(ver detalle de recursos en el punto siguiente)_. 

- Opcionalmente se puede especificar a continuación el id de un recurso en particular con el siguiente formato:
http://localhost/WEB2/TPE2-REST/api/recurso/id  
_(ver detalle de recursos en el punto siguiente)_. 

###  RECURSOS
Actualmente están disponibles para consulta mediante nuestra API los siguientes recursos:

:point_right: products

:point_right: categories

```
Nota: Si se agrega un id numérico, la consulta devuelve el detalle del recurso especificado que coincide con el id especificado.
```

###  PARAMETROS
Los parámetros disponibles y opcionales para acceder a consultas de la API son los siguientes: 

- **orderBy** indica que los resultados serán visualizados de forma ordenada por el campo que sea especificado por el usuario. Se debe ingresar en formato minúsculas y coincidir exactamente con el nombre de una columna de la tabla del ***recurso*** en la base de datos. De lo contrario la consulta arroja un error. Por defecto, los resultados se muestran ordenados alfabéticamente por la denominación del ***recurso***. Se utiliza combinado con el valor del parámetro **orderMode**.
- **orderMode** especifica si los resultados se muestran en orden ascendente o descendente. Puede tomar solamente los valores *ASC* y *DESC*. Por defecto, los resultados se muestran ordenados ascendentemente. 
- **page** Este parámetro se utiliza en combinación con el parámetro **elements**. En caso de indicarse en la consulta, debe tomar el valor de un número entero mayor 0 (cero). Por defecto la consulta devuelve la primera página. 
- **elements** En caso de indicarse en la consulta, debe tomar el valor de un número entero mayor a 0 (cero). Por defecto la consulta devuelve los resultados paginados de a 5 elementos por página.
- **filterBy** indica el nombre de una columna de la tabla del ***recurso*** en la base de datos por la cual se filtrarán los resultados. Se debe ingresar en formato minúsculas y coincidir exactamente con el nombre de una columna de la tabla del ***recurso*** en la base de datos. De lo contrario la consulta arroja un error. No tiene valor por defecto. En caso de que no se indique, los resultados de la consulta no son filtrados, recupera todos los registros que cumplan con los criterios de consulta. Se utiliza combinado con el valor del parámetro **equalTo**.
- **equalTo** contiene el valor por el cual serán filtrados los resultados de la consulta. Si no hay ningún registro que coincida con este valor, el resultado de la consulta es un objeto vacío (no devuelve error). 

###  CONSUMO DE LA API
Están disponibles para su utilización en esta API los métodos GET, POST, PUT y DELETE permitiendo realizar la totalidad de las operaciones de ABM en la base de datos. 

##### Metodo GET

Al consultar los recursos con el método GET, obtendrá la siguiente información detallada de cada uno de ellos, 

Ejemplo de una consulta GET sobre el recurso ***categories*** con id = 1
```
{
    "id": 1,
    "categoria": "Cuchillos",
    "segmento": "Bronce"
}
```

Ejemplo de una consulta GET sobre el recurso ***products*** con id = 27

```
{
    "id": 27,
    "nombre": "Bombilla",
    "descripcion": "Bombilla de alpaca grabada a mano",
    "imagen": "uploaded_files/634c7e9f6b1faWhatsApp Image 2022-10-16 at 18.44.08.jpeg",
    "precio": 350,
    "id_categoria": 4,
    "categoria": "Materos"
}
```
```
Nota: En el caso de no especificar un id, se obtendrá la colección de recursos, según los parámetros opcionales especificados 
_(ver detalle de parámetros en punto anterior)_
```
##### Metodo POST

Para realizar una inserción de elemento con el método POST, se debe especificar la siguiente información en formato JSON, según el recurso correspondiente:

Ejemplo de método POST sobre el recurso ***categories***.

```
{
    "categoria": "Cuchillos",
    "segmento": "Bronce"
}
```

Ejemplo de método POST sobre el recurso ***products***.

```
{
    "nombre": "Bombilla",
    "descripcion": "Bombilla de alpaca grabada a mano",
    "imagen": "uploaded_files/634c7e9f6b1faWhatsApp Image 2022-10-16 at 18.44.08.jpeg",
    "precio": 350,
    "id_categoria": 4,
}
```
##### Metodo PUT

Para realizar una modificación sobre un recurso, debe conocer su ***id***, de lo contrario no podrá actualizar la información. 


Para realizar una modificación de elemento con el método PUT, se debe especificar la siguiente información en formato JSON, según el recurso correspondiente:

Ejemplo de método PUT sobre el recurso ***categories***.

```
{
    "id": 1,
    "categoria": "Cuchillos",
    "segmento": "Bronce"
}
```

Ejemplo de método PUT sobre el recurso ***products***.

```
{
    "id": 27,
    "nombre": "Bombilla",
    "descripcion": "Bombilla de alpaca grabada a mano",
    "imagen": "uploaded_files/634c7e9f6b1faWhatsApp Image 2022-10-16 at 18.44.08.jpeg",
    "precio": 350,
    "id_categoria": 4,
}
```
###  RESULTADOS / ERRORES

Al finalizar una transacción con la API exitosamente, la misma devuelve el registro creado/modificado/eliminado o una colección de registros según corresponda.

Ejemplo de error en la consulta:

- Código de respuesta 404: "El producto con el id 29 no existe"  



