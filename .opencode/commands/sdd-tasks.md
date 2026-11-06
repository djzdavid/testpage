---
description: SDD · Ajusta tareas puntualmente (Uso: /sdd-tasks 001-feature)
agent: coordinator
---

Aplica la skill sdd sobre `specs/$1/`. Pide al planner ajustar solo tareas a partir de RF y enfoque existentes, dentro de spec.md compacta o tasks.md extendido. Usa una a cuatro tareas con checkbox, RF, archivos afectados y criterio verificable. Conserva progreso válido.
No regeneres tareas ya vigentes ni exijas este comando tras /sdd-spec o /sdd-plan. Si falta enfoque, prepara el paquete completo. Si cambia alcance o decisiones aprobadas, presenta el cambio para aprobación antes de implementar; reordenamientos internos no requieren otra aprobación.
