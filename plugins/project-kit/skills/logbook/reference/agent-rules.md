# Reglas del agente — el bloque que escribe `init`

Las reglas del día a día (registrar deuda, ciclo de tarea, códigos) tienen que
valer en **todas** las sesiones, aunque el skill no esté cargado. Por eso `init`
copia este bloque al archivo de instrucciones que el agente lee siempre (ver
`init.md`, paso 5).

Se copia **tal cual**, marcas incluidas. Todo lo que está entre
`<!-- logbook:start` y `<!-- logbook:end -->` es del skill: al volver a correr
`init` se reemplaza entero.

~~~markdown
<!-- logbook:start — lo escribe el skill logbook (init); se reemplaza entero al volver a correrlo -->
## Logbook (`docs/logbook/`)

Cada proyecto registra su trabajo en cuatro archivos versionados en git dentro
de `docs/logbook/`. `docs/` arriba queda para material conceptual (visión,
definición); el registro operativo vive bajo `docs/logbook/`.

| Archivo | Prefijo | Qué guarda |
|---|---|---|
| `technical-debt.md` | `TD-###` | Algo que está **mal ahora** en el código existente. |
| `roadmap.md` | `RM-###` | Trabajo **comprometido**, se va a hacer. |
| `wishlist.md` | `WL-###` | Ideas, **quizá nunca**. |
| `changelog.md` | — | Registro **permanente** de todo lo terminado. |

**Reglas pasivas (siempre activas, sin comando):**

- **Deuda técnica:** si la notas mientras trabajas, regístrala en
  `technical-debt.md` (nunca como comentario en el código). Formato de entrada:

  ```markdown
  ## [TD-001] Título corto
  - **Ubicación:** `ruta/al/archivo.ext:línea`
  - **Riesgo:** N/10  (1-3 cosmético · 4-6 ralentiza/moderado · 7-9 bug latente o seguridad · 10 crítico)
  - **Problema:** qué está mal, sintetizado.
  - **Impacto futuro:** qué puede causar si no se atiende.
  - **Fecha:** YYYY-MM-DD · **Estado:** Abierto
  ```

- **Ciclo de tarea:** al **empezar** una tarea (`RM`, `TD` o `WL`) márcala
  `En progreso (YYYY-MM-DD)` en su bandeja; al **terminar**, muévela al
  `changelog.md` conservando su prefijo y bórrala de la bandeja. Formato del
  changelog (orden inverso): `## [CÓDIGO] Título (YYYY-MM-DD HH:MM)` + resumen
  en ≤2 líneas. **La fecha/hora es el reloj local al terminar; nunca se consulta
  git para obtenerla.**
- **Códigos:** nunca se reutilizan; el siguiente = el mayor usado +1 mirando
  bandeja + changelog. Ejecutar una tarea no cambia su código: un `WL` se
  trabaja directo y entra al changelog como `WL`. Promover `WL → RM` es solo
  una decisión de prioridad que pide el usuario, nunca un paso previo.
- **Archivos bajo demanda:** no crees archivos vacíos; cada uno nace la primera
  vez que hay algo real que poner.

**Mecánica pesada → skill `logbook`:** para montar o migrar el sistema (`init`),
recomendar una tarea (`next`) o auditar deuda (`audit`), usa el skill. Ahí viven
los formatos completos, los casos especiales (promoción WL→RM, wontfix) y los
procedimientos.
<!-- logbook:end -->
~~~
