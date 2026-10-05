# Definition of Ready (DoR)

_Antes de que una historia entre a desarrollo, tiene que pasar un filtro: el Definition of
Ready. Es un acuerdo del equipo sobre qué condiciones mínimas debe cumplir una historia para
considerarse "lista para trabajar". Si no las cumple, vuelve a refinamiento._

---

## Checklist del equipo

_7 ítems, en formato sí/no verificable._

| # | Ítem | Justificación (qué problema evita) |
|---|------|--------------------------------------------------------|
| 1 | ¿Tiene criterios de aceptación redactados de forma concreta y sin ambigüedad? | Sin criterios objetivos no hay forma de acordar cuándo la historia está terminada. |
| 2 | ¿Todos los requisitos funcionales asociados están incluidos? | Si falta un RF relevante, se puede implementar la historia sin cubrir algo ya acordado con el comitente. |
| 3 | ¿Posee un tamaño estimado capaz de ser completado en un sprint? | Una historia demasiado grande ("épica disfrazada") no da feedback rápido ni permite detectar problemas a tiempo. |
| 4 | ¿Identifica claramente al actor que la ejecuta? | La ambigüedad sobre quién realiza la acción genera errores de permisos y de diseño de pantallas para el rol equivocado. |
| 5 | ¿Puede verificarse que la historia esté terminada? | Sin una forma concreta de comprobarlo, el cierre de la historia queda a juicio subjetivo de quien la revisa. |
| 6 | ¿Los datos de entrada/salida necesarios se encuentran especificados? | Sin los campos concretos definidos, cada desarrollador completa el formulario o la salida a su criterio. |
| 7 | ¿Identifica claramente el valor que obtiene? | Sin un beneficio explícito, el equipo puede terminar construyendo funcionalidad que nadie necesita. |

---

## Aplicación a tres historias propias

_Las tres historias corresponden al propio proyecto (Sistema de e-commerce Mundo Sport). Las
Historias 1 y 2 son hipotéticas: se construyeron para este ejercicio a partir de requisitos y
casos de uso ya relevados, y no figuran en `docs/historias-de-usuario.md`. La Historia 3 es la
HU-02 real del proyecto. Es esperable —y deseable— que alguna no pase._

### Historia 1 — Alta de usuario del personal (hipotética)

> Como Dueño, quiero crear usuarios del personal y asignarles un rol, para permitir que
> los empleados accedan al sistema según sus responsabilidades. (RF-01, RF-04, RF-05)

| Ítem (según checklist) | ¿Pasa? | Qué le falta (si no pasa) |
|-------------------------|--------|-----------------------------|
| 1 | **No** | No tiene criterios de aceptación redactados: existe el CU-03 con su secuencia y excepciones, pero no una lista de criterios verificables para la historia. |
| 2 | Sí | RF-01 (alta con rol), RF-04 (ingreso con las funcionalidades del rol) y RF-05 (funcionalidades por rol) cubren la historia. |
| 3 | Sí | El alcance se limita a crear un usuario del personal y asignarle un rol; entra cómodo en un sprint. |
| 4 | Sí | Actor "Dueño" identificado sin ambigüedad (RF-01). |
| 5 | Sí | El sistema muestra una confirmación y el nuevo usuario aparece en el listado del personal (CU-03, pasos 3 y 4). |
| 6 | **No** | CU-03 deja los campos del formulario abiertos ("nombre, apellido, email, teléfono, etc.") y no define el formato de la salida. |
| 7 | Sí | El valor ("permitir que los empleados accedan al sistema según sus responsabilidades") está explícito. |

---

### Historia 2 — Aplicar cupón de descuento en el carrito (hipotética)

> Como Cliente, quiero aplicar un cupón de descuento en mi carrito, para pagar menos por mi
> compra. (RF-27, RF-33)

| Ítem (según checklist) | ¿Pasa? | Qué le falta (si no pasa) |
|-------------------------|--------|-----------------------------|
| 1 | **No** | No tiene ningún criterio de aceptación redactado. |
| 2 | Parcial | RF-27 (carrito) y RF-33 (vigencia, límite de usos y un solo cupón por pedido) cubren la acción, pero ningún requisito dice si un cupón se acumula con una promoción activa (RF-32). |
| 3 | **No** | Mezcla validar el cupón, calcular el descuento y actualizar el resumen del pedido sin desglosar. |
| 4 | Sí | Actor "Cliente" identificado sin ambigüedad. |
| 5 | **No** | No hay ningún criterio de terminado definido. |
| 6 | **No** | No especifica el dato de entrada (código del cupón) ni cómo se muestra el descuento aplicado. |
| 7 | Sí | El valor ("pagar menos por mi compra") está explícito. |

---

### Historia 3 — HU-02: Consulta de historial de compras y estado de pedidos

> Como cliente, quiero visualizar el historial de mis compras y el estado de mis pedidos
> dentro de "Mi Cuenta", para hacer seguimiento de mis pedidos y consultar mis compras
> anteriores. (RF-07)

| Ítem (según checklist) | ¿Pasa? | Qué le falta (si no pasa) |
|-------------------------|--------|-----------------------------|
| 1 | Sí | Tiene 3 criterios concretos en `docs/historias-de-usuario.md`: listado cronológico, datos de cada pedido (código, fecha, importe y estado) y detalle (artículos, cantidades y método de entrega). |
| 2 | **No** | Cita solo RF-07; los estados que muestra salen de RF-30 (Pendiente de pago, Pagado / En preparación, Enviado, Listo para retirar, Entregado y Cancelado), que no está incluido. |
| 3 | Sí | Es solo lectura de datos que ya existen; no agrega lógica nueva y entra en un sprint. |
| 4 | Sí | Actor "cliente" identificado sin ambigüedad. |
| 5 | Sí | Se puede comprobar que los pedidos del cliente aparezcan con sus datos, detalle y estado (criterios 1 a 3). |
| 6 | Sí | Los criterios 2 y 3 enumeran lo que se muestra: código, fecha, importe y estado en el listado; artículos, cantidades y método de entrega en el detalle. No requiere datos de entrada. |
| 7 | Sí | El valor ("hacer seguimiento de mis pedidos y consultar mis compras anteriores") está explícito. |
