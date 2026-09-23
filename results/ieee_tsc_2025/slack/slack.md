I'll investigate Slack's official documentation to reconstruct its logical interfaces and classify each. Let me also glance at the boundary-case reference first.Let me pull the official Slack developer docs index to build the worklist of access mechanisms.I have the core developer APIs. Now let me check the less obvious access mechanisms: an official MCP server, Slack AI assistant, the CLI, and the first-party clients.Slack ships an official MCP server (mcp.slack.com) and a conversational Slackbot. Let me confirm details from official sources and check the CLI and first-party clients.The MCP server is confirmed as Agentic (tool discovery over JSON-RPC at mcp.slack.com). Let me verify the CLI (whether it has a TUI), the first-party desktop/mobile clients, and the conversational Slackbot.Let me confirm the first-party desktop/mobile clients and the conversational Slackbot from official Slack sources.# Análisis de interfaces y canales de acceso: Slack

## Resumen del SaaS

**Slack** (Slack Technologies, LLC, empresa de Salesforce). Se identifican **13 interfaces lógicas** repartidas sobre un número menor de tecnologías. Esas interfaces se distribuyen en **5 canales distintos** con al menos una interfaz clasificada en cada uno.

## Tabla de clasificación de interfaces

| Interfaz                            | Canal          | Tecnología de interacción                                              | Procedencia                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| ----------------------------------- | -------------- | ---------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Cliente web                         | Interactive    | Aplicación web en `app.slack.com`                                      | slack.com/downloads describe el cliente web junto a las apps nativas. El primitivo es la manipulación de affordances (canales, mensajes, menús) sobre una representación persistente y navegable del estado del servicio.                                                                                                                                                                                                                                       |
| App de escritorio                   | Interactive    | Cliente nativo Windows / macOS / Linux                                 | Páginas oficiales de descarga (slack.com/downloads/windows, /mac, /linux) publican instaladores nativos con integración de bandeja del sistema y atajos globales. Superficie de cliente distinta con el mismo paradigma de manipulación de affordances.                                                                                                                                                                                                         |
| App móvil                           | Interactive    | Apps nativas iOS / Android                                             | slack.com/downloads/ios y /android documentan apps nativas con sincronización en tiempo real. Superficie de cliente independiente, mismo primitivo de manipulación de affordances.                                                                                                                                                                                                                                                                              |
| Web API                             | Programmatic   | Métodos HTTP RPC en `slack.com/api/METHOD.method`, token bearer        | docs.slack.dev/apis/web-api documenta más de 220 métodos de estilo RPC sobre HTTPS. El consumidor invoca operaciones definidas por el proveedor de forma explícita (Operation Invocation). Absorbe Conversations, Calls, Presence, métodos de Slack Connect, Legal Holds, métodos admin y la Real-Time Search API, que comparten base y autenticación. Vigente.                                                                                                 |
| Incoming Webhooks                   | Programmatic   | POST a una URL secreta en `hooks.slack.com/services/...`               | El repositorio oficial node-slack-sdk (@slack/webhook) describe el envío de notificaciones a un canal. Pese al nombre "webhook", la dirección es consumidor hacia Slack: el consumidor invoca la operación de publicar mensaje. Base y modelo de autenticación distintos de la Web API. Vigente.                                                                                                                                                                |
| SCIM API                            | Programmatic   | REST estándar SCIM 2.0, token de admin                                 | docs.slack.dev/apis expone la SCIM API para aprovisionamiento y gestión de usuarios. Contrato de invocación propio (protocolo SCIM), base y autenticación distintas de la Web API, pero mismo paradigma de invocación de operaciones. Vigente.                                                                                                                                                                                                                  |
| Audit Logs API                      | Programmatic   | Endpoints REST de auditoría, token de admin de organización            | docs.slack.dev (cliente Audit Logs del SDK de Python) documenta el endpoint `/logs` para herramientas SIEM. Invocación explícita de operaciones sobre una base y autenticación propias. Vigente.                                                                                                                                                                                                                                                                |
| Status API                          | Programmatic   | API de monitorización de salud del producto                            | El índice oficial de APIs (docs.slack.dev/apis) la describe como una vía programática para monitorizar la salud de Slack. El consumidor consulta operaciones definidas por el proveedor. Vigente.                                                                                                                                                                                                                                                               |
| Slack CLI                           | Programmatic   | Interfaz de comandos para crear y gestionar apps                       | docs.slack.dev/tools/slack-cli describe una CLI para crear, gestionar y desplegar apps desde la línea de comandos, autorizada contra el workspace. El primitivo son comandos explícitos. La documentación de comandos no presenta un panel TUI persistente y navegable, por lo que no genera una segunda interfaz Interactive. Vigente.                                                                                                                         |
| Events API e interactividad         | Event          | Entrega HTTP a Request URL, o Socket Mode (WebSocket)                  | docs.slack.dev/apis documenta la Events API y su entrega vía HTTP Request URLs o Socket Mode, junto con los payloads de interactividad (slash commands, shortcuts, block actions, envíos de vista). El servicio inicia la interacción al ocurrir un evento o una interacción de usuario y la entrega a un receptor controlado por el consumidor (Event Notification). Vigente.                                                                                  |
| Legacy RTM API                      | Event          | WebSocket con flujo de eventos en tiempo real                          | docs.slack.dev/apis la describe como acceso WebSocket, ya obsoleto, a parte de la funcionalidad de las APIs Web y Events. El servicio transmite un flujo de eventos al receptor persistente del consumidor. **Obsoleta / legacy**, se conserva por completitud del inventario.                                                                                                                                                                                  |
| Slack MCP server                    | Agentic        | JSON-RPC 2.0 sobre Streamable HTTP en `mcp.slack.com/mcp`              | docs.slack.dev/ai/slack-mcp-server documenta un servidor MCP oficial que expone herramientas descritas semánticamente (buscar, leer y enviar mensajes, gestionar canvases, listas, ficheros, usuarios) que los clientes MCP descubren y seleccionan. El descubrimiento y la selección de capacidades forman parte del contrato (Capability Discovery and Invocation). Vigente, disponible de forma general.                                                     |
| Slackbot (asistente conversacional) | Conversational | Asistente de lenguaje natural con orquestación interna de herramientas | El blog oficial de Slack (slackbots-mcp-client) describe una única interfaz conversacional donde el usuario pide en lenguaje natural y Slackbot localiza la herramienta adecuada y coordina los pasos. El primitivo es el mensaje interpretado por el servicio; la orquestación de herramientas (cliente MCP de Slackbot) es interna al servicio y no un contrato de descubrimiento expuesto al consumidor, por lo que es Conversational y no Agentic. Vigente. |

