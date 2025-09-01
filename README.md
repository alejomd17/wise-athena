## Contexto

El principal driver de ventas de un producto es el precio propio. Sin embargo, algunas tiendas aplican distintos métodos de exhibiciones semanales, registrados en `store_exhibitions`. 

A continuación, se listan las tablas enviadas y sus campos respectivos. 

1. **store_metadata** – Información de cada tienda: `Store_Id`, `Retailer_Id`, `Area_Id`.  
2. **sales_transactions** – Ventas semanales por SKU y tienda: `Date`, `Store_Id`, `Sku_Id`, `Price`, `Units_Sold`.  
3. **store_exhibitions** – Métodos aplicados para aumentar ventas por SKU y tienda cada semana: `Year`, `Week`, `Store_Id`, `Sku_Id`, `Method_1`, `Method_2`, `Method_3`.  

## Objetivos

El cliente nos solicita determinar si vale la pena aplicar los métodos de exhibiciones. El objetivo n°1 es construir lo que consideres necesario para darle al cliente una respuesta concreta. Importante: ten en cuenta que el principal driver de ventas de un producto es su precio propio.

Por otro lado, desde Data Science queremos complementar la entrega con un forecasting de ventas y las elasticidades propias. Por lo tanto, el objetivo n° 2 es brindar al cliente una estimación de la elasticidad propia de los dos productos más relevantes, junto con una proyección de ventas para los próximos 6 meses. 

## Entregables

1. **Notebook 1 del objetivo n°1** con el código utilizado (intentar ser lo más conciso posible y utilizar MD solo cuando sea necesario).  

2. **Notebook 2 del objetivo n°2** con el código utilizado (intentar ser lo más conciso posible y utilizar MD solo cuando sea necesario). 

3. **Presentación para cliente**: Una ppt con no más de 2 diapositivas que respondan la pregunta del cliente inicial y la solicitud de elasticidad propia.

##### Sugerencia: intenta mantener la solución simple y enfocada a resolver los objetivos. 

---
<sub>Los datos entregados, así como la descripción de la prueba y cualquier otro material que se incluya, son propiedad exclusiva de WiseAthena y se comparten con los candidatos de forma personal e intransferible. Su única finalidad es la realización de las pruebas solicitadas. Cualquier otro uso está prohibido y, una vez finalizado el proceso, deberán eliminarse.</sub>






