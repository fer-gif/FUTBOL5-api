# API Proyecto Futbol5

Para darle funcionalidad a este proyecto y utilizar de manera correcta la API-REST, se debe escribir, siguiendo las instrucciones, las urls que se requieran para evitar posibles errores o inconvenientes.

> ## INDICE
> 
> - [IMPORTANTE!](#importante!)
> - [TOKEN](#token)
> - [EQUIPOS](#equipos)
> - [JUGADORES](#jugadores)
> - [PARTIDOS](#partidos)
> - [QUERY PARAMS](#query-params)

##  IMPORTANTE!
las urls en Postman se escriben *'http://localhost/FUTBOL5-api/api/... '   *pero en este informe cambiamos esta direccion por *'api/...'*.



### TOKEN:
Para poder acceder a las acciones de modificacion, agregar o eliminar cualquier registro de las tablas, el usuario debe tener un acceso al token que sera generado a traves de la api.
Para generar dicho token, el usuario debe loguearse con su usuario y contraseña correspondiente. Y luego de comprobar de que los datos sean correctos la api retornara el token de acceso que deberia ser usado en cada peticion con el metodo POST, PUT O DELETE. 


>- Para login de usuario el endpoint disponible "api/login" con metodo POST en el body del login aparecera:<br>

```JSON
    {
        "usuario":"Admin",
        "password":"admin1234"
    }
```

>- Si se corrobora correctamente el usuario, la respuesta sera un token que tendra que ser guardado por el usuario del lado del front-end para poder realizar futuras peticiones. El tiempo de validez del dura 60 minutos. 
    Asi se vera el la respueseta generada:<br>
    
```JSON
{
"token" : "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOjEsImlhdCI6MTY4ODQ5MjIxNiwiZXhwIjoxNjg4NDk1ODE2LCJkYXRhIjp7InVzdWFyaW8iOiJBZG1pbiIsInBlcm1pc29zIjo1LCJlcXVpcG8iOm51bGx9fQ==.5bYBKH8n0N5yaiNNNQhiLn292doZs21Y14bWUT7s90U="
}
```

Al momento de realizar una petición a la API con un método POST, PUT o DELETE, se debe incluir en el header del mensaje el atributo ‘Authorization’ : ‘Bearer ‘ + token
Por ejemplo, si se quiere realizar un fetch desde javascript para agregar un nuevo equipo debería hacerse lo siguiente
```javascript
fetch(‘url/api/equipos’, {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                    'Authorization': 'Bearer ' + token
                },
                mode: 'cors',
                credentials: 'same-origin',
                body: JSON.stringify(datos)
            });
```


### EQUIPOS:
>* Nota: El Body En  Postman se deberia de escribir de la siguiente manera:
Usar unicamente cuando se requiera MODIFICAR (PUT) o AGREGAR(POST) un equipo.<br>
```JSON
            { 
                "Nombre":"String",
                "Ciudad":"String",
                "Socios":"Number" 
            }
```

#### *¿Como escribir las urls?*

- #### api/equipos:

A traves del verbo **GET** traemos todos los equipos que se encuentran en la base de datos.

- #### api/equipos/:PARAMETRO (ID o NOMBRE):
Con el verbo **GET** y escribiendo en "**PARAMETRO**" el ID o el nombre del equipo, captamos los datos de ese equipo en particular.

- #### api/equipos/:NOMBRE/jugadores:
Utilizando nuevamente el verbo **GET** y ademas colocando en "**NOMBRE**" EL nombre del equipo, accedemos a los jugadores que tiene ese equipo.

- #### api/equipos/:NOMBRE/partidos:
Escribiendo el nombre del equipo que se requiere en "**NOMBRE**" nos traera los partidos que jugaron ese equipo, utilizando el verbo **GET**.
 
- #### api/equipos:
Ya aca utilizando el verbo **POST**, a traves del body escribir los campos requeridos, sin utilizar parametros en la URL debe agregar un nuevo equipo a la base de datos.

- #### api/equipos/:ID :
Con el verbo **PUT** y pasandole el **ID** del equipo, capturamos el equipo que queremos editar y a traves del body, insertamos en los datos a modificar del equipo.

- #### api/equipos/:ID :
En este caso utilizando el verbo **DELETE** y pasandole nuevamente el **ID** del equipo, borramos ese equipo de la base de datos.


### JUGADORES:
> NOTA: el body en el Postman para jugadores se escribe de la siguiente manera.Usar unicamente cuando se requiera MODIFICAR (PUT) o AGREGAR(POST) un jugador.<br>

```JSON
{
"nombre":"string",
"apellido":"string",
"dni" :"number",
"posicion":"string(POR,DEF,MED,DEL)",
"telefono":"number", 
"edad" :"number", 
"id_equipo":"number" 
}
```

#### *¿Como escribir las urls?*

- #### api/jugadores:
A traves del verbo **GET** traemos todos los jugadores que se encuentran en la base de datos.

- #### api/jugadores/:ID :
Con el verbo **GET** traemos un jugador segun su ID.

- #### api/jugadores
A traves del verbo **POST** y colocando en el body los campos requeridos, se registra un jugador a la base de datos.  Al momento de escribir en el body, en "posicion", los unicos valores que se permiten son : "POR";"DEF";"MED";"DEL".

- #### api/jugadores/:ID :
A traves del verbo **PUT** y pasando por parametro su **ID**, debemos escribir en el body los datos que tenemos que queremos modificar del jugador en particular.

- #### api/jugadores/:ID :
Utilizando el verbo **DELETE** y enviando por parametro el **ID**, elimina un jugador con ese id.


### PARTIDOS: 
> NOTA: el body en el Postman para partidos se escribe de la siguiente manera. Usar unicamente cuando se requiera MODIFICAR (PUT) o AGREGAR(POST) un partido.<br>

```JSON
{
"id_equipo1":"number",
"id_equipo2":"number",
"goles_equipo1" :"number", 
"goles_equipo2":"number",
"fecha":"number"
}
```

#### *¿Como escribir las urls?*

- #### api/partidos:
A traves del verbo **GET** traemos todos los partidos que se encuentran en la base de datos.

- #### api/partidos/:ID :
Con el verbo **GET** traemos un partido en particular segun su ID.

- #### api/partidos
A traves del verbo **POST** y colocando en el body los campos requeridos, se registra un partido a la base de datos. 

- #### api/partidos/:ID :
A traves del verbo **PUT** y pasando por parametro su **ID**, debemos escribir en el body los datos que tenemos que queremos modificar del partido en particular.

- #### api/partidos/:ID :
Utilizando el verbo **DELETE** y enviando por parametro el **ID**, elimina un partido con ese id.


### QUERY PARAMS:
Al momento de acceder a un endpoint para buscar una colección completa tanto del recurso equipos por medio de api/equipos o del recurso jugadores por medio 
de api/jugadores (ambos con el método GET), hay disponible los siguientes queryParams para poder organizar o filtrar los resultados:

##### TABLAS CON CAMPOS DISPONIBLES SEGUN RECURSOS:

 | EQUIPOS   | 
 | -------------  | 
 | "nombre"   | 
 | "ciudad"   | 
 | "socios"    | 
 
  |JUGADORES   | 
 | -------------  | 
 | "nombre"   | 
 | "apellido" | 
 | "dni"      | 
 | "posicion" |
 |"telefono"  |
 |  "edad"    |

- #### orderBy=:campo&order=:criterio
Ordena el resultado de la búsqueda según el valor de **:campo** y de forma que se lo indique el atributo **:criterio**.
Se puede especificar únicamente el parámetro orderBy. En este caso se retornan todos los registros que coincidan con :campo ordenados de forma ASC. <br>
---->**:campo**:debe ser un atributo del recurso. <br>
---->**:criterio**: debe ser el formato de ordenamiento. Están disponibles "ASC" o "DESC".  <br>

+ #### cantidad=:cant&pagina=:paginas
Pagina el resultado obtenido de la consulta de acuerdo a la cantidad de registros indicados en **:cant** y la página que se desea indicado en el valor de **:pagina**.
   ---->**:cant**: indica la cantidad de registros que se desean obtener de la consulta realizada.
   ---->**:pagina**: indica el numero de pagina que se desea obtener a partir del atributo :cant especificado.

>EJEMPLO: **'cantidad=10&pagina=2'**
Retornara la segunda página de los registros agrupados de a 10. Se puede especificar únicamente el parámetro cantidad. En este caso se retornan los primero **:cant** registros de la consulta. cantidad=7 retornara la primera página de los registros agrupados de a 7 elementos.

- #### filter=:filtro&value=:valor
Filtra el resultado de la búsqueda retornando los registros que en su atributo **:filtro** coincida con el valor que se le indica en **:valor**. <br>
  ---->**:filtro** indica el atributo por el cual se desea realizar la búsqueda.<br>
  ---->**:valor** indica el valor por el cual queremos filtrar el recurso. <br>

Siempre que se indique el parámetro filter se debe indicar el parámetro value. En caso contrario se retorna el recurso sin ser filtrado.

>Los queryParams pueden combinarse para obtener resultados más precisos. Así se pueden tener las siguientes combinaciones:<br>
Ordenados por un campo y paginado:<br>
**orderBy=:campo&order=:criterio&cantidad=:cant&pagina=:paginas**<br>
Filtrado por un campo filtro y ordenado por un campo:<br>
**filter=:filtro&value=:valor&orderBy=:campo&order=:criterio**<br>
Filtrado por un campo filtro y paginado:<br>
**filter=:filtro&value=:valor&cantidad=:cant&pagina=:paginas**<br>
Filtrado por un campo filtro, ordenado por un campo y paginado:<br>
**filter=:filtro&value=:valor&orderBy=:campo&order=:criterio&cantidad=:cant&pagina=:paginas**<br>

>NOTA: Los parametro pueden ubicarse de cualquier forma en la url anteponiendose el endpoint y el signo ?. Asi, la siguientes peticiones son correctas:<br>
"api/equipos?filter=ciudad&orderBy=nombre&cantidad=5&value=Necochea"<br>
"api/jugadores?orderBy=edad&order=DESC&cantidad=5&value=null&pagina=2&filter=telefono"<br>




