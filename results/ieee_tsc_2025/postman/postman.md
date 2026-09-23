## Resumen del SaaS

**Postman** (Postman, Inc.) es una plataforma de desarrollo de APIs. A partir de su documentación oficial se reconstruyen **8 interfaces lógicas**, distribuidas en **5 canales distintos** con al menos una interfaz clasificada.

## Clasificación de interfaces

| Interfaz                                         | Canal          | Tecnología de interacción                         | Procedencia                                                                                                                                                                                                                                                                                                                                  |
| ------------------------------------------------ | -------------- | ------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Aplicación web                                   | Interactive    | Cliente web en navegador                          | Docs oficiales de instalación confirman el web app como cliente de primera parte para tareas de desarrollo y prueba de APIs. El primitivo es la manipulación de affordances (vistas, controles, formularios) sobre una representación navegable del estado. (learning.postman.com/docs/getting-started/installation/install-app)             |
| Aplicación de escritorio (Windows, macOS, Linux) | Interactive    | App nativa de escritorio                          | La misma página oficial documenta la app nativa para Windows, macOS y Linux como experiencia completa. Superficie distinta del web app, mismo paradigma de manipulación de affordances. (learning.postman.com/docs/getting-started/installation/install-app)                                                                                 |
| Postman API (REST, incluye SCIM)                 | Programmatic   | API REST sobre HTTP, autenticación por API key    | La doc de la Postman API describe la invocación de operaciones definidas por el proveedor para gestionar colecciones, entornos, monitores y otros recursos. El primitivo es la invocación explícita de operaciones estructuradas. (learning.postman.com/docs/developer/postman-api/intro-api)                                                |
| Postman CLI                                      | Programmatic   | Ejecutable de línea de comandos                   | Compañero de línea de comandos que ejecuta colecciones y comprobaciones de gobernanza y seguridad mediante comandos. Invocación de operaciones por comandos estructurados. (learning.postman.com/concepts)                                                                                                                                   |
| Newman                                           | Programmatic   | Ejecutable de línea de comandos (npm)             | Runner de colecciones de primera parte (postmanlabs/newman), documentado oficialmente. Ejecutable y base distintos de Postman CLI, mismo paradigma de comandos. (learning.postman.com/docs/reference/newman-cli/command-line-integration-with-newman)                                                                                        |
| Servidor MCP de Postman                          | Agentic        | Model Context Protocol (remoto y local)           | El servidor MCP oficial expone capacidades descritas semánticamente (workspaces, colecciones, specs, mocks, monitores) que un agente descubre y selecciona. Caso límite MCP resuelto como Agentic: el descubrimiento y la selección forman parte del contrato. (learning.postman.com/docs/reference/postman-api/postman-mcp-server/overview) |
| Agent Mode (antes Postbot)                       | Conversational | Asistente de lenguaje natural integrado en la app | El consumidor interactúa mediante mensajes en lenguaje natural; la orquestación de herramientas es interna al servicio. Caso límite resuelto como Conversational, no Agentic. (learning.postman.com/docs/use/agent-mode/overview)                                                                                                            |
| Webhooks personalizados (entrega de eventos)     | Event          | Webhooks salientes hacia una URL receptora        | Postman inicia la interacción cuando ocurren eventos (resultados de monitores, feeds de actividad de equipo y colección, copias de seguridad) y los entrega a un receptor controlado por el consumidor. (learning.postman.com/docs/integrations/webhooks)                                                                                    |

## Registro de cobertura

| Mecanismo de acceso                                               | Disposición                                                                                                                                             |
| ----------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Cliente web                                                       | Interfaz: Aplicación web (Interactive)                                                                                                                  |
| Cliente de escritorio                                             | Interfaz: Aplicación de escritorio (Interactive)                                                                                                        |
| Cliente móvil (iOS/Android)                                       | Excluido: no existe cliente móvil oficial de primera parte; solo consta como petición de funcionalidad de larga data                                    |
| Terminal / TUI                                                    | Excluido: las CLI (Postman CLI, Newman) son basadas en comandos; ninguna expone una TUI persistente y navegable                                         |
| Postman API (REST)                                                | Interfaz: Postman API (Programmatic)                                                                                                                    |
| SCIM API                                                          | Plegado en la Postman API: mismo paradigma REST de invocación de operaciones (subconjunto de aprovisionamiento)                                         |
| Postman CLI                                                       | Interfaz: Postman CLI (Programmatic)                                                                                                                    |
| Newman                                                            | Interfaz: Newman (Programmatic)                                                                                                                         |
| Servidor MCP de Postman                                           | Interfaz: Servidor MCP de Postman (Agentic)                                                                                                             |
| Agent Mode / Postbot                                              | Interfaz: Agent Mode (Conversational)                                                                                                                   |
| Postman Flows                                                     | Excluido: editor visual dentro del web/escritorio; mismo paradigma de manipulación de affordances que la interfaz Interactive, no una interfaz distinta |
| Webhooks salientes (resultados de monitor, actividad)             | Interfaz: Webhooks personalizados (Event)                                                                                                               |
| Webhook entrante que dispara colecciones                          | Excluido: disparador de automatización donde Postman es el receptor, creado vía Postman API; no es una interfaz de acceso propia                        |
| Índice de integraciones (Slack, GitHub, CI, etc.)                 | Excluido: integraciones de terceros, no interfaces lógicas definidas por el proveedor                                                                   |
| SDKs (Collection SDK, Postman SDK)                                | Excluido: librerías cliente, no interfaces                                                                                                              |
| Constructores de peticiones gRPC / WebSocket / GraphQL / SOAP     | Excluido: funciones para probar las APIs objetivo del usuario, no para acceder a Postman como servicio                                                  |
| MCP Requests / AI Agent Builder (probar servidores MCP y modelos) | Excluido: función para probar servidores MCP y modelos externos, no una vía de acceso a Postman                                                         |
| Índice llms.txt / llms-full.txt                                   | Excluido: formato de documentación, no una interfaz de acceso                                                                                           |

