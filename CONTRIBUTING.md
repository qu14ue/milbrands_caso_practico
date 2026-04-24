# Guía de Contribución - Claude Code

## Comunicación con Claude Code en VS Code

Usa prefijos para optimizar tokens y respuestas:

### Prefijos Disponibles

| Prefijo | Cuándo | Ejemplo |
|---------|--------|---------|
| `[CÓDIGO]` | Solo quieres código | `[CÓDIGO] Navbar responsive` |
| `[CONCISO]` | Respuesta sin contexto | `[CONCISO] ¿Funciona esto?` |
| `[FIX]` | Corregir error | `[FIX] Línea 42: undefined` |
| `[RAPIDO]` | Máximo 1 línea | `[RAPIDO] ¿CSS o JavaScript?` |
| `[EXPLICAR]` | Necesitas contexto | `[EXPLICAR] Cómo funciona fetch` |

### Ejemplos de Uso

#### ✅ BIEN: Debugging
```
[FIX] Error en línea 45: Cannot read property 'map' of undefined
```
Claude responde: "Cambiar `array.map()` a `array?.map()`"

#### ✅ BIEN: Implementación
```
[CÓDIGO] Función que cuenta palabras en un string
```
Claude responde: Solo el código, sin explicación

#### ✅ BIEN: Refactorización
```
[CONCISO] Refactoriza esta función para usar async/await
```
Claude responde: Código refactorizado, máximo 2 líneas de explicación

#### ❌ MAL: Sin Prefijo
```
Hola, necesito ayuda. Tengo un error que dice 'undefined is not a function'
y no sé por qué. Puedes revisar mi código y decirme qué está mal?
Necesito que me expliques también por qué pasó esto...
```
Claude responde: 200+ tokens de contexto innecesario

### Impacto en Tokens

Usar prefijos correctamente = **70% menos tokens**

### Reglas de Oro

1. **Sé específico:**
   - ✅ `[CÓDIGO] Función para capitalizar string`
   - ❌ `[CÓDIGO] Nueva función`

2. **Un problema por pregunta:**
   - ✅ `[FIX] Error de CORS en fetch`
   - ❌ `[FIX] Error de CORS y también el localStorage no funciona`

3. **Contexto mínimo:**
   - ✅ `[CONCISO] ¿Debería usar fetch o axios?`
   - ❌ `[CONCISO] Tengo que hacer una solicitud HTTP. Acabo de aprender JavaScript hace poco. ¿Qué debo usar?`

4. **Usa el prefijo correcto:**
   - Quieres **código** → `[CÓDIGO]`
   - Tienes un **error** → `[FIX]`
   - Pregunta **sí/no** → `[RAPIDO]`
   - Quieres **cambios** → `[CONCISO]`
   - Necesitas **entender** → `[EXPLICAR]`

### Cuándo NO Usar Prefijos

Usa `[EXPLICAR]` o sin prefijo en:
- **Conceptos nuevos:** `[EXPLICAR] ¿Qué es una promesa?`
- **Decisiones arquitectónicas:** `¿Debería usar React o Vue?`
- **Bugs complejos:** Cuando necesites análisis profundo
- **Seguridad:** Preguntas críticas sobre XSS, CSRF, etc.

### Flujo Típico de Desarrollo

```
1. Crear feature
   [CÓDIGO] Botón que abre modal

2. Testear en navegador (manual)
   
3. Bugs encontrados
   [FIX] Modal no se cierra al hacer click fuera

4. Refactorizar
   [CONCISO] Refactoriza este CSS duplicado

5. Revisar antes de merge
   [REVISAR] ¿Está listo para producción?
```

### Performance

Respuestas típicas con prefijos:
- `[CÓDIGO]`: 30-80 tokens
- `[FIX]`: 40-100 tokens
- `[RAPIDO]`: 10-40 tokens
- `[CONCISO]`: 50-150 tokens

Respuestas típicas sin prefijos:
- Promedio: 200-400 tokens

**Ahorro al usar prefijos: ~70%**

### Archivo `.claude-instructions`

Este proyecto incluye `.claude-instructions` en la raíz.
Claude lee automáticamente este archivo.

**No necesitas mencionar "modo conciso" manualmente.**
Los prefijos hacen todo el trabajo.

### Preguntas Frecuentes

**P: ¿Puedo combinar prefijos?**
R: No. Usa uno solo. `[CÓDIGO]` y `[CONCISO]` son exclusivos.

**P: ¿Y si no sé qué prefijo usar?**
R: Pregúntate: ¿Quiero código? `[CÓDIGO]`. ¿Un sí/no? `[RAPIDO]`. ¿Cambios? `[CONCISO]`.

**P: ¿Funciona en Claude Web también?**
R: Parcialmente. Los prefijos funcionan, pero es mejor mandar instrucción global al inicio del chat.

### Tips Avanzados

Si tienes muchas preguntas seguidas:
```
[CÓDIGO] Navbar responsive
[CÓDIGO] Footer sticky
[CÓDIGO] Modal component
```

Claude entenderá el contexto y mantendrá el modo conciso.

Si hay cambio de contexto:
```
[CÓDIGO] Función para validar emails

[EXPLICAR] ¿Cómo funcionan las regex?
```

Claude reconoce que `[EXPLICAR]` requiere más contexto.
