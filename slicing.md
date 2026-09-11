# Slicing — HU-01: Registro, Autenticación y Gestión de Perfil de Cliente

## HU-01 — Registro, Autenticación y Gestión de Perfil de Cliente

**Historia original:**
Como cliente, quiero registrarme ingresando mis datos obligatorios, iniciar sesión y acceder a mi perfil, para administrar mi información personal, consultar el historial y estado de mis pedidos y realizar compras en la plataforma.

**Módulo:** 02 - Clientes y Cuentas

---

# Slice 01 — Registro de cliente

### Historia

Como cliente, quiero registrarme ingresando mis datos obligatorios, para crear una cuenta y poder utilizar las funcionalidades de la plataforma asociadas a usuarios registrados.

### Requisitos relacionados

RF-08, RF-09

### Criterios de aceptación

1. El sistema debe solicitar todos los datos definidos como obligatorios para el registro.
2. El sistema debe validar que el correo electrónico tenga un formato válido.
3. El sistema debe validar que el DNI ingresado tenga un formato válido.
4. El sistema debe impedir el registro cuando el correo electrónico ya se encuentre asociado a otra cuenta.
5. Si todos los datos son válidos, el sistema debe crear la cuenta del cliente correctamente.
6. Si existen datos inválidos o faltantes, el sistema debe informar el error y no crear la cuenta.

### Validación INVEST

| Criterio      | ¿Se cumple? | Observación                                                                              |
| ------------- | ----------- | ---------------------------------------------------------------------------------------- |
| Independiente | Sí          | Puede desarrollarse y probarse sin depender del inicio de sesión, pagos o envíos.        |
| Negociable    | Sí          | Los datos obligatorios y sus reglas de validación pueden ajustarse según los requisitos. |
| Valiosa       | Sí          | Permite al cliente crear una cuenta para acceder a funcionalidades personalizadas.       |
| Estimable     | Sí          | El alcance está limitado al proceso de alta y validación de datos.                       |
| Pequeña       | Sí          | Se concentra únicamente en el registro de una cuenta.                                    |
| Verificable   | Sí          | Puede comprobarse mediante registros válidos, inválidos y correos duplicados.            |

---

# Slice 02 — Inicio de sesión

### Historia

Como cliente registrado, quiero iniciar sesión con mis credenciales, para acceder de forma segura a mi cuenta y a las funcionalidades disponibles para usuarios autenticados.

### Requisitos relacionados

RF-10, RF-11

### Criterios de aceptación

1. El sistema debe permitir ingresar el correo electrónico y la contraseña asociados a una cuenta registrada.
2. El sistema debe verificar que las credenciales ingresadas sean correctas.
3. Si las credenciales son válidas, el sistema debe autenticar al cliente y permitirle acceder a su cuenta.
4. Si las credenciales son incorrectas, el sistema debe informar que los datos ingresados no son válidos.
5. El sistema no debe permitir el acceso a la cuenta cuando la autenticación sea incorrecta.
6. El cliente autenticado debe poder acceder a la sección "Mi Cuenta".

### Validación INVEST

| Criterio      | ¿Se cumple? | Observación                                                                                   |
| ------------- | ----------- | --------------------------------------------------------------------------------------------- |
| Independiente | Sí          | Puede probarse a partir de una cuenta previamente registrada, sin depender de pagos o envíos. |
| Negociable    | Sí          | El mecanismo y las reglas de autenticación pueden ajustarse.                                  |
| Valiosa       | Sí          | Permite al cliente acceder de forma segura a su cuenta.                                       |
| Estimable     | Sí          | El alcance se limita al proceso de autenticación.                                             |
| Pequeña       | Sí          | Se concentra en el acceso de un cliente registrado.                                           |
| Verificable   | Sí          | Puede comprobarse utilizando credenciales válidas e inválidas.                                |

---

# Slice 03 — Recuperación de contraseña

### Historia

Como cliente registrado, quiero recuperar mi contraseña mediante un enlace enviado a mi correo electrónico, para volver a acceder a mi cuenta cuando haya olvidado mis credenciales.

### Requisitos relacionados

RF-12, RF-13

### Criterios de aceptación

1. El sistema debe ofrecer una opción para iniciar el proceso de recuperación de contraseña.
2. El cliente debe poder indicar el correo electrónico asociado a su cuenta.
3. Si el correo corresponde a una cuenta registrada, el sistema debe enviar un enlace de recuperación al correo electrónico.
4. El enlace enviado debe permitir al cliente establecer una nueva contraseña.
5. La nueva contraseña debe cumplir con las reglas de seguridad definidas por el sistema.
6. Una vez modificada la contraseña, el cliente debe poder utilizarla para iniciar sesión.
7. El sistema no debe modificar la contraseña si el proceso de recuperación no se completa correctamente.

