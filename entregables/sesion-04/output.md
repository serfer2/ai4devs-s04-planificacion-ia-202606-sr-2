# User Stories — FlowSync MVP

> Backlog derivado del PRD (`docs/PRD.md`), sección "Qué incluye el MVP" y requisitos funcionales (sección 3). Solo funcionalidades del MVP. Las inferencias no explícitas en el PRD están marcadas con `(asumido)`.

---

## Épica 1 — Autenticación y gestión de cuenta

### Story: Registro de cuenta con email y contraseña
**Como** visitante, **quiero** crear una cuenta con mi email y contraseña, **para** empezar a usar FlowSync con datos propios y privados.

#### AC (Given/When/Then)
**Given** un visitante en la pantalla de registro
**When** introduce un email válido y una contraseña de al menos 8 caracteres
**Then** se crea su cuenta y queda autenticado

**Given** un visitante en la pantalla de registro
**When** introduce una contraseña de menos de 8 caracteres
**Then** se muestra un mensaje de validación comprensible y no se crea la cuenta

**Given** un visitante que introduce un email con formato inválido (asumido)
**When** intenta registrarse
**Then** se muestra un error de validación claro y no se crea la cuenta

**Given** un email que ya está registrado
**When** el visitante intenta registrarse con ese email
**Then** el sistema lo indica y ofrece un enlace para ir al inicio de sesión

---

### Story: Pantalla de bienvenida tras el registro
**Como** usuario recién registrado, **quiero** ver una pantalla de bienvenida que explique qué hace FlowSync, **para** entender el producto y crear mi primera tarea.

#### AC (Given/When/Then)
**Given** un usuario que acaba de completar el registro con éxito
**When** se completa el alta
**Then** es llevado a una pantalla de bienvenida (onboarding mínimo)

**Given** la pantalla de bienvenida
**When** el usuario la visualiza
**Then** ve en una frase qué hace FlowSync y una invitación a crear su primera tarea

**Given** la pantalla de bienvenida
**When** el usuario acepta la invitación a crear su primera tarea
**Then** es dirigido al flujo de creación de tarea (asumido)

---

### Story: Inicio de sesión
**Como** usuario registrado, **quiero** iniciar sesión con mi email y contraseña, **para** acceder a mis tareas.

#### AC (Given/When/Then)
**Given** un usuario en la pantalla de inicio de sesión
**When** introduce credenciales válidas (email y contraseña)
**Then** se inicia sesión y es redirigido a la home (asumido)

**Given** un usuario en la pantalla de inicio de sesión
**When** introduce credenciales incorrectas
**Then** se muestra un error claro y no se inicia sesión

**Given** un usuario con sesión iniciada
**When** vuelve a la aplicación con su token de acceso vigente
**Then** la sesión se mantiene sin pedir credenciales de nuevo

---

### Story: Cierre de sesión
**Como** usuario autenticado, **quiero** cerrar sesión, **para** proteger el acceso a mi cuenta.

#### AC (Given/When/Then)
**Given** un usuario autenticado
**When** selecciona cerrar sesión
**Then** la sesión finaliza y deja de tener acceso a sus tareas

**Given** un usuario que ha cerrado sesión
**When** intenta acceder a una pantalla privada (asumido)
**Then** es redirigido a la pantalla de inicio de sesión (asumido)

---

### Story: Aislamiento de datos entre usuarios
**Como** usuario, **quiero** que mis datos no sean visibles para otros usuarios, **para** mantener mi información privada.

#### AC (Given/When/Then)
**Given** dos usuarios distintos con sus propias tareas
**When** un usuario ve su listado de tareas
**Then** solo ve sus propias tareas y nunca las de otro usuario

**Given** un usuario autenticado
**When** intenta acceder a una tarea que pertenece a otro usuario (asumido)
**Then** el sistema no se la muestra (asumido)

---

## Épica 2 — Gestión de tareas (CRUD)

### Story: Crear una tarea
**Como** usuario, **quiero** crear una tarea indicando al menos un título, **para** registrar un pendiente.

#### AC (Given/When/Then)
**Given** un usuario autenticado en el formulario de creación de tarea
**When** introduce un título y guarda
**Then** la tarea se crea y aparece en su listado

