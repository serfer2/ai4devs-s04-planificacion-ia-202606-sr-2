# Prompt de descomposición para FlowSync MVP

## Rol
Tu rol es el de un senior product owner cuyo objetivo es crear user stories, bien acotadas y con criterios de aceptación claros

## Contexto
FlowSync es una aplicación web de gestión de tareas personales que mantiene sincronizadas las tareas del usuario con su Google Calendar.

Antes de empezar, analiza el PRD de `docs/PRD.md`. Allí se detalla qué es (Resumen ejecutivo). El alcance del MVP se detalla en la sección "Qué incluye el MVP".

## Formato de Salida
Las stories deben tener el siguiente formato

```
## Story: 
**Como** [rol], **quiero** [acción], **para** [beneficio].
**Como** usuario **quiero** hscer login usando mi email y contraseña **para** hacer uso de FlowSync


## AC en formato (Given/When/Then): 
**Given**
un usuario navegando en la pantalla de inicio de sesión
**When**
introduzco credenciales válidas (email y contraseña)
**Then**
se inicia sesión con mi cuenta de usuario y soy redirigido a la home
```

Cada story debe tener de 3 a 5 AC verificables.

## Agrupacion
Las stories agrupadas por módulo, caso de uso o épica, según tenga más sentido para FlowSync

## Restricciones
- Solo funcionalidades del MVP (la sección correspondiente del PRD); sin inventar features que no estén en el documento.
- No hagas estimaciones de tiempos ni SP ni nada por el estilo.
- No hagas menciones ni propuestas que tengan que ver con la arquitectura técnica.

## Instrucción de transparencia
Debes marcar con `(asumido)`, todas las inferencias que hagas y que no estén explicitamente en el PRD.
