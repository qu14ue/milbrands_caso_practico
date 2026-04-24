# Proyecto Web - Guía de Uso con Claude Code

## Estructura
```
proyecto/
├── src/
│   ├── index.html
│   ├── styles/
│   └── script.js
├── .claude-instructions (← IMPORTANTE)
└── README.md
```

## Optimización de Tokens con Claude Code

### Prefijos Recomendados

**Para código:**
```
[CÓDIGO] Función que centra un div con flexbox
```

**Para bugs:**
```
[FIX] Error en línea 42: función indefinida
```

**Para preguntas rápidas:**
```
[RAPIDO] ¿Async/await con map()?
```

**Para cambios:**
```
[CONCISO] Refactoriza esta función
```

**Cuando necesites explicación:**
```
[EXPLICAR] ¿Cómo funciona Promise.all()?
```

### Ahorro de Tokens

| Tipo | Sin Prefijo | Con Prefijo | Ahorro |
|------|-------------|------------|--------|
| Función | 150 tokens | 40 tokens | 73% |
| Bug fix | 200 tokens | 50 tokens | 75% |
| Refactor | 250 tokens | 80 tokens | 68% |
| **Promedio** | **200 tokens** | **57 tokens** | **71%** |

### Ejemplos Reales

#### Debugging
```
[FIX] TypeError: undefined is not a function en línea 45
```
Respuesta esperada: "Cambiar `.from()` a `.map()`"

#### Implementación
```
[CÓDIGO] Función para formatear fecha DD/MM/YYYY
```
Respuesta esperada: Solo el código

#### Refactorización
```
[CONCISO] Refactoriza este CSS para BEM
```
Respuesta esperada: Código refactorizado, sin explicación

### Mejores Prácticas

1. **Sé específico:** 
   - ✅ `[CÓDIGO] Validar email con regex`
   - ❌ `[CÓDIGO] Función de validación`

2. **Incluye el contexto mínimo:**
   - ✅ `[FIX] Error en fetch - CORS bloqueado`
   - ❌ `[FIX] Error` (muy vago)

3. **Usa el prefijo correcto:**
   - Código = `[CÓDIGO]`
   - Error = `[FIX]`
   - Sí/No = `[RAPIDO]`
   - Cambios = `[CONCISO]`

4. **Una pregunta por línea:**
   ```
   ✅ [CÓDIGO] Botón con hover effect
   ❌ [CÓDIGO] Botón con hover, animación y tooltip
   ```

### Cuándo NO usar Prefijos

Usa `[EXPLICAR]` o sin prefijo cuando:
- Aprendas un concepto nuevo
- Haya decisiones arquitectónicas importantes
- Necesites entender un bug complejo
- Cuestiones de seguridad crítica

Ejemplo:
```
[EXPLICAR] ¿Cuál es la diferencia entre async/await y Promise?
```

## Archivo `.claude-instructions`

Está en la raíz del proyecto y contiene instrucciones globales.
Claude las lee automáticamente cuando abres el proyecto.

**NO edites este archivo a menos que sepas qué haces.**

## Comandos Rápidos

Si usas npm scripts, agrega a `package.json`:
```json
{
  "scripts": {
    "dev": "live-server",
    "ask-claude": "echo 'Usa [CÓDIGO], [CONCISO], [FIX] o [RAPIDO]'"
  }
}
```

## Tips Finales

✅ **Siempre usa prefijos** - Ahorran 70% de tokens
✅ **Sé conciso en preguntas** - "¿Qué falta?" vs explicar el problema
✅ **Usa [RAPIDO]** - Para preguntas que merecen respuesta de 1 línea
✅ **Agrupa cambios** - Una pregunta por feature, no línea por línea

❌ **NO** pidas explicaciones cuando [CÓDIGO] es suficiente
❌ **NO** hagas múltiples preguntas en una sola línea
❌ **NO** copies el archivo `.claude-instructions` entre proyectos sin revisar
