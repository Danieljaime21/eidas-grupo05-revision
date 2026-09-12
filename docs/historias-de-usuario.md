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


## HU-05 — Control de Stock Unificado e Ingreso de Mercadería

| Campo | Detalle |
|-------|---------|
| Historia | Como usuario con rol Depósito o Administrador, quiero registrar el ingreso de nueva mercadería y consultar los movimientos de stock centralizados, para mantener alineado el inventario entre las ventas presenciales y la tienda online, evitando sobreventas. |
| Módulo |04 - Inventario y Stock |
| Requisitos relacionados | RF-36, RF-37, RF-38, RF-39, RF-40, RF-41, RF-42, RF-43, RF-44, RF-45, RF-47, RF-48 |

### Criterios de aceptación

1. El sistema actualiza en tiempo real el stock centralizado, descontando prendas únicamente tras la aprobación confirmada del pago online.
2. El personal de Depósito puede registrar ingresos de productos indicando proveedor, contacto, cantidad, ID de producto, fecha y costo unitario.
3. El sistema emite una notificación en el panel y por correo al área de Depósito cuando el stock de una variante cae por debajo del umbral mínimo configurado.

### Validación INVEST

| Criterio | ¿Se cumple? | Observación |
|----------|-------------|-------------|
| Independiente |Sí |Funciona de manera aislada como un módulo de auditoría y actualización de existencias. |
| Negociable |Sí |Los umbrales para las alertas de bajo stock y los campos de reporte son parametrizables. |
| Valiosa |Sí |Evita la falta de coincidencia de inventario entre el local físico y la tienda web. |
| Estimable |Sí |Consiste en operaciones CRUD sobre las entidades de stock e inventario. |
| Pequeña |Sí |Se centra en el registro de ingresos y la actualización del stock disponible. |
| Verificable |Sí |Se valida realizando un ingreso de stock y comprobando su reflejo en la tienda online. |


## HU-06 — Solicitud, Gestión y Resolución de Devoluciones

| Campo | Detalle |
|-------|---------|
| Historia | Como cliente registrado, quiero iniciar solicitudes de devolución desde "Mi Cuenta" adjuntando motivo y fotografías, para obtener el cambio del producto o la emisión de una nota de crédito ante fallas o inconvenientes de talle. |
| Módulo |06 - Devoluciones y Cambios |
| Requisitos relacionados | RF-88, RF-89, RF-90, RF-91, RF-92, RF-93, RF-94, RF-95, RF-96, RF-97, RF-98, RF-99, RF-100, RF-101 |

### Criterios de aceptación

1. La opción de solicitar devolución solo se habilita para pedidos finalizados dentro de los 5 días hábiles posteriores al retiro o entrega, exigiendo seleccionar el motivo y permitiendo adjuntar fotos.
2.  El sistema impide crear solicitudes fuera del plazo legal estipulado de 5 días hábiles y permite al rol Ventas revisar y cambiar el estado del caso.
3. Al aprobarse una devolución sin cambio de producto, el sistema genera de forma automática la nota de crédito, reingresa la prenda al inventario y notifica al cliente.

### Validación INVEST

| Criterio | ¿Se cumple? | Observación |
|----------|-------------|-------------|
| Independiente |Sí |Opera como un flujo posterior sobre órdenes finalizadas sin afectar el checkout. |
| Negociable |Sí |La cantidad de imágenes adjuntas o los motivos predefinidos pueden ampliarse. |
| Valiosa |Sí |Brinda respaldo postventa al consumidor garantizando el cumplimiento normativo. |
| Estimable |Sí |Implica validaciones de fechas, subida de archivos y generación de notas de crédito. |
| Pequeña |Sí |Se limita al trámite del reclamo, revisión y actualización contable/de stock. |
| Verificable |Sí |Se prueba emitiendo reclamos dentro y fuera de plazo y verificando la nota de crédito. |
