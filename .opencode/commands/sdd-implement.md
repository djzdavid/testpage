---
description: SDD · Implementa, valida y cierra el paquete aprobado (Uso: /sdd-implement 001-feature)
agent: coordinator
---

Aplica la skill sdd sobre `specs/$1/`. Verifica aprobación explícita del paquete y registra la autorización si ya la dio el usuario; no la solicites de nuevo. Con borrador sin aprobación, presenta el paquete y espera.
Delega al implementer las tareas pendientes, con TDD continuo, pruebas afectadas durante desarrollo y suite completa al finalizar. Reutiliza evidencia válida sobre el mismo estado del código.
Pasa automáticamente al reviewer para revisión final RF por RF. Corrige hallazgos dentro del alcance y revalida lo afectado (máximo dos rondas). Sin pendientes y con APROBADO, registra cerrada y actualiza MEMORY.md. No exijas /sdd-validate posterior ni confirmación de cierre.
