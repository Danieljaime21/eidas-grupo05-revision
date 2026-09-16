# Casos de uso

## Diagrama general

_Incluir el código PlantUML en `diagramas/casos-de-uso.puml`._
_Visualizar en [plantuml.com](https://www.plantuml.com/plantuml/uml/)._

_Describir brevemente los actores identificados y las relaciones principales (include, extend)._

---

## CU-01 — [Nombre]

| Campo | Detalle |
|-------|---------|
| Identificador | CU-01 |
| Nombre |Registro y Autenticación de Cliente |
| Descripción |El cliente completa el formulario con sus datos personales para crear una cuenta e iniciar sesión en la plataforma, habilitando la navegación personalizada y el acceso obligatorio al paso de compra. |
| Actores | Principal: Cliente/ Secundario: Sistema |
| Precondiciones |- El cliente se encuentra navegando en la plataforma. - El cliente no cuenta con una sesión activa. |
| Postcondiciones | Éxito:La cuenta del cliente queda registrada con la contraseña cifrada, la sesión se inicia automáticamente y el usuario accede a sus funciones privadas. / Fallo: El registro no se realiza, la sesión no se inicia y se informa al cliente el motivo del error. |

### Secuencia normal

| # | Acción (actor) | Reacción (sistema) |
|---|----------------|--------------------|
| 1 | El cliente selecciona la opción "Registrarse" o es redirigido desde el flujo de checkout.| El sistema muestra el formulario de registro solicitando todos los datos obligatorios(nombre, apellido, email, fecha de nacimiento, teléfono, DNI, contraseña, dirección, CP, ciudad, provincia).|
| 2 | El cliente completa los campos solicitados y selecciona "Crear Cuenta".| El sistema valida la estructura del email y DNI, verifica que no existan previamente en la base de datos (RF-06) y cifra la contraseña de forma segura.|
| 3 | El cliente confirma el registro. |El sistema crea la cuenta de usuario, inicia la sesión automáticamente y muestra un mensaje de confirmación de registro exitoso.|

### Excepciones

| # | Situación | Respuesta del sistema |
|---|-----------|-----------------------|
| E1 | El cliente intenta registrarse omitiendo campos obligatorios o con datos con formato inválido.| El sistema no completará el registro, resaltará los campos con error y mostrará un mensaje indicando las correcciones requeridas (RNF-10) |
| E2 | El cliente intenta registrarse con un correo electrónico o DNI previamente existente. | El sistema informará que el usuario ya existe y ofrecerá opciones directas para iniciar sesión o recuperar la contraseña.|
| E3 | El cliente intenta finalizar una compra sin haber iniciado sesión. |El sistema interrumpe el checkout, exige el registro o inicio de sesión obligatorio (RF-10) y, tras completarse con éxito, redirige al cliente a la confirmación de su pedido. | 
| E4 | Se produce un error de conexión o servidor durante el proceso. | El sistema informa que no fue posible procesar la solicitud y mantiene el formulario con los datos ingresados para reintentar. |

| Campo | Detalle |
|-------|---------|
| Rendimiento |El sistema procesará las solicitudes de registro e inicio de sesión en un máximo de 3 segundos (RNF-01). |
| Frecuencia |Se estima una media de 50 a 100 ejecuciones diarias. |
| Importancia |Vital |
| Urgencia |Inmediatamente |

---

## CU-02 — [Nombre]

| Campo | Detalle |
|-------|---------|
| Identificador | CU-02 |
| Nombre |Gestionar Productos y Variantes |
| Descripción |El dueño crea nuevos productos con sus variantes de talle y color, modifica sus características e imágenes o desactiva productos/variantes para administrar el catálogo disponible en la tienda. |
| Actores | Principal: Dueño / Secundario: Sistema |
| Precondiciones |- El dueño se encuentra autenticado en el panel de administración con los permisos del rol correspondientes (RF-05, RF-12). - El catálogo se encuentra disponible. |
| Postcondiciones | Éxito: El producto o variante queda creado, modificado o desactivado en la base de datos y los cambios se reflejan inmediatamente en el catálogo público. / Fallo: El producto no se crea, modifica ni desactiva y se informa al dueño el motivo del error. |

### Secuencia normal

| # | Acción (actor) | Reacción (sistema) |
|---|----------------|--------------------|
| 1 | El dueño ingresa a la sección "Gestión de Productos" en el panel de administración. | El sistema muestra el listado de productos registrados y habilita la opción "Crear Producto".|
| 2 | El dueño selecciona "Crear Producto" o elige un producto existente para "Modificar". | El sistema despliega el formulario solicitando datos del producto (nombre, descripción, precio, categoría, tabla de medidas y carga de 2 a 4 fotos) junto con la gestión de sus variantes (talle, color y stock unificado).|
| 3 | El dueño completa o edita los datos, asigna las variantes correspondientes y selecciona "Guardar". | El sistema comprueba que los datos sean válidos y que la cantidad de fotos esté entre 2 y 4 (RF-11), comprime las imágenes a un tamaño menor a 300 KB (RNF-14) y guarda la información.|
| 4 | El dueño selecciona "Desactivar" sobre un producto o variante activa. | El sistema solicita confirmación, cambia el estado a inactivo y actualiza el catálogo público para ocultar el elemento sin perder su historial.|

### Excepciones

| # | Situación | Respuesta del sistema |
|---|-----------|-----------------------|
| E1 | El dueño intenta guardar un producto omitiendo campos obligatorios o con valores numéricos inválidos. | El sistema no guardará los cambios, resaltará los campos con error y mostrará un mensaje indicando las correcciones necesarias (RNF-10). |
| E2 | El dueño intenta guardar un producto con menos de 2 o más de 4 fotografías. | El sistema notifica que se deben subir entre 2 y 4 imágenes por producto y detiene el proceso de guardado (RF-11). |
| E3 | Se produce un error durante la compresión o carga de imágenes en el servidor. | El sistema informa que no fue posible guardar el producto y mantiene el formulario cargado para reintentar. |

| Campo | Detalle |
|-------|---------|
| Rendimiento |Las consultas a la base de datos para mostrar y modificar productos y stock responderán en menos de 2 segundos (RNF-13). |
| Frecuencia |Se estima una media de 10 a 20 ejecuciones diarias. |
| Importancia |Vital |
| Urgencia |Inmediatamente |

---

## CU-03 — [Nombre]

| Campo | Detalle |
|-------|---------|
| Identificador | CU-03 |
| Nombre |Gestionar carrito de compras |
| Descripción |El cliente agrega productos al carrito, modifica cantidades, elimina productos o vacía el carrito para organizar su compra antes de realizar el checkout. |
| Actores | Principal: Cliente / Secundario: Sistema |
| Precondiciones |- El catálogo se encuentra disponible. - Existe al menos un producto disponible para agregar al carrito. - El cliente se encuentra navegando el catálogo. |
| Postcondiciones | Éxito: El carrito queda actualizado con los productos, cantidades y subtotales correspondientes. Si el cliente elimina productos o vacía el carrito, los cambios quedan registrados en el carrito. / Fallo: El carrito no se modifica y se informa al cliente el motivo del error. |

### Secuencia normal

| # | Acción (actor) | Reacción (sistema) |
|---|----------------|--------------------|
| 1 | El cliente selecciona un producto del catálogo. | El sistema muestra la información del producto, sus variantes disponibles y la opción de agregarlo al carrito.|
| 2 | El cliente selecciona cantidad, talle, color y selecciona "Agregar al carrito". | El sistema valida que exista stock para la combinación producto-talle-color (RF-13), agrega el producto y actualiza el carrito. Muestra mensaje de confirmación.|
| 3 | El cliente consulta el carrito. | El sistema muestra los productos con sus cantidades, precios unitarios y subtotales.|
| 4 | El cliente modifica la cantidad de un producto. | El sistema valida el stock disponible, actualiza la cantidad y recalcula el subtotal.|
| 5 | El cliente elimina un producto. | El sistema elimina el producto y actualiza el carrito.|
| 6 | El cliente selecciona "Vaciar carrito". | El sistema solicita confirmación. (Si el cliente cancela el vaciado, el sistema deberá mantener el carrito sin cambios).|
| 7 | El cliente confirma el vaciado. | El sistema elimina todos los productos y muestra el carrito vacío.|

### Excepciones

| # | Situación | Respuesta del sistema |
|---|-----------|-----------------------|
| E1 | El cliente intenta agregar un producto sin seleccionar talle o color. | El sistema no agregará el producto y deberá mostrar un mensaje de error indicando que debe seleccionar talle y color (RNF-10). |
| E2 | El cliente intenta agregar una cantidad mayor al stock disponible. | El sistema muestra un mensaje indicando que la cantidad solicitada no está disponible y no permite agregar esa cantidad. |
| E3 | El cliente intenta agregar un producto sin stock. | El sistema deberá informar que el producto no está disponible y no podrá agregarlo al carrito. |
| E4 | Se produce un error al actualizar el carrito. | El sistema informa que no fue posible actualizar el carrito y mantiene su estado anterior. |

| Campo | Detalle |
|-------|---------|
| Rendimiento |El sistema deberá realizar las acciones descritas en los pasos 1 al 7 en un máximo de 3 segundos (RNF-01). |
| Frecuencia |Se espera que este caso de uso se lleve a cabo una media de 100 veces al día. |
| Importancia |Vital |
| Urgencia |Inmediatamente |

---

## CU-04 — [Nombre]

| Campo | Detalle |
|-------|---------|
| Identificador | CU-04 |
| Nombre |Realizar checkout con datos de entrega y de envío |
| Descripción |El cliente confirma o edita sus datos de entrega, selecciona la modalidad de despacho (envío a domicilio o retiro en el local) y obtiene el costo correspondiente para continuar con la compra. |
| Actores | Principal: Cliente / Secundario: Sistema |
| Precondiciones |- El cliente debe haber iniciado sesión en la plataforma. - El carrito de compras debe contener al menos un producto. - Los productos seleccionados están disponibles. |
| Postcondiciones | Éxito: Los datos de entrega quedan confirmados, el tipo de entrega queda seleccionado, el costo de envío queda calculated cuando corresponde y el checkout queda listo para continuar con el pago. / Fallo: El pedido no avanza al siguiente paso, la información de envío no se guarda y el pedido se mantiene sin cambios en el carrito de compras. |

### Secuencia normal

| # | Acción (actor) | Reacción (sistema) |
|---|----------------|--------------------|
| 1 | El cliente hace click en "Finalizar Compra" desde la pantalla del carrito de compras. | El sistema muestra el resumen del carrito con los datos precargados del cliente.|
| 2 | El cliente confirma o modifica los datos de contacto y la dirección de entrega predeterminada (calle, número, piso/dpto, ciudad, provincia, código postal). | El sistema valida que los campos requeridos estén completos.|
| 3 | El cliente selecciona la opción "Envío a domicilio" (o "Retiro en local"). | El sistema calcula y muestra el costo de envío correspondiente según proveedor logístico y actualiza el total final (Subtotal + Envío). Si elige retiro en local, fija el costo en $0.00, muestra dirección e informa plazo de 15 días.|
| 4 | El cliente presiona el botón "Continuar al pago". | El sistema guarda la información de entrega asociada al pedido en estado borrador y redirige al usuario a la pasarela de pago.|

### Excepciones

| # | Situación | Respuesta del sistema |
|---|-----------|-----------------------|
| E1 | El cliente intenta avanzar dejando campos obligatorios vacíos (dirección, ciudad, código postal o teléfono). | El sistema deberá impedir el avance e indicar el campo que contiene el error o que debe completarse. |
| E2 | El cliente no está autenticado. | El sistema deberá redirigirlo al inicio de sesión o registro (RF-10). |
| E3 | El cliente ingresa un código postal no cubierto o inválido. | El sistema deberá notificar que no hay cobertura de envío a domicilio para esa zona y sugerir la opción de retiro en local o corrección de datos. |
| E4 | Falla el servicio del proveedor logístico al consultar la tarifa. | El sistema deberá calcular la tarifa base de respaldo o solicitar reintentar el cálculo sin perder la información cargada. |

| Campo | Detalle |
|-------|---------|
| Rendimiento |El sistema deberá realizar las acciones descritas en los pasos 1 al 4 en un máximo de 5 segundos. |
| Frecuencia |Este caso de uso se espera que se lleve a cabo una media de 50 veces al día. |
| Importancia |Vital |
| Urgencia |Inmediatamente |

---

## CU-05 — [Nombre]

| Campo | Detalle |
|-------|---------|
| Identificador | CU-05 |
| Nombre |Procesar pago con Mercado Pago |
| Descripción |El cliente realiza el pago de su compra mediante tarjeta de crédito o débito a través de Mercado Pago. |
| Actores | Principal: Cliente / Secundario: Sistema, Mercado Pago (pasarela de pago) |
| Precondiciones |- El cliente completó el checkout. - Existe un importe a pagar. - Mercado Pago se encuentra disponible. |
| Postcondiciones | Éxito: El pago queda registrado con estado, fecha, importe y medio de pago. El pedido queda en estado "pagado". / Fallo: El pago es rechazado, el pedido permanece "pendiente de pago" y se informa al cliente. |

### Secuencia normal

| # | Acción (actor) | Reacción (sistema) |
|---|----------------|--------------------|
| 1 | El cliente selecciona "Pagar con Mercado Pago". | El sistema redirige a la pasarela de Mercado Pago.|
| 2 | El cliente selecciona tarjeta de crédito o débito e ingresa los datos solicitados. | Mercado Pago procesa la operación.|
| 3 | Mercado Pago devuelve el resultado de la transacción. | El sistema registra estado, fecha, importe y medio de pago (RF-22).|
| 4 | Mercado Pago informa el resultado aprobado. | El sistema actualiza el pedido a estado "pagado" y notifica al cliente por email (RF-23).|

### Excepciones

| # | Situación | Respuesta del sistema |
|---|-----------|-----------------------|
| E1 | Mercado Pago no está disponible. | El sistema deberá mostrar un mensaje de error indicando que el servicio de pago no está disponible temporalmente. |
| E2 | Mercado Pago rechaza el pago. | El sistema informa al cliente que el pago fue rechazado y el pedido no pasa a "pagado". |

| Campo | Detalle |
|-------|---------|
| Rendimiento |El sistema deberá completar el flujo de pago en un máximo de 5 segundos, sin contar el tiempo de respuesta de Mercado Pago (RNF-02). |
| Frecuencia |Se espera que este caso de uso se lleve a cabo una media de 70 veces al día. |
| Importancia |Vital |
| Urgencia |Inmediatamente |

---

## CU-06 — [Nombre]

| Campo | Detalle |
|-------|---------|
| Identificador | CU-06 |
| Nombre |Consultar seguimiento del pedido |
| Descripción |El cliente consulta desde "Mi Cuenta" el estado y el número de seguimiento de un pedido con envío a domicilio, para conocer el estado de su entrega. |
| Actores | Principal: Cliente / Secundario: Sistema, proveedor logístico |
| Precondiciones |- El cliente está registrado y autenticado. - El cliente tiene un pedido con envío a domicilio. - El pedido fue pagado. - El pedido tiene un número de seguimiento informado por el proveedor logístico. |
| Postcondiciones | Éxito: El cliente puede consultar el estado de su pedido, visualizar el número de seguimiento y la información del seguimiento queda asociada al pedido. / Fallo: El estado del pedido no se modifica y el sistema informa al cliente que la información de seguimiento no está disponible. |

### Secuencia normal

| # | Acción (actor) | Reacción (sistema) |
|---|----------------|--------------------|
| 1 | El cliente ingresa a "Mis pedidos". | El sistema muestra sus pedidos.|
| 2 | El cliente selecciona un pedido. | El sistema muestra los datos del pedido y la opción de "Seguimiento detallado". (Si no posee envío a domicilio o el seguimiento no está disponible, el sistema lo informa).|
| 3 | El cliente consulta seguimiento detallado. | El sistema obtiene y muestra el número de seguimiento con la información actualizada del proveedor logístico (Estado del envío: "En preparación", "En camino", "Recibido").|

### Excepciones

| # | Situación | Respuesta del sistema |
|---|-----------|-----------------------|
| E1 | El proveedor logístico no está disponible temporalmente. | El sistema deberá mostrar un mensaje de error indicando que no se puede obtener el seguimiento en este momento. |
| E2 | El pedido todavía no posee un número de seguimiento registrado. | El sistema informará que todavía no se encuentra disponible. |

| Campo | Detalle |
|-------|---------|
| Rendimiento |La consulta de la información del pedido desde "Mis pedidos" deberá responder en un máximo de 3 segundos. |
| Frecuencia |Se espera que este caso de uso se lleve a cabo una media de 50 veces al día. |
| Importancia |Importante |
| Urgencia |Hay presión |
