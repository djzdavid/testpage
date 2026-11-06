---
description: SDD · Consulta estado y siguiente acción (Uso: /sdd-status 001-feature)
agent: coordinator
---

Lee MEMORY.md y `specs/$1/spec.md`; consulta plan.md/tasks.md solo si el formato es extendido. No edites ni delegues por rutina.
Informa en máximo ocho líneas: estado persistido, aprobación, formato, tareas terminadas/total, validación y bloqueos. Cero tareas no implica 100%; todas completas no implica cerrada.
Siguiente acción: aprobar paquete en borrador, /sdd-implement para trabajo aprobado pendiente, /sdd-validate para validación pendiente, /sdd-change para nuevo alcance. Si cerrada, indica que no hay acciones pendientes. Si falta la spec, sugiere /sdd-spec.
