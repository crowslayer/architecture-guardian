# Architecture Guardian

**Una Agent Skill agnóstica al lenguaje para auditar arquitectura de software con evidencia.** Descubre el stack y el dominio, traza casos de uso y evalúa límites, invariantes, dependencias y decisiones de diseño sin imponer patrones por defecto.

**Español** · [English](README.md) · **Alpha** · [Licencia MIT](LICENSE) · [Compartir resultados](.github/ISSUE_TEMPLATE/skill-evaluation.md)

> Este proyecto es experimental. La calidad de la auditoría depende del agente, el modelo, el contexto del repositorio y las herramientas disponibles. Verifica los hallazgos contra el código y los requisitos del proyecto.

## Qué hace

- Audita Arquitectura Hexagonal y Clean Architecture, DDD, CQRS, sistemas dirigidos por eventos, SOLID y patrones pertinentes en cualquier lenguaje o tecnología.
- Descubre conceptos del dominio a partir de requisitos, contratos, pruebas y código; traza casos de uso representativos, sus efectos y sus rutas de fallo.
- Distingue defectos confirmados, riesgos potenciales, supuestos, incógnitas y mejoras opcionales.
- Recomienda validaciones existentes sin instalar dependencias ni ejecutar comandos automáticamente.
- No incluye scripts ejecutables. Sus escenarios manuales de comportamiento están en [references/skill-evaluation.md](references/skill-evaluation.md).

## Inicio rápido

Copia el **directorio completo `architecture-guardian`**, incluyendo `SKILL.md`, `references/` y `templates/`, en una ruta de skills que reconozca tu agente. Consulta abajo las rutas documentadas por plataforma. Después pide una auditoría en modo Audit, o solicita explícitamente Review o Refactor.

Ejemplo de solicitud:

```text
Usa Architecture Guardian en modo Audit. Descubre el stack y el dominio,
traza los casos de uso principales e informa hallazgos arquitectónicos con
su evidencia. No ejecutes comandos ni modifiques archivos.
```

## Plataformas

La portabilidad de Agent Skills se refiere al formato y las instrucciones. No significa que cada modelo o producto descubra la skill, lea sus referencias o tenga las mismas herramientas automáticamente. Las rutas y funciones disponibles pueden cambiar.

| Plataforma | Ruta o método de carga documentado | Validación de comportamiento en este proyecto |
| --- | --- | --- |
| OpenCode | `.opencode/skills/architecture-guardian/` o `~/.config/opencode/skills/architecture-guardian/` | Aún no registrada |
| Claude Code | `.claude/skills/architecture-guardian/` o `~/.claude/skills/architecture-guardian/` | Aún no registrada |
| Claude.ai | Importar un ZIP de la skill si Skills está disponible para la cuenta | Aún no registrada |
| Gemini CLI | `.gemini/skills/architecture-guardian/` o `.agents/skills/architecture-guardian/` | Aún no registrada |
| Codex | `.agents/skills/architecture-guardian/` en un ámbito de usuario o proyecto compatible | Aún no registrada |
| DeepSeek Deep Code | `.deepcode/skills/architecture-guardian/` o `~/.agents/skills/architecture-guardian/` | Aún no registrada |
| Cursor | Depende del descubrimiento de skills y la configuración del agente | Dos ejecuciones de campo en un proyecto TypeScript/MongoDB; regresión G parcialmente superada |

Las rutas se basan en documentación de los proveedores, no en pruebas de extremo a extremo de esta skill. Otros productos de Anthropic, Google, OpenAI o DeepSeek no quedan cubiertos por usar modelos del mismo proveedor.

Documentación oficial: [Especificación Agent Skills](https://agentskills.io/specification) · [OpenCode](https://docs.opencode.ai/docs/skills/) · [Claude Code](https://code.claude.com/docs/en/skills) · [Gemini CLI](https://geminicli.com/docs/cli/using-agent-skills/) · [Skills en ChatGPT](https://help.openai.com/en/articles/20001066-skills-in-chatgpt) · [Skills API de OpenAI](https://developers.openai.com/api/docs/guides/tools-skills) · [Codex](https://developers.openai.com/blog/skills-agents-sdk) · [DeepSeek Deep Code](https://api-docs.deepseek.com/quick_start/agent_integrations/deepcode/)

## Cómo evaluarla

1. Proporciona un repositorio representativo o un escenario de `references/skill-evaluation.md`.
2. Registra la versión de la skill, plataforma, modelo, stack del proyecto, alcance y salida relevante.
3. Revisa la evidencia, la coherencia entre conteos y estados, el fundamento de severidad y que las áreas no inspeccionadas queden como incógnitas.
4. No tomes una recomendación como comportamiento verificado. Confirma las afirmaciones en el código, pruebas, documentación o validaciones autorizadas.
5. Cuando encuentres un defecto, añade un escenario de regresión antes de modificar la skill y vuelve a ejecutar los escenarios afectados.

La guía arquitectónica es portable; los comandos, convenciones y reglas de análisis estático deben adaptarse al stack detectado. Si falta evidencia o conocimiento del ecosistema, el agente debe decirlo en vez de inventar reglas.

## Estado de validación

- **Estructura:** `quick_validate.py` pasó con Python 3.11 y PyYAML 6.0.3 en la validación anterior.
- **Escenarios manuales:** A–F pasaron una autoevaluación manual frente a sus resultados esperados. No sustituye una evaluación independiente con varios modelos o plataformas.
- **Evaluación de campo con Cursor:** dos ejecuciones sobre una aplicación TypeScript/MongoDB mejoraron los conteos, estados y clasificación de mejoras opcionales. El segundo informe aún presentó ambiguamente `bulkWrite` de MongoDB como alternativa a un reemplazo atómico multi-documento. Por ello, el escenario G **pasa parcialmente**; consulta los [criterios de evaluación](references/skill-evaluation.md).
- **Informe de otro proyecto:** una auditoría TypeScript/Express/Sequelize mantuvo conteos ejecutivos coherentes y trazas útiles de dominio y casos de uso. Reveló puntos de calibración sobre normalización no requerida, hallazgos solapados y severidad de módulos no cableados. El escenario H ahora cubre estos casos; aún no se ha vuelto a ejecutar en un harness. El informe compartido no identificó plataforma ni modelo, así que no se cuenta como prueba específica de plataforma.

## Versionado

Este repositorio distribuye instrucciones y referencias, no un paquete de runtime. Las versiones se identifican mediante tags Git y GitHub Releases; la skill no tiene un campo de versión ejecutable.

Se usa Semantic Versioning con identificadores de pre-lanzamiento:

- `v0.1.0-alpha.1`: primera alpha pública.
- `v0.1.0-alpha.2`, `v0.1.0-alpha.3`: siguientes iteraciones con mejoras y comentarios recibidos.
- `v0.1.0-beta.1`: conjunto de funciones suficientemente estable para validación más amplia.
- `v1.0.0`: flujo y compatibilidad definidos con criterios de aceptación y validados suficientemente para una versión estable.

En cada release, actualiza `CHANGELOG.md`, crea un tag anotado sobre el commit revisado y publica notas coincidentes como GitHub prerelease hasta llegar a `v1.0.0`.

## Contribuir

Consulta la [guía de contribución](CONTRIBUTING.md). No incluyas código propietario, credenciales, datos de clientes ni otra información sensible en informes públicos de auditoría.
