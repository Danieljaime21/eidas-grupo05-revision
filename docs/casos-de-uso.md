# Casos de uso

## Diagrama general

_Incluir el código PlantUML en `diagramas/casos-de-uso.puml`._
_Visualizar en [plantuml.com](https://www.plantuml.com/plantuml/uml/)._

_Describir brevemente los actores identificados y las relaciones principales (include, extend)._

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
| E2 | El email ingresado no se encuentra registrado en el sistema. | El sistema notifica que el email no está asociado a ninguna cuenta existente y ofrecerá opción directa para registrarse. |

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
| E4 | Error interno al guardar el usuario. | El sistema deberá informarlo y registrar fecha, hora y descripción del error (RNF-16). |


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
| 3 | Selecciona uno o más filtros (talle, color, marca). | El sistema muestra solo los productos que cumplen todos los filtros seleccionados. |



### Excepciones

| # | Situación | Respuesta del sistema |
|---|-----------|-----------------------|
| E1 | Ningún producto cumple los filtros elegidos. | El sistema deberá mostrar un mensaje indicando que ningún producto cumple con los filtros seleccionados y sugerirá quitar algunos de estos. |
| E2 | Error al consultar el catálogo. | El sistema deberá mostrar un mensaje de error y registrar fecha, hora y descripción del error (RNF-16). |
| E3 | Una operación demora más de 1 segundo. | El sistema deberá mostrar un indicador de carga (RNF-11). |
| E4 | | |


| Campo | Detalle |
|-------|---------|
| Rendimiento | El sistema deberá realizar las acciones descritas en los pasos 1 al 3 en un máximo de 3 segundos con 50 usuarios simultáneos (RNF-01), y las consultas a la base de datos en menos de 2 segundos (RNF-13). |
| Frecuencia | Este caso de uso se espera que se lleve a cabo una media de 200 veces al día. |
| Importancia | Vital |
| Urgencia | Inmediatamente |


---


## CU-05 — [Procesar pago con Mercado Pago]

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

## CU-06 — [Consultar seguimiento del pedido]

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
