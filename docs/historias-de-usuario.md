# Historias de usuario

_Presentar al menos una historia de usuario representativa por módulo._
_Cada historia debe incluir formato clásico, criterios de aceptación y validación INVEST._

---
---
## HU-01 — Registro, Autenticación y Gestión de Perfil de Cliente

| Campo                   | Detalle                                                                                                                                                 |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Historia                | Como cliente, quiero registrarme ingresando mis datos obligatorios, iniciar sesión y acceder a mi perfil,  para administrar mi información personal, consultar el historial y estado de mis pedidos y realizar compras en la plataforma. |
| Módulo                  | 02- Clientes y Cuentas                                                                                                                                     |
| Requisitos relacionados | RF-08, RF-09, RF-10, RF-11, RF-12, RF-13, RF-14, RF-15, RF-16, RF-17                                                                                                                                     |

### Criterios de aceptación

1. El sistema exige todos los campos obligatorios para el alta de usuario, validando el formato del email y DNI e impidiendo el registro si el correo ya existe.
2. El cliente puede autenticarse con sus credenciales o recuperar la clave mediante un enlace enviado a su correo electrónico en caso de olvido. 
3. Desde la sección "Mi Cuenta", el cliente autenticado puede consultar y modificar sus datos de contacto (con el DNI bloqueado para edición) y revisar el historial de pedidos.


### Validación INVEST

| Criterio      | ¿Se cumple? | Observación                                                                                   |
| ------------- | ----------- | --------------------------------------------------------------------------------------------- |
| Independiente | Sí          | Se implementa y prueba de forma autónoma sin depender de los módulos de pago o envíos.                           |
| Negociable    | Sí          | Los datos requeridos en el registro pueden ajustarse.            |
| Valiosa       | Sí          | Permite personalizar la experiencia y asociar los pedidos a un usuario registrado.                       |
| Estimable     | Sí          | Representa un flujo de autenticación estándar.                             |
| Pequeña       | Sí          | Se limita al flujo de alta, acceso y edición de perfil de un cliente.                               |
| Verificable   | Sí          | Se verifica creando cuentas, iniciando sesión y editando campos. |

## HU-02 — Consulta, Búsqueda y Filtrado de Productos por Variante

| Campo | Detalle |
|-------|---------|
| Historia | Como cliente, quiero buscar prendas por palabra clave y aplicar filtros por categoría, talle, color y precio, para encontrar rápidamente las prendas que me interesan y agilizar mi proceso de compra. |
| Módulo |03 - Catálogo y Productos |
| Requisitos relacionados | RF-24, RF-25, RF-26, RF-27, RF-28, RF-32, RF-33, RF-34, RF-35 |

### Criterios de aceptación

1. El catálogo se encuentra disponible públicamente y exhibe para cada prenda entre 2 y 4 fotos, descripción, tabla de medidas y la matriz de variantes.
2. El sistema permite filtrar prendas por categoría, precio, talle, color y disponibilidad, así como ordenarlas por precio (asc/desc), novedad o popularidad.
3. Si una variante alcanza stock cero, la interfaz muestra el indicador "Sin stock" e inhabilita su agregado al carrito de compras.

### Validación INVEST

| Criterio | ¿Se cumple? | Observación |
|----------|-------------|-------------|
| Independiente |Sí  |Consulta directamente las lecturas del catálogo de la base de datos sin depender del carrito. |
| Negociable |Sí  |La distribución visual de los filtros y el diseño de la tabla de medidas pueden ajustarse. |
| Valiosa | Sí |Mejora la usabilidad y reduce el tiempo que el usuario busca un artículo. |
| Estimable | Sí |Basada en consultas estructuradas de lectura y maquetación de fichas de producto. |
| Pequeña | Sí |Se concentra exclusivamente en la búsqueda, filtrado y renderizado del catálogo. |
| Verificable | Sí |Se prueba aplicando filtros cruzados y verificando la ficha de prendas con y sin stock. |



## HU-03 — Gestión del carrito de compras

