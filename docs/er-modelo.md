# Modelo Entidad-Relación

## Diagrama

_Incluir el código PlantUML en `diagramas/er.puml`._
_Visualizar en [plantuml.com]()._

## Entidades

| Entidad | Descripción | Relaciones clave |
|---------|-------------|-----------------|
| USUARIO | Es la entidad base que contiene los datos necesarios para el inicio de sesión, las credenciales y la seguridad de la plataforma. Se utiliza tanto para los clientes como para los empleados. | Relación 1:1 con CLIENTE y EMPLEADO mediante id_usuario. |
| CLIENTE | Representa a las personas que realizan compras en el e-commerce. Contiene sus datos de contacto y la información necesaria para la entrega de los pedidos. | Relación 1:1 con USUARIO. Relación 1:1 con CARRITO. Relación 1:N con PEDIDO. |
| EMPLEADO | Representa al personal interno que trabaja en la empresa y se encarga de tareas administrativas, comerciales, logísticas o relacionadas con el depósito y el ingreso de mercadería. | Relación 1:1 con USUARIO. Relación 1:N con INGRESO_STOCK. |
| CATEGORIA | Permite organizar y clasificar los productos que forman parte del catálogo de la tienda. | Relación 1:N con PRODUCTO. |
| PRODUCTO | Contiene la información general de cada artículo que se ofrece en la tienda, como su nombre, descripción y datos comerciales. | Relación N:1 con CATEGORIA. Relación 1:N con VARIANTE_PRODUCTO. Relación N:M con PROVEEDOR mediante PRODUCTO_PROVEEDOR. |
| VARIANTE_PRODUCTO | Representa las distintas opciones de un producto, por ejemplo, según talle o color. Permite llevar un control de cada variante disponible en el stock mediante un SKU único. | Relación N:1 con PRODUCTO. Relación 1:N con DETALLE_CARRITO y DETALLE_PEDIDO. |
| PROVEEDOR | Guarda los datos de las empresas que abastecen de mercadería al negocio, incluyendo información comercial y fiscal. | Relación N:M con PRODUCTO mediante PRODUCTO_PROVEEDOR. Relación 1:N con INGRESO_STOCK. |
| PRODUCTO_PROVEEDOR | Es la tabla intermedia que permite relacionar los productos con los proveedores que los pueden abastecer. | Relación N:1 con PRODUCTO y N:1 con PROVEEDOR. |
| INGRESO_STOCK | Registra cada ingreso o reposición de mercadería que llega al negocio. También permite saber qué proveedor realizó el ingreso y qué empleado lo registró. | Relación N:1 con EMPLEADO y N:1 con PROVEEDOR. |
| DETALLE_INGRESO_STOCK | Contiene el detalle de cada variante y cantidad ingresada en un movimiento de stock. | Relación N:1 con INGRESO_STOCK y N:1 con VARIANTE_PRODUCTO. |
| CARRITO | Representa el carrito de compra de un cliente y permite mantener los productos que seleccionó antes de confirmar el pedido. | Relación 1:1 con CLIENTE. Relación 1:N con DETALLE_CARRITO. |
| DETALLE_CARRITO | Guarda las variantes de productos y las cantidades que el cliente agregó temporalmente a su carrito. | Relación N:1 con CARRITO y N:1 con VARIANTE_PRODUCTO. |
| PEDIDO | Representa una compra confirmada por el cliente. Contiene la información general de la operación, como el estado del pago, el monto total y la modalidad de entrega. | Relación N:1 con CLIENTE. Relación 1:N con DETALLE_PEDIDO. |
| DETALLE_PEDIDO | Contiene los productos que forman parte de un pedido confirmado, junto con sus cantidades y valores correspondientes al momento de la compra. | Relación N:1 con PEDIDO y N:1 con VARIANTE_PRODUCTO. |
| PROMOCION | Representa descuentos porcentuales o fijos aplicables a un producto específico, a una categoría o al catálogo completo, con fechas de vigencia. | Relación N:1 opcional con PRODUCTO o CATEGORIA. |
| CUPON | Representa cupones de descuento de uso único o múltiple, con límite de usos y período de vigencia. | Relación 1:N con CUPON_USADO. |
| CUPON_USADO | Registra cada uso de un cupón en un pedido concreto. | Relación N:1 con CUPON, PEDIDO y CLIENTE. |
| RESENA | Almacena la calificación (1-5 estrellas) y el comentario opcional que un cliente realiza sobre un producto que compró. | Relación N:1 con PRODUCTO, CLIENTE y PEDIDO. |
| DEVOLUCION | Representa la solicitud de devolución de un pedido dentro de los 5 días hábiles posteriores a la entrega o retiro. | Relación N:1 con PEDIDO y CLIENTE. Relación 1:N con DETALLE_DEVOLUCION. Relación 0:1 con NOTA_CREDITO. |
| DETALLE_DEVOLUCION | Contiene los productos específicos que se incluyen en una solicitud de devolución. | Relación N:1 con DEVOLUCION y N:1 con VARIANTE_PRODUCTO. |
| NOTA_CREDITO | Representa la nota de crédito emitida a favor del cliente cuando una devolución es aprobada. | Relación N:1 con DEVOLUCION, CLIENTE y EMPLEADO. |

