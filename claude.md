# prompt shortcuts

| ATAJO | DESCRIPCIÓN                                                             |
| ----- | ----------------------------------------------------------------------- |
| `!`   | Modo bash — ejecuta el resto de la línea como un comando del shell.     |
| `/`   | Comandos — invoca un slash command de Claude Code.                      |
| `@`   | Rutas de archivo — adjunta un archivo o carpeta al contexto del prompt. |
| `&`   | Background — lanza la tarea en segundo plano para seguir trabajando.    |
| `#`   | Comentario — agrega información a memoria de forma rápida.              |

# Configuración inicial

| COMANDO               | DESCRIPCIÓN                                                                  |
| --------------------- | ---------------------------------------------------------------------------- |
| `/init`               | Inicializa el proyecto creando la guía CLAUDE.md.                            |
| `/login`              | Inicia sesión en tu cuenta de Anthropic.                                     |
| `/logout`             | Cierra la sesión actual de tu cuenta de Anthropic.                           |
| `/config`             | Abre la interfaz de Settings (tema, modelo, output style). Alias: /settings. |
| `/permissions`        | Gestiona reglas de permisos (allow / ask / deny) y revisa denegaciones.      |
| `/model [model]`      | Selecciona o cambia el modelo de IA y su nivel de esfuerzo.                  |
| `/theme`              | Cambia el tema de color (auto, light, dark, daltonized, ANSI o custom).      |
| `/terminal-setup`     | Configura keybindings del terminal (Shift+Enter, etc.).                      |
| `/statusline`         | Configura la status line de Claude Code (auto-detecta tu shell prompt).      |
| `/doctor`             | Diagnostica y verifica la instalación y configuración.                       |
| `/mcp`                | Gestiona conexiones a servidores MCP y autenticación OAuth.                  |
| `/hooks`              | Muestra las configuraciones de hooks para eventos de herramientas.           |
| `/chrome`             | Configura los ajustes de Claude in Chrome.                                   |
| `/install-github-app` | Instala la app de Claude GitHub Actions en un repositorio.                   |
| `/install-slack-app`  | Instala la app de Claude para Slack vía OAuth.                               |
| `/setup-bedrock`      | Configura autenticación, región y modelo de Amazon Bedrock.                  |
| `/setup-vertex`       | Configura autenticación, proyecto y modelo de Google Vertex AI.              |

# Flujo de trabajo diario

| COMANDO           | DESCRIPCIÓN                                                                   |
| ----------------- | ----------------------------------------------------------------------------- |
| `/compact`        | Libera contexto resumiendo la conversación. Acepta instrucciones de foco.     |
| `/memory`         | Edita archivos `CLAUDE.md` y gestiona auto-memory.                            |
| `/context`        | Visualiza el uso actual del contexto en una grilla de colores.                |
| `/plan`           | Entra en modo planificación con una tarea opcional como argumento.            |
| `/resume`         | Reanuda una conversación por ID o nombre. Alias: `/continue .`                |
| `/clear`          | Inicia una conversación nueva con contexto vacío. Alias: `/reset`, `/new`.    |
| `/add-dir <path>` | Agrega un directorio al acceso de archivos de la sesión.                      |
| `/copy [N]`       | Copia la última (o N-ésima) respuesta del asistente al portapapeles.          |
| `/export`         | Exporta la conversación actual como texto plano.                              |
| `/recap`          | Genera un resumen breve de la sesión actual bajo demanda.                     |
| `/focus`          | Activa la vista enfocada (último prompt + diff resumido + respuesta).         |
| `/color`          | Define el color de la barra del prompt para la sesión.                        |
| `/keybindings`    | Abre o crea tu archivo de configuración de keybindings.                       |
| `/voice`          | Activa el dictado por voz (modos hold, tap u off).                            |
| `/skills`         | Lista las skills disponibles. Pulsa t para ordenar por tokens.                |
| `/tasks`          | Lista y gestiona tareas en background. Alias: `/bashes`.                      |
| `/agents`         | Gestiona configuraciones de subagentes.                                       |
| `/fast`           | Activa o desactiva el modo rápido (velocidad sobre profundidad).              |
| `/effort`         | Ajusta el nivel de esfuerzo del modelo (low/medium/high/xhigh/max).           |
| `/extra-usage`    | Configura uso extra para seguir trabajando al alcanzar rate limits.           |
| `/loop`           | Ejecuta un prompt repetidamente mientras dura la sesión. Alias: `/proactive`. |
| `/schedule`       | Crea, edita o ejecuta routines. Alias: `/routines`.                           |
| `/batch`          | Orquesta cambios masivos en paralelo en todo el codebase con worktrees.       |

# Revisión de código y Git

| COMANDO                   | DESCRIPCIÓN                                                                         |
| ------------------------- | ----------------------------------------------------------------------------------- |
| `/review [PR]`            | Revisa un Pull Request localmente en la sesión actual.                              |
| `/code-review ultra [PR]` | Code review profundo multi-agente en sandbox cloud. Alias obsoleto: `/ultrareview`. |
| `/security-review`        | Analiza cambios pendientes buscando vulnerabilidades de seguridad.                  |
| `/diff`                   | Abre un visor interactivo de diffs (git diff y por turno).                          |
| `/branch [name]`          | Crea una rama de la conversación actual. Alias: `/fork`.                            |
| `/autofix-pr`             | Lanza una sesión web que arregla CI y comentarios del PR automáticamente.           |
| `/simplify`               | Revisa y arregla los archivos modificados (calidad, eficiencia, reuso).             |

# Depuración y diagnóstico

| COMANDO     | DESCRIPCIÓN                                                              |
| ----------- | ------------------------------------------------------------------------ |
| `/status`   | Abre Settings (Status) con versión, modelo, cuenta y conectividad.       |
| `/usage`    | Costo de la sesión, límites del plan y stats. Alias: `/cost`, `/stats`.  |
| `/cost`     | Alias de `/usage`.                                                       |
| `/stats`    | Alias de `/usage`. Abre la pestaña Stats.                                |
| `/insights` | Genera un reporte analizando tus sesiones (áreas, patrones, fricciones). |
| `/debug`    | Activa logs de debug y diagnostica problemas a partir del log de sesión. |
| `/heapdump` | Genera un heap snapshot de JS para diagnosticar uso de memoria.          |
| `/rewind`   | Vuelve la conversación o el código a un punto anterior. Alias: `/undo`.  |
| `/feedback` | Envía feedback al equipo de Anthropic. Alias: `/bug`.                    |
