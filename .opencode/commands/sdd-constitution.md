---
description: SDD · Configura la gobernanza una vez (Uso: /sdd-constitution "detalles")
agent: coordinator
---

Consulta AGENTS.md, MEMORY.md y docs/constitution.md. Información adicional: $ARGUMENTS.
Solicita al planner inspeccionar los archivos accesibles y proponer stack, arquitectura, política TDD y comandos, seguridad e idioma. No inventar tecnologías ni comandos no verificables; agrupa datos faltantes para el usuario.
Presenta la propuesta completa y espera aprobación explícita. Después coordinator guarda docs/constitution.md con sus permisos documentales y actualiza brevemente MEMORY.md. Planner no guarda fuera de specs/. No repetir esta configuración por cada feature ni pedir aprobación de nuevo si ya se autorizó la propuesta concreta.

El guardado es una acción directa del coordinator con la herramienta de escritura disponible siguiendo su esquema y las reglas de AGENTS.md, no una nueva tarea ni continuación del planner o reviewer. Tras escribir, lee los archivos guardados para confirmar persistencia. Si la aprobación concreta ya consta en el chat, reutilízala sin solicitarla nuevamente.

Determina con el contexto si el proyecto tendrá UI. Si la tiene, solicita al planner proponer también `docs/design-system.md`, usando la plantilla existente y las referencias/tokens/componentes actuales. Usa `frontend-design` para definir aspectos nuevos cuando sea necesario. Planner devuelve la propuesta, sin guardar fuera de specs/. Incluye ambas propuestas en la misma aprobación; coordinator guarda constitución, sistema de diseño y memoria directamente y comprueba su contenido. Si no tiene UI, registra no aplica. No agregues dependencias ni implementes componentes de producción durante esta configuración. Las decisiones que puedan posponerse se marcan pendientes y se resuelven en el primer paquete de spec que las necesite, sin otra fase de aprobación.

Antes de la aprobación conjunta, coordinator guarda el sistema de diseño propuesto como borrador y delega al implementer crear `docs/design-system-demo.html` conforme a la excepción de AGENTS.md. La demo HTML/CSS es autónoma y previa a cualquier spec, sin lógica de negocio, dependencias nuevas ni servicios. Incluye muestras de tipografía, colores, botones, campos, tarjetas, estados y adaptación. Presenta documento y demo para ajustes antes de pedir la única aprobación junto con la constitución. Verifica el prototipo con las herramientas de navegador disponibles en escritorio/móvil e informa limitaciones. No reutilices la aprobación previa de una constitución para declarar aprobada una base visual nueva que el usuario aún no ha visto.
