---
description: SDD · Reanuda o repite validación con motivo (Uso: /sdd-validate 001-feature)
agent: coordinator
---

Aplica la skill sdd sobre `specs/$1/`. Si ya está cerrada y no cambió código ni alcance, informa la validación vigente sin repetirla. Usa este comando para validación pendiente, cambios posteriores o revisión solicitada, indicando el motivo.
Reviewer contrasta RF y evidencia del estado actual; ejecuta comprobaciones faltantes o invalidadas. Devuelve APROBADO o CAMBIOS NECESARIOS. Reasigna correcciones dentro del alcance al implementer y revalida (máximo dos rondas). Bloqueos o verificaciones pendientes impiden cierre.
Con APROBADO sin pendientes, coordinator registra evidencia, estado cerrada y resumen en MEMORY.md. /sdd-implement ya realiza este flujo automáticamente.
