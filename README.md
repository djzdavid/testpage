# Plantilla SDD para OpenCode

Desarrollo guiado por especificaciones y TDD, con cuatro agentes y una aprobación del paquete completo por feature.

## Inicio

1. Ejecuta `/sdd-constitution` para configurar stack, idioma y comandos reales del proyecto. Aprueba la propuesta completa; coordinator la guarda. Se hace al inicio, no por cada spec.
2. Ejecuta `/sdd-spec 001-mi-feature "Descripción"`. Planner prepara requisitos, enfoque técnico y tareas juntos. Las dudas bloqueantes se presentan agrupadas. La revisión previa independiente se reserva para riesgo elevado.
3. Revisa y aprueba el paquete guardado. Esa aprobación autoriza implementar, validar y cerrar de forma continua. Si quieres solo preparar, indícalo al pedir la spec.

Si dejaste un paquete aprobado pendiente, usa `/sdd-implement 001-mi-feature` para retomarlo. Este comando ya incluye validación y cierre: no hace falta ejecutar `/sdd-validate` después.

También puedes pedirlo en lenguaje natural al coordinator. No necesitas invocar cada agente ni cada fase manualmente.

## Agentes

- **Coordinator:** conduce el flujo, registra aprobación y estado, guarda constitución y actualiza memoria.
- **Planner:** prepara el paquete completo y revisa su coherencia en una ejecución.
- **Implementer:** ejecuta tareas con TDD continuo y entrega evidencia de pruebas y UI.
- **Reviewer:** revisa el resultado final RF por RF; revisa antes de implementar cuando el riesgo lo justifique.

Las asignaciones de modelos y el MCP permanecen en `opencode.json`. Los modelos/proveedores se configuran según el entorno de destino. La reducción de llamadas y contexto repetido busca disminuir tokens y latencia; el ahorro debe medirse en ejecuciones comparables.

## Documentos proporcionales

```text
.opencode/agents/             # Cuatro roles
.opencode/commands/           # Entradas al flujo
.opencode/skills/sdd/SKILL.md  # Formatos, estados y evidencia
.opencode/skills/frontend-design/
docs/constitution.md         # Stack y comandos del proyecto destino
specs/NNN-feature/spec.md     # Paquete compacto por defecto
specs/NNN-feature/plan.md     # Solo para formato extendido
specs/NNN-feature/tasks.md    # Solo para formato extendido
AGENTS.md                    # Reglas de colaboración y límites
MEMORY.md                    # Estado y decisiones ultracompactos
opencode.json                # Modelos y MCP
```

El paquete compacto contiene objetivo, RF verificables en EARS, límites, enfoque técnico, una a cuatro tareas y una tabla RF → prueba. Para varios módulos, integraciones, migraciones o arquitectura relevante, separar enfoque y tareas sin duplicar contenido. El detalle técnico va fuera de los RF.

## Aprobación y autonomía

La aprobación explícita del paquete guardado precede cualquier código de producción o pruebas. No se solicitan aprobaciones separadas de plan, tareas e implementación. Los cambios de alcance se preparan completos y se aprueban una vez. Migraciones, contratos y dependencias deben estar autorizados explícitamente o detallados en el enfoque técnico aprobado.

El agente resuelve detalles internos y fallos reparables dentro del alcance. Consulta si cambia el comportamiento, falta una decisión de negocio o aparece un bloqueo real. Tras dos rondas de correcciones sin resolver hallazgos finales, informa el bloqueo.

Estados en spec.md: `borrador` → `aprobada` → `en implementación` → `en validación` → `cerrada`. Registrar aprobación y alcance; tareas completas no equivalen a cierre.

## Verificación sin duplicaciones

Durante TDD se ejecutan pruebas afectadas; al finalizar, la suite completa oficial. Los agentes comparten evidencia comprobable del mismo estado del código. Se repite por cambios posteriores, evidencia insuficiente o riesgo concreto, con motivo explícito. La revisión final independiente se mantiene.

UI requiere comprobación del flujo, consola, red y vistas móvil/escritorio cuando aplique. Las herramientas ausentes y las comprobaciones pendientes se informan; impiden declarar validación completa. Esta plantilla no incluye una aplicación ni un ejecutor de tests: configura los comandos en la constitución del proyecto destino.

## Comandos

| Comando | Uso |
| --- | --- |
| `/sdd-constitution` | Configuración inicial de gobernanza |
| `/sdd-spec [nombre]` | Preparar paquete completo para aprobar |
| `/sdd-implement [nombre]` | Retomar implementación, validar y cerrar |
| `/sdd-change [nombre] "cambio"` | Preparar y aprobar un cambio de alcance |
| `/sdd-status [nombre]` | Consultar estado y siguiente acción |
| `/sdd-clarify [nombre]` | Auditoría puntual opcional de dudas/riesgos |
| `/sdd-plan [nombre]` | Ajustar enfoque y tareas, sin regeneración rutinaria |
| `/sdd-tasks [nombre]` | Ajustar solo tareas |
| `/sdd-validate [nombre]` | Reanudar o repetir validación con motivo |

