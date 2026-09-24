# Tabla de clasificación de interfaces

| Interfaz                                                 | Canal        | Tecnología de interacción                     | Procedencia                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| -------------------------------------------------------- | ------------ | --------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Aplicación Quip (cliente web, escritorio Mac, móvil iOS) | Interactive  | GUI web, de escritorio y móvil                | quip.com/download y la ficha de la App Store documentan los clientes web, Mac e iOS. Las acciones se expresan manipulando vistas, menús y formularios sobre una representación navegable y persistente del estado del servicio (documentos, hojas, carpetas, salas de chat). Vigente a sept. 2026; los clientes de Windows y Android se retiraron el 6 de junio de 2024.                                                                                                          |
| API REST de Quip (métodos Automation y Admin)            | Programmatic | REST/JSON sobre HTTPS, OAuth 2.0              | quip.com/dev/automation/documentation/current y la referencia de la Admin API. El consumidor invoca operaciones definidas por el proveedor (crear, editar, copiar y exportar threads; gestionar carpetas, usuarios y permisos; monitorización de administración) mediante peticiones estructuradas. Automation y Admin comparten base (platform.quip.com), estilo de invocación (REST) y mecanismo de autenticación (OAuth 2.0), por lo que constituyen una sola interfaz lógica. |
| API SCIM 2.0                                             | Programmatic | REST según el estándar SCIM 2.0, token bearer | Documentación SCIM del portal de desarrolladores de Quip (entrada "SCIM API"). Aprovisionamiento y desaprovisionamiento de usuarios y grupos desde proveedores de identidad mediante operaciones estructuradas sobre el modelo de recursos SCIM. Se separa de la API REST general por seguir un estándar y un espacio de recursos propios, aunque ambas son Programmatic.                                                                                                         |
| WebSocket de tiempo real (Realtime)                      | Event        | WebSocket                                     | Método "Realtime / New Websocket" en la referencia de la Automation API y la app de ejemplo oficial del repositorio quip/quip-api ("websocket: Receive messages from Quip in real time"). Una vez obtenida la URL, Quip inicia la entrega y empuja mensajes y actualizaciones al receptor controlado por el consumidor a medida que se producen los eventos. El primitivo es la notificación de eventos empujada, no la petición y respuesta.                                     |

# Registro de cobertura

| Mecanismo de acceso                                                            | Disposición                                                                                                                                        |
| ------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| Cliente web                                                                    | Interfaz: Aplicación Quip (Interactive)                                                                                                            |
| Cliente de escritorio Mac                                                      | Interfaz: Aplicación Quip (Interactive)                                                                                                            |
| App móvil iOS                                                                  | Interfaz: Aplicación Quip (Interactive)                                                                                                            |
| App de escritorio Windows                                                      | Excluida: retirada el 6 de junio de 2024                                                                                                           |
| App móvil Android                                                              | Excluida: retirada el 6 de junio de 2024                                                                                                           |
| CLI/TUI de terminal                                                            | Excluida: no existe cliente CLI ni TUI oficial de primera parte; solo hay scripts de ejemplo y una biblioteca cliente de Python, que es un SDK     |
| Automation API (REST)                                                          | Interfaz: API REST de Quip (Programmatic)                                                                                                          |
| Admin API (REST)                                                               | Interfaz: API REST de Quip (misma base, autenticación e invocación)                                                                                |
| Events API (reporting de engagement)                                           | Interfaz: API REST de Quip. Es un conjunto de métodos REST de consulta (pull), no entrega de eventos, por lo que no abre un canal Event            |
| SCIM 2.0 API                                                                   | Interfaz: API SCIM 2.0 (Programmatic)                                                                                                              |
| Realtime / New Websocket                                                       | Interfaz: WebSocket de tiempo real (Event)                                                                                                         |
| Webhooks (apps de ejemplo entrantes: GitHub, PagerDuty, etc.)                  | Excluida: integraciones de ejemplo construidas sobre la API REST para publicar en threads; Quip no define una interfaz de webhooks saliente propia |
| Live Apps API/SDK                                                              | Excluida: framework y SDK de JavaScript de cliente para construir apps embebidas dentro del cliente Quip, no un canal de acceso al servicio        |
| Biblioteca cliente de Python y otros SDKs                                      | Excluida: SDK o biblioteca cliente                                                                                                                 |
| Índice de integraciones (Salesforce, Slack, Google Workspace, Jira, Box, etc.) | Excluida: integraciones de terceros, no interfaces definidas por el proveedor                                                                      |
| Endpoints de autenticación OAuth 2.0                                           | Excluida: mecanismo de autenticación, no una interfaz                                                                                              |

