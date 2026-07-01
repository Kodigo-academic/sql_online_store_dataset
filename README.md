
# Guía de Consultas SQL - Tienda en Línea (`online_store`)


### Nivel básico

**1. Listado simple con filtro**
Muestra el `product_id`, `name` y `price` de todos los productos cuyo precio
sea mayor a $500, ordenados de mayor a menor precio.

**2. Filtro por texto y rango de fechas**
Obtén `customer_id`, `first_name`, `last_name` y `registration_date` de los
clientes registrados entre el `2023-01-01` y el `2024-12-31` que vivan en
`'San Salvador'`.

### Nivel intermedio (JOINs)

**3. Catálogo con categoría**
Muestra el nombre del producto, su precio y el nombre de su categoría,
para los primeros 20 productos con mayor stock (`stock_quantity`).

**4. Órdenes con datos del cliente**
Lista las 15 órdenes más recientes mostrando `order_id`, `order_date`,
`status`, `total_amount` y el nombre completo del cliente que la realizó.

**5. Detalle completo de una orden**
Para la orden con `order_id = 1`, muestra cada producto comprado
(`name`), la cantidad, el precio unitario y el subtotal de cada línea.

### Nivel intermedio-alto (agregaciones)

**6. Ingresos por categoría**
Calcula el ingreso total (`SUM(subtotal)`) generado por cada categoría de
producto, ordenado de mayor a menor ingreso. Incluye solo categorías con
ventas registradas.

**7. Clientes más valiosos (Top N)**
Obtén los 10 clientes que más han gastado en total (`SUM(total_amount)` de
sus órdenes), mostrando nombre completo, número de órdenes realizadas y
monto total gastado.

**8. Calificación promedio por producto**
Lista los 10 productos con mejor calificación promedio (`AVG(rating)`) que
tengan al menos 3 reseñas, mostrando el nombre del producto, el promedio
(redondeado a 2 decimales) y el total de reseñas.

### Nivel avanzado (subconsultas y condiciones complejas)

**9. Productos nunca vendidos**
Encuentra todos los productos que **no** aparecen en ningún `order_items`
(productos sin ventas), mostrando su `product_id`, `name` y `category_id`.
Usa una subconsulta o `LEFT JOIN ... IS NULL`.

**10. Clientes sin pagos completados**
Lista los clientes que tienen al menos una orden, pero **ninguno** de sus
pagos tiene estado `'Completado'`. Muestra `customer_id`, nombre completo
y la cantidad de órdenes que tienen.

### Nivel experto (window functions / CTE)

**11. Ranking de productos por categoría**
Usando una función de ventana (`RANK()` o `ROW_NUMBER()`), obtén el
producto más vendido (por cantidad total, `SUM(quantity)`) **dentro de
cada categoría**. El resultado debe mostrar una sola fila por categoría:
nombre de la categoría, nombre del producto y unidades vendidas.

**12. Comparativa mensual de ventas (CTE + funciones de fecha)**
Usando un CTE (`WITH ...`), calcula el total de ventas (`SUM(total_amount)`
de `orders`) agrupado por año y mes (`YEAR(order_date)`, `MONTH(order_date)`).
Luego, en la consulta principal, calcula la diferencia respecto al mes
anterior usando `LAG()`. Ordena el resultado cronológicamente.