No es necesario ejecutar los comandos opcionales en secuencia: el flujo principal ya realiza ese trabajo.

## Sistema de diseño compartido

Configura la identidad visual en `docs/design-system.md`: dirección visual, colores, tipografía, espaciado, componentes y estados, accesibilidad y adaptación. La plantilla deja valores pendientes para cada proyecto; no prescribe una marca ni una biblioteca.

`/sdd-constitution` propone esa base junto con las reglas técnicas cuando hay UI, con una sola aprobación. Si no hay UI se marca no aplica. Los detalles todavía innecesarios pueden quedar pendientes y resolverse en el paquete de la primera spec que los necesite.

Planner e implementer consultan el sistema y aplican `frontend-design` dentro de sus reglas; reviewer comprueba su cumplimiento. Los tokens y componentes reales viven en el código según el stack, implementados bajo una spec aprobada. Cualquier cambio global se presenta dentro del paquete de la spec, sin otra fase de aprobación.

## Vista previa antes de las specs

En proyectos con UI, `/sdd-constitution` prepara la base visual y genera `docs/design-system-demo.html` antes de pedir aprobación. Puedes aportar URLs o imágenes como referencia; el agente distingue lo observado de lo inferido y declara las limitaciones de acceso.

Revisa la demo de tipografía, colores, botones, campos, tarjetas y estados en escritorio/móvil, pide ajustes y aprueba la constitución y base visual juntas. Después empieza las features con `/sdd-spec`.

La demo es un prototipo HTML/CSS autónomo permitido explícitamente antes de cualquier spec, sin dependencias nuevas, servicios ni lógica de negocio. No exige TDD. Los tokens y componentes de aplicación siguen requiriendo una spec aprobada. El HTML concreto se genera en cada proyecto al definir su identidad; la plantilla no impone un diseño de ejemplo.

## Configuración por stack

La plantilla base mantiene solo Chrome DevTools en `opencode.json`. Agrega herramientas específicas en el proyecto de destino después de definir el stack; conserva los agentes y modelos configurados. Cada perfil debe documentar requisitos/versiones, instalación, MCP, comprobaciones y manejo de instrucciones generadas. Los demás stacks pueden incorporar perfiles siguiendo esa estructura, sin activar herramientas que el proyecto no utiliza.

### Laravel + Vue + PostgreSQL + daisyUI

#### Requisitos y configuración inicial

Parte de una aplicación Laravel existente con `composer.json` y `artisan`, su entorno PHP/Composer y Node.js compatible con las herramientas elegidas. Define las versiones de Laravel, Vue, Tailwind CSS y daisyUI, y los comandos reales de pruebas/build en `/sdd-constitution`. Configura PostgreSQL en el entorno local de Laravel, sin guardar credenciales en esta plantilla. El MCP de daisyUI no instala la biblioteca en la aplicación.

#### Laravel Boost

Desde la raíz de la aplicación Laravel, ejecuta:

```bash
composer require laravel/boost --dev
php artisan boost:install
```