## Descripción de atributos principales

_Para cada entidad, describir brevemente los atributos más relevantes y su propósito._

### [USUARIO]

- `id_usuario` INT (PK): Identificador interno del usuario. Es autoincremental, no tiene significado de negocio y nunca cambia.
- `dni` VARCHAR(20) (UK): Documento Nacional de Identidad o CUIT del usuario. Es único, pero no es la clave primaria: si se carga mal, se puede corregir sin afectar a las demás tablas.
- `nombre` VARCHAR(100): Nombre de pila del usuario.
- `apellido` VARCHAR(100): Apellido del usuario.
- `email` VARCHAR(150): Credencial única utilizada para iniciar sesión y recibir notificaciones.
- `contrasena_hash` VARCHAR(255): Contraseña almacenada de forma segura mediante un algoritmo de hash de un solo sentido, de acuerdo con RNF-06.
- `rol` VARCHAR(30): Define el perfil y los permisos de acceso dentro del sistema (Dueño, Empleado, Cliente).
- `estado_activo` BOOLEAN: Indica si la cuenta se encuentra activa o inhabilitada.
- `intentos_fallidos` INTEGER: Contador utilizado para controlar los intentos incorrectos de inicio de sesión.
- `bloqueado_hasta` DATETIME: Fecha y hora hasta la cual el usuario permanece bloqueado, de acuerdo con RNF-07.
- `fecha_alta` DATETIME: Fecha y hora en que se dio de alta el usuario.

### [CLIENTE]

- `id_usuario` INT (PK, FK): Identificador del cliente y clave foránea que referencia a USUARIO.id_usuario.
- `fecha_nacimiento` DATE: Fecha de nacimiento declarada en el registro (RF-06).
- `telefono` VARCHAR(30): Número telefónico utilizado para contacto y notificaciones.
- `direccion` VARCHAR(255): Domicilio de entrega predeterminado registrado por el cliente.
- `codigo_postal` VARCHAR(10): Código postal del domicilio predeterminado; se usa para calcular el costo de envío.
- `ciudad` VARCHAR(100): Ciudad del domicilio predeterminado.
- `provincia` VARCHAR(100): Provincia del domicilio predeterminado.

### [EMPLEADO]

- `id_usuario` INT (PK, FK): Identificador del empleado y clave foránea que referencia a USUARIO.id_usuario.
- `departamento` VARCHAR(50): Área operativa a la que pertenece el empleado.
- `fecha_ingreso` DATE: Fecha de ingreso a la empresa.

### [CATEGORIA]

- `id_categoria` INT (PK): Identificador único de la categoría.
- `nombre` VARCHAR(100): Nombre de la categoría comercial.
- `descripcion` TEXT: Descripción opcional de la categoría.
- `estado_activo` BOOLEAN: Indica si la categoría está habilitada o desactivada.

