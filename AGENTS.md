# Guía de Trabajo del Asistente de IA

## Propósito y Contexto
Este archivo define la metodología de colaboración y los límites de actuación para el asistente de IA en este repositorio. Este proyecto utiliza estrictamente **Spec-Driven Development (SDD)**.

---

## Arquitectura y Gobernanza

La fuente de verdad técnica, el stack tecnológico (frameworks, base de datos, ejecutores de prueba), los convenios de código y las reglas específicas del proyecto están formalmente definidos en **`docs/constitution.md`**.

---

## Forma de Trabajar (Flujo SDD)

1. **Contexto:** Consultar `docs/constitution.md`, `MEMORY.md` y la spec activa una vez por ejecución; releer si cambian. La skill `.opencode/skills/sdd/SKILL.md` define formatos, estados y evidencia.
2. **Preparación conjunta:** Redactar requisitos, enfoque técnico y tareas en una ejecución. Formato compacto por defecto; documentos separados cuando la complejidad lo justifique.
3. **Aprobación única:** Presentar el paquete completo guardado y obtener aprobación explícita antes de escribir código de producción o pruebas. La aprobación autoriza implementación, validación y cierre continuos; respetar si el usuario solicita solo preparación.
4. **Clarificación:** Agrupar dudas de negocio bloqueantes durante la preparación. `/sdd-clarify` es opcional. Resolver detalles técnicos internos con las convenciones existentes.
5. **Cambios enfocados:** No anticipar funcionalidades. Cambios de comportamiento o alcance requieren actualizar el paquete y aprobar el cambio; no volver a aprobar decisiones vigentes.
6. **Cierre:** Revisión final independiente; revisión previa solo por riesgo justificado. Coordinator registra `cerrada` y actualiza memoria únicamente sin verificaciones obligatorias pendientes.

---

## Límites de Actuación

### ✅ Siempre
- Responder y redactar la documentación en el idioma establecido en `docs/constitution.md`.
- Respetar la arquitectura, convenciones de tipado estricto y estándares definidos en la constitución.
- Validar, sanitizar y convertir tipos de las entradas externas antes de persistirlas o procesarlas.
- Preservar la trazabilidad y la inmutabilidad de los registros históricos de datos.

### ⚠ Pregunta Antes
- Crear o modificar migraciones y esquemas de base de datos.
- Alterar contratos de API, endpoints o DTOs existentes.
- Agregar o eliminar dependencias/paquetes del proyecto.

*Estas acciones requieren autorización explícita o estar expresamente detalladas en el plan técnico de la spec aprobada.*

### 🚫 Nunca
- Agregar, refactorizar o modificar código de producción sin una spec aprobada que lo cubra.
- Escribir en duro (*hardcode*) valores normativos, variables de entorno, credenciales o datos de configuración en el código base.
- Persistir datos inválidos o silenciar errores críticos con valores de reemplazo por defecto.
- Guardar credenciales, tokens o datos sensibles en repositorios, documentación o archivos de memoria.

---

## Uso de herramientas de escritura

- Respetar el esquema y formato de la herramienta disponible. Para documentos, preferir `edit` para sustituciones concretas o `write` para archivos nuevos o reemplazos completos previamente leídos.
- Si se utiliza una herramienta de patch que exige el formato `apply_patch`, enviar el texto del patch sin cercas Markdown ni explicaciones: primera línea exacta `*** Begin Patch`, operaciones como `*** Update File: ruta`, bloques de cambios y última línea `*** End Patch`. No enviar un diff de Git como sustituto.
- Un fallo de formato del patch no implica falta de permisos. Corregir el formato y reintentar la misma operación autorizada; no pedir otra aprobación ni delegarla por este motivo. Leer después los archivos para comprobar lo persistido.

## Verificación y Calidad de Funcionalidades

### 1. Pruebas Automatizadas (TDD)
- **Estrategia:** Consultar en `docs/constitution.md` el ejecutor y comando oficial de pruebas del proyecto.
- **Enfoque TDD:** Toda tarea debe implementar sus pruebas correspondientes (unitarias/integración) antes o en paralelo al código de producción.
- **Aislamiento:** Aislar dependencias externas e integraciones mediante respuestas simuladas (*mocks* / *fixtures* controlados).
- **Rigor en la ejecución:** Ejecutar pruebas afectadas durante TDD y la suite completa al finalizar. Compartir evidencia válida del mismo estado del código entre agentes; repetir por cambios, evidencia insuficiente o riesgo concreto. Informar comando, resultado y estado verificado sin asumir comprobaciones no realizadas.

### 2. Verificación Visual e Interfaz de Usuario (si aplica)
- Para cambios en UI/frontend, utilizar las herramientas de inspección o emulación disponibles (navegador local / DevTools MCP).
- **Checklist de Inspección:**
  1. Navegar e interactuar con el flujo implementado en pantalla.
  2. Confirmar que no existan errores ni advertencias en la consola de JavaScript.
  3. Verificar en la pestaña de red (*Network*) las respuestas correctas de los endpoints.
  4. Comprobar la adaptabilidad en vistas móviles y de escritorio.

---

## Comandos SDD Disponibles