### Validación INVEST

| Criterio      | ¿Se cumple? | Observación                                                                                  |
| ------------- | ----------- | -------------------------------------------------------------------------------------------- |
| Independiente | Sí          | Puede desarrollarse como una funcionalidad independiente del resto de la gestión del perfil. |
| Negociable    | Sí          | El mecanismo de recuperación y las reglas de contraseña pueden ajustarse.                    |
| Valiosa       | Sí          | Permite recuperar el acceso a una cuenta sin necesidad de crear una nueva.                   |
| Estimable     | Sí          | El alcance está limitado al flujo de recuperación y cambio de contraseña.                    |
| Pequeña       | Sí          | Se limita a la recuperación de credenciales.                                                 |
| Verificable   | Sí          | Puede comprobarse solicitando la recuperación y estableciendo una nueva contraseña.          |

---

# Slice 04 — Consulta de perfil

### Historia

Como cliente autenticado, quiero consultar mis datos personales y de contacto desde la sección "Mi Cuenta", para conocer la información asociada a mi cuenta.

### Requisitos relacionados

RF-14

### Criterios de aceptación

1. El cliente autenticado debe poder acceder a la sección "Mi Cuenta".
2. El sistema debe mostrar los datos personales y de contacto asociados a la cuenta.
3. La información mostrada debe corresponder al cliente autenticado.
4. El sistema debe permitir visualizar el DNI registrado.
5. El cliente no debe poder modificar sus datos mientras se encuentre únicamente en modo consulta.
6. Un cliente no autenticado no debe poder acceder a la información de una cuenta.

### Validación INVEST

| Criterio      | ¿Se cumple? | Observación                                                                               |
| ------------- | ----------- | ----------------------------------------------------------------------------------------- |
| Independiente | Sí          | Puede desarrollarse y probarse con una cuenta autenticada, sin depender de otros módulos. |
| Negociable    | Sí          | La información mostrada puede ajustarse según los datos definidos para el perfil.         |
| Valiosa       | Sí          | Permite al cliente consultar la información asociada a su cuenta.                         |
| Estimable     | Sí          | El alcance se limita a la visualización de los datos del perfil.                          |
| Pequeña       | Sí          | Solo contempla la consulta de información, sin modificación.                              |
| Verificable   | Sí          | Puede comprobarse accediendo con diferentes cuentas y verificando los datos mostrados.    |

---

# Slice 05 — Edición de perfil

### Historia

Como cliente autenticado, quiero modificar mis datos de contacto desde la sección "Mi Cuenta", para mantener actualizada mi información personal.

### Requisitos relacionados

RF-15, RF-16

### Criterios de aceptación

1. El cliente autenticado debe poder acceder a la opción de edición de su perfil.
2. El sistema debe permitir modificar los datos de contacto definidos como editables.
3. El DNI debe mostrarse bloqueado y no debe poder modificarse.
4. El sistema debe validar los datos ingresados antes de guardar los cambios.
5. Si los datos son válidos, el sistema debe actualizar correctamente la información del perfil.
6. Si existe algún dato inválido, el sistema debe informar el error y no guardar los cambios correspondientes.
7. Una vez guardados los cambios, el sistema debe mostrar la información actualizada.

### Validación INVEST

| Criterio      | ¿Se cumple? | Observación                                                                             |
| ------------- | ----------- | --------------------------------------------------------------------------------------- |
| Independiente | Sí          | Puede desarrollarse sobre un perfil existente sin depender de pagos o envíos.           |
| Negociable    | Sí          | Los datos editables y sus reglas de validación pueden ajustarse.                        |
| Valiosa       | Sí          | Permite al cliente mantener actualizada su información de contacto.                     |
| Estimable     | Sí          | El alcance se limita a la modificación y validación de datos del perfil.                |
| Pequeña       | Sí          | Se concentra exclusivamente en la edición del perfil.                                   |
| Verificable   | Sí          | Puede comprobarse modificando datos válidos e inválidos y verificando el DNI bloqueado. |

---

# Slicing — HU-02: Consulta, Búsqueda y Filtrado de Productos por Variante

## Slice 01 — Consulta del catálogo

### Historia

Como cliente, quiero consultar el catálogo de productos, para conocer las prendas disponibles antes de realizar una compra.

### Requisitos relacionados

RF-24, RF-25

### Criterios de aceptación