### [PRODUCTO]

- `id_producto` INT (PK): Identificador único del producto.
- `id_categoria` INT (FK): Referencia a la categoría a la que pertenece el producto.
- `nombre` VARCHAR(150): Denominación comercial del artículo.
- `descripcion` TEXT: Información descriptiva y características del producto.
- `precio_base` DECIMAL(10,2): Precio de referencia del producto.
- `tabla_medidas_url` VARCHAR(255): Enlace a la tabla de medidas del producto.
- `estado_activo` BOOLEAN: Indica si el producto está habilitado en el catálogo.

### [VARIANTE_PRODUCTO]

- `sku` VARCHAR(50) (PK): Código alfanumérico único que identifica la variante del producto.
- `id_producto` INT (FK): Referencia al producto al que pertenece la variante.
- `talle` VARCHAR(20): Talle correspondiente a la variante.
- `color` VARCHAR(50): Color correspondiente a la variante.
- `stock` INT: Cantidad de unidades disponibles para la venta (stock unificado online + local).
- `stock_minimo` INT: Umbral a partir del cual se genera alerta de stock crítico.
- `estado_activo` BOOLEAN: Indica si la variante está habilitada.

### [PROVEEDOR]

- `id_proveedor` INT (PK): Identificador único del proveedor.
- `razon_social` VARCHAR(150): Denominación legal de la empresa proveedora.
- `cuit` VARCHAR(20): Clave Única de Identificación Tributaria del proveedor.
- `telefono` VARCHAR(30): Teléfono de contacto.
- `email` VARCHAR(150): Correo electrónico de contacto.
- `direccion` VARCHAR(255): Domicilio del proveedor.
- `estado_activo` BOOLEAN: Indica si el proveedor se encuentra habilitado.

### [PRODUCTO_PROVEEDOR]

- `id_producto` INT (PK, FK): Referencia al producto asociado al proveedor.
- `id_proveedor` INT (PK, FK): Referencia al proveedor asociado al producto.

- La combinación de `id_producto` e `id_proveedor` constituye una clave primaria compuesta.

### [INGRESO_STOCK]

- `id_ingreso` INT (PK): Identificador único del ingreso de mercadería.
- `id_empleado` INT (FK): Identifica al empleado responsable del ingreso.
- `id_proveedor` INT (FK): Identifica al proveedor que realizó el envío.
- `fecha_ingreso` DATETIME: Fecha y hora en la que se procesó el ingreso.
- `observaciones` TEXT: Comentarios opcionales sobre el ingreso.

### [DETALLE_INGRESO_STOCK]

- `id_detalle_ingreso` INT (PK): Identificador único de cada línea del ingreso.
- `id_ingreso` INT (FK): Referencia al ingreso al que pertenece el detalle.
- `sku` VARCHAR(50) (FK): Referencia a la variante de producto ingresada.
- `cantidad` INT: Cantidad de unidades ingresadas.
- `costo_unitario` DECIMAL(10,2): Costo unitario opcional para control de costos.

### [CARRITO]

- `id_carrito` INT (PK): Identificador único del carrito.
- `id_cliente` INT (FK): Referencia al cliente propietario del carrito.
- `fecha_actualizacion` DATETIME: Fecha y hora de la última modificación del carrito.

### [DETALLE_CARRITO]

- `id_detalle_carrito` INT (PK): Identificador único de cada línea del carrito.
- `id_carrito` INT (FK): Referencia al carrito al que pertenece el detalle.
- `sku` VARCHAR(50) (FK): Referencia a la variante de producto seleccionada.
- `cantidad` INT: Cantidad de unidades agregadas temporalmente al carrito.

### [PEDIDO]

