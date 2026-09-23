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

- `id_xxx` (PK): 
- `atributo`: 

### [CLIENTE]

- `id_xxx` (PK): 
- `atributo`: 

### [EMPLEADO]

- `id_xxx` (PK): 
- `atributo`: 

### [CATEGORIA]

- `id_xxx` (PK): 
- `atributo`: 

### [PRODUCTO]

- `id_xxx` (PK): 
- `atributo`: 

### [VARIANTE_PRODUCTO]

- `id_xxx` (PK): 
- `atributo`: 

### [PROVEEDOR]

- `id_xxx` (PK): 
- `atributo`: 

### [PRODUCTO_PROVEEDOR]

- `id_xxx` (PK): 
- `atributo`: 

### [INGRESO_STOCK]

- `id_xxx` (PK): 
- `atributo`: 

### [CARRITO]

- `id_xxx` (PK): 
- `atributo`: 

### [DETALLE_CARRITO]

- `id_xxx` (PK): 
- `atributo`: 

### [PEDIDO]

- `id_xxx` (PK): 
- `atributo`: 

### [DETALLE_PEDIDO]

- `id_xxx` (PK): 
- `atributo`: 

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
