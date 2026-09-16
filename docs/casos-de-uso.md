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
| Descripción |El cliente completa el formulario con sus datos personales para crear una cuenta e iniciar
sesión en la plataforma, habilitando la navegación personalizada y el acceso obligatorio al
paso de compra. |
| Actores | Principal: Cliente/ Secundario: Sistema |
| Precondiciones |- El cliente se encuentra navegando en la plataforma.
- El cliente no cuenta con una sesión activa. |
| Postcondiciones | Éxito:La cuenta del cliente queda registrada con la contraseña cifrada, la sesión se inicia
automáticamente y el usuario accede a sus funciones privadas. / Fallo: El registro no se realiza, la sesión no se inicia y se informa al cliente el motivo del error. |

### Secuencia normal

| # | Acción (actor) | Reacción (sistema) |
|---|----------------|--------------------|
| 1 | |El cliente selecciona la opción
"Registrarse" o es redirigido desde el
flujo de checkout. |El sistema muestra el formulario de registro
solicitando todos los datos obligatorios
(nombre, apellido, email, fecha de
nacimiento, teléfono, DNI, contraseña,
dirección, CP, ciudad, provincia).
| 2 | |El cliente completa los campos
solicitados y selecciona "Crear Cuenta". |El sistema valida la estructura del email y
DNI, verifica que no existan previamente en
la base de datos (RF-06) y cifra la contraseña
de forma segura.
| 3 | |El cliente confirma el registro. |El sistema crea la cuenta de usuario, inicia la
sesión automáticamente y muestra un
mensaje de confirmación de registro exitoso.

### Excepciones

| # | Situación | Respuesta del sistema |
|---|-----------|-----------------------|
| E1 | |El cliente intenta registrarse omitiendo
campos obligatorios o con datos con
formato inválido. |El sistema no completará el registro, resaltará
los campos con error y mostrará un mensaje
indicando las correcciones requeridas
(RNF-10)
| E2 | El cliente intenta registrarse con un
correo electrónico o DNI previamente
existente. | El sistema informará que el usuario ya existe
y ofrecerá opciones directas para iniciar
sesión o recuperar la contraseña.
| E3 | |El cliente intenta finalizar una compra
sin haber iniciado sesión. |El sistema interrumpe el checkout, exige el
registro o inicio de sesión obligatorio (RF-10)
y, tras completarse con éxito, redirige al
cliente a la confirmación de su pedido.
| E4 | |Se produce un error de conexión o
servidor durante el proceso. | El sistema informa que no fue posible
procesar la solicitud y mantiene el formulario
con los datos ingresados para reintentar.

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
| Nombre | |
| Descripción | |
| Actores | Principal: / Secundario: |
| Precondiciones | |
| Postcondiciones | Éxito: / Fallo: |

### Secuencia normal

| # | Acción (actor) | Reacción (sistema) |
|---|----------------|--------------------|
| 1 | | |
| 2 | | |

### Excepciones

| # | Situación | Respuesta del sistema |
|---|-----------|-----------------------|
| E1 | | |

| Campo | Detalle |
|-------|---------|
| Rendimiento | |
| Frecuencia | |
| Importancia | |
| Urgencia | |