- `id_pedido` INT (PK): Identificador único de la orden de compra.
- `id_cliente` INT (FK, nullable): Referencia al cliente que realizó el pedido. Es nulo en ventas presenciales.
- `id_empleado` INT (FK): Empleado que registró la venta presencial o gestionó el pedido.
- `fecha_pedido` DATETIME: Fecha y hora correspondiente al inicio del checkout o de la venta.
- `estado_pedido` VARCHAR(50): Estado operativo del pedido (Pendiente de pago, Pagado / En preparación, Enviado, Listo para Retirar, Entregado, Cancelado).
- `tipo_entrega` VARCHAR(50): Modalidad seleccionada (Envío a domicilio o Retiro en local).
- `telefono_contacto` VARCHAR(30): Teléfono confirmado por el cliente para este pedido (CU-09). Puede diferir del de su cuenta.
- `direccion_entrega` VARCHAR(255): Domicilio de entrega confirmado para este pedido. Es nulo en retiro en local y en ventas presenciales.
- `codigo_postal_entrega` VARCHAR(10): Código postal de la entrega, usado para calcular el costo de envío. Nulo si no hay envío.
- `ciudad_entrega` VARCHAR(100): Ciudad de la entrega. Nula si no hay envío.
- `provincia_entrega` VARCHAR(100): Provincia de la entrega. Nula si no hay envío.
- `costo_envio` DECIMAL(10,2): Importe correspondiente al costo del envío.
- `monto_total` DECIMAL(10,2): Importe total de la operación.
- `medio_pago` VARCHAR(50): Medio de pago utilizado (efectivo, tarjeta de débito, tarjeta de crédito, transferencia/QR o Mercado Pago).
- `id_transaccion_mp` VARCHAR(100): Identificador de la transacción generada por Mercado Pago.
- `estado_pago` VARCHAR(50): Estado informado por el procesador de pagos.
- `numero_seguimiento` VARCHAR(100): Código utilizado para realizar el seguimiento del envío.
- `fecha_vencimiento_retiro` DATETIME: Fecha límite para retirar el pedido en sucursal.
- `es_presencial` BOOLEAN: Indica si se trata de una venta realizada en el local.

### [DETALLE_PEDIDO]

- `id_detalle_pedido` INT (PK): Identificador único de cada línea del pedido.
- `id_pedido` INT (FK): Referencia al pedido al que pertenece el detalle.
- `sku` VARCHAR(50) (FK): Referencia a la variante de producto vendida.
- `cantidad` INT: Cantidad de unidades adquiridas.
- `precio_unitario` DECIMAL(10,2): Precio de la variante al momento de realizar la compra (precio histórico).

### [PROMOCION]

- `id_promocion` INT (PK): Identificador único de la promoción.
- `nombre` VARCHAR(150): Nombre descriptivo de la promoción.
- `tipo_descuento` VARCHAR(20): Tipo de descuento (porcentual o fijo).
- `valor_descuento` DECIMAL(10,2): Valor del descuento.
- `aplicacion` VARCHAR(30): Alcance de la promoción (producto, categoria o catalogo).
- `id_producto` INT (FK, nullable): Producto al que aplica (si corresponde).
- `id_categoria` INT (FK, nullable): Categoría a la que aplica (si corresponde).
- `fecha_inicio` DATETIME: Fecha y hora de inicio de la promoción.
- `fecha_fin` DATETIME: Fecha y hora de fin de la promoción.
- `estado_activo` BOOLEAN: Indica si la promoción está vigente.

### [CUPON]

- `id_cupon` INT (PK): Identificador único del cupón.
- `codigo` VARCHAR(50) (UK): Código que el cliente ingresa para aplicar el descuento.
- `tipo_descuento` VARCHAR(20): Tipo de descuento (porcentual o fijo).
- `valor_descuento` DECIMAL(10,2): Valor del descuento.
- `uso_unico` BOOLEAN: Indica si el cupón solo puede usarse una vez por cliente.
- `limite_usos` INT: Cantidad máxima de usos permitidos.
- `usos_actuales` INT: Contador de usos realizados.
- `fecha_inicio` DATETIME: Fecha y hora de inicio de vigencia.
- `fecha_fin` DATETIME: Fecha y hora de fin de vigencia.
- `estado_activo` BOOLEAN: Indica si el cupón está habilitado.

### [CUPON_USADO]

