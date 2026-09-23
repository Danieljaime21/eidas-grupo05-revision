# Modelo Entidad-Relación

## Diagrama

_Incluir el código PlantUML en `diagramas/er.puml`._
_Visualizar en [plantuml.com](https://www.plantuml.com/plantuml/uml/)._

## Entidades

| Entidad | Descripción | Relaciones clave |
|---------|-------------|-----------------|
| USUARIO | Es la entidad base que contiene los datos necesarios para el inicio de sesión, las credenciales y la seguridad de la plataforma. Se utiliza tanto para los clientes como para los empleados. | Relación 1:1 con CLIENTE y EMPLEADO mediante dni. |
| CLIENTE | Representa a las personas que realizan compras en el e-commerce. Contiene sus datos de contacto y la información necesaria para la entrega de los pedidos. | Relación 1:1 con USUARIO. Relación 1:1 con CARRITO. Relación 1:N con PEDIDO. |
| EMPLEADO | Representa al personal interno que trabaja en la empresa y se encarga de tareas administrativas, comerciales, logísticas o relacionadas con el depósito y el ingreso de mercadería. | Relación 1:1 con USUARIO. Relación 1:N con INGRESO_STOCK. |
| CATEGORIA | Permite organizar y clasificar los productos que forman parte del catálogo de la tienda. | Relación 1:N con PRODUCTO. |
| PRODUCTO | Contiene la información general de cada artículo que se ofrece en la tienda, como su nombre, descripción y datos comerciales. | Relación N:1 con CATEGORIA. Relación 1:N con VARIANTE_PRODUCTO. Relación N:M con PROVEEDOR mediante PRODUCTO_PROVEEDOR. |
| VARIANTE_PRODUCTO | Representa las distintas opciones de un producto, por ejemplo, según talle o color. Permite llevar un control de cada variante disponible en el stock mediante un SKU único. | Relación N:1 con PRODUCTO. Relación 1:N con DETALLE_CARRITO y DETALLE_PEDIDO. |
| PROVEEDOR | Guarda los datos de las empresas que abastecen de mercadería al negocio, incluyendo información comercial y fiscal. | Relación N:M con PRODUCTO mediante PRODUCTO_PROVEEDOR. Relación 1:N con INGRESO_STOCK. |
| PRODUCTO_PROVEEDOR | Es la tabla intermedia que permite relacionar los productos con los proveedores que los pueden abastecer. | Relación N:1 con PRODUCTO y N:1 con PROVEEDOR. |
| INGRESO_STOCK | Registra cada ingreso o reposición de mercadería que llega al negocio. También permite saber qué proveedor realizó el ingreso y qué empleado lo registró. | Relación N:1 con EMPLEADO y N:1 con PROVEEDOR. |
| CARRITO | Representa el carrito de compra de un cliente y permite mantener los productos que seleccionó antes de confirmar el pedido. | Relación 1:1 con CLIENTE. Relación 1:N con DETALLE_CARRITO. |
| DETALLE_CARRITO | Guarda las variantes de productos y las cantidades que el cliente agregó temporalmente a su carrito. | Relación N:1 con CARRITO y N:1 con VARIANTE_PRODUCTO. |
| PEDIDO | Representa una compra confirmada por el cliente. Contiene la información general de la operación, como el estado del pago, el monto total y la modalidad de entrega. | Relación N:1 con CLIENTE. Relación 1:N con DETALLE_PEDIDO. |
| DETALLE_PEDIDO | Contiene los productos que forman parte de un pedido confirmado, junto con sus cantidades y valores correspondientes al momento de la compra. | Relación N:1 con PEDIDO y N:1 con VARIANTE_PRODUCTO. |

## Descripción de atributos principales

_Para cada entidad, describir brevemente los atributos más relevantes y su propósito._

### [USUARIO]

- `dni` (PK): Documento Nacional de Identidad o CUIT que identifica de manera única al usuario.
- `nombre`: Nombre y apellido del usuario.
- `email`: Credencial única utilizada para iniciar sesión y recibir notificaciones.
- `contrasena_hash`: Contraseña almacenada de forma segura mediante un algoritmo de hash de un solo sentido, de acuerdo con RNF-06.
- `rol`: Define el perfil y los permisos de acceso dentro del sistema.
- `estado_activo`: Indica si la cuenta se encuentra activa o inhabilitada.
- `intentos_fallidos`: Contador utilizado para controlar los intentos incorrectos de inicio de sesión.
- `bloqueado_hasta`: Fecha y hora hasta la cual el usuario permanece bloqueado, de acuerdo con RNF-07.

### [CLIENTE]

- `dni` (PK, FK): Identificador del cliente y clave foránea que referencia a USUARIO.dni.
- `telefono`: Número telefónico utilizado para contacto y notificaciones.
- `direccion`: Domicilio de entrega predeterminado registrado por el cliente.

### [EMPLEADO]

- `dni` (PK, FK): Identificador del empleado y clave foránea que referencia a USUARIO.dni.
- `departamento`: Área operativa a la que pertenece el empleado.

### [CATEGORIA]

- `id_categoria` (PK): Identificador único de la categoría.
- `nombre`: Nombre de la categoría comercial.
- `descripcion`: Descripción opcional de la categoría.

### [PRODUCTO]

- `id_producto` (PK): Identificador único del producto.
- `id_categoria` (FK): Referencia a la categoría a la que pertenece el producto.
- `nombre`: Denominación comercial del artículo.
- `descripcion`: Información descriptiva y características del producto.
- `precio_base`: Precio de referencia del producto.
- `tabla_medidas_url`: Enlace a la tabla de medidas del producto, de acuerdo con RF-11.
- `estado_activo`: Indica si el producto está habilitado en el catálogo.

### [VARIANTE_PRODUCTO]

- `sku` (PK): Código alfanumérico único que identifica la variante del producto.
- `id_producto` (FK): Referencia al producto al que pertenece la variante.
- `talle`: Talle correspondiente a la variante.
- `color`: Color correspondiente a la variante.
- `stock`: Cantidad de unidades disponibles para la venta, de acuerdo con RF-13.

### [PROVEEDOR]

- `id_proveedor` (PK): Identificador único del proveedor.
- `razon_social`: Denominación legal de la empresa proveedora.
- `cuit`: Clave Única de Identificación Tributaria del proveedor.
- `estado_activo`: Indica si el proveedor se encuentra habilitado.

### [PRODUCTO_PROVEEDOR]

- `id_producto` (PK, FK): Referencia al producto asociado al proveedor.
- `id_proveedor` (PK, FK): Referencia al proveedor asociado al producto.

- La combinación de `id_producto` e `id_proveedor` constituye una clave primaria compuesta.

### [INGRESO_STOCK]

- `id_ingreso` (PK): Identificador único del ingreso de mercadería.
- `dni_empleado` (FK): Identifica al empleado responsable del ingreso.
- `id_proveedor` (FK): Identifica al proveedor que realizó el envío.
- `fecha_ingreso`: Fecha y hora en la que se procesó el ingreso.

### [CARRITO]

- `id_carrito` (PK): Identificador único del carrito.
- `dni_cliente` (FK): Referencia al cliente propietario del carrito.
- `fecha_actualizacion`: Fecha y hora de la última modificación del carrito, utilizada para controlar la inactividad de 3 horas.

### [DETALLE_CARRITO]

- `id_detalle_carrito` (PK): Identificador único de cada línea del carrito.
- `id_carrito` (FK): Referencia al carrito al que pertenece el detalle.
- `sku` (FK): Referencia a la variante de producto seleccionada.
- `cantidad`: Cantidad de unidades agregadas temporalmente al carrito.

### [PEDIDO]

- `id_pedido` (PK): Identificador único de la orden de compra.
- `dni_cliente` (FK): Referencia al cliente que realizó el pedido.
- `fecha_pedido`: Fecha y hora correspondiente al inicio del checkout.
- `estado_pedido`: Estado operativo del pedido, por ejemplo Pendiente, Aprobado, Listo para retirar o Despachado.
- `tipo_entrega`: Modalidad seleccionada, como Envío a domicilio o Retiro en sucursal.
- `costo_envio`: Importe correspondiente al costo del envío.
- `monto_total`: Importe total de la operación.
- `id_transaccion_mp`: Identificador de la transacción generada por Mercado Pago.
- `estado_pago`: Estado informado por el procesador de pagos.
- `numero_seguimiento`: Código utilizado para realizar el seguimiento del envío.
- `fecha_vencimiento_retiro`: Fecha límite para retirar el pedido en sucursal, de acuerdo con RF-29.

### [DETALLE_PEDIDO]

- `id_detalle_pedido` (PK): Identificador único de cada línea del pedido.
- `id_pedido` (FK): Referencia al pedido al que pertenece el detalle.
- `sku` (FK): Referencia a la variante de producto vendida.
- `cantidad`: Cantidad de unidades adquiridas.
- `precio_unitario`: Precio de la variante al momento de realizar la compra.

## Decisiones de diseño

_Justificar al menos dos decisiones de diseño relevantes: por qué se modeló de esa manera,
qué alternativas se consideraron y por qué se descartaron._

### Decisión 1 — [Separación de Credenciales e Integración de Actores mediante Herencia (USUARIO -> CLIENTE / EMPLEADO)]

Decisión

Decidimos implementar una especialización 1:1, donde USUARIO sea la entidad principal y se encargue de manejar los datos de acceso, como el email, la contraseña, los intentos fallidos y el rol. A partir de esta entidad se relacionan CLIENTE y EMPLEADO, cada uno con sus datos específicos.

Justificación

Elegimos esta opción porque nos permite no repetir los datos de seguridad y acceso entre los distintos tipos de usuarios. También ayuda a mantener las mismas reglas para el inicio de sesión y el bloqueo de cuentas (RNF-06 y RNF-07). Además, permite relacionar a los empleados con las tareas que realizan dentro del sistema, por ejemplo, cuando se registra un INGRESO_STOCK.

Alternativas descartadas

USUARIO aislado y CLIENTE independiente: Se descartó porque podía generar datos repetidos y problemas de consistencia con las credenciales. También dificultaba relacionar a los empleados con las operaciones que realizan en el sistema.

Una única tabla USUARIO con todos los atributos: Se descartó porque tendría muchos campos que no serían necesarios para todos los usuarios, generando valores NULL. Por ejemplo, un cliente no tendría legajo y un empleado podría no necesitar los mismos datos de dirección que un cliente.

### Decisión 2 — [Desacoplamiento de Inventario mediante la Entidad VARIANTE_PRODUCTO]