1. El catálogo debe estar disponible públicamente.
2. Cada prenda debe mostrar entre 2 y 4 fotos, descripción, tabla de medidas y sus variantes.
3. La información mostrada debe corresponder al producto seleccionado.

### Validación INVEST

| Criterio      | ¿Se cumple? | Observación                                     |
| ------------- | ----------- | ----------------------------------------------- |
| Independiente | Sí          | Puede consultarse sin depender del carrito.     |
| Negociable    | Sí          | El diseño visual puede modificarse.             |
| Valiosa       | Sí          | Permite conocer los productos disponibles.      |
| Estimable     | Sí          | Se limita a la visualización del catálogo.      |
| Pequeña       | Sí          | Se concentra en la consulta de productos.       |
| Verificable   | Sí          | Se comprueba visualizando diferentes productos. |

---

## Slice 02 — Búsqueda de productos

### Historia

Como cliente, quiero buscar productos mediante palabras clave, para encontrar rápidamente las prendas que me interesan.

### Requisitos relacionados

RF-26

### Criterios de aceptación

1. El sistema debe permitir ingresar una palabra clave.
2. Debe mostrar los productos relacionados con la búsqueda.
3. Si no existen coincidencias, debe informar que no se encontraron productos.

### Validación INVEST

| Criterio      | ¿Se cumple? | Observación                                     |
| ------------- | ----------- | ----------------------------------------------- |
| Independiente | Sí          | Funciona sobre el catálogo existente.           |
| Negociable    | Sí          | El mecanismo de búsqueda puede ajustarse.       |
| Valiosa       | Sí          | Reduce el tiempo de búsqueda.                   |
| Estimable     | Sí          | Tiene un alcance acotado.                       |
| Pequeña       | Sí          | Se limita a la búsqueda.                        |
| Verificable   | Sí          | Se prueba con palabras con y sin coincidencias. |

---

## Slice 03 — Filtrado de productos

### Historia

Como cliente, quiero filtrar los productos por categoría, talle, color, precio y disponibilidad, para encontrar prendas que se adapten a mis preferencias.

### Requisitos relacionados

RF-27, RF-28, RF-32

### Criterios de aceptación

1. El sistema debe permitir aplicar filtros por categoría, talle, color, precio y disponibilidad.
2. Los filtros deben poder combinarse.
3. El catálogo debe mostrar únicamente los productos que cumplan con los filtros seleccionados.

### Validación INVEST

| Criterio      | ¿Se cumple? | Observación                                            |
| ------------- | ----------- | ------------------------------------------------------ |
| Independiente | Sí          | No depende del carrito ni del proceso de compra.       |
| Negociable    | Sí          | Los filtros pueden modificarse según las necesidades.  |
| Valiosa       | Sí          | Facilita encontrar productos específicos.              |
| Estimable     | Sí          | El alcance está limitado al filtrado.                  |
| Pequeña       | Sí          | Agrupa filtros relacionados.                           |
| Verificable   | Sí          | Se prueba aplicando filtros individuales y combinados. |

---

## Slice 04 — Ordenamiento de productos

### Historia

Como cliente, quiero ordenar los productos por precio, novedad o popularidad, para visualizar primero los que sean más relevantes para mí.

### Requisitos relacionados

RF-33, RF-34

### Criterios de aceptación

1. El sistema debe permitir ordenar por precio ascendente y descendente.
2. Debe permitir ordenar por novedad y popularidad.
3. Los productos deben mostrarse respetando el criterio seleccionado.

### Validación INVEST

| Criterio      | ¿Se cumple? | Observación                                                      |
| ------------- | ----------- | ---------------------------------------------------------------- |
| Independiente | Sí          | Puede aplicarse sobre el catálogo sin depender de otros módulos. |
| Negociable    | Sí          | Los criterios de ordenamiento pueden ajustarse.                  |
| Valiosa       | Sí          | Facilita la exploración del catálogo.                            |
| Estimable     | Sí          | Se limita al ordenamiento de resultados.                         |
| Pequeña       | Sí          | Tiene un alcance reducido.                                       |
| Verificable   | Sí          | Se comprueba utilizando cada criterio de ordenamiento.           |

---

## Slice 05 — Disponibilidad por variante

### Historia

Como cliente, quiero conocer la disponibilidad de cada variante de una prenda, para evitar seleccionar productos que no tengan stock.

### Requisitos relacionados

RF-35

### Criterios de aceptación

1. El sistema debe mostrar las variantes disponibles de cada prenda.
2. Cuando una variante tenga stock cero, debe mostrar el indicador "Sin stock".
3. Una variante sin stock no debe poder agregarse al carrito.