## Cobertura de canales

| Canal          | Evidencia |
| -------------- | --------- |
| Interactive    | Observado |
| Agentic        | Observado |
| Conversational | Observado |
| Event          | Observado |
| Programmatic   | Observado |

## Notas de clasificación

Newman está documentado como oficial y sigue vigente, pero la propia documentación indica que no es compatible con el formato de colección v3 de Postman v12 en adelante y recomienda migrar a la Postman CLI. Se clasifica como interfaz actual con esa salvedad de vigencia; su canal (Programmatic) no cambia por ello.

Las dos decisiones límite se resolvieron con el árbol de decisión aplicado en orden: el servidor MCP es Agentic porque el descubrimiento y la selección de capacidades forman parte del contrato, y Agent Mode es Conversational porque el consumidor interactúa por mensajes con orquestación de herramientas interna al servicio.

## Veredicto multicanal

**Multichannel** (5 paradigmas distintos observados).

```json
{
  "schema_version": "1.0",
  "generator": {
    "platform": "Claude",
    "provider": "Anthropic",
    "model": "claude-opus-4-8",
    "skill": "saas-interface-channel-analyzer",
    "skill_version": "1.0"
  },
  "generated_at": "2026-09-22T00:00:00Z",
  "evidence_checked_at": "2026-09-22T00:00:00Z",
  "saas": {
    "name": "Postman"
  },
  "interfaces": [
    {
      "name": "Web application",
      "technology": "Browser-based web client",
      "channel": "Interactive",
      "classification_rationale": "Actions are expressed by manipulating presented affordances (views, controls, forms) over a persistent, navigable representation of service state.",
      "provenance": [
        {
          "url": "https://learning.postman.com/docs/getting-started/installation/install-app",
          "evidence": "Official install docs confirm Postman is available as a web app for API development and testing tasks in the browser."
        }
      ]
    },
    {
      "name": "Desktop application",
      "technology": "Native desktop app (Windows, macOS, Linux)",
      "channel": "Interactive",
      "classification_rationale": "Native GUI client whose primitive is affordance manipulation over a navigable state representation; a distinct surface from the web app.",
      "provenance": [
        {
          "url": "https://learning.postman.com/docs/getting-started/installation/install-app",
          "evidence": "Official install docs confirm the native desktop app for Windows, macOS and Linux as the full Postman experience."
        }
      ]
    },
    {
      "name": "Postman API",
      "technology": "REST API over HTTP with API key auth (includes SCIM subset)",
      "channel": "Programmatic",
      "classification_rationale": "Consumer explicitly invokes provider-defined operations through structured HTTP requests to manage collections, environments, monitors and other assets.",
      "provenance": [
        {
          "url": "https://learning.postman.com/docs/developer/postman-api/intro-api",
          "evidence": "Official docs describe programmatically managing Postman assets via the REST API; SCIM API shares the same REST invocation paradigm for provisioning."
        }
      ]
    },
    {
      "name": "Postman CLI",
      "technology": "Command-line executable",
      "channel": "Programmatic",
      "classification_rationale": "Command-based invocation of provider-defined operations (run collections, governance and security checks) from the command line.",
      "provenance": [
        {
          "url": "https://learning.postman.com/concepts",
          "evidence": "Official overview presents the Postman CLI as a secure command-line companion that runs collections and checks API definitions."
        }
      ]
    },
    {
      "name": "Newman",
      "technology": "Command-line collection runner (npm package)",
      "channel": "Programmatic",
      "classification_rationale": "First-party command-line runner invoking collection runs via structured commands; distinct executable and base from Postman CLI, same command paradigm.",
      "provenance": [
        {
          "url": "https://learning.postman.com/docs/reference/newman-cli/command-line-integration-with-newman",
          "evidence": "Official docs describe Newman as a command-line tool for running Postman Collections; noted as legacy for v12 collections with recommended migration to Postman CLI."
        }
      ]
    },
    {
      "name": "Postman MCP server",
      "technology": "Model Context Protocol server (remote and local)",
      "channel": "Agentic",
      "classification_rationale": "Exposes semantically described capabilities over Postman resources that an agent discovers and selects; discovery and selection are part of the interaction contract (MCP boundary case resolves to Agentic).",
      "provenance": [
        {
          "url": "https://learning.postman.com/docs/reference/postman-api/postman-mcp-server/overview",
          "evidence": "Official docs state the Postman MCP server enables AI agents to manage Postman resources, translating natural language commands into API workflows via exposed tools."
        }
      ]
    },
    {
      "name": "Agent Mode",
      "technology": "In-app natural-language assistant (formerly Postbot)",
      "channel": "Conversational",
      "classification_rationale": "Consumer interacts through natural-language messages interpreted by the service; tool orchestration is internal and not part of the consumer-facing contract (natural-language-assistant boundary case resolves to Conversational).",
      "provenance": [
        {
          "url": "https://learning.postman.com/docs/use/agent-mode/overview",
          "evidence": "Official docs describe Agent Mode as turning natural-language words into action across the API lifecycle using built-in tools within Postman."
        }
      ]
    },
    {
      "name": "Custom webhooks (outbound event delivery)",
      "technology": "Outbound webhooks to a consumer-controlled URL",
      "channel": "Event",
      "classification_rationale": "The service initiates delivery when subscribed events occur (monitor results, team and collection activity feeds, backups) to a consumer-controlled receiver endpoint.",
      "provenance": [
        {
          "url": "https://learning.postman.com/docs/integrations/webhooks",
          "evidence": "Official docs describe configuring custom webhooks to send events such as monitor results and activity feeds to a webhook URL whenever those events occur."
        }
      ]
    }
  ],
  "access_mechanism_ledger": [
    {
      "mechanism": "Web client",
      "disposition": "interface",
      "detail": "Web application (Interactive)"
    },
    {
      "mechanism": "Desktop client",
      "disposition": "interface",
      "detail": "Desktop application (Interactive)"
    },
    {
      "mechanism": "Mobile client (iOS/Android)",
      "disposition": "excluded",
      "detail": "No official first-party mobile client; only a long-standing feature request"
    },
    {
      "mechanism": "Terminal / TUI",
      "disposition": "excluded",
      "detail": "CLIs are command-based; no persistent navigable TUI is shipped"
    },
    {
      "mechanism": "Postman API (REST)",
      "disposition": "interface",
      "detail": "Postman API (Programmatic)"
    },
    {
      "mechanism": "SCIM API",
      "disposition": "excluded",
      "detail": "Folded into Postman API: same REST operation-invocation paradigm (provisioning subset)"
    },
    {
      "mechanism": "Postman CLI",
      "disposition": "interface",
      "detail": "Postman CLI (Programmatic)"
    },
    {
      "mechanism": "Newman",
      "disposition": "interface",
      "detail": "Newman (Programmatic)"
    },
    {
      "mechanism": "Postman MCP server",
      "disposition": "interface",
      "detail": "Postman MCP server (Agentic)"
    },
    {
      "mechanism": "Agent Mode / Postbot",
      "disposition": "interface",
      "detail": "Agent Mode (Conversational)"
    },
    {
      "mechanism": "Postman Flows",
      "disposition": "excluded",
      "detail": "Visual editor within the web/desktop app; same affordance-manipulation paradigm as the Interactive UI"
    },
    {
      "mechanism": "Outbound custom webhooks",
      "disposition": "interface",
      "detail": "Custom webhooks (Event)"
    },
    {
      "mechanism": "Inbound collection-trigger webhook",
      "disposition": "excluded",
      "detail": "Automation trigger where Postman is the receiver, created via the Postman API; not a distinct access interface"
    },
    {
      "mechanism": "Integrations index (Slack, GitHub, CI, etc.)",
      "disposition": "excluded",
      "detail": "Third-party integrations, not provider-defined logical interfaces"
    },
    {
      "mechanism": "SDKs (Collection SDK, Postman SDK)",
      "disposition": "excluded",
      "detail": "Client libraries, not interfaces"
    },
    {
      "mechanism": "gRPC / WebSocket / GraphQL / SOAP request builders",
      "disposition": "excluded",
      "detail": "Features for testing the user's target APIs, not for accessing Postman itself"
    },
    {
      "mechanism": "MCP Requests / AI Agent Builder",
      "disposition": "excluded",
      "detail": "Feature for testing external MCP servers and AI models, not a Postman access interface"
    },
    {
      "mechanism": "llms.txt / llms-full.txt",
      "disposition": "excluded",
      "detail": "Documentation format, not an access interface"
    }
  ],
  "channel_evidence": {
    "Interactive": "observed",
    "Agentic": "observed",
    "Conversational": "observed",
    "Event": "observed",
    "Programmatic": "observed"
  },
  "number_of_interfaces": 8,
  "multi_interface": true,
  "number_of_channels": 5,
  "multi_channel": true
}
```
