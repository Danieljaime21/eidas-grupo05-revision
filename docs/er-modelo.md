# Modelo Entidad-Relación

## Diagrama

_Incluir el código PlantUML en `diagramas/er.puml`._
_Visualizar en [plantuml.com](https://www.plantuml.com/plantuml/uml/)._

## Entidades

| Entidad | Descripción | Relaciones clave |
|---------|-------------|-----------------|
|USUARIO |Entidad padre/base que centraliza la autenticación, credenciales de acceso y control de seguridad global de la plataforma, tanto para clientes como para el personal interno. |Relación 1:1 de herencia con CLIENTE y EMPLEADO (a través de id_usuario). |
| CLIENTE| Entidad especializada que extiende a USUARIO (1:1) para almacenar la información de contacto y entrega de los compradores del e-commerce.| Relación 1:1 de especialización con USUARIO. Relación 1:1 con CARRITO. Relación 1:N con PEDIDO.|
| EMPLEADO| Entidad especializada que extiende a USUARIO (1:1) para almacenar los datos operativos e identificación interna del personal administrativo o de depósito. | Relación 1:1 de especialización con USUARIO. Relación 1:N con INGRESO_STOCK (para auditoría de reposiciones de mercadería).|
|CATEGORIA|Estructura la clasificación taxonómica y jerárquica de los artículos del catálogo.|Relación 1:N con PRODUCTO. |
|PRODUCTO|Agrupa la información conceptual, comercial y descriptiva general de un modelo publicado en la tienda. |Relación N:1 con CATEGORIA. Relación 1:N con VARIANTE_PRODUCTO. Relación N:M con PROVEEDOR (vía PRODUCTO_PROVEEDOR).|
|VARIANTE_PRODUCTO|Modela la existencia física individual categorizada por talle y color para permitir el control estricto de inventario unificado. |Relación N:1 con PRODUCTO. Relación 1:N con DETALLE_CARRITO y DETALLE_PEDIDO.|
|PROVEEDOR|Registra la información comercial, identificación fiscal y datos de contacto de las firmas abastecedoras. |Relación N:M con PRODUCTO (vía PRODUCTO_PROVEEDOR). Relación 1:N con INGRESO_STOCK. |
|PRODUCTO_PROVEEDOR|Tabla intermedia que resuelve la asociación N:M entre los modelos de productos y sus respectivos abastecedores. | Relación N:1 con PRODUCTO y N:1 con PROVEEDOR.|
|INGRESO_STOCK|Entidad de trazabilidad y auditoría que registra los ingresos o reposiciones de mercadería enviadas por proveedores e ingresadas por el personal de depósito. |Relación N:1 con EMPLEADO y N:1 con PROVEEDOR. |
|CARRITO|Mantiene el estado de la sesión activa de compra temporal del cliente. |Relación 1:1 con CLIENTE. Relación 1:N con DETALLE_CARRITO.|
|DETALLE_CARRITO|Especifica los ítems y cantidades de variantes seleccionados temporalmente por el cliente. |Relación N:1 con CARRITO y N:1 con VARIANTE_PRODUCTO. |
|PEDIDO|Centraliza la transacción comercial concretada, consolidando el estado del pago, el monto y la modalidad logística acordada |Relación N:1 con CLIENTE. Relación 1:N con DETALLE_PEDIDO.|
|DETALLE_PEDIDO|Registra los renglones definitivos de una orden comercial concretada, congelando los valores históricos.| Relación N:1 con PEDIDO y N:1 con VARIANTE_PRODUCTO.|

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

### Decisión 1 — [Título]

### Decisión 2 — [Título]
