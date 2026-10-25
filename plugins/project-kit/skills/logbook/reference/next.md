# /logbook next — recomendar una tarea

Objetivo: romper la inercia. El usuario sabe que tiene que avanzar pero no sabe
por dónde empezar y termina sin hacer nada. Dale **un primer empuje concreto**,
no un volcado de todo el backlog.

## Reglas

- **Solo lee el logbook** (`roadmap.md`, `technical-debt.md`, `wishlist.md`) y,
  si hace falta para juzgar esfuerzo, echa un vistazo barato al código. **No
  consultes git.**
- Si pasan contexto extra (`/logbook next deuda`, `/logbook next rápido`),
  sesga la recomendación hacia eso.
- Si no hay nada en ninguna bandeja, dilo y ofrece correr `/logbook audit` o
  capturar ideas en la wishlist.

## Cómo elegir

El sesgo es **arrancar**, no "lo más importante" (que suele ser lo más grande y
abrumador). Pondera:

- **Esfuerzo bajo** para entrar en flow (quick-win) — peso alto.
- **Riesgo** alto en `TD` (7-10) — súbelo aunque no sea quick-win, pero avísalo.
- Trabajo `RM` ya marcado `En progreso` — retomarlo gana, evita dejar cosas a
  medias.
- Dependencias obvias (no recomiendes algo bloqueado por otra tarea sin hacer).

## Salida

Presenta **1 recomendación principal + 2 alternativas**, cada una con una línea
de porqué:

```
🎯 Empieza por: [RM-003] Tracking inteligente en vivo
   Por qué: arranca el corazón de v1.5 y ya tienes el modelo de datos listo.

Alternativas:
   ⚡ Rápida   — [TD-006] Mostrar errores de red en los hooks (~30 min, quita fricción real).
   🏗️ De fondo — [TD-005] Auth básica antes de exponer por el tunnel (riesgo 6/10).
```

Cierra ofreciendo **marcar la elegida como `En progreso (YYYY-MM-DD)`** en su
bandeja (el marcador WIP del ciclo de tarea). No la marques sin confirmación.
