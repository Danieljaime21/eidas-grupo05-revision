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

_Las tres historias corresponden al propio proyecto (Sistema de e-commerce Mundo Sport). La
Historia 1 ya está redactada en `docs/historias-de-usuario.md`; las Historias 2 y 3 se
construyeron para este ejercicio a partir de requisitos funcionales ya relevados. Es
esperable —y deseable— que alguna no pase._

### Historia 1 — HU-01: Crear usuario interno

> Como Administrador, quiero crear usuarios internos y asignarles un rol, para permitir que
> los empleados accedan al sistema según sus responsabilidades. (RF-01, RF-03, RF-04)

| Ítem (según checklist) | ¿Pasa? | Qué le falta (si no pasa) |
|-------------------------|--------|-----------------------------|
| 1 | Parcial | 3 de los 4 criterios son concretos, pero el primero ("ingresar los datos necesarios") no dice cuáles son esos datos. |
| 2 | **No** | Faltan RF-05 (el Administrador gestiona usuarios, incluida su creación) y RF-06 (registrar qué usuario hizo cada modificación), ambos aplicables a esta acción y no citados. |
| 3 | Sí | El alcance se limita a crear un usuario y asignarle un rol; entra cómodo en un sprint. |
| 4 | Sí | Actor "Administrador" identificado sin ambigüedad. |
| 5 | Sí | El sistema informa al Administrador si el usuario fue creado correctamente. |
| 6 | **No** | No están definidos los campos exactos del formulario de alta. |
| 7 | Sí | El valor ("permitir que los empleados accedan al sistema según sus responsabilidades") está explícito. |

---

### Historia 2 — Aplicar cupón de descuento en el carrito

> Como Cliente, quiero aplicar un cupón de descuento en mi carrito, para pagar menos por mi
> compra. (RF-116, RF-117, RF-118)

| Ítem (según checklist) | ¿Pasa? | Qué le falta (si no pasa) |
|-------------------------|--------|-----------------------------|
| 1 | **No** | No tiene ningún criterio de aceptación redactado. |
| 2 | Sí | RF-116, RF-117 y RF-118 cubren la acción de aplicar el cupón; los de creación del cupón (RF-108 a RF-112) corresponden a otra historia (HU-09). |
| 3 | **No** | Mezcla validar el cupón, calcular el descuento y actualizar el resumen del pedido sin desglosar. |
| 4 | Sí | Actor "Cliente" identificado sin ambigüedad. |
| 5 | **No** | No hay ningún criterio de terminado definido. |
| 6 | **No** | No especifica el dato de entrada (código del cupón) ni cómo se muestra el descuento aplicado. |
| 7 | Sí | El valor ("pagar menos por mi compra") está explícito. |

---

### Historia 3 — Consultar estado de pedido desde "Mi Cuenta"

> Como Cliente, quiero consultar el estado actual de mis pedidos desde "Mi Cuenta", para saber
> en qué etapa se encuentra mi compra sin tener que contactar a la tienda. (RF-72, RF-75, RF-78)

| Ítem (según checklist) | ¿Pasa? | Qué le falta (si no pasa) |
|-------------------------|--------|-----------------------------|
| 1 | **No** | No tiene ningún criterio de aceptación redactado. |
| 2 | Sí | RF-72 (consultar estado), RF-75 (estados posibles) y RF-78 (fecha/hora de cada cambio) cubren la historia completa. |
| 3 | Sí | Es solo lectura de un estado ya calculado por el sistema; no agrega lógica nueva. |
| 4 | Sí | Actor "Cliente" identificado sin ambigüedad. |
| 5 | Sí | Se puede comprobar que el estado mostrado coincide con el registrado en la base. |
| 6 | **No** | No se especifica qué se muestra exactamente en pantalla (solo el estado, o también fecha/hora del cambio, historial completo, etc.). |
| 7 | Sí | El valor ("saber en qué etapa está mi compra sin contactar a la tienda") está explícito. |