## Tabla del registro de cobertura

| Mecanismo de acceso                                                           | Disposición                                                                                                                                         |
| ----------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| Web API (Conversations, Calls, Presence, Slack Connect, Real-Time Search API) | Interfaz: Web API                                                                                                                                   |
| Incoming Webhooks                                                             | Interfaz: Incoming Webhooks                                                                                                                         |
| SCIM API                                                                      | Interfaz: SCIM API                                                                                                                                  |
| Audit Logs API                                                                | Interfaz: Audit Logs API                                                                                                                            |
| Legal Holds API                                                               | Excluida: familia de métodos que comparte base y autenticación con la Web API; incorporada a Web API                                                |
| Admin Oversight API / métodos admin                                           | Excluida: familia de métodos con la misma base y autenticación; incorporada a Web API                                                               |
| Status API                                                                    | Interfaz: Status API                                                                                                                                |
| Slack CLI                                                                     | Interfaz: Slack CLI                                                                                                                                 |
| Events API                                                                    | Interfaz: Events API e interactividad                                                                                                               |
| Interactividad (slash commands, shortcuts, block actions, vistas/modales)     | Interfaz: Events API e interactividad (mismo paradigma de entrada por evento)                                                                       |
| HTTP Request URLs                                                             | Excluida: configuración de entrega de la Events API e interactividad, no es una interfaz                                                            |
| Socket Mode                                                                   | Excluida: transporte alternativo (WebSocket) para Events API e interactividad, no es una interfaz separada                                          |
| Legacy RTM API                                                                | Interfaz: Legacy RTM API (obsoleta)                                                                                                                 |
| Legacy Outgoing Webhooks                                                      | Excluida: integración personalizada legacy superada por la Events API; mismo paradigma Event                                                        |
| Slack MCP server (`mcp.slack.com`)                                            | Interfaz: Slack MCP server                                                                                                                          |
| Slackbot como cliente MCP                                                     | Excluida: Slack consumiendo servidores externos, no una vía de acceso a Slack; su lado orientado al usuario es el asistente conversacional Slackbot |
| Slackbot / asistente de IA conversacional                                     | Interfaz: Slackbot (asistente conversacional)                                                                                                       |
| Cliente web                                                                   | Interfaz: Cliente web                                                                                                                               |
| App de escritorio (Windows/macOS/Linux)                                       | Interfaz: App de escritorio                                                                                                                         |
| App móvil (iOS/Android)                                                       | Interfaz: App móvil                                                                                                                                 |
| Workflow Builder                                                              | Excluida: función de manipulación de affordances dentro del cliente web/escritorio, mismo paradigma y contrato, no es una interfaz separada         |
| Block Kit / Block Kit Builder                                                 | Excluida: framework de UI y su playground de diseño, no un mecanismo de acceso                                                                      |
| Slack MCP and Skills Plugin                                                   | Excluida: empaquetado del servidor MCP y skills para herramientas de codificación con IA, parte de la vía MCP, no una interfaz de acceso separada   |
| Bolt frameworks (Java/JS/Python), Deno Slack SDK, SDKs y librerías cliente    | Excluidas: SDKs y frameworks, no son interfaces                                                                                                     |
| Slack GitHub Action                                                           | Excluida: envoltorio de CI sobre la CLI/API, no una interfaz                                                                                        |
| OAuth / gestión de tokens                                                     | Excluida: mecanismo de autenticación                                                                                                                |
| App manifests                                                                 | Excluida: formato de configuración                                                                                                                  |
| Slack Marketplace / integraciones de terceros                                 | Excluida: distribución de apps de terceros, no una interfaz definida por el proveedor                                                               |

