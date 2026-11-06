# Constitución Técnica del Proyecto

## Principios Innegociables

1. **Simplicidad del Stack:** [PENDIENTE: Especificar tecnologías principales - Ej. Laravel, Vue 3, PostgreSQL / Node.js, React, MongoDB / Python, FastAPI, SQLite].
2. **Gobernanza de Especificación:** Ninguna línea de código de producción existe sin una spec aprobada previamente en la carpeta `specs/`.
3. **Arquitectura:** Lógica de negocio desacoplada de la capa de presentación y de las dependencias externas.
4. **Política de Tests (TDD):** Cobertura obligatoria antes de implementar código de producción. Las pruebas deben ejecutarse en verde antes de dar por completada una tarea.
5. **Seguridad y Privacidad:** Manejo estricto de secretos y variables de entorno (`.env`). No incluir credenciales ni datos sensibles en el repositorio.
6. **Convenio de Idioma:**
   - **Código, Tests y Commits:** [PENDIENTE: Especificar idioma - Ej. Inglés / Español].
   - **Documentación y UI:** [PENDIENTE: Especificar idioma - Ej. Español].

---

## Comandos Oficiales del Proyecto

- **Ejecución de Tests:** `[PENDIENTE: Ej. npm test / pytest / ./vendor/bin/pest]`
- **Análisis Estático y Linter:** `[PENDIENTE: Ej. npm run lint / flake8 / ./vendor/bin/pint]`
- **Servidor de Desarrollo / Build:** `[PENDIENTE: Ej. npm run dev / php artisan serve]`

## Sistema de diseño (proyectos con UI)

Toda interfaz debe respetar las decisiones aprobadas en `docs/design-system.md` y reutilizar los tokens, estilos y componentes existentes del proyecto. Configurar su aplicabilidad e identidad durante `/sdd-constitution`; si no hay UI, marcar no aplica. `frontend-design` complementa estas reglas. Los cambios globales se incluyen explícitamente en el paquete sometido a aprobación, sin una aprobación visual separada.

## Prototipo visual previo a las specs

Durante la configuración de un proyecto con UI se permite crear y ajustar `docs/design-system-demo.html` antes de aprobar la constitución y antes de cualquier spec. Es una excepción acotada para validar la propuesta visual: HTML/CSS autónomo, sin dependencias nuevas, servicios, llamadas de red, lógica de negocio ni cambios en el código de la aplicación. Usar contenido ficticio y recursos locales existentes o alternativas del sistema.

La demo muestra tipografía, paleta, botones, campos, tarjetas, estados visuales y adaptación a escritorio/móvil; solo incluir patrones relevantes. Los estados pueden representarse como ejemplos estáticos. Aplicar `frontend-design` y mantener coherencia con el borrador de `docs/design-system.md`. No requiere TDD ni una spec ficticia; sí inspección visual cuando haya herramientas, registrando limitaciones sin inventar resultados.

Presentar documento y demo como borradores para ajustes. Aprobar la base visual y la constitución juntas, sin una aprobación adicional para generar la demo. Esta aprobación no autoriza código de aplicación: tokens y componentes de producción siguen requiriendo una spec aprobada. Cambios globales posteriores se incluyen en el paquete de la spec afectada.
