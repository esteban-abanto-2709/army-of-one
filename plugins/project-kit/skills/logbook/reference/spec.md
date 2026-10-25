# Logbook — convención completa

Todo el trabajo del proyecto se registra en cuatro archivos dentro de
`docs/logbook/`, **siempre versionados en git** (git es el respaldo de todo lo
que se borra). `docs/` arriba queda para material conceptual (visión,
definición del proyecto); el registro operativo vive bajo `docs/logbook/`.

| Archivo | Prefijo | Qué guarda |
|---|---|---|
| `technical-debt.md` | `TD-###` | Algo que está **mal ahora** en el código existente. |
| `roadmap.md` | `RM-###` | Trabajo **comprometido**, se va a hacer. |
| `wishlist.md` | `WL-###` | Ideas, **quizá nunca**. |
| `changelog.md` | — | Registro **permanente** de todo lo terminado. |

Carpeta preparada, archivos bajo demanda: cada archivo se crea (con su
cabecera-plantilla de abajo) la primera vez que hay algo real que poner. No
crees archivos vacíos ni otros distintos a estos cuatro.

## Reglas de los códigos

- **Nunca se reutilizan.** El siguiente número de un prefijo = el mayor ya usado
  +1, mirando **bandeja + changelog**. (Si un código se quemó por un error de
  proceso y nunca representó una tarea real, sí puede reclamarse.)
- El prefijo dice solo en qué archivo está la tarea (`RM-007` → `roadmap.md`).

## Ciclo de una tarea

El usuario pide trabajar por código: *"quiero trabajar en la RM-007…"*. Vale
igual para `RM`, `TD` y `WL`: un `WL` **se ejecuta directo desde la wishlist**,
sin promoverlo antes.

1. **Al empezar:** marca la entrada como `En progreso (YYYY-MM-DD)` en su bandeja
   (marcador WIP, por si se corta la sesión).
2. **Al terminar:** mueve la entrada al **changelog conservando su propio
   prefijo** (un `WL` terminado entra como `WL`, un `TD` como `TD`) y **bórrala**
   de la bandeja. El changelog registra los tres tipos.

Ejecutar una tarea **no cambia su código**.

## Casos especiales

- **Promoción `WL → RM`:** es una **decisión de prioridad**, no un paso para
  ejecutar: el usuario decide que una idea pasa a ser trabajo comprometido,
  aunque no se vaya a hacer ahora. Solo cuando él lo pide; nunca la propongas
  como requisito para trabajar un `WL`. Borra el `WL`, crea un `RM` nuevo.
  **No pasa por changelog** (no se terminó nada, solo se movió).
- **Descartar (wontfix):** **borrado silencioso** de la bandeja. Git conserva el
  historial; no se registra en changelog.
- **Technical-debt unificado:** un `TD` resuelto **también** se mueve al changelog
  y se borra. No se conserva `Estado: Resuelto` dentro del archivo.

---

# Formatos y cabeceras

## `technical-debt.md` (`TD-###`)

Entrada:

```markdown
## [TD-001] Título corto
- **Ubicación:** `ruta/al/archivo.ext:línea`
- **Riesgo:** N/10
- **Problema:** Descripción sintetizada de qué está mal.
- **Impacto futuro:** Qué problemas puede causar si no se atiende.
- **Fecha:** YYYY-MM-DD · **Estado:** Abierto
```

Escala de riesgo:

```
1-3  cosmético / sin impacto funcional
4-6  ralentiza el desarrollo o riesgo moderado
7-9  bug latente, pérdida de datos o seguridad
 10  crítico, atacar de inmediato
```

Cabecera-plantilla (al crear el archivo):

```markdown
# Deuda Técnica

Registro de atajos, decisiones pendientes y riesgos a futuro de este proyecto.
Código `TD-###` (nunca se reutiliza). Al resolverse, la entrada se mueve al
changelog y se borra de aquí.

**Formato de cada entrada:**
- **Ubicación:** `archivo:línea` afectado.
- **Riesgo:** del 1 al 10 (1-3 cosmético · 4-6 ralentiza/moderado · 7-9 bug latente o seguridad · 10 crítico).
- **Problema:** qué está mal, sintetizado.
- **Impacto futuro:** qué puede causar si no se atiende.
- **Fecha** y **Estado** (Abierto / En progreso).

---
```

## `roadmap.md` (`RM-###`)

Entrada (estructurada):

```markdown
## [RM-001] Título corto
- **Objetivo:** qué se quiere lograr.
- **Hecho cuando:** criterio claro de finalización.
- **Fecha:** YYYY-MM-DD · **Estado:** Abierto
```

Cabecera-plantilla:

```markdown
# Roadmap

Trabajo comprometido: lo que sí se va a hacer. Código `RM-###` (nunca se reutiliza).
Al terminar una tarea se mueve al changelog y se borra de aquí.

**Formato de cada entrada:**
- **Objetivo:** qué se quiere lograr.
- **Hecho cuando:** criterio claro de finalización.
- **Fecha** y **Estado** (Abierto / En progreso).

---
```

## `wishlist.md` (`WL-###`)

Entrada (liviana, sin campos):

```markdown
## [WL-001] Título corto
Idea en 1–2 líneas.
```

Cabecera-plantilla:

```markdown
# Wishlist

Ideas y mejoras posibles, sin compromiso (quizá nunca). Código `WL-###` (nunca se reutiliza).
Si una idea se promueve, se borra de aquí y nace un `RM` nuevo.

**Formato:** título + idea en 1–2 líneas, sin campos.

---
```

## `changelog.md`

Entrada (orden inverso, lo más nuevo arriba):

```markdown
## [CÓDIGO] Título (YYYY-MM-DD HH:MM)
Resumen en ≤2 líneas de lo que se hizo.
```

La fecha y hora son el momento en que se termina la tarea (reloj local de la
sesión). **Nunca se consulta git ni otra fuente externa para obtenerlas.**

Cabecera-plantilla:

~~~markdown
# Changelog

Registro permanente de todo el trabajo terminado. Indexado por código de tarea
(`TD-`, `RM-`, `WL-`). Orden inverso: lo más nuevo arriba.

**Formato de cada entrada:**

```
## [CÓDIGO] Título (YYYY-MM-DD HH:MM)
Resumen en ≤2 líneas de lo que se hizo.
```

---
~~~