Selecciona OpenCode si lo ofrece el instalador. Revisa el diff generado para conservar las reglas SDD, los agentes, las skills y el sistema de diseño; integra las guías de Boost sin duplicar ni sustituir esas reglas. La instalación agrega una dependencia de desarrollo al proyecto destino: no ejecutarla en esta plantilla ni durante la demo visual aislada. [Instalación y herramientas de Boost](https://github.com/laravel/docs/blob/13.x/boost.md).

#### MCP para este stack

| Servidor | Para qué usarlo | Activación |
| --- | --- | --- |
| Laravel Boost | Contexto de la aplicación, documentación de paquetes Laravel, rutas, esquema y consultas de base de datos | Tras instalar Boost |
| Context7 | Documentación concreta de Vue, Tailwind y daisyUI; complementar lo no cubierto por Boost | Para este stack |
| daisyUI GitMCP | Documentación específica de daisyUI | Opcional si Context7 no cubre la consulta |
| Playwright | Navegación y verificación de flujos responsive | Para este stack; evitar repetir comprobaciones ya hechas con Chrome DevTools |
| PostgreSQL dedicado | Inspección de otra conexión o necesidades no cubiertas por Boost | Opcional; no duplicar acceso a la misma base sin motivo |

En OpenCode 2 puedes registrar los servidores locales así, desde la raíz de la aplicación:

```bash
opencode mcp add laravel-boost -- php artisan boost:mcp
opencode mcp add context7 -- npx -y @upstash/context7-mcp@latest
opencode mcp add playwright -- npx -y @playwright/mcp@latest
```

No registres otra entrada de Boost si `boost:install` ya la creó. Para documentación adicional de daisyUI, opcionalmente:

```bash
opencode mcp add daisyui -- npx -y mcp-remote https://gitmcp.io/saadeghi/daisyui
```

Se usa el paquete oficial `@playwright/mcp`, no `@modelcontextprotocol/server-playwright`. Para daisyUI se usa GitMCP, una alternativa documentada por el proyecto, en lugar del paquete no verificado `@daisyui/mcp-server`. [Playwright MCP](https://playwright.dev/docs/getting-started-mcp), [opciones MCP de daisyUI](https://github.com/saadeghi/daisyui/blob/master/packages/docs/src/routes/%28routes%29/docs/editor/claude/%2Bpage.md?plain=1), [Context7](https://github.com/upstash/context7).

Para PostgreSQL, usar primero las herramientas de esquema/consulta de Boost cuando basten. El paquete que se propuso inicialmente, `@modelcontextprotocol/server-postgres`, es de lectura y está archivado; no se activa por defecto para proyectos nuevos. Si necesitas compatibilidad temporal con ese servidor, este es el fragmento de referencia, con conexión externa al repositorio:

```json
{
  "postgres": {
    "type": "local",
    "command": [
      "npx",
      "-y",
      "@modelcontextprotocol/server-postgres",
      "{env:POSTGRES_MCP_URL}"
    ]
  }
}
```

Integra esa entrada en el mapa de servidores de la versión utilizada: `mcp.servers` en OpenCode 2; `mcp` en OpenCode 1. Define `POSTGRES_MCP_URL` en el entorno del proceso de OpenCode mediante tu mecanismo local de secretos; no asumas que OpenCode carga el `.env` de Laravel. Usa una conexión de desarrollo con permisos de lectura. Para necesidades nuevas que requieran un servidor dedicado, evalúa uno mantenido antes de configurarlo. [Servidor Postgres archivado](https://github.com/modelcontextprotocol/servers-archived/blob/main/src/postgres/README.md), [variables de OpenCode](https://opencode.ai/v2/docs/config#variables).

#### Comprobación y uso

En OpenCode 2, ejecuta `opencode mcp list` y comprueba los servidores conectados. No basta con que el JSON sea válido. Verifica la versión con `opencode --version`: la plantilla conserva su configuración base anterior, mientras que estos comandos corresponden a OpenCode 2. Si editas manualmente la configuración de esa versión, usa `mcp.servers`; evita duplicar las entradas de la estructura anterior. [Configuración MCP de OpenCode 2](https://opencode.ai/v2/docs/mcp-servers).

Consulta documentación por necesidad concreta, comparte conclusiones entre agentes y elige un navegador principal por verificación. Las herramientas de Boost que ejecutan código o consultan datos deben respetar el alcance aprobado y las restricciones de cada rol; su instalación no amplía esas autorizaciones. No ejecutar mutaciones de datos mediante Tinker o SQL como atajo para eludir la gobernanza de migraciones.

#### Perfiles futuros

Para incorporar otro stack, añade una subsección con: requisitos/versiones, instalación local, servidores necesarios y opcionales, comprobaciones y convivencia de las instrucciones generadas con SDD. Mantén los ejemplos específicos en el README y la configuración base agnóstica.

### Permisos MCP de los agentes

Las reglas compartidas viven en AGENTS.md; cada agente define además sus permisos de herramientas. Las entradas de permisos no conectan ni instalan servidores. Solo se usan herramientas correspondientes al stack configurado.

- Coordinator delega consultas y reutiliza evidencia; no llama directamente a los MCP del perfil.
- Planner dispone de consultas documentales y metadatos; no ejecuta código ni mutaciones.
- Implementer usa documentación, navegador y herramientas autorizadas dentro del alcance.
- Reviewer inspecciona y valida; Tinker y evaluación arbitraria de JavaScript están bloqueados.

Los permisos se basan en los identificadores del perfil (`context7`, `daisyui`, `laravel-boost`, `postgres`, `playwright`, `chrome-devtools`). Se permiten automáticamente las operaciones documentales concretas de Context7 y de metadatos/documentación de Boost; otras herramientas de esos servidores requieren revisión de ejecución, salvo los límites explícitos de cada rol. Los navegadores están habilitados para implementer/reviewer, siempre bajo las restricciones de entorno y fixtures de AGENTS.md.

Al agregar otro stack o cambiar nombres, descubre los nombres y capacidades reales, configura permisos por rol y conserva el orden de reglas (la última coincidencia prevalece). No asumas que negar shell o edición impide acciones equivalentes mediante MCP. Para operaciones SQL de inspección usa una conexión con permisos de lectura. No concedas acceso global a un servidor que incluya operaciones de escritura solo para habilitar su documentación. [Permisos MCP y nombres de herramientas en OpenCode 2](https://opencode.ai/v2/docs/permissions).

### Skill local de daisyUI

La plantilla incluye la skill oficial en `.opencode/skills/daisyui/`, con sus guías de componentes y licencia MIT. Fuente: [saadeghi/daisyui — skills/daisyui](https://github.com/saadeghi/daisyui/tree/master/skills/daisyui). No requiere suscripción ni un servidor MCP para consultar los archivos locales. La versión incluida documenta daisyUI 5 y Tailwind CSS 4.

Planner e implementer la aplican únicamente si el proyecto adopta daisyUI y la tarea afecta UI. `frontend-design` guía la dirección visual; la skill daisyUI aporta sintaxis, componentes y temas dentro del sistema de diseño aprobado. No implica instalar paquetes ni cambiar versiones. Para otros stacks se omite; se leen solo las referencias necesarias para la tarea.
