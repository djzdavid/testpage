---
description: SDD · Prepara y aprueba un cambio de alcance (Uso: /sdd-change 001-feature "cambio")
agent: coordinator
---

Cambio solicitado para `specs/$1/`: $ARGUMENTS.
Aplica la skill sdd. En una ejecución planner actualiza primero requisitos y alcance, después enfoque y tareas afectados; conserva historial y progreso válido. Marca borrador y cambio pendiente de aprobación. No escribas código.
Presenta diff e impacto del paquete completo y solicita una sola aprobación del cambio. Tras ella registra autorización y continúa con implementación, revisión y cierre, salvo que el usuario haya pedido solo preparar. No vuelvas a aprobar decisiones que siguen vigentes.