# Cobertura por canal

| Canal          | Evidencia            |
| -------------- | -------------------- |
| Interactive    | Observed             |
| Agentic        | No evidence observed |
| Conversational | No evidence observed |
| Event          | Observed             |
| Programmatic   | Observed             |

# Notas de clasificación

El WebSocket de tiempo real se clasifica como Event pese a que el endpoint "New Websocket" que entrega la URL es en sí una llamada REST. Lo determinante es el contrato del flujo resultante: una conexión persistente sobre la que el servicio empuja mensajes y actualizaciones cuando ocurren los eventos, un primitivo y una estructura de control distintos de la petición y respuesta de la API REST.

El canal Conversational queda sin evidencia. Las salas de chat de Quip son mensajería entre personas dentro de la interfaz interactiva, no un mecanismo de lenguaje natural interpretado por el servicio para ejecutar acciones. No se localizó ningún asistente conversacional ni interfaz de agente (MCP o protocolo similar) definidos por el proveedor, por lo que Agentic también queda sin evidencia. Ausencia de evidencia no equivale a ausencia del canal.

# Veredicto multicanal

`Multichannel` (3 paradigmas distintos observados: Interactive, Programmatic, Event).

```json
{
  "schema_version": "1.0",
  "generator": {
    "platform": "Claude",
    "provider": "Anthropic",
    "model": "UNKNOWN",
    "skill": "saas-interface-channel-analyzer",
    "skill_version": "1.0"
  },
  "generated_at": "2026-09-24T00:00:00Z",
  "evidence_checked_at": "2026-09-24T00:00:00Z",
  "saas": {
    "name": "Quip"
  },
  "interfaces": [
    {
      "name": "Quip application (web, Mac desktop, iOS mobile clients)",
      "technology": "Web, desktop and mobile GUI",
      "channel": "Interactive",
      "classification_rationale": "Actions are expressed by manipulating presented affordances (views, menus, forms) of a persistent, navigable representation of service state such as documents, spreadsheets, folders and chat rooms.",
      "provenance": [
        {
          "url": "https://quip.com/download",
          "evidence": "Official download page for the web, Mac desktop and mobile clients."
        },
        {
          "url": "https://apps.apple.com/us/app/quip-docs-chat-sheets/id647922896",
          "evidence": "Provider App Store listing for the Mac/iPad/iPhone client."
        },
        {
          "url": "https://quip.com/release-notes",
          "evidence": "Release notes confirming retirement of the Windows and Android apps on June 6, 2024, leaving web, Mac and iOS current."
        }
      ]
    },
    {
      "name": "Quip REST API (Automation and Admin methods)",
      "technology": "REST/JSON over HTTPS, OAuth 2.0",
      "channel": "Programmatic",
      "classification_rationale": "The consumer explicitly invokes provider-defined operations (thread/folder/user management, export, admin monitoring) through structured HTTP requests. Automation and Admin share base, invocation style and auth, so they are one logical interface.",
      "provenance": [
        {
          "url": "https://quip.com/dev/automation/documentation/current",
          "evidence": "REST-based Automation API with OAuth 2.0; documents operations on threads, folders, messages and users."
        },
        {
          "url": "https://quip.com/dev/admin/documentation/current",
          "evidence": "Admin API for site-wide/security operations, same base and OAuth 2.0 auth as the Automation API. The engagement 'Events API' here is a pull reporting method set, not event delivery."
        }
      ]
    },
    {
      "name": "SCIM 2.0 API",
      "technology": "REST following the SCIM 2.0 standard, bearer token",
      "channel": "Programmatic",
      "classification_rationale": "The consumer invokes standardized SCIM operations over a distinct resource model to provision and deprovision users and groups from identity providers. Distinct standard and resource namespace from the general REST API; both Programmatic.",
      "provenance": [
        {
          "url": "https://quip.com/dev/admin/documentation/current",
          "evidence": "Developer portal lists the SCIM API for automated user/group provisioning from identity providers."
        }
      ]
    },
    {
      "name": "Realtime WebSocket",
      "technology": "WebSocket",
      "channel": "Event",
      "classification_rationale": "After obtaining the socket URL, the service initiates delivery and pushes messages and updates to the consumer-controlled connection as events occur. The primitive is pushed event notification rather than request/response.",
      "provenance": [
        {
          "url": "https://quip.com/dev/automation/documentation/current",
          "evidence": "Automation API reference lists a 'Realtime / New Websocket' method that returns a websocket for receiving real-time updates."
        },
        {
          "url": "https://github.com/quip/quip-api/tree/master/samples/websocket",
          "evidence": "Official sample: opens a websocket and listens for real-time updates pushed from Quip."
        }
      ]
    }
  ],
  "access_mechanism_ledger": [
    {
      "mechanism": "Web client",
      "disposition": "interface",
      "detail": "Quip application (Interactive)"
    },
    {
      "mechanism": "Mac desktop client",
      "disposition": "interface",
      "detail": "Quip application (Interactive)"
    },
    {
      "mechanism": "iOS mobile app",
      "disposition": "interface",
      "detail": "Quip application (Interactive)"
    },
    {
      "mechanism": "Windows desktop app",
      "disposition": "excluded",
      "detail": "Retired on June 6, 2024"
    },
    {
      "mechanism": "Android mobile app",
      "disposition": "excluded",
      "detail": "Retired on June 6, 2024"
    },
    {
      "mechanism": "Terminal CLI/TUI",
      "disposition": "excluded",
      "detail": "No official first-party CLI or TUI; only sample scripts and a Python client library, which is an SDK"
    },
    {
      "mechanism": "Automation API (REST)",
      "disposition": "interface",
      "detail": "Quip REST API (Programmatic)"
    },
    {
      "mechanism": "Admin API (REST)",
      "disposition": "interface",
      "detail": "Quip REST API (same base, auth and invocation)"
    },
    {
      "mechanism": "Events API (engagement reporting)",
      "disposition": "interface",
      "detail": "Quip REST API; pull query methods, not event delivery"
    },
    {
      "mechanism": "SCIM 2.0 API",
      "disposition": "interface",
      "detail": "SCIM 2.0 API (Programmatic)"
    },
    {
      "mechanism": "Realtime / New Websocket",
      "disposition": "interface",
      "detail": "Realtime WebSocket (Event)"
    },
    {
      "mechanism": "Webhooks (inbound sample apps: GitHub, PagerDuty, etc.)",
      "disposition": "excluded",
      "detail": "Sample integrations built on the REST API to post into threads; no provider-defined outbound webhook interface"
    },
    {
      "mechanism": "Live Apps API/SDK",
      "disposition": "excluded",
      "detail": "Client-side JavaScript framework/SDK for embedded apps, not a service access channel"
    },
    {
      "mechanism": "Python client library and other SDKs",
      "disposition": "excluded",
      "detail": "SDK/client library"
    },
    {
      "mechanism": "Integrations index (Salesforce, Slack, Google Workspace, Jira, Box, etc.)",
      "disposition": "excluded",
      "detail": "Third-party integrations, not provider-defined interfaces"
    },
    {
      "mechanism": "OAuth 2.0 authentication endpoints",
      "disposition": "excluded",
      "detail": "Authentication mechanism, not an interface"
    }
  ],
  "channel_evidence": {
    "Interactive": "observed",
    "Agentic": "no_evidence_observed",
    "Conversational": "no_evidence_observed",
    "Event": "observed",
    "Programmatic": "observed"
  },
  "number_of_interfaces": 4,
  "multi_interface": true,
  "number_of_channels": 3,
  "multi_channel": true
}
```