### Validación INVEST

| Criterio      | ¿Se cumple? | Observación                                      |
| ------------- | ----------- | ------------------------------------------------ |
| Independiente | Sí          | La disponibilidad se consulta desde el catálogo. |
| Negociable    | Sí          | La forma de mostrar el stock puede modificarse.  |
| Valiosa       | Sí          | Evita seleccionar productos no disponibles.      |
| Estimable     | Sí          | Se limita al control de disponibilidad.          |
| Pequeña       | Sí          | Tiene un alcance concreto.                       |
| Verificable   | Sí          | Se prueba con variantes con y sin stock.         |


# Slicing — HU-03: Selección de Variantes, Carrito y Reserva Temporal de Stock

## Slice 01 — Selección de variantes

### Historia

Como cliente, quiero seleccionar una variante específica de una prenda, para agregar al carrito el producto que deseo comprar.

### Requisitos relacionados

RF-49, RF-50

### Criterios de aceptación

1. El sistema debe permitir seleccionar las variantes disponibles de una prenda.
2. El cliente debe poder seleccionar talle y color cuando correspondan.
3. El sistema debe permitir agregar al carrito la variante seleccionada.

### Validación INVEST

| Criterio      | ¿Se cumple? | Observación                                     |
| ------------- | ----------- | ----------------------------------------------- |
| Independiente | Sí          | Puede probarse desde el catálogo.               |
| Negociable    | Sí          | La forma de selección puede modificarse.        |
| Valiosa       | Sí          | Permite elegir exactamente el producto deseado. |
| Estimable     | Sí          | Tiene un alcance concreto.                      |
| Pequeña       | Sí          | Se limita a la selección de variantes.          |
| Verificable   | Sí          | Se prueba seleccionando diferentes variantes.   |

---

## Slice 02 — Agregar productos al carrito

### Historia

Como cliente, quiero agregar prendas al carrito, para reunir los productos que deseo comprar.

### Requisitos relacionados

RF-51, RF-52

### Criterios de aceptación

1. El cliente debe poder agregar una variante seleccionada al carrito.
2. El carrito debe mostrar los productos agregados y sus cantidades.
3. El sistema debe actualizar el contenido del carrito al agregar un producto.

### Validación INVEST

| Criterio      | ¿Se cumple? | Observación                                          |
| ------------- | ----------- | ---------------------------------------------------- |
| Independiente | Sí          | No requiere confirmar el pedido ni realizar el pago. |
| Negociable    | Sí          | La presentación del carrito puede ajustarse.         |
| Valiosa       | Sí          | Permite reunir los productos antes de comprar.       |
| Estimable     | Sí          | Es una funcionalidad de alcance definido.            |
| Pequeña       | Sí          | Se limita al agregado de productos.                  |
| Verificable   | Sí          | Se comprueba agregando diferentes productos.         |

---

## Slice 03 — Modificar y eliminar productos

### Historia

Como cliente, quiero modificar cantidades o eliminar productos del carrito, para ajustar mi compra antes de confirmarla.

### Requisitos relacionados

RF-53, RF-54

### Criterios de aceptación

1. El cliente debe poder aumentar o disminuir la cantidad de un producto.
2. El cliente debe poder eliminar un producto del carrito.
3. El sistema debe actualizar el contenido del carrito después de cada modificación.

### Validación INVEST

| Criterio      | ¿Se cumple? | Observación                                              |
| ------------- | ----------- | -------------------------------------------------------- |
| Independiente | Sí          | Se realiza sobre productos ya agregados al carrito.      |
| Negociable    | Sí          | La interfaz de edición puede modificarse.                |
| Valiosa       | Sí          | Permite ajustar la compra antes de confirmarla.          |
| Estimable     | Sí          | El alcance está limitado a editar y eliminar productos.  |
| Pequeña       | Sí          | Agrupa acciones relacionadas del carrito.                |
| Verificable   | Sí          | Se prueba modificando cantidades y eliminando productos. |

---

## Slice 04 — Cálculo del total

### Historia

Como cliente, quiero que el carrito recalcule automáticamente los importes, para conocer el monto de mi compra en todo momento.

### Requisitos relacionados

RF-55, RF-56

### Criterios de aceptación

1. El sistema debe calcular el subtotal de los productos del carrito.
2. El sistema debe actualizar automáticamente los importes al modificar cantidades.
3. El total mostrado debe corresponder a los productos y cantidades actuales.

### Validación INVEST