**Given** un usuario en el formulario de creación de tarea
**When** intenta guardar sin título
**Then** se muestra un error de validación claro y no se crea la tarea

**Given** un usuario creando una tarea
**When** añade opcionalmente descripción y/o fecha límite
**Then** la tarea se guarda con esos campos opcionales

**Given** una tarea recién creada
**When** se guarda
**Then** nace con estado `pending`

---

### Story: Ver el listado de tareas
**Como** usuario, **quiero** ver el listado de mis tareas, **para** saber qué tengo pendiente.

#### AC (Given/When/Then)
**Given** un usuario autenticado con tareas creadas
**When** abre el listado de tareas
**Then** ve sus tareas con al menos título y estado (asumido)

**Given** un usuario con tareas
**When** se carga el listado
**Then** las tareas se muestran ordenadas con las más relevantes para "hoy" primero

**Given** un usuario con hasta 200 tareas
**When** abre el listado
**Then** el listado carga en menos de 1 segundo

---

### Story: Editar una tarea
**Como** usuario, **quiero** editar cualquier campo de una tarea existente, **para** mantenerla actualizada.

#### AC (Given/When/Then)
**Given** un usuario que ha abierto una tarea existente
**When** modifica título, descripción y/o fecha límite y guarda
**Then** los cambios quedan reflejados en la tarea

**Given** un usuario editando una tarea
**When** borra el título dejándolo vacío
**Then** se muestra un error de validación y no se guarda el cambio (asumido)

**Given** un usuario que ha editado una tarea
**When** vuelve al listado
**Then** ve los datos actualizados de la tarea

---

### Story: Borrar una tarea
**Como** usuario, **quiero** borrar una tarea, **para** eliminar pendientes que ya no necesito.

#### AC (Given/When/Then)
**Given** un usuario con una tarea en su listado
**When** selecciona borrarla
**Then** la tarea deja de aparecer en su listado

**Given** un usuario que va a borrar una tarea
**When** se solicita confirmación de borrado (asumido)
**Then** la tarea solo se elimina si confirma (asumido)

---

### Story: Cambiar el estado de una tarea
**Como** usuario, **quiero** cambiar el estado de una tarea, **para** reflejar su situación (pendiente, completada o archivada).

#### AC (Given/When/Then)
**Given** una tarea en estado `pending`
**When** el usuario la marca como completada
**Then** la tarea pasa a estado `completed`

**Given** una tarea en estado `pending` o `completed`
**When** el usuario la archiva
**Then** la tarea pasa a estado `archived`

**Given** una tarea cuyo estado ha cambiado
**When** el usuario consulta el listado
**Then** la tarea refleja su nuevo estado

---

## Épica 3 — Organización y filtrado

### Story: Filtrar tareas por estado
**Como** usuario, **quiero** filtrar mis tareas por estado, **para** centrarme solo en las que me interesan.

#### AC (Given/When/Then)
**Given** un usuario con tareas en distintos estados
**When** filtra por `pending`
**Then** solo ve las tareas pendientes

**Given** un usuario con tareas en distintos estados
**When** filtra por `completed`
**Then** solo ve las tareas completadas

**Given** un usuario con un filtro aplicado
**When** quita el filtro (asumido)
**Then** vuelve a ver todas sus tareas (asumido)

---

### Story: Estado vacío del listado
**Como** usuario sin tareas, **quiero** ver un mensaje que me invite a crear la primera, **para** saber cómo empezar.

#### AC (Given/When/Then)
**Given** un usuario con una cuenta nueva y sin tareas
**When** abre el listado
**Then** ve un estado vacío con una invitación a crear la primera tarea

**Given** un usuario cuyas tareas están todas archivadas
**When** abre el listado por defecto (asumido)
**Then** ve el estado vacío con la invitación a crear una tarea

**Given** un usuario en el estado vacío
**When** acepta la invitación
**Then** es dirigido a la creación de tarea (asumido)

---

## Épica 4 — Exportación

### Story: Exportar tareas a CSV
**Como** usuario, **quiero** exportar mis tareas a un archivo CSV, **para** llevarme mis datos.

#### AC (Given/When/Then)
**Given** un usuario autenticado con tareas
**When** solicita exportar a CSV
**Then** se genera un archivo CSV descargable con sus tareas

**Given** el archivo CSV generado
**When** el usuario lo abre
**Then** cada fila incluye al menos título, descripción, estado y fecha límite de la tarea