## Tabla de cobertura de canales

| Canal          | Evidencia |
| -------------- | --------- |
| Interactive    | Observed  |
| Agentic        | Observed  |
| Conversational | Observed  |
| Event          | Observed  |
| Programmatic   | Observed  |

## Notas de clasificación

La Events API y los payloads de interactividad (slash commands, shortcuts, acciones de bloque, envíos de vista) se presentan como una sola interfaz Event porque comparten primitivo y estructura de control: el servicio inicia la entrega hacia un receptor controlado por el consumidor ante un evento o una interacción. Aunque se separaran por su contrato (la interactividad espera una respuesta síncrona con `trigger_id` y `response_url`, mientras que los eventos siguen un patrón de acuse), ambas permanecerían en el canal Event, de modo que el veredicto por canal no cambia.

Incoming Webhooks se clasifica como Programmatic pese a su nombre. La dirección del flujo es del consumidor hacia Slack: el consumidor invoca la operación de publicar un mensaje contra una URL. Los antiguos Outgoing Webhooks eran lo contrario, entrega del servicio hacia el consumidor ante palabras disparadoras, es decir, paradigma Event, y hoy están superados por la Events API.

Slackbot se sitúa en Conversational y no en Agentic. El consumidor interactúa mediante mensajes en lenguaje natural y la orquestación de herramientas ocurre dentro del servicio a través del cliente MCP de Slackbot, sin que ese descubrimiento de capacidades sea parte del contrato orientado al usuario. El Slack MCP server sí es Agentic porque el descubrimiento y la selección de herramientas descritas semánticamente estructuran su contrato de interacción.

