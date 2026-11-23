---
title: "Ejercicio 4 - Supervisar y administrar agentes"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

En los últimos ejercicios has pedido a Copilot cloud agent que realice tres tareas distintas para mejorar la experiencia de usuario y añadir funcionalidad. Aunque cloud agent trabaja de forma autónoma y asíncrona, es importante poder supervisar esas tareas.

Hay varias herramientas para administrar las tareas asignadas a cloud agent, como la [página de agentes][agents-page] de GitHub.com. Desde Mission Control puedes ver las tareas de los agentes que tienen solicitudes de incorporación de cambios abiertas, explorar las operaciones realizadas y guiar una sesión en curso.

En esta lección:

- explorarás la página de agentes para supervisar las tareas de cloud agent.
- guiarás una sesión en curso para pedir funcionalidad adicional.

## Escenario

Después de asignar al agente la implementación del modo de alto contraste, el equipo se dio cuenta de que también sería un buen momento para añadir el modo claro. Como ya estaba trabajando en actualizar los estilos del sitio y añadir controles, tenía sentido incluir esta mejora. Guiarás el trabajo del agente para que añada ambos modos.

## Revisa las tareas de Copilot cloud agent

Consulta el estado de las tareas asignadas a Copilot cloud agent.

1. Ve a la [página de agentes de Copilot](https://github.com/copilot/agents).
2. Revisa las tareas que aparecen en los paneles principal e izquierdo. Deberías ver las tareas asignadas a Copilot, entre ellas:
   - Actualizar la documentación del código.
   - Generar API para modificar juegos.
   - Añadir un modo de alto contraste al sitio web.
3. Selecciona una de las tareas en curso y revisa las operaciones realizadas por Copilot, que pueden incluir:
   - Obtener el código del repositorio.
   - Crear el entorno de trabajo.
   - Configurar servidores MCP.
   - Realizar los pasos necesarios para completar la tarea.

> [!NOTE]
> Los pasos concretos varían según el estado del trabajo de Copilot y el enfoque que haya elegido.

4. Fíjate también en el panel de solicitudes de incorporación de cambios (PR) de la derecha. Desde ahí puedes ver la solicitud y los archivos modificados para seguir el trabajo.

## Guía a cloud agent

Ya has visto las tareas activas. Ahora pide a Copilot que incluya un control del modo claro mientras trabaja en el modo de alto contraste.

1. Selecciona la sesión relacionada con el modo de alto contraste. El título exacto depende del nombre que Copilot haya asignado y del estado del trabajo.

    ![Sesión de accesibilidad en Mission Control](../../../_images/ex6-accessibility-session.png)

2. Supervisa la sesión durante unos minutos, hasta que indique que ha terminado la configuración y empezado a trabajar. Verás mensajes parecidos a los siguientes.
3. En el cuadro de diálogo **Steer active session while Copilot is working**, escribe este prompt:

   ```plaintext
   While we are working on a high contrast mode, let's also add a light mode. There should be a switch for this mode as well where users can select their desired display mode.
   ```

    ![Captura de la tarea de cloud agent en la página de agentes con el cuadro de diálogo para guiar la sesión activa resaltado](../../../_images/ex6-steer-cloud-agent-task.png)

4. Pulsa <kbd>Enter</kbd> para enviar el prompt.
5. Observa cómo Copilot lo confirma y lo incorpora a su trabajo.

## Deja que Copilot trabaje

Copilot continuará con la tarea actualizada. Incorporará la nueva solicitud al flujo cuando termine el paso en el que estaba trabajando.

Como antes, el proceso tardará varios minutos. Puedes aprovechar el tiempo para repasar lo que has aprendido hasta ahora.

## Resumen y pasos siguientes

En esta lección has explorado la página de agentes de Copilot, el centro de control para supervisar y guiar las tareas de GitHub Copilot cloud agent. Puedes seguir las tareas activas y completadas, revisar el trabajo realizado y redirigir las tareas en curso para ajustar el alcance o proporcionar instrucciones.

Has aprendido a:

- explorar Mission Control y la página de agentes para supervisar las tareas de cloud agent.
- redirigir una sesión en curso para pedir funcionalidad adicional.

Mientras Copilot termina las funciones de accesibilidad, [revisarás las solicitudes de incorporación de cambios que ha creado][next-lesson].

## Recursos

- [Página de agentes de Copilot][agents-page]
- [Acerca de los agentes personalizados][custom-agents]

---

| [← Lección anterior: Agentes personalizados][previous-lesson] | [Siguiente lección: Iterar sobre el trabajo de Copilot →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