**Given** un usuario sin tareas (asumido)
**When** solicita exportar a CSV
**Then** se genera un CSV solo con la cabecera, sin filas de datos (asumido)

---

## Épica 5 — Sincronización con Google Calendar

### Story: Conectar la cuenta de Google
**Como** usuario, **quiero** conectar mi cuenta de Google a FlowSync, **para** que mis tareas se reflejen en mi calendario.

#### AC (Given/When/Then)
**Given** un usuario autenticado que aún no ha conectado Google
**When** inicia la conexión de Google
**Then** se le solicita la autorización OAuth de Google

**Given** un usuario que completa la autorización OAuth con éxito
**When** vuelve a FlowSync
**Then** su cuenta de Google queda conectada

**Given** un usuario que cancela o rechaza la autorización (asumido)
**When** vuelve a FlowSync
**Then** la cuenta no queda conectada y se le informa de forma clara (asumido)

---

### Story: Las tareas con fecha aparecen como eventos
**Como** usuario con Google conectado, **quiero** que mis tareas con fecha límite aparezcan como eventos, **para** no copiarlas a mano al calendario.

#### AC (Given/When/Then)
**Given** un usuario con Google conectado
**When** crea una tarea con fecha límite
**Then** se crea un evento correspondiente en su Google Calendar

**Given** un usuario con Google conectado
**When** crea una tarea sin fecha límite
**Then** no se crea ningún evento en el calendario (asumido)

**Given** un usuario que conecta Google teniendo ya tareas con fecha (asumido)
**When** se completa la conexión
**Then** esas tareas con fecha se reflejan como eventos en el calendario (asumido)

---

### Story: Actualizar el evento al cambiar la fecha de una tarea
**Como** usuario con Google conectado, **quiero** que al cambiar la fecha de una tarea se actualice su evento, **para** mantener el calendario alineado.

#### AC (Given/When/Then)
**Given** una tarea con fecha límite ya reflejada como evento
**When** el usuario cambia la fecha de la tarea en FlowSync
**Then** el evento correspondiente en Google Calendar se actualiza con la nueva fecha

**Given** una tarea sin fecha límite y sin evento
**When** el usuario le añade una fecha límite
**Then** se crea el evento correspondiente en el calendario (asumido)

---

### Story: Reflejar en el calendario la finalización o el borrado de una tarea
**Como** usuario con Google conectado, **quiero** que al completar o borrar una tarea su evento se actualice o elimine, **para** que el calendario no muestre pendientes que ya no existen.

#### AC (Given/When/Then)
**Given** una tarea con evento en el calendario
**When** el usuario completa la tarea en FlowSync
**Then** el evento correspondiente se marca o elimina según corresponda

**Given** una tarea con evento en el calendario
**When** el usuario borra la tarea en FlowSync
**Then** el evento correspondiente se elimina del calendario

---

### Story: Desconectar la cuenta de Google
**Como** usuario, **quiero** desconectar mi cuenta de Google en cualquier momento, **para** dejar de sincronizar sin perder mis tareas.

#### AC (Given/When/Then)
**Given** un usuario con Google conectado
**When** desconecta su cuenta de Google
**Then** FlowSync deja de sincronizar con el calendario

**Given** un usuario que desconecta Google
**When** se completa la desconexión
**Then** las tareas ya creadas en FlowSync se conservan

**Given** un usuario que ha desconectado Google
**When** crea o edita una tarea con fecha
**Then** no se crea ni actualiza ningún evento en el calendario (asumido)

---

### Story: Sincronización resiliente ante fallos de la API de Google
**Como** usuario, **quiero** que mis tareas se guarden aunque la sincronización falle, **para** no perder datos cuando Google no esté disponible.

#### AC (Given/When/Then)
**Given** un usuario con Google conectado y la API de Google no disponible o devolviendo error
**When** crea o modifica una tarea con fecha
**Then** la tarea se guarda en FlowSync aunque la sincronización falle

**Given** una operación de sincronización que ha fallado
**When** el sistema la procesa más tarde
**Then** la sincronización se reintenta

**Given** operaciones de sincronización con Google
**When** se ejecutan (con éxito o con fallo)
**Then** quedan registradas en logs para poder diagnosticar fallos
