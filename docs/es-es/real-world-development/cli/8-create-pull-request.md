---
title: "Lección 8 - Crea y combina la solicitud de la funcionalidad"
description: "Revisa en conjunto los filtros, las instrucciones, la habilidad actualizada, el perfil de QA y las pruebas; después, crea una solicitud de incorporación de cambios y usa Agent Merge."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

La implementación de los filtros, las actualizaciones de instrucciones, la actualización de la habilidad, el perfil de garantía de calidad (QA) y las pruebas están guardados en una rama. Ahora toca revisarlo todo y abrir una solicitud de incorporación de cambios. Tú combinaste la solicitud de las valoraciones con estrellas; esta vez dejarás que **Agent Merge** gestione el proceso.

> [!NOTE]
> Lo habitual sería separar la funcionalidad, las actualizaciones de instrucciones, la actualización de la habilidad y el agente de QA en varias solicitudes. Para simplificar el taller, has mantenido todo el trabajo de filtrado y del flujo de calidad en una sola conversación y rama, y lo incluirás en esta solicitud.

En esta lección:

- aprenderás qué es Agent Merge y cómo automatiza el ciclo de vida de una solicitud.
- inspeccionarás el cambio completo de la funcionalidad y las pruebas de validación.
- crearás la solicitud de filtrado.
- activarás Agent Merge solo después de la revisión y confirmarás que se ha combinado la solicitud.

## Escenario

Durante el trabajo de filtrado, has usado Copilot para planificar, implementar y validar una funcionalidad. Tailspin Toys quiere automatizar el trabajo restante de la solicitud, pero mantener bajo el control del desarrollador la autorización para combinarla.

## Introducción a Agent Merge

**Agent Merge** automatiza el trabajo restante necesario para integrar una solicitud de incorporación de cambios. Al activarlo, Copilot resuelve los bloqueos: corrige las comprobaciones de integración continua (CI) que fallan, responde a comentarios de revisión y vuelve a integrar los cambios cuando sea necesario. Después, si el repositorio lo permite, habilita la combinación automática de GitHub.

Hasta ahora tú mismo seleccionabas **Merge pull request**. Agent Merge puede encargarse de esa tarea. Revisa el trabajo y confirma que está listo antes de activarlo.

## Usa Agent Merge para gestionar la solicitud

Ya has creado todo el código. Revísalo, crea la solicitud y deja que Agent Merge se encargue del resto del proceso.

1. Vuelve a Codespace.
2. Abre el cuadro de diálogo del agente con `/agent`.
3. Selecciona **Default** en la lista y pulsa <kbd>Enter</kbd>.
4. Crea una solicitud con el comando `/pr create`.
5. Activa Agent Merge con `/pr agentmerge`.
6. Copilot seguirá el proceso de integración continua de la solicitud. Cuando todo termine correctamente, realizará la combinación.
7. Comprueba que Copilot muestra un mensaje parecido a «PR #14 was squash-merged successfully».

> [!IMPORTANT]
> Agent Merge no omite las aprobaciones obligatorias, la protección de ramas, las colas de combinación, la configuración del repositorio ni los permisos que falten. Si el proceso se bloquea, revisa el motivo indicado y realiza manualmente la combinación revisada cuando el repositorio lo permita.

## Resumen y pasos siguientes

Has automatizado varias partes del proceso de desarrollo: generar código, probarlo y validarlo, y ahora gestionar la solicitud de incorporación de cambios. En esta lección:

- has aprendido qué es Agent Merge y cómo automatiza el ciclo de vida de una solicitud.
- has inspeccionado el cambio completo de la funcionalidad y las pruebas de validación.
- has creado la solicitud de filtrado.
- has activado Agent Merge después de la revisión y has confirmado que la solicitud se ha combinado.

A continuación, [explorarás otros comandos de barra de Copilot CLI][next-lesson] para administrar el contexto y los modelos, compartir sesiones y, si quieres, delegar tareas en la nube.

## Recursos

- [Gestionar solicitudes de incorporación de cambios con Copilot CLI][manage-prs]
- [Referencia de comandos de Copilot CLI][cli-reference]

[previous-lesson]: ../7-qa-agent/
[next-lesson]: ../9-cli-power-tools/
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
