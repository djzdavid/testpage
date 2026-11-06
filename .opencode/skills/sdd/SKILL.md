---
name: sdd
description: "Usar para preparar, cambiar, implementar o validar especificaciones SDD en este proyecto."
---

# Spec-Driven Development (SDD)

## Flujo y aprobación
Constitución configurada → Preparación conjunta → Aprobación única → Implementación TDD → Revisión final → Cierre.
- Preparar requisitos, enfoque técnico y tareas en una llamada al planner, antes de solicitar aprobación.
- La aprobación explícita del paquete autoriza su implementación y validación continuas. No pedir aprobaciones separadas de spec, plan, tareas e implementación.
- Ningún código de producción o de prueba se escribe sin una spec aprobada que lo cubra.
- Agrupar preguntas de negocio bloqueantes; registrar decisiones técnicas rutinarias dentro del alcance sin consultar de nuevo.
- Cambios de alcance o de comportamiento requieren actualizar primero el paquete y aprobar el cambio. Migraciones, contratos y dependencias requieren autorización explícita o estar detallados en el enfoque técnico aprobado.
- La revisión previa independiente solo se activa por riesgo: seguridad, permisos, datos sensibles, migraciones, contratos o reglas de negocio críticas. Resolver hallazgos antes de presentar el paquete completo.
- Las modificaciones metodológicas de esta plantilla son documentales; no requieren inventar una feature de aplicación.

## Documentos proporcionales
Cada feature vive en `specs/NNN-nombre/`.
- **Compacta (por defecto):** un `spec.md` con requisitos, enfoque técnico, tareas y validación. Adecuada para cambios locales que siguen patrones existentes.
- **Extendida:** `spec.md`, `plan.md` y `tasks.md` cuando hay varios módulos, integraciones, migraciones o decisiones arquitectónicas relevantes. Indicar enlaces desde la spec; no duplicar contenidos.
- Mantener secciones solo si aportan decisiones o evidencia. No exigir historias, DTOs, pseudocódigo ni alternativas descartadas cuando no sean necesarios.

## Plantilla de spec.md
# Spec NNN — <Nombre>
Estado: borrador
Formato: compacta | extendida
Riesgo: normal | elevado — <motivo>
Aprobación: pendiente

### Objetivo y alcance
<Resultado esperado y exclusiones.>
### Requisitos verificables
- RF-1: CUANDO <evento>, EL SISTEMA DEBERÁ <comportamiento>.
### Casos límite y dudas
<Solo los relevantes; señalar preguntas bloqueantes.>
### Enfoque técnico
<Archivos, decisiones y comprobaciones previstas; en extendida, enlace a plan.md.>
### Tareas
- [ ] T1. <Trabajo>. RF-1. Hecho cuando: <criterio verificable>.
<Una a cuatro tareas; en extendida, enlace a tasks.md.>
### Validación
| RF | Prueba o comprobación | Resultado |
| --- | --- | --- |
| RF-1 | <Prueba prevista; actualizar con evidencia real> | Pendiente |

Los RF describen comportamiento sin arquitectura; los detalles técnicos van en su sección. Esta tabla es la única matriz RF → prueba; los demás archivos la referencian.

## Estado persistente
- `borrador`: paquete sin aprobar; sin código autorizado.
- `aprobada`: coordinator registra la aprobación explícita del usuario y su alcance en `Aprobación`.
- `en implementación`: implementer comienza el trabajo aprobado.
- `en validación`: tareas completas; revisión final pendiente.
- `cerrada`: reviewer aprueba, sin comprobaciones obligatorias pendientes; coordinator registra resumen y actualiza `MEMORY.md`.
- Un bloqueo se registra con motivo y siguiente acción, conservando el estado alcanzado. No equiparar tareas completas con cierre.
- Un cambio de alcance devuelve el paquete a borrador; conservar el registro de la aprobación anterior y señalar qué cambio espera aprobación.

## Evidencia y contexto
- Pruebas afectadas durante Red-Green-Refactor y suite completa al cierre. Usar el ejecutor oficial de la constitución; no inventar comandos pendientes.
- Una ejecución completa válida sobre el mismo estado del código se comparte entre agentes. Repetir por cambios posteriores, evidencia insuficiente o riesgo concreto, indicando el motivo.
- Registrar comando, resultado y estado del código verificado; no declarar verificaciones que no se realizaron.
- UI: comprobar flujo, consola, red y vistas móvil/escritorio cuando aplique. Si faltan herramientas, registrar la limitación y no declarar validación completa.
- Delegar solo objetivo, rutas, decisiones del usuario y hallazgos relevantes. Cada agente consulta las reglas y documentos necesarios una vez por ejecución y vuelve a leerlos si cambian.

## Sistema de diseño

En proyectos con UI, consultar `docs/design-system.md` y reutilizar tokens/componentes. Configurar su base junto con la constitución con una sola aprobación. `frontend-design` complementa el sistema aprobado; no reinventa la identidad por spec. Si faltan decisiones necesarias, proponerlas en el paquete antes de implementar. Las modificaciones globales se presentan con su impacto dentro de la aprobación del paquete; coordinator guarda el documento y el implementer materializa código bajo la spec aprobada. Reviewer verifica coherencia visual con esas decisiones.

## Demo inicial sin spec

La excepción de AGENTS.md permite `docs/design-system-demo.html` como prototipo estático aislado antes de aprobar la constitución y antes de cualquier spec. No requiere TDD ni spec ficticia; nunca habilita código de aplicación. Coordinator guarda el borrador del sistema de diseño con estado y aprobación pendientes; implementer genera la demo autónoma usando frontend-design. Presentar juntos demo, documento y constitución para ajustes y una sola aprobación. Verificar escritorio/móvil si hay herramientas; registrar pendientes. No instalar dependencias ni introducir servicios, red o lógica de negocio.

## Herramientas del stack

Aplicar las reglas MCP de AGENTS.md: capacidades pertinentes al stack, documentación por necesidad, permisos por herramienta y rol, una fuente de evidencia compartida y un navegador principal por flujo. Las herramientas opcionales ausentes no bloquean si existe una alternativa suficiente. Si una comprobación obligatoria no puede realizarse, registrar el pendiente. Los servidores especializados no amplían el alcance de la spec ni autorizan migraciones, dependencias o ejecución arbitraria.
