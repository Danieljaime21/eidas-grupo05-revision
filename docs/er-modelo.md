# Modelo Entidad-Relación

## Diagrama

_Incluir el código PlantUML en `diagramas/er.puml`._
_Visualizar en [plantuml.com](//www.plantuml.com/plantuml/png/fLR1RkCs4BtxAuXSsYwQmnvwMImMgzhgLbZ73XHdhyAOdCX4A58bgRJPfFzUoX93aP0DetiJPzvmtfiPalfiB6ZRDM9X7hbiGKD3jEeaeqfBrEItYLrmYVQvHQAqFQY9mno0gR-vhCa328EB1KhBxJEvkh-xpyfYUqN0aF6Rl2m8USSa9n_8jwnS_fcLvEF7sw-VFZdxzNNlbAhPQmp-teODS16Rg99MWq49rG7C8NPgbQ3HM4Uo0chvatAktxVRTPvjUXUNrX5MfdBi1MVAE7UnsJdNNgY_EkpZN0OBphxATlckkCaN_mQLotMHRtRvKUNuVKhbh-IFYLAB0X-KL15JnZLIofKCrcco_ERMyLuDDVMBYz8v0BQWBJIzsldTbqxUbsrPP8COlnhsvwoYOB5MciDGeWiwnz1GpTlJWcxBxUf-kHi4-SLRmbOhrb6hPlFDCnebNqx6OLkDpbZjmVG1gtnPt6Hhvx2m5r0ro3W3KtNwig5Av7tByzMszFg6rLJW4o9JUbwXXkzALaPH3kduTznUpYOfTfNIIitd6k2dAk6V0gPv7SiYS-UYYhgTM7tRpMCtVpcabDAEMn02qqj2A1sRZ5NqSOYTKYmsNyhyRblTxRRBhqTwaUMj85pM6is9WMIILzYq0e6fICFPYddd0z83X0JpbqrMbiLOl_5xSZgrvlOCDIeuIejJPaboeBO3mR_3S4PcATpcgsAyW8RFC2pzGVcH_647dpWCjlT5pRIyLHLAgx66jFF6zgudhg8Z_QvHqZciiY0YX-DlDKW3nzktQjfeFyy1wfY1x1hKgZ9OTxpfrSNkGTKJIZfwAusMQwzmMjPLlilMwxoQTjZRqaupFCxw-Owd4n6AdHonOAVWo31WGy0SkqdpOrFAxUmm-5dvtyp2dTr9Ra57JNQqVo8bYkCGeo7u3r3h20CHG7W3DSg5_nrvVRs-Lg_-tNQRNBc0dzz_UF_BLOhnhsqCMeoX7kLRvK2MeqIFYs0l_kGur07e4RJfD_CvF2o-WnnQOysDrV0M4Hxf8IIyeGuDjUxQW0tN-wdjOG_6OY2KHimz5IxC3JWB8ZpcV8n10iU7ZL0bVMmQcZmHeQuXsrXm7v4U6OUlEz0iL64eVOeF3U6IYkuv94Wud4tbH9ck0GB2Xv-Fzebzy518b3xwirjtZVWF)._

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

- `dni` VARCHAR(20) (PK): Documento Nacional de Identidad o CUIT que identifica de manera única al usuario.
- `nombre` VARCHAR(100): Nombre y apellido del usuario.
- `email` VARCHAR(150): Credencial única utilizada para iniciar sesión y recibir notificaciones.
- `contrasena_hash` VARCHAR(255): Contraseña almacenada de forma segura mediante un algoritmo de hash de un solo sentido, de acuerdo con RNF-06.
- `rol` VARCHAR(30): Define el perfil y los permisos de acceso dentro del sistema.
- `estado_activo`BOOLEAN: Indica si la cuenta se encuentra activa o inhabilitada.
- `intentos_fallidos` INTEGER: Contador utilizado para controlar los intentos incorrectos de inicio de sesión.
- `bloqueado_hasta` DATETIME: Fecha y hora hasta la cual el usuario permanece bloqueado, de acuerdo con RNF-07.

### [CLIENTE]

- `dni` VARCHAR(20) (PK, FK): Identificador del cliente y clave foránea que referencia a USUARIO.dni.
- `telefono` VARCHAR(30): Número telefónico utilizado para contacto y notificaciones.
- `direccion` VARCHAR(255): Domicilio de entrega predeterminado registrado por el cliente.

### [EMPLEADO]

- `dni` VARCHAR(20) (PK, FK): Identificador del empleado y clave foránea que referencia a USUARIO.dni.
- `departamento` VARCHAR(50): Área operativa a la que pertenece el empleado.

### [CATEGORIA]

- `id_categoria` (PK): Identificador único de la categoría.
- `nombre` VARCHAR(100): Nombre de la categoría comercial.
- `descripcion` TEXT: Descripción opcional de la categoría.

### [PRODUCTO]

- `id_producto` INT (PK): Identificador único del producto.
- `id_categoria` INT (FK): Referencia a la categoría a la que pertenece el producto.
- `nombre` VARCHAR(150): Denominación comercial del artículo.
- `descripcion` TEXT: Información descriptiva y características del producto.
- `precio_base` DECIMAL(10,2): Precio de referencia del producto.
- `tabla_medidas_url` VARCHAR(255): Enlace a la tabla de medidas del producto, de acuerdo con RF-11.
- `estado_activo` BOOLEAN: Indica si el producto está habilitado en el catálogo.

### [VARIANTE_PRODUCTO]

- `sku` VARCHAR(50) (PK) Código alfanumérico único que identifica la variante del producto.
- `id_producto` INT (FK): Referencia al producto al que pertenece la variante.
- `talle` VARCHAR(20): Talle correspondiente a la variante.
- `color` VARCHAR(50): Color correspondiente a la variante.
- `stock` INT: Cantidad de unidades disponibles para la venta, de acuerdo con RF-13.

### [PROVEEDOR]

- `id_proveedor` INT (PK): Identificador único del proveedor.
- `razon_social` VARCHAR(150): Denominación legal de la empresa proveedora.
- `cuit` VARCHAR(20): Clave Única de Identificación Tributaria del proveedor.
- `estado_activo` BOOLEAN: Indica si el proveedor se encuentra habilitado.

### [PRODUCTO_PROVEEDOR]

- `id_producto` INT (PK, FK): Referencia al producto asociado al proveedor.
- `id_proveedor` INT (PK, FK): Referencia al proveedor asociado al producto.

- La combinación de `id_producto` e `id_proveedor` constituye una clave primaria compuesta.

### [INGRESO_STOCK]

- `id_ingreso` INT (PK): Identificador único del ingreso de mercadería.
- `dni_empleado` VARCHAR(20) (FK): Identifica al empleado responsable del ingreso.
- `id_proveedor` INT (FK): Identifica al proveedor que realizó el envío.
- `fecha_ingreso` DATETIME: Fecha y hora en la que se procesó el ingreso.

### [CARRITO]

- `id_carrito` INT (PK): Identificador único del carrito.
- `dni_cliente` VARCHAR(20) (FK): Referencia al cliente propietario del carrito.
- `fecha_actualizacion` DATETIME: Fecha y hora de la última modificación del carrito, utilizada para controlar la inactividad de 3 horas.

### [DETALLE_CARRITO]

- `id_detalle_carrito` INT (PK): Identificador único de cada línea del carrito.
- `id_carrito` INT (FK): Referencia al carrito al que pertenece el detalle.
- `sku` VARCHAR(50) (FK): Referencia a la variante de producto seleccionada.
- `cantidad` INT: Cantidad de unidades agregadas temporalmente al carrito.

### [PEDIDO]

- `id_pedido` INT (PK): Identificador único de la orden de compra.
- `dni_cliente` VARCHAR(20) (FK): Referencia al cliente que realizó el pedido.
- `fecha_pedido` DATETIME: Fecha y hora correspondiente al inicio del checkout.
- `estado_pedido` VARCHAR(50): Estado operativo del pedido, por ejemplo Pendiente, Aprobado, Listo para retirar o Despachado.
- `tipo_entrega` VARCHAR(50): Modalidad seleccionada, como Envío a domicilio o Retiro en sucursal.
- `costo_envio` DECIMAL(10,2): Importe correspondiente al costo del envío.
- `monto_total` DECIMAL(10,2): Importe total de la operación.
- `id_transaccion_mp` VARCHAR(100): Identificador de la transacción generada por Mercado Pago.
- `estado_pago` VARCHAR(50): Estado informado por el procesador de pagos.
- `numero_seguimiento` VARCHAR(100): Código utilizado para realizar el seguimiento del envío.
- `fecha_vencimiento_retiro` DATETIME: Fecha límite para retirar el pedido en sucursal, de acuerdo con RF-29.

### [DETALLE_PEDIDO]

- `id_detalle_pedido` INT (PK): Identificador único de cada línea del pedido.
- `id_pedido` INT (FK): Referencia al pedido al que pertenece el detalle.
- `sku` VARCHAR(50) (FK): Referencia a la variante de producto vendida.
- `cantidad` INT: Cantidad de unidades adquiridas.
- `precio_unitario` DECIMAL(10,2): Precio de la variante al momento de realizar la compra.

## Decisiones de diseño

_Justificar al menos dos decisiones de diseño relevantes: por qué se modeló de esa manera,
qué alternativas se consideraron y por qué se descartaron._

### Decisión 1 — [Identificación Principal basada en DNI y Herencia (USUARIO -> CLIENTE / EMPLEADO)]

Decisión

Usar el DNI como la clave principal (PK) en USUARIO y reutilizar ese mismo DNI para identificar a CLIENTE y EMPLEADO.

Justificación

El DNI ya es un número único que identifica a cada persona en la vida real. Usarlo en todas las tablas evita inventar números de ID artificiales (como id_cliente o id_empleado) y simplifica la búsqueda de usuarios.

Alternativa descartada

Crear un ID autoincremental distinto para cada tabla. Se descartó porque agregaba números innecesarios cuando el DNI ya cumple perfectamente esa función.

### Decisión 2 — [Uso del SKU como Clave Primaria en VARIANTE_PRODUCTO]

Decisión

Guardar la cantidad de stock en la tabla VARIANTE_PRODUCTO (asociada a un talle y color específicos) en lugar de guardarlo en la tabla general PRODUCTO. Además, usarmos el código sku como identificador principal de la variante.

Justificación

Nadie compra una "Remera" en abstracto; la gente compra una remera Talle M, Color Negro. Si pusiéramos el stock en el producto general, no sabríamos si nos quedamos sin talle M o sin talle S. El stock tiene que estar donde está la prenda física real.

Alternativa descartada

Poner el stock en la tabla PRODUCTO. Se descartó porque haría imposible saber qué talles o colores específicos quedan en el depósito.

### Decisión 3 — [Integración Directa de Metadatos Transaccionales y Logísticos en PEDIDO]

Decisión

Incluir la información de Mercado Pago (id_transaccion_mp, estado_pago) y del envío (numero_seguimiento, fecha_vencimiento_retiro) directamente como campos de la tabla PEDIDO.

Justificación

Cada pedido tiene un solo pago y un solo envío. Guardar todo en la misma tabla hace que consultar el estado de una compra sea mucho más rápido y no requiera juntar múltiples tablas complejas.

Alternativa descartada

Crear tablas separadas llamadas PAGO y ENVIO. Se descartó porque complicaba el sistema sin aportar ningún beneficio real para este tipo de negocio.

### Decisión 4 — [Congelamiento de Importe Histórico en DETALLE_PEDIDO]

Decisión

Guardar el precio_unitario de la prenda dentro de DETALLE_PEDIDO al momento exacto en que el cliente realiza la compra.

Justificación

Los precios de la tienda cambian con el tiempo (por aumentos o promociones). Si no guardamos el precio al que se vendió en su momento, cuando el cliente revise un pedido viejo el sistema mostraría el precio actual, alterando el historial de lo que realmente pagó.

Alternativa descartada

Leer siempre el precio desde la tabla PRODUCTO. Se descartó porque arruinaría la contabilidad y el historial de compras pasadas.