| Campo | Detalle |
|-------|---------|
| Historia | Como cliente, quiero gestionar mi carrito (agregar productos, modificar cantidades, eliminar o vaciar), para organizar mi compra antes del checkout. |
| Módulo |03 - Carrito, Pedidos y Promociones |
| Requisitos relacionados | RF-20, RNF-01, RNF-09, RNF-10, RNF-11, RNF-12 |

### Criterios de aceptación

1. Al agregar producto, el sistema exige seleccionar talle y color.
2. El carrito muestra productos, cantidades y subtotales.
3. El cliente puede modificar cantidades.
4. El cliente puede eliminar productos.
5. El cliente puede vaciar el carrito.


### Validación INVEST

| Criterio | ¿Se cumple? | Observación |
|----------|-------------|-------------|
| Independiente |Sí |No depende de otras HU |
| Negociable |Sí |El diseño del carrito puede discutirse con el negocio. |
| Valiosa |Sí |Permite al cliente organizar los productos que desea comprar antes del checkout. |
| Estimable |Sí |El alcance está delimitado a las operaciones del carrito. |
| Pequeña |Sí |Tiene un objetivo concreto y funcionalidades relacionadas. |
| Verificable |Sí |Se puede comprobar viendo que los productos se agreguen, visualicen, modifiquen, eliminen y que el carrito pueda vaciarse. |




## HU-04 — Checkout con datos de entrega y envío

| Campo | Detalle |
|-------|---------|
| Historia | Como cliente, quiero realizar el checkout confirmando mis datos de entrega, seleccionando el tipo de envío con el costo correspondiente, para completar mi compra correctamente. |
| Módulo |03 - Carrito, Pedidos y Promociones |
| Requisitos relacionados | RF-21, RNF-01, RNF-02, RNF-09, RNF-10, RNF-11, RNF-12 |

### Criterios de aceptación

1. El cliente puede confirmar o editar sus datos de entrega. 
2. El cliente puede elegir entre envío a domicilio o retiro en local.
3. Si elige envío a domicilio, el sistema calcula el costo correspondiente.
4. Si elige retiro en local, el sistema no cobra costo de envío.
5. El sistema no permite continuar si faltan datos obligatorios de entrega y muestra un mensaje indicando qué dato debe completarse.


### Validación INVEST

| Criterio | ¿Se cumple? | Observación |
|----------|-------------|-------------|
| Independiente |Sí |No depende de otras HU |
| Negociable |Sí |La forma de presentar los datos y las opciones de entrega puede acordarse con el negocio. |
| Valiosa |Sí |Permite al cliente definir cómo recibirá su pedido y completar correctamente sus datos de entrega. |
| Estimable |Sí |Solo se limita a los datos de entrega y las opciones de envío. |
| Pequeña |Sí |Tiene un objetivo concreto y solo implica la pantalla de checkout. |
| Verificable |Sí |Se puede comprobar el funcionamiento con las opciones de selección  de envío a domicilio y retiro en local, incluyendo la validación de datos obligatorios. |


## HU-05 — Pago con Mercado Pago

| Campo | Detalle |
|-------|---------|
| Historia | Como cliente, quiero pagar con tarjeta de crédito o débito a través de Mercado Pago, para completar mi compra de forma segura. |
| Módulo |03 - Carrito, Pedidos y Promociones |
| Requisitos relacionados | RF-22, RNF-02, RNF-05 |

### Criterios de aceptación

1. El sistema se integra con Mercado Pago.
2. El cliente puede pagar con tarjeta de crédito y débito.
3. El sistema registra el estado, fecha, importe y medio de pago.
4. Si el pago es aprobado, el pedido pasa al estado "pagado".
5. Si el pago es rechazado, el sistema informa al cliente.


### Validación INVEST

