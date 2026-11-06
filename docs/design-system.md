# Sistema de diseño del proyecto

Estado: pendiente de configuración
Aplicabilidad: pendiente — con UI | sin UI
Aprobación: pendiente

Esta plantilla se completa durante `/sdd-constitution` si el proyecto tiene interfaz. No representa una identidad visual aprobada. Si no hay UI, marcar no aplica y omitir las secciones restantes.

## Dirección visual y referencias
- Producto, usuarios y necesidades: [PENDIENTE]
- Identidad, tono y referencias aprobadas: [PENDIENTE]
- Diseño o biblioteca existente que se debe preservar: [PENDIENTE]

## Tokens
Registrar valores aprobados y su ubicación real en el código. Usar los nombres y mecanismos del stack elegido; no crear otro sistema paralelo.

| Área | Decisión o escala aprobada | Ubicación en código |
| --- | --- | --- |
| Colores | [PENDIENTE: fondo, superficie, texto, acción, foco y estados semánticos] | [PENDIENTE] |
| Tipografía | [PENDIENTE: familias, tamaños, pesos y alturas de línea] | [PENDIENTE] |
| Espaciado | [PENDIENTE: escala y reglas de uso] | [PENDIENTE] |
| Bordes y elevación | [PENDIENTE: radios, grosores y sombras] | [PENDIENTE] |
| Movimiento | [PENDIENTE: duración y movimiento reducido] | [PENDIENTE] |

## Componentes y patrones
Documentar únicamente componentes existentes o necesarios para el alcance actual. No implementar un catálogo futuro por anticipado.

| Componente o patrón | Referencia reutilizable | Variantes, estados y reglas |
| --- | --- | --- |
| [PENDIENTE] | [PENDIENTE: ruta o referencia] | [PENDIENTE: normal, foco, deshabilitado, carga y error según corresponda] |

## Layout y adaptación
- Contenedores, alineación, densidad y navegación: [PENDIENTE]
- Reglas de adaptación, puntos de cambio y tamaños de verificación: [PENDIENTE]
- Formularios, validación, vacíos, carga y errores: [PENDIENTE según alcance]

## Accesibilidad y contenido
- Objetivo y comprobaciones de accesibilidad: [PENDIENTE]
- Cubrir contraste, teclado, foco visible, etiquetas, errores y movimiento reducido según la UI.
- Idioma y tono del contenido: seguir la constitución; documentar aquí solo reglas específicas de interfaz.

## Uso y evolución
- Toda UI respeta las decisiones aprobadas de este documento y reutiliza tokens/componentes del código. `frontend-design` opera dentro de esas reglas.
- Una sección pendiente no autoriza inventar una decisión global durante implementación. Proponer lo necesario en el paquete de la primera spec afectada y aprobarlo junto con ella; no crear una fase adicional.
- Las specs referencian estas reglas sin copiarlas. Cualquier modificación global debe identificar su impacto y quedar explícita en el paquete antes de aprobarlo.
- Coordinator guarda las decisiones documentales aprobadas. Los tokens y componentes se implementan mediante una spec aprobada y el stack del proyecto.
- Si documento y código divergen, registrar y resolver la discrepancia dentro del alcance aprobado; no sustituir el sistema silenciosamente.

## Demo para revisión inicial

- Archivo: `docs/design-system-demo.html` (se genera al configurar la identidad de cada proyecto con UI).
- Prototipo HTML/CSS autónomo conforme a la excepción de AGENTS.md, anterior a las specs; sin lógica de negocio, servicios ni dependencias nuevas.
- Mostrar ejemplos de la paleta, escala tipográfica, botones, campos, tarjetas, estados y adaptación coherentes con este documento. Registrar decisiones inferidas desde referencias.
- Generar y ajustar con estado borrador; presentar junto con constitución y documento para la misma aprobación. La demo no es código de aplicación ni autoriza implementarlo.
- Inspección visual realizada y limitaciones: [PENDIENTE al generar la demo].