| Criterio      | ¿Se cumple? | Observación                                            |
| ------------- | ----------- | ------------------------------------------------------ |
| Independiente | Sí          | Puede probarse con productos y cantidades del carrito. |
| Negociable    | Sí          | La forma de presentar los importes puede modificarse.  |
| Valiosa       | Sí          | Permite conocer el monto acumulado de la compra.       |
| Estimable     | Sí          | Se limita al cálculo y actualización de importes.      |
| Pequeña       | Sí          | Tiene un alcance concreto.                             |
| Verificable   | Sí          | Se comprueban los cálculos con diferentes cantidades.  |

---

## Slice 05 — Persistencia y reserva temporal de stock

### Historia

Como cliente, quiero conservar los productos de mi carrito durante un período limitado, para mantener mi selección mientras decido completar la compra.

### Requisitos relacionados

RF-57, RF-58

### Criterios de aceptación

1. Los productos agregados deben conservarse aunque el cliente cierre el navegador o finalice la sesión.
2. El carrito debe conservarse durante un máximo de 24 horas.
3. Una vez transcurridas las 24 horas, el sistema debe liberar la reserva temporal del stock correspondiente.
4. El sistema debe reflejar correctamente la disponibilidad una vez liberado el stock.

### Validación INVEST

| Criterio      | ¿Se cumple? | Observación                                                             |
| ------------- | ----------- | ----------------------------------------------------------------------- |
| Independiente | Sí          | Puede probarse sin completar el proceso de pago.                        |
| Negociable    | Sí          | La presentación del tiempo de reserva puede modificarse.                |
| Valiosa       | Sí          | Permite conservar temporalmente la selección del cliente.               |
| Estimable     | Sí          | El alcance está limitado a persistencia y reserva temporal.             |
| Pequeña       | Sí          | Agrupa funcionalidades relacionadas con la permanencia del carrito.     |
| Verificable   | Sí          | Se prueba cerrando la sesión y verificando la liberación tras 24 horas. |


# Slicing — HU-04: Checkout, Pago Integrado y Transición de Estados del Pedido

## Slice 01 — Modalidad de entrega

### Historia

Como cliente, quiero seleccionar la modalidad de entrega, para elegir cómo recibir mi pedido.

### Requisitos relacionados

RF-59, RF-60

### Criterios de aceptación

1. El sistema debe permitir elegir entre envío a domicilio o retiro en local.
2. El envío debe calcular su costo correspondiente.
3. El retiro en local debe tener costo $0.

### Validación INVEST

| Criterio      | ¿Se cumple? | Observación                                |
| ------------- | ----------- | ------------------------------------------ |
| Independiente | Sí          | Puede seleccionarse antes del pago.        |
| Negociable    | Sí          | Las modalidades y reglas pueden ajustarse. |
| Valiosa       | Sí          | Permite elegir cómo recibir la compra.     |
| Estimable     | Sí          | Tiene un alcance concreto.                 |
| Pequeña       | Sí          | Se limita a la selección de entrega.       |
| Verificable   | Sí          | Se prueba cada modalidad y su costo.       |

---

## Slice 02 — Pago mediante Mercado Pago

### Historia

Como cliente, quiero pagar mi compra mediante Mercado Pago, para completar la transacción de forma segura.

### Requisitos relacionados

RF-61, RF-62, RF-63

### Criterios de aceptación

1. El sistema debe permitir iniciar el pago mediante Mercado Pago.
2. Debe registrar el resultado del pago.
3. Los pagos aprobados deben continuar con la generación del pedido.

### Validación INVEST

| Criterio      | ¿Se cumple? | Observación                                      |
| ------------- | ----------- | ------------------------------------------------ |
| Independiente | Sí          | Se integra directamente con la pasarela de pago. |
| Negociable    | Sí          | Las reglas de integración pueden ajustarse.      |
| Valiosa       | Sí          | Permite concretar la compra.                     |
| Estimable     | Sí          | Se basa en la integración con la pasarela.       |
| Pequeña       | Sí          | Se limita al procesamiento del pago.             |
| Verificable   | Sí          | Se prueba con pagos aprobados y rechazados.      |

---

## Slice 03 — Generación del pedido

### Historia

Como cliente, quiero que se genere mi pedido cuando el pago sea aprobado, para confirmar mi compra.

### Requisitos relacionados

RF-64, RF-65, RF-66

### Criterios de aceptación

1. El sistema debe generar un número de pedido único tras un pago aprobado.
2. Debe registrar los productos, cantidades e importe de la compra.
3. Debe descontar el stock correspondiente.

### Validación INVEST

