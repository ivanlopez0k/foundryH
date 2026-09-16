# Informacion de gentle-ai

Este documento describe como esta construido y configurado gentle-ai a partir de evidencia local verificada el 2026-09-12. Todo lo observado incluye el comando o la ruta que lo respalda. Lo no observado se marca explicitamente como por verificar.

## 1. Identificacion

| Dato | Valor observado | Evidencia |
|------|-----------------|-----------|
| Version | 2.7.0 | `gentle-ai version` |
| Binario | `C:\Users\Usuario\go\bin\gentle-ai.exe` | `Get-Command gentle-ai` |
| Estado de salud | healthy (8 controles correctos, 0 fallos) | `gentle-ai doctor` |
| Documentacion publica | https://github.com/Gentleman-Programming/gentle-ai | `gentle-ai --help` |
| Agente instalado | pi (1 agente) | `gentle-ai doctor` |
| Herramientas detectadas | gentle-ai, gga, engram, pi | `gentle-ai doctor` |

## 2. Stack tecnico

| Capa | Tecnologia | Evidencia |
|------|------------|-----------|
| CLI nativo | gentle-ai 2.7.0 (binario Go, en `go/bin`) | `gentle-ai version`, `Get-Command` |
| Orquestacion de agentes | opencode, con `@opencode-ai/plugin` 1.18.30 | `package.json` en `.config\opencode` |
| Memoria persistente | engram v1.20.0 (binario MCP local) | `engram --help`, `opencode.jsonc` (seccion `mcp.engram`) |
| Grafo de codigo | CodeGraph via MCP (`codegraph serve --mcp`) | `opencode.jsonc` (seccion `mcp.codegraph`) |
| Documentacion externa | Context7 via MCP remoto (`https://mcp.context7.com/mcp`) | `opencode.jsonc` (seccion `mcp.context7`) |
| Interfaz | TUI de opencode con complementos personalizados | `tui.json` |
| Telemetria | Anonima, con opcion de exclusion (`telemetry status|enable|disable|preview|trigger`) | `gentle-ai --help` |

Complementos TUI registrados (`tui.json`, verificado):

- `opencode-sdd-engram-manage`
- `opencode-subagent-statusline`
- `C:\Users\Usuario\.config\opencode\tui-plugins\gentle-logo.tsx`

## 3. Arquitectura

El agente predeterminado es `gentle-orchestrator` (modelo `opencode/muse-spark-1.3-contributor-free`). Funciona exclusivamente como coordinador: mantiene una conversacion principal, delega todo el trabajo real a subagentes y sintetiza resultados. No ejecuta trabajo directamente.

Agentes configurados en `opencode.jsonc` (nombres verificados; el detalle de cada prompt existe en el mismo archivo o en `prompts/sdd/`):

| Agente | Funcion |
|--------|---------|
| `gentle-orchestrator` | Coordinador principal (unico `mode: primary`) |
| `explore` | Exploracion de solo lectura, sin edicion ni ejecucion |
| `general` | Tareas auxiliares no estructuradas; no lanza subagentes |
| `sdd-explore`, `sdd-propose`, `sdd-spec`, `sdd-design`, `sdd-research`, `sdd-tasks`, `sdd-apply`, `sdd-verify`, `sdd-archive`, `sdd-init`, `sdd-onboard` | Ejecutores de cada fase SDD (prompts en `prompts/sdd/*.md`) |
| `review-risk`, `review-readability`, `review-reliability`, `review-resilience` | Revisores por lente (riesgo, legibilidad, confiabilidad, resiliencia) |
| `review-refuter`, `review-validator` | Refutacion adversarial y validacion dirigida de hallazgos |
| `jd-judge-a`, `jd-judge-b`, `jd-fix-agent` | Protocolo judgment-day (doble juez ciego + agente de correccion) |

El orquestador solo puede delegar en esa lista cerrada (`permission.task` con negacion por defecto y permisos explicitos por agente). Detalle de los permisos de bash, lectura y git pendiente de transcripcion completa: por verificar en `opencode.jsonc`, lineas 430-456 (reglas observadas parcialmente: git commit/push/rebase/reset requieren confirmacion; lectura denegada en claves, secretos y archivos `.env`).

## 4. Estructura del repositorio de configuracion

Raiz verificada: `C:\Users\Usuario\.config\opencode\`

```text
.config\opencode\
  AGENTS.md                        # Contratos globales: CodeGraph, persona, protocolo Engram
  opencode.jsonc                   # Agentes, MCP, permisos, agente por defecto
  package.json                     # Dependencia @opencode-ai/plugin 1.18.30
  tui.json                         # Complementos de interfaz
  .gentle-ai-default-agent.json    # Estado: {"schema": "gentle-ai.opencode-default-agent", "version": 1, "state": "managed"}
  .gitignore
  commands\                        # 13 comandos slash (ver lista en seccion 9)
  prompts\sdd\                     # 11 prompts de fase SDD (*.md)
  skills\                          # 25 directorios de skills (ver seccion 7)
  plugins\  profiles\  themes\     # Contenido no inspeccionado: por verificar
  node_modules\                    # Dependencias instaladas, no inspeccionadas
  tui-plugins\                     # Complemento de logotipo
