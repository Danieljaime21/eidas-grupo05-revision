# Casos de uso

## Diagrama general

_Incluir el código PlantUML en `diagramas/casos-de-uso.puml`._
_Visualizar en [plantuml.com](https://www.plantuml.com/plantuml/uml/)._

## Actores
| Actor | Tipo | Descripción |
|-------|------|-------------|
| Visitante | Principal | Persona no autenticada que navega el catálogo, puede armar un carrito y decide registrarse para concretar la compra. |
| Cliente | Principal | Usuario registrado y autenticado. Hereda las capacidades del Visitante y suma las funcionalidades de checkout, envío y pago, seguimiento de pedidos y devoluciones. |
| Dueño | Principal | Usuario con máximos privilegios. Administra el personal y el catálogo de productos. |
| Empleado | Principal | Usuario del personal operativo del local. Registra las ventas presenciales descontando stock compartido con las ventas online, gestiona las devoluciones y los retiros en el local. |
| Proveedor Logístico | Secundario (externo) | Sistema externo que calcula la tarifa de envío, confirma cobertura e informa el número de seguimiento. |
| Mercado Pago | Secundario (externo) | Pasarela de pago externa que procesa la transacción. |

## Casos de uso por módulo

| Módulo (requisitos) | Casos de uso |
|---------------------|--------------|
| 1 — Usuarios y Clientes | CU-01 Registrar cliente · CU-02 Iniciar sesión (cliente) · CU-03 Registrar usuario del personal |
| 2 — Productos, Stock y Proveedores | CU-04 Consultar catálogo · CU-05 Agregar producto al catálogo · CU-11 Registrar venta presencial · CU-16 Verificar stock disponible |
| 3 — Carrito, Pedidos y Promociones | CU-06 Agregar productos al carrito · CU-07 Modificar cantidad o eliminar producto del carrito · CU-08 Vaciar carrito de compras · CU-09 Realizar verificación con datos de entrega y de envío · CU-10 Realizar pago · CU-12 Consultar estado y seguimiento de pedidos |
| 4 — Envíos y Devoluciones | CU-13 Solicitar devolución · CU-14 Gestionar solicitud de devolución · CU-15 Gestionar retiro en el local |
| 5 — Reportes y Panel de Administración | Sin casos de uso desarrollados (corresponden a HU-09, HU-10 y HU-11). |

## Relaciones `<<include>>` (obligatorias)

_`<<include>>` significa que el caso de uso base **siempre** ejecuta al caso incluido, como un paso propio. Lo que ocurre "antes" es una precondición, no un include._

| Caso origen | Caso incluido | Justificación |
|-------------|---------------|---------------|
| CU-06 Agregar productos al carrito | CU-16 Verificar stock disponible | Toda vez que se agrega un producto al carrito, el sistema ejecuta la verificación de stock como parte de su paso 2. |
| CU-11 Registrar venta presencial | CU-16 Verificar stock disponible | Toda vez que el empleado agrega una prenda a la venta, el sistema ejecuta la misma verificación sobre el stock unificado (RF-20) en su paso 2. |

CU-07 (Modificar cantidad o eliminar producto) también verifica el stock, pero solo cuando se aumenta una cantidad y no al eliminar un producto; por eso no se modela como `<<include>>`.
---


## Relaciones `<<extend>>` (opcionales /condicionales )

_`<<extend>>` significa que el caso de uso de la flecha agrega, solo bajo una condición, un comportamiento al caso base. La flecha va del caso que extiende hacia el caso base._

| Caso que extiende | Caso base | Condición y justificación |
|-------------------|-----------|---------------------------|
| CU-02 Iniciar sesión (cliente) | CU-09 Realizar verificación con datos de entrega y de envío | Solo si quien hace el checkout es un Visitante sin sesión iniciada: debe iniciar sesión para continuar. Un Cliente ya autenticado no ejecuta CU-02 durante el checkout (RF-12). |
| CU-01 Registrar cliente | CU-09 Realizar verificación con datos de entrega y de envío | Solo si el Visitante no tiene cuenta: se le ofrece registrarse en ese momento y su carrito se conserva (RF-12). |

---


## CU-01 — Registrar cliente

| Campo | Detalle |
|-------|---------|
| Identificador | CU-01 |
| Nombre | Registrar cliente |
| Descripción | El Visitante se registra en el sistema cargando sus datos personales para obtener una cuenta de Cliente que le permita comprar y consultar sus pedidos. |
| Actores | Principal: Visitante |
| Precondiciones | El visitante no tiene una sesión iniciada. |
| Postcondiciones | Éxito: Se crea una cuenta de Cliente habilitada. El nuevo cliente puede iniciar sesión. Si el visitante llegó desde la finalización de una compra, el contenido de su carrito se conserva (RF-12). |

### Secuencia normal

| # | Acción (actor) | Reacción (sistema) |
|---|----------------|--------------------|
| 1 | El visitante selecciona la opción "Registrarse". | El sistema solicita la identificación inicial pidiendo únicamente el número de DNI. |
| 2 | Ingresa su DNI y presiona "Continuar". | El sistema valida el formato del DNI y verifica que no exista previamente en la base de datos. Al no existir, habilita y muestra el formulario completo con los campos restantes: nombre, apellido, email, fecha de nacimiento, teléfono, contraseña, dirección, CP, ciudad, provincia. |
| 3 | El visitante completa los datos restantes y confirma el registro. | El sistema valida que los datos estén completos y tengan un formato válido, y que el email no esté registrado. |
| 4 | El visitante confirma el registro. | El sistema crea la cuenta de cliente, muestra un mensaje de confirmación de registro exitoso. |

### Excepciones

| # | Situación | Respuesta del sistema |
|---|-----------|-----------------------|
| E1 | El visitante intenta registrarse omitiendo campos obligatorios o con datos con formato inválido. | El sistema no completará el registro, resaltará los campos con error y mostrará un mensaje indicando las correcciones requeridas (RNF-10). |
| E2 | El visitante intenta registrarse con un DNI previamente existente. | El sistema informará que el usuario ya existe y ofrecerá opciones directas para iniciar sesión o recuperar la contraseña. |
| E3 | Se produce un error de conexión o servidor durante el proceso. | El sistema informa que no fue posible procesar la solicitud y mantiene el formulario con los datos ingresados para reintentar. |

| Campo | Detalle |
|-------|---------|
| Rendimiento | El sistema procesará las solicitudes de registro en un máximo de 3 segundos (RNF-01). |
| Frecuencia | Este caso de uso se espera que se lleve a cabo una media de 40 veces al día. |
| Importancia | Vital |
| Urgencia | Inmediatamente |

---

## CU-02 — Iniciar sesión (cliente)

| Campo | Detalle |
|-------|---------|
| Identificador | CU-02 |
| Nombre | Iniciar sesión (cliente) |
| Descripción | El Cliente ingresa su email y contraseña para acceder a su cuenta y a las funcionalidades correspondientes a su rol. |
| Actores | Principal: Cliente |
| Precondiciones | El cliente posee una cuenta habilitada. |
| Postcondiciones | Éxito: El cliente queda autenticado. |

### Secuencia normal

| # | Acción (actor) | Reacción (sistema) |
|---|----------------|--------------------|
| 1 | El cliente selecciona la opción "Iniciar sesión". | El sistema muestra el formulario con los campos email y contraseña. |
| 2 | Ingresa su email y contraseña y confirma. | Verifica que la cuenta exista y que la contraseña sea correcta. |
| 3 | | Inicia la sesión y redirige al cliente a la pantalla principal de la tienda. |

### Excepciones

| # | Situación | Respuesta del sistema |
|---|-----------|-----------------------|
| E1 | El email o la contraseña son incorrectos. | El sistema deberá informar que las credenciales son inválidas (sin indicar cuál de los dos datos falló), sumar un intento fallido y volver al paso 1. Si acumula 5 intentos fallidos de inicio de sesión, el sistema deberá bloquear su acceso durante 15 minutos e informárselo (RNF-07). |
| E2 | El email ingresado no se encuentra registrado en el sistema. | El sistema responde igual que en E1 (credenciales inválidas, sin indicar cuál de los datos falló) para no revelar qué emails existen, y la pantalla ofrece siempre el enlace "Crear cuenta" (CU-01). |

| Campo | Detalle |
|-------|---------|
| Rendimiento | El sistema deberá realizar las acciones descriptas en un máximo de 3 segundos. |
| Frecuencia | Este caso de uso se espera que se lleve a cabo una media de 100 veces al día. |
| Importancia | Vital. |
| Urgencia | Inmediatamente. |


---


## CU-03 — Registrar usuario del personal

| Campo | Detalle |
|-------|---------|
| Identificador | CU-03 |
| Nombre | Registrar usuario del personal |
| Descripción | El Dueño da de alta a un nuevo usuario del personal y le asigna un rol, para que pueda operar el sistema con los permisos correspondientes. |
| Actores | Principal: Dueño |
| Precondiciones | El Dueño tiene una sesión iniciada. Existe al menos un rol del personal definido. |
| Postcondiciones | Éxito: El usuario del personal queda creado, habilitado y con el rol asignado. |

### Secuencia normal

| # | Acción (actor) | Reacción (sistema) |
|---|----------------|--------------------|
| 1 | Accede a la sección "Personal" y selecciona "Alta de usuario". | El sistema solicita la identificación del empleado pidiendo únicamente el número de DNI. |
| 2 | Ingresa el DNI del empleado y presiona "Continuar". | El sistema valida el formato del DNI y verifica que no pertenezca a un usuario existente. Al no existir, habilita el formulario con los campos restantes (nombre, apellido, email, teléfono, etc.) y la lista de roles disponibles. |
| 3 | Completa los datos personales restantes, selecciona el rol correspondiente y confirma. | Valida la estructura de los datos (email, teléfono, etc.) y que el email no esté registrado previamente. Crea el usuario habilitado con el rol asignado y muestra un mensaje de confirmación. |
| 4 | | Actualiza el listado de usuarios del personal, mostrando al nuevo integrante con su rol y estado. |

### Excepciones

| # | Situación | Respuesta del sistema |
|---|-----------|-----------------------|
| E1 | El DNI ya pertenece a un usuario existente. | El sistema muestra un mensaje indicando que el empleado ya existe. |
| E2 | El dueño deja campos obligatorios vacíos o con formato incorrecto. | El sistema indica el campo específico con error y vuelve al paso 3 manteniendo la información ingresada. |
| E3 | El email ingresado pertenece a otro usuario. | El sistema informa el error y permite corregir solo ese campo sin borrar el resto de la información. |
| E4 | Error interno al guardar el usuario. | El sistema deberá informarlo y registrar fecha, hora y descripción del error (RNF-18). |


| Campo | Detalle |
|-------|---------|
| Rendimiento | El sistema deberá realizar las acciones descritas en un máximo de 3 segundos (RNF-01). |
| Frecuencia | Este caso de uso se espera que se lleve a cabo aproximadamente 1 vez cada dos meses. |
| Importancia | Importante |
| Urgencia | Hay presión |

---


## CU-04 — Consultar catálogo

| Campo | Detalle |
|-------|---------|
| Identificador | CU-04 |
| Nombre | Consultar catálogo |
| Descripción | El Visitante o el Cliente consulta el catálogo y lo filtra por categoría, talle y color para encontrar los productos que le interesan. |
| Actores | Principal: Cliente, Visitante |
| Precondiciones | Existen productos activos en el catálogo. |
| Postcondiciones | Éxito: El sistema muestra los productos que cumplen los criterios elegidos. |

### Secuencia normal

| # | Acción (actor) | Reacción (sistema) |
|---|----------------|--------------------|
| 1 | Ingresa a la sección "Catálogo". | El sistema muestra un menú desplegable con las diferentes categorías disponibles. |
| 2 | Selecciona la categoría deseada. | El sistema muestra los primeros 20 productos de esa categoría. |
| 3 | Selecciona uno o más filtros (talle y color; RF-19). | El sistema muestra solo los productos que cumplen todos los filtros seleccionados. |



### Excepciones

| # | Situación | Respuesta del sistema |
|---|-----------|-----------------------|
| E1 | Ningún producto cumple los filtros elegidos. | El sistema deberá mostrar un mensaje indicando que ningún producto cumple con los filtros seleccionados y sugerirá quitar algunos de estos. |
| E2 | Error al consultar el catálogo. | El sistema deberá mostrar un mensaje de error y registrar fecha, hora y descripción del error (RNF-18). |
| E3 | Una operación demora más de 1 segundo. | El sistema deberá mostrar un indicador de carga (RNF-11). |
| E4 | | |


| Campo | Detalle |
|-------|---------|
| Rendimiento | El sistema deberá realizar las acciones descritas en los pasos 1 al 3 en un máximo de 3 segundos con 50 usuarios simultáneos (RNF-01), y las consultas a la base de datos en menos de 2 segundos (RNF-13). |
| Frecuencia | Este caso de uso se espera que se lleve a cabo una media de 200 veces al día. |
| Importancia | Vital |
| Urgencia | Inmediatamente |


---

## CU-05 — Agregar producto al catálogo

| Campo | Detalle |
|-------|---------|
| Identificador | CU-05 |
| Nombre | Agregar producto al catálogo |
| Descripción | El Dueño agrega un nuevo producto al catálogo con sus datos, categoría, talles, colores y fotografías, para ponerlo a disposición de los visitantes y clientes. |
| Actores | Principal: Dueño |
| Precondiciones | El Dueño tiene una sesión iniciada. Existe al menos una categoría activa (RF-18). |
| Postcondiciones | Éxito: El producto queda registrado, activo y asignado a una categoría. El producto tiene entre 2 y 4 fotografías y su tabla de medidas. El producto se muestra en el catálogo. |

### Secuencia normal

| # | Acción (actor) | Reacción (sistema) |
|---|----------------|--------------------|
| 1 | Accede a la sección "Productos" y selecciona "Agregar producto". | El sistema muestra el formulario a llenar con: nombre, descripción, precio, categoría (lista de categorías activas), talles, colores y fotografías. |
| 2 | Completa los datos, elige la categoría, los talles y los colores, adjunta entre 2 y 4 fotografías y confirma. | El sistema valida los datos ingresados. Comprime cada fotografía a menos de 300 KB (RNF-14). Guarda el producto como activo y muestra una confirmación. |
| 3 | | Actualiza el listado de productos y el catálogo con el nuevo producto. |

### Excepciones

| # | Situación | Respuesta del sistema |
|---|-----------|-----------------------|
| E1 | Falta algún dato obligatorio o la cantidad de fotografías no está entre 2 y 4. | El sistema deberá indicar el campo con error y volver al paso 2 (RNF-10). |
| E2 | El archivo adjunto no es una imagen válida. | El sistema deberá indicar que no es una imagen válida y solicitar que se reemplace. |
| E3 | El Dueño cancela la operación. | El sistema deberá descartar los datos y las fotografías cargadas y volver al listado de productos. |
| E4 | Ocurre un error al guardar el producto. | El sistema deberá informarlo, registrar fecha, hora y descripción del error (RNF-18), conservar los datos ingresados y dar la posibilidad de reintentar. |


| Campo | Detalle |
|-------|---------|
| Rendimiento | El sistema deberá realizar la acción descrita en el paso 2 en un máximo de 5 segundos. |
| Frecuencia | Este caso de uso se espera que se lleve a cabo una media de 10 veces al mes. |
| Importancia | Vital |
| Urgencia | Hay presión |

---


## CU-06 — Agregar productos al carrito

| Campo | Detalle |
|-------|---------|
| Identificador | CU-06 |
| Nombre | Agregar productos al carrito |
| Descripción | El Cliente o Visitante elige un producto del catálogo especificando obligatoriamente su talle y color, y lo suma a su carrito de compras. |
| Actores | Principal: Cliente, Visitante |
| Precondiciones | El catálogo de productos está disponible. El producto seleccionado cuenta con stock. |
| Postcondiciones | Éxito: El producto se incorpora al carrito con el talle, color y cantidad elegidos, actualizando la suma total a pagar. Fallo: El producto no se suma al carrito y el sistema le informa el motivo al cliente/visitante. |

### Secuencia normal

| # | Acción (actor) | Reacción (sistema) |
|---|----------------|--------------------|
| 1 | El cliente elige un producto que le gusta del catálogo. | El sistema le muestra la información del producto, los talles y colores disponibles, y la opción para sumarlo al carrito. |
| 2 | El cliente elige el talle, el color y cuántas unidades quiere, y pide agregar el producto al carrito. | El sistema verifica que se hayan seleccionado talle y color (RF-27), valida que haya stock suficiente (RF-20) ejecutando CU-16, guarda el producto en el carrito y le confirma la acción. |

### Excepciones

| # | Situación | Respuesta del sistema |
|---|-----------|-----------------------|
| E1 | El cliente intenta agregar un producto sin elegir el talle o el color. | El sistema no lo deja avanzar y le avisa que tiene que seleccionar talle y color obligatoriamente. |
| E2 | El cliente pide más unidades de las que hay guardadas en el depósito. | El sistema no suma esa cantidad y le avisa que no hay tantas unidades disponibles en stock. |
| E3 | El cliente quiere agregar un producto que no tiene stock. | El sistema le avisa que el producto está agotado y no lo suma al carrito. |
| E4 | Se corta la conexión u ocurre un error al intentar guardar el producto. | El sistema le avisa que no se pudo agregar el producto y deja el carrito como estaba antes del intento. |

| Campo | Detalle |
|-------|---------|
| Rendimiento | Cada paso debe responder al instante, en menos de 3 segundos (RNF-01). |
| Frecuencia | Se calcula que se va a usar unas 100 veces por día. |
| Importancia | Vital. |
| Urgencia | Inmediatamente. |

---


## CU-07 — Modificar cantidad o eliminar producto del carrito

| Campo | Detalle |
|-------|---------|
| Identificador | CU-07 |
| Nombre | Modificar cantidad o eliminar producto del carrito |
| Descripción | El cliente o visitante revisa los productos guardados en su carrito y ajusta la cantidad de unidades de un ítem o lo remueve individualmente de la lista. |
| Actores | Principal: Cliente, Visitante |
| Precondiciones | El cliente tiene al menos un producto guardado en su carrito de compras. |
| Postcondiciones | Éxito: Las cantidades o el listado de productos se actualizan y el sistema recalcula los montos automáticamente. Fallo: El carrito no sufre cambios y se mantiene como estaba antes del intento. |

### Secuencia normal

| # | Acción (actor) | Reacción (sistema) |
|---|----------------|--------------------|
| 1 | El cliente entra a ver su carrito de compras. | El sistema le muestra el listado de productos elegidos con talle, color, precio de cada uno y el total a pagar. |
| 2 | El cliente cambia la cantidad de unidades de uno de los productos de su lista. | El sistema valida si hay stock suficiente para esa nueva cantidad, actualiza el número de productos y vuelve a calcular el total. |
| 3 | El cliente pide quitar un producto que ya no quiere de su lista. | El sistema borra ese producto del carrito y recalcula el monto total. |

### Excepciones

| # | Situación | Respuesta del sistema |
|---|-----------|-----------------------|
| E1 | El cliente intenta aumentar las unidades a un número mayor que el stock disponible en depósito. | El sistema no actualiza la cantidad y le avisa que no hay tantos productos disponibles. |
| E2 | Ocurre un fallo en el sistema o de conexión al intentar actualizar el carrito. | El sistema avisa que no se pudo procesar la modificación y conserva las cantidades anteriores. |

| Campo | Detalle |
|-------|---------|
| Rendimiento | Cada paso debe responder al instante, en menos de 3 segundos (RNF-01). |
| Frecuencia | Estimado de 60 ejecuciones diarias. |
| Importancia | Alta. |
| Urgencia | Inmediata. |

---


## CU-08 — Vaciar carrito de compras

| Campo | Detalle |
|-------|---------|
| Identificador | CU-08 |
| Nombre | Vaciar carrito de compras |
| Descripción | El cliente/visitante elimina de una sola vez la totalidad de los productos almacenados en su carrito de compras. |
| Actores | Principal: Cliente/Visitante |
| Precondiciones | El carrito contiene al menos un producto. |
| Postcondiciones | Éxito: El carrito queda totalmente vacío y el importe total se reinicia en cero. Fallo: El contenido del carrito se conserva intacto. |

### Secuencia normal

| # | Acción (actor) | Reacción (sistema) |
|---|----------------|--------------------|
| 1 | El cliente entra a ver su carrito de compras. | El sistema le muestra la lista de productos acumulados y la suma total. |
| 2 | El cliente solicita vaciar todo el carrito. | El sistema le pide confirmación antes de borrar el contenido para evitar descuidos. |
| 3 | El cliente confirma que desea borrar todo. | El sistema elimina todos los productos guardados y deja la lista vacía con el total en cero. |

### Excepciones

| # | Situación | Respuesta del sistema |
|---|-----------|-----------------------|
| E1 | En el paso 2, el cliente cancela la confirmación de vaciado. | El sistema interrumpe el proceso y mantiene los productos en el carrito tal como estaban. |
| E2 | Ocurre un error de sistema o corte de conexión al intentar vaciar la lista. | El sistema informa que no se pudo vaciar el carrito y mantiene los productos guardados. |

| Campo | Detalle |
|-------|---------|
| Rendimiento | Cada paso debe responder al instante, en menos de 3 segundos (RNF-01). |
| Frecuencia | Estimado de 20 ejecuciones diarias. |
| Importancia | Media. |
| Urgencia | Inmediata. |


---



## CU-09 — Realizar verificación con datos de entrega y de envío

| Campo | Detalle |
|-------|---------|
| Identificador | CU-09 |
| Nombre | Realizar verificación con datos de entrega y de envío |
| Descripción | El cliente confirma o edita sus datos de entrega, elige cómo va a recibir el pedido (envío a domicilio o retiro en el local) y ve el costo correspondiente antes de continuar con el pago. |
| Actores | Principal: Visitante o Cliente. Secundario: Proveedor logístico. |
| Precondiciones | El carrito contiene al menos un producto. Los productos elegidos siguen disponibles. |
| Postcondiciones | Éxito: Los datos de entrega quedan confirmados, el tipo de entrega queda elegido, el costo de envío queda calculado cuando corresponde y el checkout queda listo para continuar con el pago. Fallo: El pedido no avanza, la información de envío no se guarda y el pedido se mantiene sin cambios en el carrito. |

### Secuencia normal

| # | Acción (actor) | Reacción (sistema) |
|---|----------------|--------------------|
| 1 | Hace clic en "Finalizar Compra" desde el carrito. | Muestra el resumen del carrito con los datos del cliente ya cargados. |
| 2 | Confirma o modifica los datos de contacto y la dirección de entrega (calle, número, piso/dpto, ciudad, provincia, código postal). | Valida que los campos obligatorios estén completos. |
| 3 | Elige "Envío a domicilio". | Calcula y muestra el costo de envío según la dirección, y actualiza el total (subtotal + envío). |
| 3.1 | Si en cambio elige "Retiro en local"... | ...fija el costo de envío en $0, muestra la dirección del local y su horario. |

### Excepciones

| # | Situación | Respuesta del sistema |
|---|-----------|-----------------------|
| E1 | El cliente intenta avanzar dejando campos obligatorios vacíos (dirección, ciudad, código postal o teléfono). | Impide avanzar e indica qué campo falta o está mal completado. |
| E2 | El cliente ingresa un código postal no cubierto o inválido. | Avisa que no hay cobertura de envío a domicilio para esa zona y sugiere retirar en el local o corregir el dato. |
| E3 | Falla la consulta de tarifa al proveedor logístico. | Pide reintentar sin perder los datos ya cargados. |

| Campo | Detalle |
|-------|---------|
| Rendimiento | El sistema realiza los pasos 1 a 3 en un máximo de 5 segundos. |
| Frecuencia | Se estima una media de 50 ejecuciones diarias. |
| Importancia | Vital. |
| Urgencia | Inmediatamente. |


---

## CU-10 — Realizar pago

| Campo | Detalle |
|-------|---------|
| Identificador | CU-10 |
| Nombre | Realizar pago |
| Descripción | El cliente paga a través de Mercado Pago. |
| Actores | Principal: Cliente. Secundario: Mercado Pago (pasarela de pago). |
| Precondiciones | El cliente completó los datos para la verificación. Existe un importe a pagar. Mercado Pago está disponible. |
| Postcondiciones | Éxito: El pago queda registrado con estado, fecha, importe y medio de pago; el pedido pasa a "Pagado". Fallo: El pago es rechazado, el pedido no cambia de estado y se informa al cliente. |

### Secuencia normal

| # | Acción (actor) | Reacción (sistema) |
|---|----------------|--------------------|
| 1 | Selecciona "Pagar con Mercado Pago". | Redirige a la pasarela de Mercado Pago. |
| 2 | Elige la modalidad de pago y confirma. | Mercado Pago procesa la operación y el sistema registra estado, fecha, importe y medio de pago (RF-29). |
| 3 | | El sistema actualiza el pedido a "Pagado" y notifica al cliente por email (RF-30). |

### Excepciones

| # | Situación | Respuesta del sistema |
|---|-----------|-----------------------|
| E1 | Mercado Pago no está disponible. | Muestra un mensaje indicando que el servicio de pago no está disponible por el momento. |
| E2 | Mercado Pago rechaza el pago. | Informa al cliente que el pago fue rechazado y el pedido no pasa a "Pagado". |
| E3 | Mercado Pago informa que el pago quedó pendiente de verificación | Deja el pedido en estado "Pendiente de pago" y avisa al cliente que se está confirmando el pago. |


| Campo | Detalle |
|-------|---------|
| Rendimiento |  El sistema completa el flujo de pago en un máximo de 5 segundos, sin contar el tiempo de respuesta de Mercado Pago. |
| Frecuencia | Se estima una media de 45 ejecuciones diarias: nunca más que los checkouts de CU-09 (50 por día), porque no todos los checkouts llegan a pagarse. |
| Importancia | Vital |
| Urgencia | Inmediatamente. |

---


## CU-11 — Registrar venta presencial

| Campo | Detalle |
|-------|---------|
| Identificador | CU-11 |
| Nombre | Registrar venta presencial |
| Descripción | El Empleado registra una venta realizada en el local, indicando productos, cantidades y medio de pago. |
| Actores | Principal: Empleado |
| Precondiciones | El empleado tiene una sesión iniciada. Hay disponibilidad de stock de las prendas. |
| Postcondiciones | Éxito: La venta queda registrada con sus productos, cantidades y medio de pago. El stock de cada combinación producto-talle-color vendida se descuenta sobre el mismo stock que usan las ventas online (RF-20). Fallo: La venta no se guarda y no se realiza ningún descuento sobre el stock. |

### Secuencia normal

| # | Acción (actor) | Reacción (sistema) |
|---|----------------|--------------------|
| 1 | El empleado solicita registrar una venta. | Muestra el formulario de registro de venta con buscador de productos y detalle de venta vacío. Muestra la interfaz del terminal de punto de venta presencial. |
| 2 | Busca las prendas, selecciona el talle, color y cantidad vendida, y presiona "Agregar". | Valida la disponibilidad de stock ejecutando CU-16 y calcula el subtotal. |
| 3 | Selecciona el medio de pago (efectivo, débito, crédito o transferencia) y confirma la transacción. | Registra la venta con fecha, hora y empleado que la realizó, descuenta el stock de cada combinación vendida y muestra un resumen de la venta. |

### Excepciones

| # | Situación | Respuesta del sistema |
|---|-----------|-----------------------|
| E1 | El empleado intenta agregar una cantidad de unidades superior al stock disponible. | El sistema no agregará el ítem y mostrará un mensaje indicando las unidades exactas en existencia. |
| E2 | El empleado intenta confirmar la venta sin seleccionar el medio de pago. | El sistema detendrá la operación, resaltará el campo de selección de medio de pago y requerirá su definición (RNF-10). |
| E3 | Ocurre un fallo en la base de datos durante la confirmación del cobro. | El sistema anulará la transacción, conservará los ítems en la pantalla del punto de venta y registrará el error (RNF-18). |


| Campo | Detalle |
|-------|---------|
| Rendimiento | El sistema registrará la venta presencial en un máximo de 3 segundos (RNF-01). |
| Frecuencia | Este caso de uso se espera que se lleve a cabo una media de 80 veces al día. |
| Importancia | Vital |
| Urgencia | Inmediatamente |

---


## CU-12 — Consultar estado y seguimiento de pedidos

| Campo | Detalle |
|-------|---------|
| Identificador | CU-12 |
| Nombre | Consultar estado y seguimiento de pedidos |
| Descripción | El Cliente consulta desde "Mi Cuenta" el historial de sus pedidos, el estado actual de cada uno y, si corresponde, el número de seguimiento del envío o la fecha límite para retirarlo. |
| Actores | Principal: Cliente. Secundario: Proveedor logístico (informa el número de seguimiento). |
| Precondiciones | El Cliente tiene una sesión iniciada. |
| Postcondiciones | Éxito: El Cliente visualiza sus pedidos con su estado actualizado. Fallo: No se muestra información y no se modifica ningún dato. |

### Secuencia normal

| # | Acción (actor) | Reacción (sistema) |
|---|----------------|--------------------|
| 1 | Ingresa a "Mi Cuenta" y selecciona "Mis pedidos". | El sistema muestra el listado de sus pedidos, del más reciente al más antiguo, con número de pedido, fecha, importe total y estado (RF-07). |
| 2 | Selecciona un pedido. | El sistema muestra el detalle: productos con talle, color y cantidad, método de entrega y estado actual (Pendiente de pago, Pagado / En preparación, Enviado, Listo para retirar, Entregado o Cancelado; RF-30). |
| 3 | Consulta el seguimiento o el plazo de retiro del pedido. | Si el pedido tiene envío, el sistema muestra el número de seguimiento informado por el proveedor logístico (RF-34). Si está listo para retirar, muestra la fecha límite de retiro (RF-36). |

### Excepciones

| # | Situación | Respuesta del sistema |
|---|-----------|-----------------------|
| E1 | El Cliente todavía no realizó ninguna compra. | El sistema muestra un mensaje indicando que no tiene pedidos y ofrece ir al catálogo. |
| E2 | El pedido fue enviado pero el proveedor logístico todavía no informó el número de seguimiento. | El sistema indica que el número de seguimiento aún no está disponible. |
| E3 | Error al consultar los pedidos. | El sistema muestra un mensaje de error y registra fecha, hora y descripción del error (RNF-18). |
| E4 | Una operación demora más de 1 segundo. | El sistema muestra un indicador de carga (RNF-11). |

| Campo | Detalle |
|-------|---------|
| Rendimiento | El sistema deberá mostrar el listado y el detalle en un máximo de 3 segundos con 50 usuarios simultáneos (RNF-01). |
| Frecuencia | Se estima una media de 120 ejecuciones diarias. |
| Importancia | Alta. |
| Urgencia | Inmediata. |

---


## CU-13 — Solicitar devolución

| Campo | Detalle |
|-------|---------|
| Identificador | CU-13 |
| Nombre | Solicitar devolución |
| Descripción | El Cliente solicita desde "Mi Cuenta" la devolución de un pedido ya entregado o retirado, indicando el motivo, dentro del plazo de 5 días hábiles. |
| Actores | Principal: Cliente |
| Precondiciones | El Cliente tiene una sesión iniciada. El pedido está en estado "Entregado" y no pasaron más de 5 días hábiles desde la entrega o el retiro. |
| Postcondiciones | Éxito: La solicitud queda registrada en estado "Solicitada" con fecha y hora, el Cliente recibe una confirmación y la solicitud aparece como pendiente en el panel del personal (RF-44). Fallo: No se registra la solicitud. |

### Secuencia normal

| # | Acción (actor) | Reacción (sistema) |
|---|----------------|--------------------|
| 1 | Desde el detalle de un pedido entregado, selecciona "Solicitar devolución". | El sistema verifica que el pedido esté dentro de los 5 días hábiles posteriores a la entrega o el retiro (RF-38) y muestra el formulario con el pedido seleccionado y el motivo. |
| 2 | Elige el motivo (talle incorrecto, producto defectuoso o producto equivocado), agrega comentarios si lo desea y confirma. | El sistema valida los datos, registra la solicitud en estado "Solicitada", muestra una confirmación y notifica al Cliente por email (RF-39). |

### Excepciones

| # | Situación | Respuesta del sistema |
|---|-----------|-----------------------|
| E1 | Pasaron más de 5 días hábiles desde la entrega o el retiro. | El sistema no permite iniciar la solicitud: muestra la acción deshabilitada junto con la fecha en que venció el plazo. |
| E2 | El Cliente confirma sin elegir un motivo. | El sistema resalta el campo "Motivo" y no registra la solicitud (RNF-10). |
| E3 | El pedido no está entregado (por ejemplo, está cancelado o todavía en preparación). | El sistema no ofrece la acción "Solicitar devolución" para ese pedido. |
| E4 | Error al guardar la solicitud. | El sistema informa que no se pudo registrar, conserva los datos cargados, permite reintentar y registra fecha, hora y descripción del error (RNF-18). |

| Campo | Detalle |
|-------|---------|
| Rendimiento | El sistema deberá registrar la solicitud en un máximo de 3 segundos (RNF-01). |
| Frecuencia | Se estima una media de 2 ejecuciones diarias. |
| Importancia | Importante. |
| Urgencia | Hay presión. |

---


## CU-14 — Gestionar solicitud de devolución

| Campo | Detalle |
|-------|---------|
| Identificador | CU-14 |
| Nombre | Gestionar solicitud de devolución |
| Descripción | El Empleado revisa una solicitud de devolución, la aprueba o la rechaza y, si la aprueba sin cambio de producto, emite una nota de crédito a favor del Cliente. |
| Actores | Principal: Empleado |
| Precondiciones | El Empleado tiene una sesión iniciada. Existe una solicitud en estado "Solicitada" o "En revisión". |
| Postcondiciones | Éxito: La solicitud queda "Aprobada" o "Rechazada" (y luego "Producto recibido" y "Finalizada" si corresponde), el Cliente es notificado de cada cambio y, si se aprobó sin cambio, queda emitida la nota de crédito. Fallo: La solicitud conserva su estado anterior. |

### Secuencia normal

| # | Acción (actor) | Reacción (sistema) |
|---|----------------|--------------------|
| 1 | Accede a las devoluciones pendientes desde el panel (RF-44) y abre una solicitud. | El sistema muestra el pedido, el motivo, los comentarios del Cliente y la fecha, y pasa la solicitud a "En revisión". |
| 2 | Aprueba o rechaza la solicitud e indica una observación (RF-40). | El sistema registra la decisión con el empleado, la fecha y la hora, y notifica al Cliente por email (RF-39). |
| 3 | Si aprobó la solicitud y no corresponde un cambio de producto, solicita emitir la nota de crédito (RF-41). | El sistema genera la nota de crédito a favor del Cliente por el importe de los productos devueltos y registra su emisión. |
| 4 | Cuando el Cliente entrega la prenda, confirma "Producto recibido" y cierra el trámite. | El sistema actualiza el estado a "Producto recibido", luego a "Finalizada", y notifica al Cliente (RF-39). |

### Excepciones

| # | Situación | Respuesta del sistema |
|---|-----------|-----------------------|
| E1 | El Empleado rechaza la solicitud sin escribir una observación. | El sistema exige una observación, que se informa al Cliente junto con el rechazo. |
| E2 | Se aprueba la solicitud y el Cliente prefiere un cambio de producto. | El sistema no emite nota de crédito y registra la resolución como cambio de producto. |
| E3 | Otro empleado ya resolvió la solicitud. | El sistema informa el estado actual y no permite resolverla de nuevo. |
| E4 | Error al guardar la resolución. | El sistema informa el error, conserva el estado anterior de la solicitud y registra fecha, hora y descripción del error (RNF-18). |

| Campo | Detalle |
|-------|---------|
| Rendimiento | El sistema deberá registrar cada acción en un máximo de 3 segundos (RNF-01). |
| Frecuencia | Se estima una media de 2 ejecuciones diarias. |
| Importancia | Importante. |
| Urgencia | Hay presión. |

---


## CU-15 — Gestionar retiro en el local

| Campo | Detalle |
|-------|---------|
| Identificador | CU-15 |
| Nombre | Gestionar retiro en el local |
| Descripción | El Empleado marca un pedido con retiro en el local como "Listo para retirar", lo que inicia un plazo de 15 días corridos, y confirma el retiro cuando el Cliente lo busca. |
| Actores | Principal: Empleado |
| Precondiciones | El Empleado tiene una sesión iniciada. El pedido tiene entrega "Retiro en el local" y está pagado y preparado. |
| Postcondiciones | Éxito: El pedido queda "Listo para retirar" con su fecha límite, y luego "Entregado" con la fecha y hora del retiro registradas. Fallo: El pedido conserva su estado anterior. |

### Secuencia normal

| # | Acción (actor) | Reacción (sistema) |
|---|----------------|--------------------|
| 1 | Desde el panel, selecciona un pedido con retiro en el local ya preparado y lo marca como "Listo para retirar" (RF-36). | El sistema cambia el estado, calcula la fecha límite (15 días corridos desde ese momento) y notifica al Cliente por email (RF-30). |
| 2 | | El sistema notifica al Cliente el vencimiento del plazo en el día 12 y en el día 15 (RF-37). |
| 3 | Cuando el Cliente se presenta en el local, busca su pedido por número. | El sistema muestra el pedido con sus productos y su estado. |
| 4 | Confirma el retiro (RF-35). | El sistema registra la fecha y la hora del retiro, cambia el estado a "Entregado" y notifica al Cliente (RF-30). |

### Excepciones

| # | Situación | Respuesta del sistema |
|---|-----------|-----------------------|
| E1 | Vence el plazo de 15 días y el pedido no fue retirado. | El sistema cambia el pedido a "Cancelado", repone el stock de sus productos y notifica al Cliente. |
| E2 | El Empleado intenta confirmar el retiro de un pedido que no está "Listo para retirar". | El sistema no lo permite e indica el estado actual del pedido. |
| E3 | Error al guardar el cambio de estado. | El sistema informa el error, conserva el estado anterior y registra fecha, hora y descripción del error (RNF-18). |

| Campo | Detalle |
|-------|---------|
| Rendimiento | El sistema deberá realizar cada acción en un máximo de 3 segundos (RNF-01). |
| Frecuencia | Se estima una media de 25 ejecuciones diarias. |
| Importancia | Importante. |
| Urgencia | Hay presión. |

---


## CU-16 — Verificar stock disponible

| Campo | Detalle |
|-------|---------|
| Identificador | CU-16 |
| Nombre | Verificar stock disponible |
| Descripción | El sistema consulta el stock unificado (tienda online y local) de una combinación producto-talle-color y confirma si hay unidades suficientes. Es un caso de uso incluido: lo ejecutan siempre, como un paso propio, CU-06 y CU-11. |
| Actores | Ninguno directo (es invocado por CU-06 y CU-11). |
| Precondiciones | La variante existe y está activa. |
| Postcondiciones | Éxito: El caso de uso base recibe la confirmación de que hay unidades suficientes. Fallo: El caso de uso base recibe la cantidad disponible (que puede ser cero) y no continúa con la cantidad pedida. |

### Secuencia normal

| # | Acción (actor) | Reacción (sistema) |
|---|----------------|--------------------|
| 1 | | El sistema recibe la variante (producto, talle y color) y la cantidad pedida por el caso de uso base. |
| 2 | | Consulta el stock unificado de esa variante (RF-20) y lo compara con la cantidad pedida. |
| 3 | | Si hay unidades suficientes, informa la disponibilidad al caso de uso base. |

### Excepciones

| # | Situación | Respuesta del sistema |
|---|-----------|-----------------------|
| E1 | La cantidad pedida supera el stock. | El sistema devuelve las unidades disponibles para que el caso base informe la cantidad exacta (CU-06 E2, CU-11 E1). |
| E2 | La variante no tiene stock. | El sistema devuelve cero unidades disponibles (CU-06 E3). |
| E3 | Error al consultar el stock. | El sistema informa el error al caso base y registra fecha, hora y descripción del error (RNF-18). |

| Campo | Detalle |
|-------|---------|
| Rendimiento | El sistema deberá resolver la consulta en menos de 2 segundos (RNF-13). |
| Frecuencia | Se estima una media de 180 ejecuciones diarias (las de CU-06, 100, más las de CU-11, 80). |
| Importancia | Vital. |
| Urgencia | Inmediatamente. |