| Criterio      | ¿Se cumple? | Observación                                         |
| ------------- | ----------- | --------------------------------------------------- |
| Independiente | Sí          | Se ejecuta luego de recibir la aprobación del pago. |
| Negociable    | Sí          | El formato del número de pedido puede ajustarse.    |
| Valiosa       | Sí          | Confirma y registra la compra.                      |
| Estimable     | Sí          | Tiene un alcance definido.                          |
| Pequeña       | Sí          | Se limita a generar y registrar el pedido.          |
| Verificable   | Sí          | Se comprueba con un pago aprobado.                  |

---

## Slice 04 — Estados del pedido

### Historia

Como cliente, quiero conocer el estado de mi pedido, para saber en qué etapa se encuentra mi compra.

### Requisitos relacionados

RF-68, RF-69, RF-70

### Criterios de aceptación

1. El sistema debe actualizar el estado del pedido según su avance.
2. El cliente debe poder consultar el estado actual.
3. Cada cambio debe quedar registrado correctamente.

### Validación INVEST

| Criterio      | ¿Se cumple? | Observación                                     |
| ------------- | ----------- | ----------------------------------------------- |
| Independiente | Sí          | Puede gestionarse sobre pedidos existentes.     |
| Negociable    | Sí          | Los estados y su presentación pueden ajustarse. |
| Valiosa       | Sí          | Permite realizar seguimiento de la compra.      |
| Estimable     | Sí          | Se limita a la gestión de estados.              |
| Pequeña       | Sí          | Agrupa funcionalidades relacionadas.            |
| Verificable   | Sí          | Se prueba avanzando el pedido entre estados.    |

---

## Slice 05 — Notificaciones del pedido

### Historia

Como cliente, quiero recibir notificaciones sobre los cambios de estado de mi pedido, para mantenerme informado sobre su evolución.

### Requisitos relacionados

RF-74, RF-75, RF-77

### Criterios de aceptación

1. El sistema debe notificar al cliente cuando cambie el estado de su pedido.
2. La notificación debe enviarse por email y mostrarse en la plataforma.
3. El mensaje debe informar el nuevo estado del pedido.

### Validación INVEST

| Criterio      | ¿Se cumple? | Observación                                            |
| ------------- | ----------- | ------------------------------------------------------ |
| Independiente | Sí          | Se activa a partir de cambios de estado.               |
| Negociable    | Sí          | Los medios y formato de notificación pueden ajustarse. |
| Valiosa       | Sí          | Mantiene informado al cliente.                         |
| Estimable     | Sí          | Tiene un alcance definido.                             |
| Pequeña       | Sí          | Se concentra en las notificaciones.                    |
| Verificable   | Sí          | Se prueba generando cambios de estado.                 |

# Slicing — HU-05: Control de Stock Unificado e Ingreso de Mercadería

## Slice 01 — Consulta de stock

### Historia

Como usuario de Depósito o Administrador, quiero consultar el stock disponible, para conocer las existencias actuales.

### Requisitos relacionados

RF-36, RF-37

### Criterios de aceptación

1. El sistema debe mostrar el stock disponible por producto y variante.
2. La información debe mantenerse centralizada.
3. Solo los usuarios autorizados deben acceder a esta información.

### Validación INVEST

| Criterio      | ¿Se cumple? | Observación                                      |
| ------------- | ----------- | ------------------------------------------------ |
| Independiente | Sí          | Puede consultarse sin depender de otros módulos. |
| Negociable    | Sí          | La forma de visualización puede ajustarse.       |
| Valiosa       | Sí          | Permite conocer las existencias.                 |
| Estimable     | Sí          | Tiene un alcance concreto.                       |
| Pequeña       | Sí          | Se limita a la consulta.                         |
| Verificable   | Sí          | Se comprueba consultando diferentes variantes.   |

---

## Slice 02 — Registro de ingreso de mercadería

### Historia

Como usuario de Depósito, quiero registrar el ingreso de mercadería, para actualizar las existencias disponibles.

### Requisitos relacionados

RF-38, RF-39, RF-40

### Criterios de aceptación

1. El sistema debe permitir registrar proveedor, contacto, producto, cantidad, fecha y costo unitario.
2. Debe validar los datos obligatorios antes de guardar el ingreso.
3. El stock debe actualizarse con la cantidad ingresada.

### Validación INVEST