```

## 5. Comandos nativos (verificados con `gentle-ai --help`)

Gestion del sistema:

- `gentle-ai` — inicia la TUI interactiva.
- `gentle-ai install` / `uninstall` / `sync` — configura, elimina o sincroniza los agentes y skills.
- `gentle-ai update` / `upgrade` — comprueba o aplica actualizaciones.
- `gentle-ai restore` — restaura una copia de seguridad de configuracion.
- `gentle-ai doctor` — diagnostico de salud (verificado: healthy).
- `gentle-ai version` — muestra la version.
- `gentle-ai telemetry <status|enable|disable|preview|trigger>` — telemetria anonima con exclusion voluntaria.
- `gentle-ai skill-registry refresh` — regenera `.atl/skill-registry.md`.

SDD nativo:

- `gentle-ai sdd-status [change]` — estado de fase SDD del cambio activo.
- `gentle-ai sdd-continue [change]` — salida de enrutamiento del despachador nativo.
- `gentle-ai sdd-attempt <acquire|settle> --cwd <repo> --change <change>` — orquestacion normal acotada.
- `gentle-ai sdd-attempt <status|begin|finish|reset|repair> --cwd <repo> --change <change>` — diagnostico o recuperacion del registro de intentos.
- `gentle-ai sdd-verify-validate --input <path|-> --requirements <n> --scenarios <n>` — valida el informe de verificacion sin persistencia.

Revision (RDD):

- `gentle-ai review start [--cwd <repo>] [--base-ref <ref>] [--focus <risk|resilience|readability|reliability>] [--locale <en|es>]`
- `gentle-ai review capture-result | capture-correction-plan | capture-refuter | capture-validation` — admision de resultados de revisores.
- `gentle-ai review inspect-candidate ...` — vista inmutable acotada de un candidato.
- `gentle-ai review validate --gate <gate>` — valida la sintaxis de la puerta de entrega.
- `gentle-ai review status [--cwd <repo>]` — inventario de solo lectura.
- `gentle-ai review repair --preflight [--cwd <repo>]` — clasifica el inventario antes de la reparacion.
- `gentle-ai review mode <enable|disable|status>` — interruptor de parada controlado por el usuario.
- Comandos de compatibilidad con la autoridad v1 anterior (`review-start`, `review-step`, `review-resume`, `review-bundle-export`, `review-bundle-import`, `review-validate`): superficies de solo lectura que rechazan mutaciones nuevas.

Notas observadas:

- `gentle-ai sdd-status --help` no existe: devuelve error `unknown sdd-status argument "--help"`. El estado se obtiene ejecutando `gentle-ai sdd-status` directamente.
- `gentle-ai review mode status` observado: `receipt-driven development: off (decided by default)`, ambitos global y local sin definir.
- `gentle-ai review status` observado en `C:\Users\Usuario\Desktop\Proyectos`: `status: clean`, sin entradas ni bloqueos.

## 6. Contratos globales (`AGENTS.md`, verificado)

1. Contrato de idioma de artefactos: los artefactos tecnicos usan ingles por defecto; si se solicitan explicitamente en espanol, se usa espanol neutro/profesional, sin jerga regional ni enfasis estilistico de la personalidad. La personalidad rige solo el texto de respuesta, nunca el contenido de los artefactos.
2. Guia CodeGraph: ante preguntas estructurales, usar CodeGraph antes que busquedas amplias; orden obligatorio (raiz git, comprobar `.codegraph/`, inicializar con `gentle-ai codegraph init --cwd <raiz>` si falta, consultar via `codegraph_explore` o CLI de solo lectura; nunca comandos destructivos).
3. Protocolo Engram: guardado proactivo tras decisiones, correcciones o descubrimientos; busqueda (`mem_context`, `mem_search`) ante referencias a trabajo previo; resumen de sesion obligatorio al cierre; el guardado es contabilidad interna y nunca sustituye la respuesta al usuario.

## 7. Skills instalados (nombres verificados en `skills\`)

Directorios existentes (25): `branch-pr`, `chained-pr`, `cognitive-doc-design`, `comment-writer`, `gentle-ai-bench`, `go-testing`, `issue-creation`, `judgment-day`, `rdd-defect-workflow`, `sdd-apply`, `sdd-archive`, `sdd-design`, `sdd-explore`, `sdd-init`, `sdd-onboard`, `sdd-propose`, `sdd-research`, `sdd-spec`, `sdd-tasks`, `sdd-verify`, `skill-creator`, `skill-improver`, `skill-registry`, `systemic-issue-triage`, `work-unit-commits`, mas `_shared` (contratos compartidos, incluido `sdd-status-contract.md` citado por el comando `sdd-status`).

Contenido verificado por lectura directa (2 skills):

- `cognitive-doc-design`: documentar con la respuesta primero, divulgacion progresiva, fragmentacion en secciones pequenas, senalizacion con encabezados y tablas, y listas de comprobacion. Estructura sugerida: titulo orientado al resultado, ruta rapida, detalles, lista de comprobacion, paso siguiente.
- `rdd-defect-workflow`: comprobar primero el interruptor RDD del usuario; exigir incidencia aprobada y reproduccion en `main` limpio; agrupar por invariante causal con una incidencia y un PR por linea de autoridad; limite estricto de 400 lineas anadidas mas eliminadas; pruebas de comportamiento primero; validacion candidata independiente de solo lectura antes de publicar.

Proposito del resto de los skills: por verificar (solo se confirmaron los nombres de directorio; no se leyo cada `SKILL.md`).

Registro de skills del proyecto: no resuelto. No existe `.atl/skill-registry.md` accesible y la busqueda en memoria resulto ambigua. Se trabajo sin estandares especificos del proyecto.

## 8. Despachador SDD nativo

Salida observada de `gentle-ai sdd-status` y `gentle-ai sdd-continue` (esquema `gentle-ai.sdd-status@2`, almacen `openspec`, `planning_home` en modo `repo-local` hacia `C:\Users\Usuario\Desktop\Proyectos\openspec`): sin cambios activos, todas las fases bloqueadas, `next_recommended: sdd-new` / `sdd-continue`.

Comportamiento segun contrato del comando `commands/sdd-status.md` (verificado por lectura): el JSON del despachador es autoritativo solo cuando el almacen de la sesion es `openspec` o `hibrido`; con almacen `engram` no se invoca el binario y el estado se resuelve desde Engram con el contrato compartido `_shared/sdd-status-contract.md`. Reglas de solo lectura: no crear artefactos, no inferir enrutamiento desde texto libre, usar `nextRecommended` y estados de dependencia.

Fases SDD cubiertas por prompts y comandos (nombres verificados): `init`, `explore`, `propose`, `research`, `spec`, `design`, `tasks`, `apply`, `verify`, `archive`, `onboard`, ademas de `new`, `continue`, `status`, `ff` como comandos slash. El detalle interno de cada fase (criterios de entrada/salida) es por verificar en `prompts/sdd/*.md` y en cada `SKILL.md` de `sdd-*`.

## 9. Comandos slash (`commands\`, nombres verificados)

`sdd-apply.md`, `sdd-archive.md`, `sdd-continue.md`, `sdd-explore.md`, `sdd-ff.md`, `sdd-init.md`, `sdd-new.md`, `sdd-onboard.md`, `sdd-research.md`, `sdd-status.md`, `sdd-verify.md`, `skill-creator.md`, `skill-registry.md`. Contenido interno verificado solo para `sdd-status.md`; el resto es por verificar.

## 10. Revision, RDD y judgment-day

Estado observado: RDD desactivado por defecto (`review mode status`); inventario de revision limpio (`review status`).

Contratos verificados por lectura:

- `rdd-defect-workflow` (seccion 7): interruptor del usuario, incidencia aprobada, limite de 400 lineas, validacion de solo lectura.
- Revisores `review-*` y jueces `jd-*`: prompts integrados en `opencode.jsonc` (revision por lentes con admision causal de candidato; doble juez ciego con severidades BLOCKER/CRITICAL/WARNING/SUGGESTION en JSON estricto). Transcripcion completa por verificar por la longitud del archivo.
- Ciclo de vida de revision del orquestador (enlace, linaje, correccion, refutacion, validacion, puertas de entrega): conocido solo por el contrato del orquestador, por verificar contra la evidencia local.

## 11. CodeGraph

Integracion verificada a nivel de configuracion: MCP `codegraph` (`codegraph serve --mcp`, habilitado) y guia operativa completa en `AGENTS.md` (seccion 6). Estado de indices locales, disponibilidad del binario `codegraph` y comportamiento del observador (watcher): por verificar en el entorno.

## 12. Engram

Integracion verificada: MCP local `engram` (binario en `C:\Users\Usuario\AppData\Local\engram\bin\engram.exe`, perfil de herramientas `agent`), version CLI v1.20.0, protocolo de uso obligatorio en `AGENTS.md` (seccion 6). Proyectos, observaciones y resumenes existentes: por verificar con `engram search` o las herramientas MCP de memoria.

## 13. Pendientes de verificacion

- Contenido de `prompts/sdd/*.md` (salvo existencia) y de cada `SKILL.md` de `sdd-*`, `judgment-day`, `branch-pr`, `chained-pr` y restantes.
- Transcripcion completa de los prompts de `opencode.jsonc` (truncados en lectura por longitud).
- Disponibilidad y estado del binario `codegraph` y de indices `.codegraph/`.
- Contenido de memoria Engram y registro `.atl/skill-registry.md` del proyecto.
- Contenido de `plugins\`, `profiles\`, `themes\` y `tui-plugins\` (salvo el logotipo registrado).
