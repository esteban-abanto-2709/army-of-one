# /logbook audit — barrido de deuda técnica del código

Objetivo: revisar el código en busca de deuda y llenar `technical-debt.md`. Es
un barrido **deliberado y pesado** (por eso es comando, no automático).

## 1. Antes de escanear — leer lo ya conocido

- Lee `docs/logbook/technical-debt.md` (deuda abierta) y `docs/logbook/changelog.md`
  (deuda ya resuelta, prefijo `TD`). Esto evita **duplicar** y reportar lo ya
  arreglado, y te da el próximo código `TD-###` disponible (mayor usado +1 entre
  bandeja + changelog).

## 2. Escanear

- Si pasan una ruta como contexto (`/logbook audit apps/api`), limita el barrido
  a ella. Si no, todo el repo (excluye `node_modules`, `dist`, `.next`, build
  output).
- Busca categorías típicas: falta de validación de entrada, manejo de errores
  silenciado, riesgos de seguridad (auth, secretos, inyección), problemas de
  rendimiento (N+1, cargar todo en memoria), acoplamientos frágiles, código
  muerto, configuración hardcodeada, `TODO/FIXME/HACK` en comentarios (¡y propónlos para
  migrar al logbook!).

## 3. Deduplicar y puntuar

- Descarta lo que ya esté en `technical-debt.md` o resuelto en el changelog.
- Asigna **riesgo 1-10** según la escala de `spec.md` (1-3 cosmético · 4-6
  ralentiza/moderado · 7-9 bug latente o seguridad · 10 crítico).

## 4. Confirmar ANTES de escribir

- **No escribas directo.** Presenta los hallazgos propuestos como lista
  (ubicación + riesgo + problema en una línea), ordenados por riesgo desc.
- Deja que el usuario descarte/edite. Solo tras su OK, agrega las entradas a
  `technical-debt.md` con el formato de `spec.md` y los códigos `TD-###`
  correlativos correctos.

## 5. Cierre

- Resume cuántas entradas se agregaron y con qué códigos. No hagas commit salvo
  que lo pidan.