| Criterio      | ¿Se cumple? | Observación                                     |
| ------------- | ----------- | ----------------------------------------------- |
| Independiente | Sí          | Puede realizarse sobre el inventario existente. |
| Negociable    | Sí          | Los datos y su presentación pueden ajustarse.   |
| Valiosa       | Sí          | Permite mantener actualizado el inventario.     |
| Estimable     | Sí          | Se limita al registro de ingresos.              |
| Pequeña       | Sí          | Tiene un alcance concreto.                      |
| Verificable   | Sí          | Se prueba registrando un ingreso.               |

---

## Slice 03 — Actualización de stock

### Historia

Como usuario de Depósito o Administrador, quiero que el stock se actualice automáticamente, para mantener sincronizadas las existencias.

### Requisitos relacionados

RF-41, RF-42

### Criterios de aceptación

1. El sistema debe actualizar el stock ante movimientos registrados.
2. El stock debe reflejarse correctamente en la tienda online.
3. Una venta online debe descontar stock únicamente cuando el pago sea aprobado.

### Validación INVEST

| Criterio      | ¿Se cumple? | Observación                                            |
| ------------- | ----------- | ------------------------------------------------------ |
| Independiente | Sí          | Gestiona la actualización centralizada del inventario. |
| Negociable    | Sí          | Las reglas de actualización pueden ajustarse.          |
| Valiosa       | Sí          | Evita inconsistencias de stock.                        |
| Estimable     | Sí          | Tiene reglas de actualización definidas.               |
| Pequeña       | Sí          | Se concentra en la actualización.                      |
| Verificable   | Sí          | Se comprueban diferentes movimientos de stock.         |

---

## Slice 04 — Historial de movimientos

### Historia

Como usuario de Depósito o Administrador, quiero consultar los movimientos de stock, para controlar los ingresos y modificaciones realizadas.

### Requisitos relacionados

RF-43, RF-44

### Criterios de aceptación

1. El sistema debe registrar los movimientos de stock.
2. Debe permitir consultar los movimientos realizados.
3. La información debe incluir los datos necesarios para identificar cada movimiento.

### Validación INVEST

| Criterio      | ¿Se cumple? | Observación                                         |
| ------------- | ----------- | --------------------------------------------------- |
| Independiente | Sí          | Puede consultarse sobre el inventario existente.    |
| Negociable    | Sí          | La información mostrada puede ajustarse.            |
| Valiosa       | Sí          | Facilita el control del inventario.                 |
| Estimable     | Sí          | Se limita a la consulta de movimientos.             |
| Pequeña       | Sí          | Tiene un alcance reducido.                          |
| Verificable   | Sí          | Se comprueba registrando y consultando movimientos. |

---

## Slice 05 — Alertas de bajo stock

### Historia

Como usuario de Depósito, quiero recibir alertas cuando una variante tenga poco stock, para poder reponerla a tiempo.

### Requisitos relacionados

RF-45, RF-47, RF-48

### Criterios de aceptación

1. El sistema debe comparar el stock con el umbral mínimo configurado.
2. Debe mostrar una alerta en el panel cuando el stock sea inferior al mínimo.
3. Debe enviar una notificación por correo al área de Depósito.

### Validación INVEST

| Criterio      | ¿Se cumple? | Observación                                        |
| ------------- | ----------- | -------------------------------------------------- |
| Independiente | Sí          | Funciona sobre el stock registrado.                |
| Negociable    | Sí          | El umbral y formato de alerta pueden ajustarse.    |
| Valiosa       | Sí          | Permite anticipar la reposición de mercadería.     |
| Estimable     | Sí          | Se basa en una regla de comparación definida.      |
| Pequeña       | Sí          | Se limita a las alertas de stock.                  |
| Verificable   | Sí          | Se prueba configurando distintos niveles de stock. |


# Slicing — HU-06: Solicitud, Gestión y Resolución de Devoluciones

## Slice 01 — Solicitud de devolución

### Historia

Como cliente registrado, quiero solicitar la devolución de un producto, para gestionar un cambio o devolución ante un inconveniente.

### Requisitos relacionados

RF-88, RF-89, RF-90

### Criterios de aceptación

1. El sistema debe permitir solicitar devoluciones de pedidos finalizados dentro de los 5 días hábiles.
2. El cliente debe seleccionar un motivo.
3. El cliente debe poder adjuntar fotografías del producto.

### Validación INVEST

| Criterio      | ¿Se cumple? | Observación                                       |
| ------------- | ----------- | ------------------------------------------------- |
| Independiente | Sí          | Funciona sobre pedidos finalizados.               |
| Negociable    | Sí          | Los motivos y cantidad de fotos pueden ajustarse. |
| Valiosa       | Sí          | Permite iniciar el reclamo de forma online.       |
| Estimable     | Sí          | Tiene un alcance definido.                        |
| Pequeña       | Sí          | Se limita a crear la solicitud.                   |
| Verificable   | Sí          | Se prueba creando solicitudes válidas.            |

