# 🛒  `URBAN GROCERS` 🧺 

### __Pruebas manuales de API__

![URBAN GROCERS](https://previews.123rf.com/images/castecodesign/castecodesign1907/castecodesign190700223/126285821-shopping-cart-template-vector-flat-style-product-icon-sale-concepts.jpg)

## Sobre el proyecto
Este proyecto se realiza para prácticar el análisis de requerimientos, diseño de pruebas, informes de errores y pruebas de API, aplicados a las siguientes funcionalidades de la aplicación Urban Grocers:
|Funcionalidad|Request|Endpoint|
|-----|-----|-----|
|Agregar comestibles al kit |POST |/api/v1/kits/{id}/products|
|Entrega "Order and Go"*|POST|/order-and-go/v1/delivery|

*Se solicita comprobar la disponibilidad y el costo del servicio

Las siguientes especificaciones se obtienen de la documentación back-end del producto, así como la consultada en:
```
Swagger     
Apidoc      
```
### "Agregar comestibles al kit"

Esta funcionalidad permite agregar productos comestibles a un kit, ingresando los parámetros de acuerdo con el ejemplo:

|Campo|Tipo|Descripción
|---|---|---|
|id|number|El id de kit en la tabla kit_model. Se pasa en la URL|
|products|List|	Array	Una lista de productos que se agregarán al kit. La lista contiene los ID de los artículos y sus cantidades. Debe enviarse en el cuerpo de la solicitud.|

Hay que comprobar que la solicitud se realice de forma éxitosa mostrando:
- Código de respuesta: 201
- Se agrega producto

Los parámetros se ingresan en formato json, ejemplo:
```
{
    "productsList": [
        {
            "id": 1,
            "quantity": 2
        },
        {
            "id": 6,
            "quantity": 2
        }
    ]
}
```

### "Entrega "Order and Go""
Esta funcionalidad permite realizar una orden con los siguientes parámetros:
|Campo|Tipo|Descripción|
|--|--|--|
|productsCount|number|Número de productos en el pedido|
|productsWeight|number|Peso de los productos|
|deliveryTime|number|Plazo de entrega previsto|

Para esta funcionalidad hay que comprobar:
- Disponibilidad del servicio (isItPossibleDeliver = true)
- Costo de servicio de entrega (clientDeliveryCost)
   
 
Ejemplo de cuerpo de solicitud: 
```
{
    "deliveryTime": 9,
    "productsCount": 10,
    "productsWeight": 11
}
```
La respuesta esperada:
```
HTTP/1.1 200 OK
   {
       "name": "Order and Go",
       "clientDeliveryCost": 10,
       "toBeDeliveredTime": { "min": 10, "max": 20 },
       "hostDeliveryCost": 23,
       "isItPossibleToDeliver": true
   }
```

- hostDeliveryCost es un costo constante de $7.
#
## Criterios de aceptación
1. Funcionalidad "Agregar comestibles al kit"
    - Lista de comestibles (productsCount) es menor o igual a 30 productos (no lista de cantidades acumuladas, la suma de "quantity")
    - Al superar 30 productos la lista de comestibles, el estado de la solicitud retorna "400"

2. Funcionalidad "Entrega "Order and Go"""
    - El horario de entrega del servicio es de 8:00 - 22:00 h
    
|Artículos del pedido|Peso del pedido|Tiempo de entrega|Costo del servicio de entrega|Formato de datos|
|-----|-----|-----|-----|-----|
|0-8|0-3|20-25 min|3|json|
|9-15|3.1-6|20-25 min|5|json|


Se aplica entonces:
- Si Artículos del pedido:0-8 __y__ Peso del pedido:0-3, entonces el costo de servicio de entrega (clientDeliveryCost) es igual a 3.
- Si Artículos del pedido:9-15 __o__ Peso del pedido:3.1-6, entonces el costo de servicio de entrega (clientDeliveryCost) es igual a 5.

## Pruebas   
Al contar con los requerimientos anteriores se determinaron pruebas utilizando técnicas de clases de equivalencia y valores límite.
El siguiente enlace muestra una lista de comprobación con las prueba realizadas así como el enlace a Jira para aquellos casos donde se encontraron bugs.
##  [Lista de comprobación de pruebas](https://docs.google.com/spreadsheets/d/19pMgWhbeI5hApk1n4uAWmvc518KAW3oJ/edit?usp=sharing&ouid=112711575793272570934&rtpof=true&sd=true)


## Herramientas
|Herramienta|Propósito|
|---|---|
|Postman|Realizar pruebas ingresando solicitudes (REST-API)|
|Excel|Lista de comprobación de pruebas|
|Jira|Documentación y reporte de errores encontrados|

I based on materials from Tripleten Platform given for a project. This is just a functionality, there are several test objects to test.
#
If you have got any doubt about the project fell free to contact me.



