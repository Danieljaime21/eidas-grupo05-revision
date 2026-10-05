# Ejercicio: partir una épica en slices verticales

## La épica

> Como cliente de Mundo Sport, quiero comprar prendas desde la tienda online y pagarlas con
> Mercado Pago, para recibirlas en mi casa o retirarlas en el local sin tener que ir a elegirlas
> al negocio.

_Así como está, es una épica gorda: no se puede estimar, no se puede terminar en una
iteración, y esconde decisiones que nadie tomó todavía._

Esta épica reúne HU-03 (carrito), HU-04 (checkout) y HU-05 (pago), y se apoya en RF-12, RF-27 a RF-31 y RF-33.

---

## Parte A — Historias verticales

_Entre 5 y 8 historias VERTICALES. Vertical significa que cada historia, sola, entrega algo
usable de punta a punta ("diseñar la pantalla de envío" no es vertical; "enviar dinero a un
contacto de la agenda con saldo suficiente" sí)._

### Historia 1 — Comprar con retiro en el local y pago aprobado

| Campo | Detalle |
|-------|---------|
| Historia | Como cliente registrado, quiero comprar una prenda eligiendo talle y color, retirarla en el local y pagarla con Mercado Pago, para completar mi compra sin cargar datos de envío. |
| Requisitos relacionados | RF-12, RF-27, RF-28, RF-29, RF-30 |

**Criterios de aceptación**

1. El sistema exige elegir talle y color para agregar la prenda al carrito y no permite agregar una variante sin stock.
2. Si el cliente no tiene sesión iniciada, antes de pagar se le pide ingresar o registrarse y su carrito se conserva (RF-12).
3. Al finalizar la compra, el cliente puede elegir "Retiro en el local": el envío cuesta $0 y se muestran la dirección y el horario del local.
4. El cliente paga con tarjeta de crédito o débito en Mercado Pago; si el pago es aprobado, el sistema crea el pedido con un número único, en estado "Pagado", y descuenta el stock de la prenda.
5. El cliente ve el pedido en "Mi Cuenta" y recibe un email de confirmación (RF-30).

---

### Historia 2 — Recibir la compra en mi domicilio con el costo de envío calculado

| Campo | Detalle |
|-------|---------|
| Historia | Como cliente registrado, quiero elegir el envío a domicilio y ver su costo antes de pagar, para decidir si me conviene recibir la compra en mi casa. |
| Requisitos relacionados | RF-28, RF-29 |

**Criterios de aceptación**

1. Al elegir "Envío a domicilio", el cliente confirma o edita su teléfono y su dirección (calle, número, piso/depto, ciudad, provincia y código postal); si falta un dato obligatorio, el sistema indica cuál (RNF-10).
2. El sistema calcula el costo de envío con el proveedor logístico según la dirección y lo suma al total antes del pago.
3. Si el código postal no tiene cobertura, el sistema lo informa y ofrece retirar en el local o corregir el dato.
4. Si falla la consulta de tarifa, el sistema permite reintentar sin perder los datos cargados.
5. El pedido pagado queda registrado con el costo de envío y la dirección de entrega elegida.

---

### Historia 3 — Reintentar o esperar cuando el pago no se aprueba

| Campo | Detalle |
|-------|---------|
| Historia | Como cliente, quiero que si Mercado Pago rechaza mi pago o lo deja pendiente pueda reintentar o esperar la confirmación sin perder mi compra, para no tener que armar el carrito de nuevo ni pagar dos veces. |
| Requisitos relacionados | RF-29, RF-30 |

**Criterios de aceptación**

1. Si Mercado Pago rechaza el pago, el sistema informa el rechazo, no cambia el estado del pedido ni cobra nada, y permite reintentar o volver al carrito.
2. Si el pago queda pendiente de verificación, el pedido queda en "Pendiente de pago" y el cliente recibe un aviso de que se está confirmando.
3. Cuando Mercado Pago confirma un pago pendiente, el pedido pasa a "Pagado" y el cliente recibe el email correspondiente.
4. Si el cliente reintenta el pago, el nuevo intento se asocia al mismo pedido y no se genera un segundo pedido.

---

### Historia 4 — Ajustar el carrito antes de pagar

| Campo | Detalle |
|-------|---------|
| Historia | Como visitante o cliente, quiero cambiar cantidades, quitar productos o vaciar el carrito viendo el total actualizado, para armar la compra que realmente quiero. |
| Requisitos relacionados | RF-20, RF-27 |

**Criterios de aceptación**

1. El sistema permite aumentar o disminuir la cantidad de un producto y recalcula el subtotal y el total en el momento.
2. Si la cantidad supera el stock, el sistema no la actualiza e informa cuántas unidades hay disponibles.
3. El sistema permite quitar un producto individual y vaciar todo el carrito; para vaciarlo pide confirmación.
4. Si el carrito queda sin productos, el sistema lo muestra vacío con un acceso al catálogo.

---

### Historia 5 — Seguir el estado de mi pedido

| Campo | Detalle |
|-------|---------|
| Historia | Como cliente, quiero ver el estado de mis pedidos en "Mi Cuenta" y recibir un email en cada cambio, para saber cuándo recibirlo o retirarlo sin consultar al local. |
| Requisitos relacionados | RF-07, RF-30, RF-34, RF-36 |

**Criterios de aceptación**

1. "Mi Cuenta" muestra un listado cronológico con número de pedido, fecha, importe total y estado (Pendiente de pago, Pagado / En preparación, Enviado, Listo para retirar, Entregado o Cancelado).
2. El sistema envía un email al cliente cada vez que el pedido cambia de estado.
3. Si el pedido tiene envío, el cliente ve el número de seguimiento informado por el proveedor; si está listo para retirar, ve la fecha límite de retiro.
4. Si el cliente todavía no tiene pedidos, el sistema lo informa y ofrece ir al catálogo.

---

### Historia 6 — Cancelar un pedido antes del despacho

| Campo | Detalle |
|-------|---------|
| Historia | Como cliente, quiero cancelar mi pedido mientras no fue enviado ni entregado, para no recibir una compra que ya no quiero. |
| Requisitos relacionados | RF-30, RF-31 |

**Criterios de aceptación**

1. "Cancelar pedido" solo está disponible mientras el pedido no fue enviado ni entregado; después aparece deshabilitado con el motivo.
2. Antes de cancelar, el sistema pide confirmación al cliente.
3. Al cancelar, el pedido pasa a "Cancelado", se repone el stock de sus prendas y el cliente recibe el email correspondiente.

---

### Historia 7 — Pagar menos con un cupón de descuento

| Campo | Detalle |
|-------|---------|
| Historia | Como cliente, quiero aplicar un cupón vigente en mi carrito, para pagar menos por mi compra. |
| Requisitos relacionados | RF-27, RF-33 |

**Criterios de aceptación**

1. El cliente ingresa el código del cupón en el carrito y el sistema valida que esté vigente y que tenga usos disponibles.
2. Si el cupón es válido, el sistema muestra el descuento aplicado y el nuevo total.
3. Si el cupón está vencido, agotado o ya hay otro aplicado, el sistema informa el motivo y no modifica el total (solo se admite un cupón por pedido).
4. Al confirmarse el pago, el sistema registra el uso del cupón en el pedido.

---

## Parte B — Los caminos que no salen bien

_Elijan UNA de las historias de la Parte A. Las últimas tres preguntas son las importantes:
para cada una, indiquen qué debería hacer el sistema y quién tendría que decidirlo._

**Historia elegida:** Historia 1 — Comprar con retiro en el local y pago aprobado

| Pregunta | Qué hace el sistema | Quién decide (analista / negocio / técnica) |
|----------|----------------------|-----------------------------------------------|
| ¿Qué pasa si la prenda se agota mientras el cliente paga? | Antes de enviar al cliente a Mercado Pago, el sistema vuelve a verificar el stock de cada prenda. Si alguna se agotó, no inicia el pago: avisa cuál y deja ajustar el carrito. Si el stock se agota recién con el pago ya aprobado, el pedido queda "Pagado" y se avisa al Empleado para que contacte al cliente y le ofrezca esperar la reposición o reintegrarle el pago. | Negocio (si se reserva el stock mientras el cliente paga, y qué se ofrece si se agota con el pago aprobado) + Técnica (verificar y descontar el stock de forma atómica). |
| ¿Qué pasa si Mercado Pago rechaza el pago o lo deja pendiente? | Rechazado: informa el rechazo, no cobra ni cambia el estado del pedido y permite reintentar o volver al carrito. Pendiente: el pedido queda en "Pendiente de pago", se avisa al cliente que se está confirmando y se actualiza cuando Mercado Pago lo notifica. | Analista (mensajes y estados que ve el cliente) + Negocio (cuánto tiempo se mantiene un pedido pendiente antes de cancelarlo y liberar el stock). |
| ¿Qué pasa si Mercado Pago cobra pero el sistema falla antes de crear el pedido? | Apenas Mercado Pago notifica el pago aprobado, el sistema guarda el identificador de la transacción y recién después crea el pedido. Si la creación falla, se reintenta sola con ese identificador, sin cobrar de nuevo ni duplicar el pedido. Mientras tanto el cliente ve "Estamos confirmando tu pago". Si tras los reintentos no se pudo crear, se registra el error (RNF-18) y se avisa al Dueño para completar el pedido a mano o reintegrar el pago. | Técnica (guardar la transacción antes de crear el pedido y reintentar sin duplicados) + Negocio (quién resuelve los casos que no se recuperan solos y en qué plazo se reintegra). |
| ¿Qué pasa si el cliente aprieta "Pagar" dos veces? | El botón se deshabilita en el primer clic y cada pago lleva como referencia el número del pedido, así que un segundo clic reutiliza el mismo pago de Mercado Pago: se genera un solo cobro y un solo pedido. | Técnica (que la operación sea idempotente) + Analista (qué ve el cliente: botón deshabilitado e indicador de carga, RNF-11). |
| ¿Qué pasa si se cae la conexión justo después de confirmar el pago? | El resultado no depende del navegador: Mercado Pago avisa al servidor y el pedido se crea o se actualiza igual. Cuando el cliente vuelve, "Mis pedidos" muestra el estado real (Pagado o Pendiente de pago) y recibe el email correspondiente, así que nunca queda en un estado ambiguo. | Técnica (confirmación de servidor a servidor, independiente del cliente) + Analista (cómo se comunica el estado final al volver). |

---

## Parte C — Defensa

_Se hace oral, en el plenario. No se documenta en este archivo._
