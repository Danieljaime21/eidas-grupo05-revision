# Slicing — HU-01 Registro y Autenticación de Cliente

### Historia 1 — Formulario de registro

| Campo    | Detalle                                                                    |
| -------- | -------------------------------------------------------------------------- |
| Historia | Como cliente, quiero completar mis datos personales para crear una cuenta. |

**Criterios de aceptación**

1. Se muestran todos los campos obligatorios.
2. El sistema valida que estén completos.
3. Se informa si falta algún dato.

### Historia 2 — Validación de datos

| Campo    | Detalle                                                                               |
| -------- | ------------------------------------------------------------------------------------- |
| Historia | Como cliente, quiero que mis datos sean validados para evitar errores en el registro. |

**Criterios de aceptación**

1. Se valida el formato del email y DNI.
2. No se permiten datos duplicados.
3. Se informa el error correspondiente.

### Historia 3 — Creación de cuenta

| Campo    | Detalle                                                            |
| -------- | ------------------------------------------------------------------ |
| Historia | Como cliente, quiero crear mi cuenta para acceder a la plataforma. |

**Criterios de aceptación**

1. El sistema registra los datos válidos.
2. La contraseña se almacena de forma segura.
3. Se confirma la creación de la cuenta.

### Historia 4 — Inicio de sesión

| Campo    | Detalle                                                                  |
| -------- | ------------------------------------------------------------------------ |
| Historia | Como cliente registrado, quiero iniciar sesión para acceder a mi cuenta. |

**Criterios de aceptación**

1. El sistema solicita email y contraseña.
2. Valida las credenciales.
3. Permite el acceso si son correctas.

### Historia 5 — Autenticación para compra

| Campo    | Detalle                                                           |
| -------- | ----------------------------------------------------------------- |
| Historia | Como cliente, quiero estar autenticado para finalizar una compra. |

**Criterios de aceptación**

1. El sistema verifica que el cliente haya iniciado sesión.
2. No permite finalizar la compra sin autenticación.
3. Permite continuar si el cliente está autenticado.

---

## Caminos fallidos

| Pregunta                                         | Qué hace el sistema                        | Quién decide |
| ------------------------------------------------ | ------------------------------------------ | ------------ |
| ¿Qué pasa si falta un dato obligatorio?          | Informa el campo que debe completarse.     | Negocio      |
| ¿Qué pasa si el email o DNI ya existe?           | Rechaza el registro e informa el motivo.   | Negocio      |
| ¿Qué pasa si las credenciales son incorrectas?   | Deniega el acceso e informa el error.      | Negocio      |
| ¿Qué pasa si intenta comprar sin iniciar sesión? | Solicita autenticación antes de continuar. | Negocio      |

# Slicing — HU-02 Consulta de Historial de Compras y Estado de Pedidos

### Historia 1 — Acceso al historial

| Campo    | Detalle                                                                                              |
| -------- | ---------------------------------------------------------------------------------------------------- |
| Historia | Como cliente, quiero acceder a mi historial de compras desde "Mi Cuenta" para consultar mis pedidos. |

**Criterios de aceptación**

1. El cliente autenticado puede acceder a "Mi Cuenta".
2. Se muestra el historial de pedidos.
3. Los pedidos pertenecen únicamente al cliente.

### Historia 2 — Listado de pedidos

| Campo    | Detalle                                                                                                       |
| -------- | ------------------------------------------------------------------------------------------------------------- |
| Historia | Como cliente, quiero visualizar mis pedidos ordenados cronológicamente para consultar mis compras anteriores. |

**Criterios de aceptación**

1. Los pedidos se muestran ordenados por fecha.
2. Se muestran todos los pedidos realizados.
3. Se identifica cada pedido individualmente.

### Historia 3 — Estado del pedido

| Campo    | Detalle                                                                             |
| -------- | ----------------------------------------------------------------------------------- |
| Historia | Como cliente, quiero conocer el estado de mis pedidos para realizar su seguimiento. |

**Criterios de aceptación**

1. Cada pedido muestra su estado actualizado.
2. El estado corresponde al pedido seleccionado.
3. La información se muestra de forma clara.

### Historia 4 — Datos principales del pedido

| Campo    | Detalle                                                                                        |
| -------- | ---------------------------------------------------------------------------------------------- |
| Historia | Como cliente, quiero consultar los datos principales de un pedido para conocer su información. |

**Criterios de aceptación**

1. Se muestra el código identificador.
2. Se muestra la fecha y el importe total.
3. Se muestra el método de entrega.

### Historia 5 — Detalle de compra

| Campo    | Detalle                                                                                      |
| -------- | -------------------------------------------------------------------------------------------- |
| Historia | Como cliente, quiero consultar el detalle de un pedido para conocer los productos comprados. |

**Criterios de aceptación**

1. Se muestran los artículos comprados.
2. Se muestran las cantidades.
3. El detalle corresponde al pedido seleccionado.

---

## Caminos fallidos

| Pregunta                                        | Qué hace el sistema                                     | Quién decide |
| ----------------------------------------------- | ------------------------------------------------------- | ------------ |
| ¿Qué pasa si el cliente no tiene pedidos?       | Informa que no existen compras registradas.             | Negocio      |
| ¿Qué pasa si intenta consultar un pedido ajeno? | Impide el acceso a la información.                      | Técnica      |
| ¿Qué pasa si no se puede obtener el estado?     | Informa que el estado no está disponible temporalmente. | Técnica      |
| ¿Qué pasa si el pedido no existe?               | Informa que el pedido no fue encontrado.                | Negocio      |