- `id_cupon_usado` INT (PK): Identificador único del uso.
- `id_cupon` INT (FK): Referencia al cupón utilizado.
- `id_pedido` INT (FK): Referencia al pedido en el que se aplicó.
- `id_cliente` INT (FK): Cliente que utilizó el cupón.
- `fecha_uso` DATETIME: Fecha y hora en que se aplicó el cupón.

### [RESENA]

- `id_resena` INT (PK): Identificador único de la reseña.
- `id_producto` INT (FK): Producto calificado.
- `id_cliente` INT (FK): Cliente que realizó la reseña.
- `id_pedido` INT (FK): Pedido que acredita la compra.
- `calificacion` INT: Puntuación de 1 a 5 estrellas.
- `comentario` TEXT: Comentario opcional del cliente.
- `fecha_resena` DATETIME: Fecha y hora en que se realizó la reseña.
- `estado_activo` BOOLEAN: Indica si la reseña está visible. Se pone en false cuando el Dueño la elimina por lenguaje ofensivo.

### [DEVOLUCION]

- `id_devolucion` INT (PK): Identificador único de la devolución.
- `id_pedido` INT (FK): Pedido al que corresponde la devolución.
- `id_cliente` INT (FK): Cliente que solicita la devolución.
- `fecha_solicitud` DATETIME: Fecha y hora de la solicitud.
- `motivo` VARCHAR(50): Motivo de la devolución (talle incorrecto, defectuoso, equivocado).
- `estado` VARCHAR(50): Estado de la devolución (Solicitada, En Revisión, Aprobada, Rechazada, Producto recibido, Finalizada).
- `observaciones` TEXT: Comentarios adicionales.
- `fecha_resolucion` DATETIME: Fecha y hora en que se resolvió la solicitud.
- `id_empleado` INT (FK): Empleado que aprobó o rechazó la devolución.

### [DETALLE_DEVOLUCION]

- `id_detalle_devolucion` INT (PK): Identificador único de cada línea de la devolución.
- `id_devolucion` INT (FK): Referencia a la devolución.
- `sku` VARCHAR(50) (FK): Variante de producto devuelta.
- `cantidad` INT: Cantidad de unidades devueltas.

### [NOTA_CREDITO]

- `id_nota_credito` INT (PK): Identificador único de la nota de crédito.
- `id_devolucion` INT (FK): Devolución que originó la nota.
- `id_cliente` INT (FK): Cliente beneficiario.
- `monto` DECIMAL(10,2): Importe de la nota de crédito.
- `fecha_emision` DATETIME: Fecha y hora de emisión.
- `id_empleado` INT (FK): Empleado que emitió la nota.
- `estado` VARCHAR(30): Estado de la nota de crédito.

## Decisiones de diseño

_Justificar al menos dos decisiones de diseño relevantes: por qué se modeló de esa manera,
qué alternativas se consideraron y por qué se descartaron._

### Decisión 1 — Separación de USUARIO, CLIENTE y EMPLEADO

Decisión  
Usar una entidad base USUARIO para las credenciales (email, contraseña hasheada, intentos fallidos, etc.) y dos entidades hijas: CLIENTE y EMPLEADO, relacionadas 1:1 por el id_usuario.

Justificación  
Así no se repiten los datos de login. Además permite que los empleados tengan atributos propios (departamento) y los clientes otros (fecha de nacimiento, dirección, CP, ciudad, provincia). El Dueño se maneja como un empleado con rol “Dueño”.

Alternativa descartada 
Poner todo en una sola tabla USUARIO. Generaba muchos campos nulos y complicaba las validaciones.

### Decisión 2 — Stock en VARIANTE_PRODUCTO

Decisión 
El stock y el stock mínimo se guardan en VARIANTE_PRODUCTO (por talle y color), no en PRODUCTO. Se usa el SKU como clave primaria.

Justificación  
Nadie compra “una remera” genérica, compra una remera talle M color negro. Si el stock estuviera en PRODUCTO no se sabría qué talle o color se está agotando.

Alternativa descartada  
Guardar el stock en PRODUCTO. Era imposible controlar el inventario real.

