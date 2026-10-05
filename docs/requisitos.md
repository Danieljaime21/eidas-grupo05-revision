# Requisitos del sistema

## Descripción del sistema

El sistema consiste en una plataforma de comercio electrónico para la tienda de indumentaria Mundo Sport, ubicada en Rosario. Actualmente, el negocio realiza sus ventas de manera presencial y mediante redes sociales, pero no cuenta con un canal de venta online propio. Esta modalidad genera problemas de gestión manual de pedidos, falta de control de stock en tiempo real, dificultades en el seguimiento de ventas y devoluciones, y una experiencia de compra limitada para los clientes. 

La solución plantea digitalizar y centralizar estos procesos, permitiendo administrar la información del negocio desde una única plataforma y mantener actualizado el inventario tanto del local físico como de la tienda online de forma sincronizada, ofreciendo a los clientes un catálogo organizado donde podrán seleccionar los artículos que desean comprar, utilizar un carrito de compras, realizar pagos de forma segura y consultar el estado de sus pedidos. 

Por otro lado, el personal de la tienda contará con un panel administrativo desde el cual podrá gestionar productos, stock, pedidos, ventas y devoluciones. El sistema también contará con autenticación y distintos roles de acceso para el personal. De esta manera, se busca mejorar la organización interna del negocio, garantizando una experiencia ágil tanto para el comprador como para el equipo de trabajo. 


## Requisitos funcionales


### Módulo 1 — Usuarios y Clientes

| ID | Requisito |
|----|-----------|
| RF-01 | El sistema deberá permitir al Dueño dar de alta a usuarios del personal asignándoles un rol, modificar sus datos e inhabilitarlos. |
| RF-02 | El sistema deberá permitir al Empleado modificar datos de cuentas de clientes |
| RF-03 | El sistema deberá permitir al Empleado inhabilitar cuentas de clientes. |
| RF-04 | El sistema deberá permitir a los usuarios registrados (clientes y personal) iniciar sesión con email y contraseña y acceder a las funcionalidades correspondientes a su rol. |
| RF-05 | El sistema deberá permitir al Dueño configurar las funcionalidades para cada rol del personal. |
| RF-06 | El sistema deberá permitir a los visitantes registrarse con sus datos (nombre, apellido, email, fecha nacimiento, teléfono, DNI, contraseña, dirección, CP, ciudad, provincia). |
| RF-07 | El sistema deberá permitir al Cliente consultar datos personales, historial de compras y estado de sus pedidos. |
| RF-08 | El sistema deberá permitir al Cliente modificar datos personales. |
| RF-09 | El sistema deberá permitir al Cliente recuperar su contraseña. |
| RF-10 | El sistema permitirá al cliente que haya comprado un producto calificarlo (1-5 estrellas + comentario opcional). |
| RF-11 | El sistema deberá permitir al Dueño eliminar reseñas con lenguaje ofensivo, vulgar o amenazante y su respectiva calificación. |
| RF-12 | El sistema deberá exigir al Visitante iniciar sesión o registrarse para finalizar una compra, conservando el contenido de su carrito. |
| RF-13 | El sistema deberá permitir al Empleado y al Dueño consultar el listado de clientes registrados. |


### Módulo 2 — Productos, Stock y Proveedores

