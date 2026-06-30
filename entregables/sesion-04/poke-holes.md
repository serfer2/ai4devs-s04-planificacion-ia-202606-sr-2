
- Contraseña solo espacios o muy larga — 8 espacios pasa la regla de longitud. ¿Límite máximo? PRD solo fija mínimo.
- Validación email es (asumido) ya marcado — pero el criterio concreto de validez sigue sin definir.
- Confirmación de contraseña — PRD no lo pide; ¿campo repetir contraseña? Sin cubrir (probablemente fuera de scope, confirmar).
- Privacidad/almacenamiento de contraseña — PRD §4 exige datos seguros; la story no menciona hashing. Riesgo de seguridad si no se especifica.
- "queda autenticado" asume sesión emitida al registrar (token de acceso) — PRD §3.1 confirma tokens, pero la story no lo dice explícito.