### Decisión 3 — Datos de pago y envío dentro de PEDIDO

Decisión  
Los datos de Mercado Pago, el medio de pago, el número de seguimiento y la fecha de vencimiento de retiro se guardan directamente en la tabla PEDIDO. También se permite que id_cliente sea nulo para las ventas presenciales.

Justificación  
Cada pedido tiene un solo pago y un solo envío. Meter todo junto hace más simples las consultas. Además permite registrar ventas del local sin forzar la creación de un cliente.

Alternativa descartada  
Crear tablas separadas de PAGO y ENVIO. Complicaba innecesariamente las consultas.

### Decisión 4 — Precio histórico en DETALLE_PEDIDO

Decisión  
Se guarda el precio_unitario en DETALLE_PEDIDO al momento de la compra.

Justificación 
Los precios cambian. Si no se guarda el valor de ese momento, los pedidos viejos mostrarían precios incorrectos y se romperían los reportes.

Alternativa descartada  
Leer siempre el precio actual de PRODUCTO. Alteraba el historial de ventas.

### Decisión 5 — Detalle de ingreso de stock

Decisión
Se agregó DETALLE_INGRESO_STOCK con el sku y la cantidad de cada variante que ingresa.

Justificación 
Sin este detalle no se puede actualizar el stock de cada talle/color cuando llega mercadería.

### Decisión 6 — Entidades para Devoluciones, Promociones, Cupones y Reseñas

Decisión
Se modelaron entidades propias para DEVOLUCION (con DETALLE_DEVOLUCION y NOTA_CREDITO), PROMOCION, CUPON (con CUPON_USADO) y RESENA.

Justificación 
Cada uno de estos conceptos tiene su propio ciclo de vida, estados y reglas de negocio. Las devoluciones manejan motivos y un flujo de aprobación, las promociones y cupones tienen vigencia y condiciones de aplicación distintas, y las reseñas están atadas a una compra real. Separarlos en entidades propias permite controlar mejor estas reglas y facilita los reportes.

### Decisión 7 — Clave primaria interna en USUARIO (id_usuario) y DNI único

Decisión
USUARIO usa un `id_usuario` numérico interno como clave primaria. El DNI se guarda como atributo único (UK), no como clave. CLIENTE y EMPLEADO comparten ese `id_usuario` como PK y FK, y el resto de las tablas referencian al cliente o al empleado mediante `id_cliente` e `id_empleado`.

Justificación
El DNI viaja como clave foránea a muchas tablas (carrito, pedido, uso de cupones, reseñas, devoluciones, notas de crédito, ingresos de stock). Si se carga mal y hay que corregirlo, con el DNI como clave habría que actualizarlo en todas ellas al mismo tiempo. Con un identificador interno que nunca cambia, la corrección toca un solo campo de USUARIO. Además, el DNI sigue siendo único (no puede haber dos usuarios con el mismo), que es lo que valida el registro (CU-01) y el alta de personal (CU-03).

Alternativa descartada
Usar el DNI como clave primaria (clave natural). Es más simple a primera vista, pero propaga cualquier corrección a todas las tablas relacionadas y mezcla en una misma columna un dato de negocio con la identidad técnica del registro.

### Decisión 8 — Datos de entrega copiados en PEDIDO

Decisión
PEDIDO guarda su propio teléfono de contacto y dirección de entrega (calle y número, código postal, ciudad y provincia), aparte del domicilio predeterminado que figura en CLIENTE.

Justificación
En el checkout el cliente puede confirmar o modificar los datos de entrega solo para esa compra (CU-09), por ejemplo para enviar un regalo a otra dirección. Si el pedido leyera siempre el domicilio actual del cliente, un cambio posterior en Mi Cuenta alteraría pedidos ya despachados. Es el mismo criterio que el precio histórico de la Decisión 4: el pedido conserva lo que se acordó al momento de la compra.

Alternativa descartada
Leer siempre el domicilio de CLIENTE. No permite entregar en otra dirección y deja los pedidos viejos con datos que ya no son los de ese envío.