- `/sdd-constitution`: Configura la gobernanza inicial; coordinator guarda tras aprobación.
- `/sdd-spec [nombre]`: Prepara el paquete completo para una aprobación única.
- `/sdd-implement [nombre]`: Implementa, valida y cierra lo aprobado sin pausas rutinarias.
- `/sdd-change [nombre]`: Prepara un cambio completo y solicita aprobación del cambio.
- `/sdd-status [nombre]`: Consulta estado, evidencia pendiente y siguiente acción.
- Opcionales: `/sdd-clarify` audita dudas/riesgos, `/sdd-plan` ajusta enfoque y tareas, `/sdd-tasks` ajusta tareas, `/sdd-validate` reanuda o repite validación con motivo. No ejecutarlos después de pasos que ya realizaron ese trabajo.

## Coherencia de interfaz

En tareas con UI, consultar `docs/design-system.md`, respetar sus decisiones aprobadas y reutilizar tokens/componentes existentes. Configurar la base junto con la constitución. Resolver decisiones pendientes o cambios globales dentro del paquete de la spec y su aprobación única. Aplicar `frontend-design` dentro de ese sistema; no redefinir la identidad en cada feature.

## Prototipo visual previo a las specs

Durante la configuración de un proyecto con UI se permite crear y ajustar `docs/design-system-demo.html` antes de aprobar la constitución y antes de cualquier spec. Es una excepción acotada para validar la propuesta visual: HTML/CSS autónomo, sin dependencias nuevas, servicios, llamadas de red, lógica de negocio ni cambios en el código de la aplicación. Usar contenido ficticio y recursos locales existentes o alternativas del sistema.

La demo muestra tipografía, paleta, botones, campos, tarjetas, estados visuales y adaptación a escritorio/móvil; solo incluir patrones relevantes. Los estados pueden representarse como ejemplos estáticos. Aplicar `frontend-design` y mantener coherencia con el borrador de `docs/design-system.md`. No requiere TDD ni una spec ficticia; sí inspección visual cuando haya herramientas, registrando limitaciones sin inventar resultados.

Presentar documento y demo como borradores para ajustes. Aprobar la base visual y la constitución juntas, sin una aprobación adicional para generar la demo. Esta aprobación no autoriza código de aplicación: tokens y componentes de producción siguen requiriendo una spec aprobada. Cambios globales posteriores se incluyen en el paquete de la spec afectada.

## Uso de MCP según el stack

- Consultar la constitución y las herramientas realmente disponibles. Usar solo servidores pertinentes al stack y a la tarea; no exigir ni instalar herramientas de otro stack. Los perfiles del README son configuraciones del proyecto destino, no requisitos globales.
- Resolver una consulta concreta con el contexto local primero. Si falta documentación, usar el proveedor especializado disponible (por ejemplo, Boost para Laravel o Context7 para bibliotecas compatibles); daisyUI solo si forma parte del stack. Compartir conclusiones, versión y referencia entre agentes sin repetir consultas ni volcar documentación completa.
- Un servidor configurado no equivale a uno conectado, ni concede autorización de negocio. Comprobar capacidades cuando se necesiten, una vez por ejecución; ante ausencia usar una alternativa suficiente e informar limitaciones. No iniciar una instalación ni pedir permisos para herramientas que la tarea no necesita.
- Los permisos nativos `edit`/`shell` no gobiernan automáticamente un MCP. Aplicar permisos por nombre real `<servidor>_<herramienta>` en cada rol. Las reglas incluidas cubren los identificadores del perfil README; si cambian nombres, versiones o servidores, revisar las capacidades y ajustar las reglas durante la configuración, con denegaciones generales antes de excepciones específicas. No conceder acceso global a herramientas nuevas por analogía con su nombre.
- Coordinator coordina y reutiliza evidencia; planner consulta documentación/metadatos y propone cambios sin ejecutarlos; implementer actúa dentro del alcance aprobado; reviewer inspecciona y valida sin modificar código ni datos ajenos a fixtures de prueba autorizados.
- Las herramientas de consulta SQL no garantizan por su nombre acceso de lectura: usar conexiones de desarrollo de solo lectura para inspección. No usar SQL, Tinker, evaluación JavaScript ni herramientas equivalentes para eludir permisos, migraciones o aprobaciones. Respetar también estas restricciones con MCP de otros stacks. No copiar secretos ni datos sensibles a prompts, resultados compartidos o memoria.
- Para UI, elegir Playwright o Chrome DevTools como navegador principal por flujo; recurrir al otro solo para una comprobación faltante o un problema concreto. Interacciones que escriban datos se limitan al entorno de pruebas autorizado y sus fixtures; no operar sobre producción. Reutilizar evidencia válida sin repetir navegación por cambiar de rol.
- Si una herramienta requiere aprobación de ejecución, no sustituirla por otra para evadir el control. Las autorizaciones existentes se respetan; registrar lo que sigue pendiente sin declarar éxito.

## Skills específicas del stack

La skill local `daisyui` solo se aplica si la constitución adopta esa biblioteca y la tarea afecta su interfaz. Esta condición prevalece sobre la recomendación amplia de la skill original de usarla para cualquier HTML/JSX. No obliga a adoptar daisyUI en otros stacks ni autoriza instalaciones o cambios de versión. Conservar las reglas SDD, el sistema de diseño y los límites de la demo estática.
