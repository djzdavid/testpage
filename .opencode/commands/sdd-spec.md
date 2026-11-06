---
description: SDD · Prepara el paquete completo para una aprobación (Uso: /sdd-spec 001-feature "idea")
agent: coordinator
---

Prepara `specs/$1/` a partir de: $ARGUMENTS.
Aplica la skill sdd. En una llamada al planner genera spec, enfoque y tareas, compactos por defecto, en borrador. Agrupa preguntas bloqueantes. Revisión previa independiente solo por riesgo elevado, resolviendo hallazgos antes de presentar el paquete.
Presenta los documentos guardados y solicita una aprobación única. Tras recibirla, registra aprobación y continúa con implementación, revisión final y cierre, salvo que el usuario haya pedido solo preparar. No exijas /sdd-clarify, /sdd-plan ni /sdd-tasks como pasos posteriores rutinarios.