| Criterio | ¿Se cumple? | Observación |
|----------|-------------|-------------|
| Independiente |Sí |Forma parte del proceso de checkout pero puede desarrollarse y probarse mediante pagos de prueba. |
| Negociable |Sí |Los detalles de la integración y los medios de pago pueden discutirse. |
| Valiosa |Sí |Permite al cliente completar y abonar una compra online. |
| Estimable |Sí |La funcionalidad y su alcance están definidas. |
| Pequeña |Sí |Se concentra específicamente en el procesamiento del pago. |
| Verificable |Sí |Se puede verificar realizando pagos de prueba y se comprueba su resultado y registro. |


## HU-06 — Integración con proveedor logístico


| Campo | Detalle |
|-------|---------|
| Historia | Como cliente, quiero conocer el costo de envío y obtener un número de seguimiento del proveedor logístico para conocer el estado de mi pedido.  |
| Módulo |04 - Envíos y Devoluciones |
| Requisitos relacionados | RF-27, RNF-01, RNF-05, RNF-12 |

### Criterios de aceptación

1. El sistema se integra con el proveedor logístico.
2. El cliente puede calcular el costo de envío antes de comprar.
3. El sistema obtiene el número de seguimiento del proveedor.
4. El cliente puede consultar el número de seguimiento desde "Mi Cuenta".
5. El sistema registra el número de seguimiento asociado al pedido. 


### Validación INVEST

| Criterio | ¿Se cumple? | Observación |
|----------|-------------|-------------|
| Independiente |Sí |Puede desarrollarse y probarse con pedidos y datos de prueba. |
| Negociable |Sí |El proveedor logístico puede discutirse. |
| Valiosa |Sí |Permite al cliente conocer el costo de envío y realizar el seguimiento del pedido. |
| Estimable |Sí |El alcance es definido. |
| Pequeña |Sí |Se concentra en el cálculo del envío y seguimiento. |
| Verificable |Sí |Se puede comprobar el cálculo del costo y la obtención del número de seguimiento despachando un pedido y verificando su seguimiento. |



## HU-07 — Confirmación de retiro en local

| Campo | Detalle |
|-------|---------|
| Historia | Como empleado, quiero confirmar el retiro de un pedido en el local y establecer un plazo de 15 días para retirar, para gestionar correctamente los pedidos pendientes de retiro y liberar stock no retirado. |
| Módulo | 04 - Envíos y Devoluciones |
| Requisitos relacionados | RF-28, RNF-01, RNF-12 |

### Criterios de aceptación

1. El empleado puede marcar un pedido como "retirado".
2. El sistema registra fecha y hora de retiro.
3. Se establece plazo de 15 días para retirar.
4. El sistema permite consultar la fecha límite de retiro.
5. Si no se retira en plazo, el pedido se cancela y repone stock.
6. El sistema muestra una confirmación cuando el retiro es registrado.

### Validación INVEST

| Criterio | ¿Se cumple? | Observación |
|----------|-------------|-------------|
| Independiente | Sí | Puede probarse con pedidos configurados para retiro en local. |
| Negociable | Sí | El plazo puede definirse durante el desarrollo. |
| Valiosa | Sí | Permite controlar correctamente los pedidos retirados. |
| Estimable | Sí | Las acciones están delimitadas. |
| Pequeña | Sí | Se concentra en la confirmación y plazo de retiro. |
| Verificable | Sí | Se puede confirmar el retiro y se verifica el plazo limite. |


## HU-08 — Solicitud de devolución por cliente

| Campo | Detalle |
|-------|---------|
| Historia | Como cliente, quiero solicitar una devolución desde "Mi Cuenta", seleccionando pedido y motivo, dentro de los 5 días hábiles posteriores a la entrega/retiro, para resolver problemas con mi compra. |
| Módulo | 04 - Envíos y Devoluciones |
| Requisitos relacionados | RF-30, RNF-01, RNF-05, RNF-08, RNF-10 |

### Criterios de aceptación

1. El cliente puede acceder a "Mi Cuenta" y seleccionar un pedido para solicitar una devolución.
2. El cliente puede seleccionar el motivo: talle incorrecto, producto defectuoso o producto equivocado.
3. El sistema permite solicitar la devolución únicamente dentro de los 5 días hábiles posteriores a la entrega o retiro.
4. El sistema registra la solicitud de devolución.
5. El sistema muestra una confirmación cuando la solicitud es registrada.