| ID | Requisito |
|----|-----------|
| RF-14 | El sistema deberá permitir al Visitante consultar el catálogo sin necesidad de registrarse, mostrando descripción, precio, color, talle, disponibilidad (stock/sin stock), entre 2 y 4 fotografías por producto y tabla de medidas por tipo de producto. |
| RF-15 | El sistema deberá permitir al Dueño agregar nuevos productos al catálogo. |
| RF-16 | El sistema deberá permitir al Dueño modificar productos. |
| RF-17 | El sistema deberá permitir al Dueño desactivar productos. |
| RF-18 | El sistema deberá permitir al Dueño crear, modificar y desactivar categorías y asignar cada producto a una categoría. |
| RF-19 | El sistema deberá permitir al Cliente y al Visitante filtrar el catálogo por categoría, talle y color. |
| RF-20 | El sistema deberá permitir al Empleado mantener un stock unificado para cada combinación de producto-talle-color, afectado tanto por ventas online como por ventas en local. |
| RF-21 | El sistema deberá permitir al Empleado registrar una venta presencial indicando productos, cantidades y seleccionando el medio de pago correspondiente (efectivo, tarjeta de débito, tarjeta de crédito o transferencia/QR). |
| RF-22 | El sistema deberá permitir al Empleado configurar un stock mínimo por producto-talle-color y generar una alerta visible en el panel cuando el stock sea menor o igual a ese mínimo. |
| RF-23 | El sistema deberá permitir al Empleado registrar proveedores, almacenando razón social, CUIT, teléfono, email y dirección. |
| RF-24 | El sistema deberá permitir al Empleado modificar los datos de proveedores. |
| RF-25 | El sistema deberá permitir al Empleado inhabilitar proveedores. |
| RF-26 | El sistema deberá permitir al Empleado asociar productos a proveedores. |


### Módulo 3 — Carrito, Pedidos y Promociones
| ID | Requisito |
|----|-----------|
| RF-27 | El sistema deberá permitir al Visitante y Cliente agregar productos al carrito (exigiendo talle y color), visualizar, modificar cantidades, eliminar productos y/o vaciar carrito. |
| RF-28 | El sistema deberá permitir al Cliente realizar la verificación de los datos de entrega, permitiendo seleccionar envío a domicilio o retiro en local, y calculando el costo de envío correspondiente. |
| RF-29 | El sistema deberá permitir al Cliente realizar el pago mediante Mercado Pago registrando estado, fecha, importe y medio de pago devuelto por la pasarela. |
| RF-30 | El sistema notificará al cliente mediante email por cada cambio de estado de su pedido (Pendiente de pago, Pagado / En preparación, Enviado, Listo para Retirar, Entregado y Cancelado). |
| RF-31 | El sistema permitirá al Cliente cancelar el pedido antes de su despacho. |
| RF-32 | El sistema deberá permitir al Dueño crear promociones (descuento porcentual o fijo) aplicables a producto específico, categoría o catálogo completo, con fechas de inicio y fin configurables. |
| RF-33 | El sistema permitirá al Dueño crear cupones (de uso único o múltiple, con limite de usos), definiendo un período de vigencia para su activación y desactivación, y permitirá al Cliente aplicar un cupón vigente y con usos disponibles a su carrito (un solo cupón por pedido). |


### Módulo 4 — Envios y Devoluciones

| ID | Requisito |
|----|-----------|
| RF-34 | El sistema se integrará con proveedor logístico para obtener número de seguimiento. |
| RF-35 | El sistema permitirá al Empleado confirmar el retiro en local. |
| RF-36 | El sistema deberá permitir al Empleado marcar un pedido como "Listo para retirar", lo que iniciará un plazo de 15 días corridos para retirarlo. |
| RF-37 | El sistema notificará al Cliente el vencimiento del plazo de retiro (día 12 y día 15). |
| RF-38 | El sistema deberá permitir al Cliente solicitar devolución, seleccionando el pedido y el motivo (talle incorrecto, defectuoso, equivocado), dentro de los 5 días hábiles posteriores a la entrega/retiro. |
| RF-39 | El sistema notificará al Cliente mediante email cada cambio de estado de su devolución (Solicitada, En Revisión, Aprobada, Rechazada, Producto recibido y Finalizada). |
| RF-40 | El sistema deberá permitir al Empleado aprobar o rechazar las solicitudes de devolución. |
| RF-41 | El sistema deberá permitir al Empleado emitir nota de credito a favor del cliente. |

### Módulo 5 — Reportes y Panel de Administración