---

## Slice 02 — Validación del plazo

### Historia

Como cliente, quiero que el sistema valide el plazo para solicitar una devolución, para conocer si mi pedido cumple con las condiciones establecidas.

### Requisitos relacionados

RF-91, RF-92

### Criterios de aceptación

1. El sistema debe verificar que el pedido esté dentro de los 5 días hábiles.
2. No debe permitir solicitudes fuera del plazo.
3. Debe informar al cliente cuando la devolución no sea válida por vencimiento del plazo.

### Validación INVEST

| Criterio      | ¿Se cumple? | Observación                                               |
| ------------- | ----------- | --------------------------------------------------------- |
| Independiente | Sí          | Se basa en la fecha del pedido finalizado.                |
| Negociable    | Sí          | El plazo puede configurarse según las reglas del sistema. |
| Valiosa       | Sí          | Garantiza el cumplimiento del plazo establecido.          |
| Estimable     | Sí          | Se limita a la validación de fechas.                      |
| Pequeña       | Sí          | Tiene un alcance reducido.                                |
| Verificable   | Sí          | Se prueban solicitudes dentro y fuera de plazo.           |

---

## Slice 03 — Gestión de solicitudes

### Historia

Como usuario de Ventas, quiero revisar y actualizar las solicitudes de devolución, para gestionar los reclamos de los clientes.

### Requisitos relacionados

RF-93, RF-94, RF-95

### Criterios de aceptación

1. Ventas debe poder consultar las solicitudes recibidas.
2. Debe poder actualizar el estado de una solicitud.
3. El sistema debe registrar el estado actual del caso.

### Validación INVEST

| Criterio      | ¿Se cumple? | Observación                            |
| ------------- | ----------- | -------------------------------------- |
| Independiente | Sí          | Gestiona solicitudes ya creadas.       |
| Negociable    | Sí          | Los estados pueden ajustarse.          |
| Valiosa       | Sí          | Permite administrar los reclamos.      |
| Estimable     | Sí          | Se limita a la gestión de solicitudes. |
| Pequeña       | Sí          | Agrupa acciones relacionadas.          |
| Verificable   | Sí          | Se prueba cambiando estados.           |

---

## Slice 04 — Resolución de devolución

### Historia

Como usuario de Ventas, quiero resolver una solicitud de devolución, para aprobar un cambio de producto o una devolución.

### Requisitos relacionados

RF-96, RF-97, RF-98

### Criterios de aceptación

1. El sistema debe permitir aprobar o rechazar una solicitud.
2. Si corresponde, debe permitir registrar el cambio de producto.
3. La resolución debe quedar asociada a la solicitud.

### Validación INVEST

| Criterio      | ¿Se cumple? | Observación                                   |
| ------------- | ----------- | --------------------------------------------- |
| Independiente | Sí          | Se realiza sobre solicitudes existentes.      |
| Negociable    | Sí          | Las opciones de resolución pueden ajustarse.  |
| Valiosa       | Sí          | Permite finalizar el reclamo del cliente.     |
| Estimable     | Sí          | Tiene un alcance concreto.                    |
| Pequeña       | Sí          | Se concentra en la resolución.                |
| Verificable   | Sí          | Se prueba aprobando y rechazando solicitudes. |

---

## Slice 05 — Nota de crédito y actualización de stock

### Historia

Como usuario de Ventas, quiero que una devolución aprobada genere la nota de crédito y actualice el stock, para completar correctamente la operación.

### Requisitos relacionados

RF-99, RF-100, RF-101

### Criterios de aceptación

1. Si no se realiza un cambio, el sistema debe generar automáticamente una nota de crédito.
2. El producto devuelto debe reingresar al inventario.
3. El sistema debe notificar al cliente sobre la resolución.

### Validación INVEST

| Criterio      | ¿Se cumple? | Observación                                                  |
| ------------- | ----------- | ------------------------------------------------------------ |
| Independiente | Sí          | Se ejecuta a partir de una devolución aprobada.              |
| Negociable    | Sí          | El formato de la nota y la notificación pueden ajustarse.    |
| Valiosa       | Sí          | Completa la devolución y actualiza el inventario.            |
| Estimable     | Sí          | Se limita a la resolución contable y de stock.               |
| Pequeña       | Sí          | Agrupa acciones posteriores a la aprobación.                 |
| Verificable   | Sí          | Se comprueba la nota de crédito, el stock y la notificación. |