### Validación INVEST

| Criterio | ¿Se cumple? | Observación |
|----------|-------------|-------------|
| Independiente | Sí | Puede probarse con pedidos de prueba y diferentes fechas. |
| Negociable | Sí | Los motivos, plazos y detalles del formulario pueden ajustarse. |
| Valiosa | Sí | Da garantía al cliente y le permite gestionar una devolución. |
| Estimable | Sí | El alcance esta claro y definido. |
| Pequeña | Sí | Se limita a la solicitud de devolución. |
| Verificable | Sí | Se puede comprobar una solicitud válida y otra fuera de plazo. |



## HU-09 — Reportes de ventas exportables

| Campo | Detalle |
|-------|---------|
| Historia | Como dueño, quiero consultar reportes de ventas por día, semana, mes, año y períodos de hasta 5 años anteriores, filtrando por rango de fechas y productos y pudiendo exportarlos a Excel, para analizar el desempeño del negocio. |
| Módulo | 05 - Reportes y Dashboard |
| Requisitos relacionados | RF-33, RNF-01, RNF-12, RNF-15 |

### Criterios de aceptación

1. El dueño puede acceder a los reportes de ventas.
2. Puede consultar las ventas por día, semana, mes y año.
3. Puede filtrar los resultados por rango de fechas y productos.
4. Puede consultar información de hasta 5 años anteriores.
5. Puede exportar los resultados a un archivo Excel.
6. Los resultados de la consulta se muestran en un tiempo máximo de 3 segundos.

### Validación INVEST

| Criterio | ¿Se cumple? | Observación |
|----------|-------------|-------------|
| Independiente | Sí | Puede desarrollarse y probarse utilizando datos de ventas de prueba. |
| Negociable | Sí | La presentación de los filtros y el formato del archivo pueden definirse durante el desarrollo. |
| Valiosa | Sí | Permite al dueño analizar las ventas y tomar decisiones. |
| Estimable | Sí | El alcance y las funcionalidades están bien definidas. |
| Pequeña | Sí | Se concentra en la consulta y exportación de reportes de ventas. |
| Verificable | Sí | Se pueden realizar consultas con distintos filtros y comprobar la exportación a Excel y el tiempo de respuesta. |


## HU-10 — Listados de productos y clientes

| Campo | Detalle |
|-------|---------|
| Historia | Como dueño, quiero obtener listados de productos más vendidos, con menor movimiento, ingresos totales, ventas por medio de pago, clientes nuevos (últimos 7 días) y recurrentes (más de 2 compras), para analizar el desempeño del negocio. |
| Módulo | 05 - Reportes y Dashboard |
| Requisitos relacionados | RF-34, RNF-12, RNF-15 |

### Criterios de aceptación

1. El dueño puede acceder a la información solicitada.
2. El sistema muestra los productos más vendidos.
3. El sistema muestra los productos con menor movimiento.
4. El sistema muestra los ingresos totales.
5. El sistema muestra las ventas según el medio de pago.
6. El sistema muestra los clientes nuevos de los últimos 7 días.
7. El sistema muestra los clientes recurrentes con más de 2 compras.

### Validación INVEST

| Criterio | ¿Se cumple? | Observación |
|----------|-------------|-------------|
| Independiente | Sí | Puede desarrollarse y probarse con datos de prueba, sin depender de otra HU terminada. |
| Negociable | Sí | La forma de presentar la información puede definirse durante el desarrollo. |
| Valiosa | Sí | Permite al dueño analizar las ventas, productos y clientes, otorgando una visión actual del negocio. |
| Estimable | Sí | El alcance y la información a mostrar están definidas. |
| Pequeña | Sí | Se limita a la consulta de indicadores y listados definidos en RF-34. |
| Verificable | Sí | Se puede comprobar que cada listado e indicador muestre la información correspondiente. |