| ID | Requisito |
|----|-----------|
| RF-42 | El sistema deberá permitir al Dueño generar y exportar a Excel reportes  detallados de ventas parametrizados por período (diario, semanal, mensual, anual y hasta 5 años hacia atrás), permitiendo filtrar por rango de fechas, producto o categoría. |
| RF-43 | El sistema deberá permitir al Dueño obtener,  para un período seleccionado: los 10 productos más vendidos, los 10 de menor movimiento, ingresos totales, ventas por medio de pago, clientes nuevos (registrados en los últimos 7 días) y clientes recurrentes (3 o más compras). |
| RF-44 | El sistema deberá permitir al Empleado y Dueño visualizar el panel de administración con las ventas del día, cantidad de productos con stock crítico, pedidos pendientes (Pagado y En preparación) y devoluciones pendientes (Solicitada y En revisión).|


## Requisitos no funcionales

### Módulo 1 — Rendimiento y Disponibilidad

| ID | Requisito |
|----|-----------|
| RNF-01 | El sistema responderá a consultas de catálogo, carrito y Mi Cuenta en ≤ 3 segundos al probarse con 50 usuarios simultáneos. |
| RNF-02 | El sistema completará el flujo de checkout en ≤ 5 segundos, sin contar el tiempo de respuesta de Mercado Pago.|
| RNF-03 | El sistema procesará al menos 10 pedidos por minuto en horas pico sin errores. |
| RNF-04 | El sistema deberá permanecer disponible al menos el 95% del tiempo en horario comercial (9:00 a 20:00). | 


### Módulo 2 — Seguridad y Privacidad

| ID | Requisito |
|----|-----------|
| RNF-05 | Todo el tráfico de datos entre el navegador del usuario y el servidor web debe estar cifrado de extremo a extremo utilizando el protocolo HTTPS |
| RNF-06 | El sistema deberá proteger las contraseñas de los usuarios y no almacenarlas en texto visible. |
| RNF-07 | El sistema bloqueará el acceso de un cliente por 15 minutos tras 5 intentos fallidos de inicio de sesión; y de un empleado por 30 minutos tras 3 intentos fallidos. |
| RNF-08 | El sistema debe cumplir con la Ley 25.326 de Protección de Datos personales para el almacenamiento, privacidad y gestión de la información de los clientes. |


### Módulo 3 — Usabilidad y Compatibilidad

| ID | Requisito |
|----|-----------|
| RNF-09 | El diseño será responsive, adaptándose a dispositivos móviles (360px) y de escritorio (1920px).|
| RNF-10 |El sistema mostrará un mensaje de error cuando un usuario ingrese datos inválidos en un formulario, indicando el campo que contiene el error.|
| RNF-11 |El sistema mostrará un indicador de carga mientras se ejecuten operaciones que demoren más de 1 segundo. |
| RNF-12 | El sistema funcionará correctamente en los navegadores Chrome, Firefox y Edge.| 


### Módulo 4 — Base de Datos y Almacenamiento

| ID | Requisito | 
|----|-----------|
| RNF-13 | Las consultas a la base de datos para mostrar productos y stock se ejecutarán en menos de 2 segundos.| 
| RNF-14 |Las imágenes subidas por el Administrador serán comprimidas a un tamaño menor a 300 KB.|
| RNF-15 |El sistema permitirá consultar un historial de al menos 10.000 pedidos, mostrando los resultados en un tiempo máximo de 3 segundos.| 

### Módulo 5 — Respaldo y Mantenibilidad

| ID | Requisito | 
|----|-----------|
| RNF-16 | El sistema realizará una copia de seguridad de la base de datos al menos una vez por día (02:00am) y una copia de seguridad de las imágenes y del código al menos una vez por semana.|
| RNF-17 |El código fuente del sistema deberá mantenerse versionado mediante Git.|
| RNF-18 | Los errores generados por el sistema deberán registrarse indicando como mínimo la fecha, hora y descripción del error.| 


