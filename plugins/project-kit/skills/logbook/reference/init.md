# /logbook init — montar o migrar el sistema

Objetivo: dejar `docs/logbook/` montado y absorber en él **cualquier** artefacto
de seguimiento que ya exista en el proyecto, venga con el nombre que venga. No es
una lista cerrada de casos especiales: el flujo es
**descubrir → clasificar → confirmar → migrar**. Idempotente: si ya está todo en
`docs/logbook/` y al día, no rompas nada.

Primero: ¿es repo git? Si no, avísalo (ofrece `git init`) — el respaldo de lo que
se borra depende de git.

## 1. Descubrir candidatos

Barre el repo (sin `node_modules`, `dist`, `.next`, build) buscando documentos
que **sean** seguimiento de trabajo, por nombre **y** por contenido. Los nombres
de abajo son pistas, NO una lista exhaustiva — generaliza a variantes, plurales,
mayúsculas e idiomas:

- Por hacer / ideas: `roadmap`, `todo`, `todos`, `tasks`, `backlog`, `wishlist`,
  `ideas`, `pending`, `notes`…
- Deuda / problemas: `technical-debt`, `tech-debt`, `debt`, `issues`, `fixme`…
- Terminado: `changelog`, `history`, `releases`, `done`…
- Versión anterior de este sistema: una carpeta `docs/tracking/` (ya viene casi
  en formato → caso fácil, solo renombrar y normalizar).

Cuenta también el **contenido**: un `.md` que en el fondo es una lista de
tareas/ideas/cosas hechas es candidato aunque su nombre no encaje. Marca para
preguntar cualquier archivo donde dudes entre "seguimiento" y "conceptual".

## 2. Clasificar

Mapea cada candidato — o **cada sección dentro de un archivo**, porque uno solo
puede partirse en varios buckets — a uno de los cuatro:

| Contenido | Destino |
|---|---|
| Algo mal **ahora** en el código | `technical-debt.md` (`TD`) |
| Trabajo **comprometido** | `roadmap.md` (`RM`) |
| Idea **sin compromiso** | `wishlist.md` (`WL`) |
| Ya **terminado** | `changelog.md` |

Material **conceptual** (visión de producto, hitos v1/v2/v3 en prosa) NO es
seguimiento → queda en `docs/` (p. ej. `docs/product-vision.md`). Si tiene
trabajo comprometido embebido, extrae esas piezas como `RM` y deja un puntero
cruzado.

## 3. Proponer plan y confirmar

La clasificación es difusa, así que **no muevas nada todavía**. Muéstrale al
usuario el plan: qué archivo/sección va a qué bucket, qué se queda como
conceptual, qué códigos se asignarían y en qué archivo irán las reglas del
agente (paso 5). Deja que corrija y migra solo tras su OK.
(Excepción: el rename mecánico de `docs/tracking/` puedes hacerlo directo,
avisando.)

## 4. Migrar

- `git mv` cuando un archivo entero mapea 1:1 a un destino (preserva historial);
  si se parte en varios buckets, crea los destinos y `git rm` el viejo.
- Aplica las cabeceras-plantilla de `spec.md`.
- Asigna códigos `TD/RM/WL` correlativos desde 001, sin reutilizar (bandeja +
  changelog). Si una entrada ya traía un código válido (caso `docs/tracking/`),
  **consérvalo, no renumeres**.
- Reconcilia formato: deuda con `Estado: Abierto`; changelog a
  `## [CÓDIGO] Título (YYYY-MM-DD HH:MM)`. Para entradas históricas sin hora,
  deja solo la fecha `(YYYY-MM-DD)`. **Nunca consultes git para fechas/horas.**
- Respeta "archivos bajo demanda": no crees buckets vacíos. Si no se descubrió
  nada, crea solo la carpeta `docs/logbook/` y explica que los archivos nacen
  cuando haya algo real que poner.
- Arregla punteros rotos (`README.md`, docs de visión) a rutas/nombres viejos.

## 5. Instalar las reglas del agente

Copia el bloque de `agent-rules.md` (marcas incluidas) al archivo de
instrucciones que el agente lee en cada sesión. Va en **un solo archivo, nunca
en dos**: Claude Code lee `CLAUDE.md` o `AGENTS.md`, no ambos, y duplicarlo
hace que se lea dos veces o que una copia quede sin leer.

**Antes de elegir:** si el bloque ya está en el archivo global del usuario
(`~/.claude/CLAUDE.md` o el equivalente de su agente), las reglas ya valen en
todos sus proyectos: no lo escribas en el proyecto y díselo.

**Destino en el proyecto**, la primera regla que se cumpla, mirando la raíz del
repo:

1. Hay un `CLAUDE.md` que importa `@AGENTS.md` → `AGENTS.md`.
2. Hay `CLAUDE.md` → `CLAUDE.md`.
3. Hay solo `AGENTS.md` → `AGENTS.md` (así también lo leen otros agentes).
4. No hay ninguno → crea `CLAUDE.md` con solo el bloque.

Si el usuario prefiere que las reglas valgan para todos sus proyectos, ofrécele
el archivo global en vez del del proyecto.

**Cómo escribirlo:**

- Si el destino ya tiene las marcas, reemplaza **todo** lo que hay desde la
  línea que empieza por `<!-- logbook:start` hasta `<!-- logbook:end -->`,
  ambas incluidas. Si no, agrégalo al final del archivo, separado por una línea
  en blanco.
- No toques nada fuera de las marcas.
- Si encuentras una sección de logbook **sin marcas** (versión anterior, escrita
  a mano), propón reemplazarla por el bloque; no la borres sin su OK.
- Si el bloque aparece en otro archivo además del destino, avísalo y propón
  quitar la copia sobrante.

## 6. Cierre

- Resume qué se migró/renombró, códigos conservados o asignados, próximos
  correlativos disponibles (`TD/RM/WL`), qué quedó como conceptual y en qué
  archivo quedaron las reglas del agente.
- No hagas commit salvo que el usuario lo pida (todo va por git → puede revisar
  con `git diff` y revertir si algo no cuadra).