La Legacy RTM API está clasificada sobre evidencia oficial que la marca como obsoleta. No aporta un canal nuevo, ya que el canal Event queda cubierto por la Events API vigente.

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
    "name": "Slack"
  },
  "interfaces": [
    {
      "name": "Web client",
      "technology": "Web application at app.slack.com",
      "channel": "Interactive",
      "classification_rationale": "Actions are expressed by manipulating presented affordances (channels, messages, menus, forms) over a persistent, navigable representation of workspace state.",
      "provenance": [
        {
          "url": "https://slack.com/downloads/mac",
          "evidence": "Official downloads pages present the web app alongside native clients as a first-party surface."
        }
      ]
    },
    {
      "name": "Desktop app",
      "technology": "Native Windows / macOS / Linux client",
      "channel": "Interactive",
      "classification_rationale": "A separate first-party client surface whose primitive is affordance manipulation over a navigable representation of service state.",
      "provenance": [
        {
          "url": "https://slack.com/downloads/windows",
          "evidence": "Official installer for Windows with system-tray integration and global shortcuts."
        },
        {
          "url": "https://slack.com/downloads/linux",
          "evidence": "Official .rpm and .deb Linux packages."
        }
      ]
    },
    {
      "name": "Mobile app",
      "technology": "Native iOS / Android apps",
      "channel": "Interactive",
      "classification_rationale": "Independent first-party client surface; actions are expressed through affordance manipulation with real-time sync.",
      "provenance": [
        {
          "url": "https://slack.com/downloads/android",
          "evidence": "Official Android app distributed via Google Play."
        },
        {
          "url": "https://slack.com/intl/en-gb/downloads/ios",
          "evidence": "Official iOS app distributed via the App Store."
        }
      ]
    },
    {
      "name": "Web API",
      "technology": "HTTP RPC methods at slack.com/api/METHOD.method, bearer token",
      "channel": "Programmatic",
      "classification_rationale": "The consumer explicitly invokes provider-defined operations through structured HTTP RPC requests (Operation Invocation).",
      "provenance": [
        {
          "url": "https://docs.slack.dev/apis/web-api/",
          "evidence": "Collection of 200+ HTTP RPC-style methods over HTTPS with bearer-token auth; absorbs Conversations, Calls, Presence, Slack Connect, Legal Holds, admin methods and the Real-Time Search API sharing the same base and auth."
        }
      ]
    },
    {
      "name": "Incoming Webhooks",
      "technology": "POST to a secret URL at hooks.slack.com/services/...",
      "channel": "Programmatic",
      "classification_rationale": "Consumer-to-Slack direction: the consumer invokes a post-message operation against a unique webhook URL; distinct base and auth model from the Web API.",
      "provenance": [
        {
          "url": "https://github.com/slackhq/node-slack-sdk",
          "evidence": "Official SDK describes @slack/webhook for sending notifications to a channel via incoming webhooks."
        }
      ]
    },
    {
      "name": "SCIM API",
      "technology": "SCIM 2.0 standard REST, admin token",
      "channel": "Programmatic",
      "classification_rationale": "Explicit invocation of provider-defined provisioning operations following the SCIM standard; separate base and auth but the same operation-invocation paradigm.",
      "provenance": [
        {
          "url": "https://docs.slack.dev/apis/",
          "evidence": "SCIM API listed for user provisioning and management."
        }
      ]
    },
    {
      "name": "Audit Logs API",
      "technology": "Audit REST endpoints, organization admin token",
      "channel": "Programmatic",
      "classification_rationale": "The consumer explicitly invokes audit operations (the /logs endpoint) over a distinct base and auth; Operation Invocation.",
      "provenance": [
        {
          "url": "https://docs.slack.dev/tools/python-slack-sdk/audit-logs/index.html",
          "evidence": "Official Audit Logs client documents the /logs endpoint for SIEM tools requiring an org admin token."
        }
      ]
    },
    {
      "name": "Status API",
      "technology": "Health-monitoring API",
      "channel": "Programmatic",
      "classification_rationale": "The consumer queries provider-defined operations to monitor product health; Operation Invocation.",
      "provenance": [
        {
          "url": "https://docs.slack.dev/apis/",
          "evidence": "Official APIs index describes the Status API as a programmatic way to monitor the health of the Slack product."
        }
      ]
    },
    {
      "name": "Slack CLI",
      "technology": "Command-line interface for creating and managing apps",
      "channel": "Programmatic",
      "classification_rationale": "Actions are expressed as explicit commands authorized against the workspace; the command reference shows no persistent navigable TUI dashboard, so no second Interactive interface arises.",
      "provenance": [
        {
          "url": "https://docs.slack.dev/tools/slack-cli/",
          "evidence": "CLI to create and manage Slack apps from the command line, with an authorization flow and a command reference."
        }
      ]
    },
    {
      "name": "Events API and interactivity",
      "technology": "HTTP delivery to a Request URL, or Socket Mode WebSocket",
      "channel": "Event",
      "classification_rationale": "The service initiates delivery when a subscribed event or user interaction occurs and pushes the payload to a consumer-controlled receiver (Event Notification); Socket Mode is a transport for the same contract.",
      "provenance": [
        {
          "url": "https://docs.slack.dev/apis/",
          "evidence": "Events API documented with HTTP Request URLs and Socket Mode; interactivity (slash commands, shortcuts, block actions) delivers payloads to a configured Request URL."
        }
      ]
    },
    {
      "name": "Legacy RTM API",
      "technology": "WebSocket real-time event stream",
      "channel": "Event",
      "classification_rationale": "The service streams real-time events to the consumer's persistent WebSocket receiver. Deprecated/legacy, retained for inventory completeness; adds no new channel.",
      "provenance": [
        {
          "url": "https://docs.slack.dev/apis/",
          "evidence": "Described as an outmoded WebSocket API providing access to some functionality of the Web and Events APIs."
        }
      ]
    },
    {
      "name": "Slack MCP server",
      "technology": "JSON-RPC 2.0 over Streamable HTTP at mcp.slack.com/mcp",
      "channel": "Agentic",
      "classification_rationale": "Exposes semantically described tools (search, read/send messages, canvases, lists, files, users) that MCP clients discover and select as part of the interaction contract (Capability Discovery and Invocation).",
      "provenance": [
        {
          "url": "https://docs.slack.dev/ai/slack-mcp-server",
          "evidence": "Official MCP server at mcp.slack.com/mcp exposing a documented tool set over JSON-RPC 2.0, with OAuth and admin-approved client apps."
        }
      ]
    },
    {
      "name": "Slackbot AI assistant",
      "technology": "Natural-language conversational assistant with internal tool orchestration",
      "channel": "Conversational",
      "classification_rationale": "The consumer interacts through natural-language messages interpreted by the service; tool orchestration via Slackbot's MCP client is internal, not a consumer-facing discovery contract, so it is Conversational rather than Agentic.",
      "provenance": [
        {
          "url": "https://slack.com/blog/news/slackbots-mcp-client",
          "evidence": "Slackbot presented as a single conversational interface: the user asks in plain language and Slackbot locates the right tool and coordinates the steps."
        }
      ]
    }
  ],
  "access_mechanism_ledger": [
    {
      "mechanism": "Web API (Conversations, Calls, Presence, Slack Connect, Real-Time Search API)",
      "disposition": "interface",
      "detail": "Web API"
    },
    {
      "mechanism": "Incoming Webhooks",
      "disposition": "interface",
      "detail": "Incoming Webhooks"
    },
    {
      "mechanism": "SCIM API",
      "disposition": "interface",
      "detail": "SCIM API"
    },
    {
      "mechanism": "Audit Logs API",
      "disposition": "interface",
      "detail": "Audit Logs API"
    },
    {
      "mechanism": "Legal Holds API",
      "disposition": "excluded",
      "detail": "Method family sharing base and auth with the Web API; folded into Web API"
    },
    {
      "mechanism": "Admin Oversight API / admin methods",
      "disposition": "excluded",
      "detail": "Method family with the same base and auth; folded into Web API"
    },
    {
      "mechanism": "Status API",
      "disposition": "interface",
      "detail": "Status API"
    },
    {
      "mechanism": "Slack CLI",
      "disposition": "interface",
      "detail": "Slack CLI"
    },
    {
      "mechanism": "Events API",
      "disposition": "interface",
      "detail": "Events API and interactivity"
    },
    {
      "mechanism": "Interactivity (slash commands, shortcuts, block actions, views)",
      "disposition": "interface",
      "detail": "Events API and interactivity (same event-delivery paradigm)"
    },
    {
      "mechanism": "HTTP Request URLs",
      "disposition": "excluded",
      "detail": "Delivery configuration for Events API and interactivity, not an interface"
    },
    {
      "mechanism": "Socket Mode",
      "disposition": "excluded",
      "detail": "Alternate WebSocket transport for Events API and interactivity, not a separate interface"
    },
    {
      "mechanism": "Legacy RTM API",
      "disposition": "interface",
      "detail": "Legacy RTM API (deprecated)"
    },
    {
      "mechanism": "Legacy Outgoing Webhooks",
      "disposition": "excluded",
      "detail": "Legacy custom integration superseded by the Events API; same Event paradigm"
    },
    {
      "mechanism": "Slack MCP server (mcp.slack.com)",
      "disposition": "interface",
      "detail": "Slack MCP server"
    },
    {
      "mechanism": "Slackbot as MCP client",
      "disposition": "excluded",
      "detail": "Slack consuming external servers, not an access path into Slack; its user-facing side is the Slackbot conversational assistant"
    },
    {
      "mechanism": "Slackbot / conversational AI assistant",
      "disposition": "interface",
      "detail": "Slackbot AI assistant"
    },
    {
      "mechanism": "Web client",
      "disposition": "interface",
      "detail": "Web client"
    },
    {
      "mechanism": "Desktop app (Windows/macOS/Linux)",
      "disposition": "interface",
      "detail": "Desktop app"
    },
    {
      "mechanism": "Mobile app (iOS/Android)",
      "disposition": "interface",
      "detail": "Mobile app"
    },
    {
      "mechanism": "Workflow Builder",
      "disposition": "excluded",
      "detail": "Affordance-manipulation feature within the web/desktop client, same paradigm and contract, not a separate interface"
    },
    {
      "mechanism": "Block Kit / Block Kit Builder",
      "disposition": "excluded",
      "detail": "UI framework and its design playground, not an access mechanism"
    },
    {
      "mechanism": "Slack MCP and Skills Plugin",
      "disposition": "excluded",
      "detail": "Packaging of the MCP server and skills for AI coding tools, part of the MCP path, not a separate access interface"
    },
    {
      "mechanism": "Bolt frameworks (Java/JS/Python), Deno Slack SDK, client libraries",
      "disposition": "excluded",
      "detail": "SDKs and frameworks, not interfaces"
    },
    {
      "mechanism": "Slack GitHub Action",
      "disposition": "excluded",
      "detail": "CI wrapper over the CLI/API, not an interface"
    },
    {
      "mechanism": "OAuth / token handling",
      "disposition": "excluded",
      "detail": "Authentication mechanism"
    },
    {
      "mechanism": "App manifests",
      "disposition": "excluded",
      "detail": "Configuration format"
    },
    {
      "mechanism": "Slack Marketplace / third-party integrations",
      "disposition": "excluded",
      "detail": "Third-party app distribution, not a provider-defined interface"
    }
  ],
  "channel_evidence": {
    "Interactive": "observed",
    "Agentic": "observed",
    "Conversational": "observed",
    "Event": "observed",
    "Programmatic": "observed"
  },
  "number_of_interfaces": 13,
  "multi_interface": true,
  "number_of_channels": 5,
  "multi_channel": true
}
```
