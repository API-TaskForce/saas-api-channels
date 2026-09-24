## Resumen del SaaS

Wrike (Wrike, Inc.) es una plataforma de gestión del trabajo. A partir de su documentación oficial identifico **8 interfaces lógicas** repartidas en **5 canales distintos** con al menos una interfaz clasificada. El proveedor publica su portal de desarrolladores en developers.wrike.com y su producto en wrike.com, con centros de datos en US, US2 y EU.

La base de la API REST v4 es https://www.wrike.com/api/v4 y todas las peticiones usan un token OAuth 2.0. La API de DataHub es una superficie separada, servida bajo https://www.wrike.com/app/wrike_v2_web con rutas /public/api/v1. Existe además un servidor MCP propio en https://mcp.wrike.com/v2, que usa Streamable HTTP y expone un conjunto fijo de herramientas descubribles por asistentes de IA. Dentro del producto, Wrike Copilot es un asistente de IA integrado en los proyectos que responde preguntas y resume trabajo cuando el usuario simplemente le pregunta.

## Tabla de clasificación de interfaces

| Interfaz                                                                                   | Canal          | Tecnología de interacción                    | Procedencia                                                                                                                                                                                                                                                                                                                                                                                 |
| ------------------------------------------------------------------------------------------ | -------------- | -------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Wrike Workspace (aplicación web, también entregada como cliente de escritorio Windows/Mac) | Interactive    | Aplicación web / cliente de escritorio       | Producto oficial accesible por navegador; el usuario actúa manipulando vistas, menús y formularios de una representación navegable del estado. Fuente: wrike.com/apps/mobile-and-desktop. Primitivo = manipulación de affordances. Evidencia actual.                                                                                                                                        |
| Wrike mobile app (iOS/Android)                                                             | Interactive    | App nativa móvil                             | Wrike publica app nativa de Android e iOS para acceder al trabajo desde el móvil (wrike.com/apps/mobile-and-desktop, try-mobile). Contrato de interacción táctil nativo, genuinamente distinto del web. Manipulación de affordances.                                                                                                                                                        |
| Wrike REST API v4                                                                          | Programmatic   | API REST HTTP (OAuth 2.0)                    | Los métodos se organizan de forma RESTful y admiten GET, POST, PUT y DELETE, con autorización OAuth 2.0; base www.wrike.com/api/v4. El consumidor invoca operaciones definidas por el proveedor. Evidencia actual.                                                                                                                                                                          |
| Wrike DataHub Public API                                                                   | Programmatic   | API REST HTTP (OAuth 2.0), base distinta     | Superficie de API separada con su propia especificación OpenAPI; servidores www.wrike.com/app/wrike_v2_web y rutas /public/api/v1/databases. Base y estructura de control (idempotencia por requestId, tokens de página de sesión) genuinamente distintas de v4. Invocación de operaciones.                                                                                                 |
| Email-to-Wrike (creación/edición de tareas por correo)                                     | Programmatic   | Envío por correo (SMTP) a dirección de Wrike | Enviando un correo a la dirección de Wrike se crea y asigna una tarea, con la ubicación, fechas y estado codificados entre corchetes en el asunto (help.wrike.com; wrike.com/apps/email-integration). Sintaxis estructurada, no lenguaje natural interpretado. El consumidor invoca la operación crear/editar tarea vía SMTP.                                                               |
| Wrike Webhooks                                                                             | Event          | Notificaciones HTTP salientes                | Los webhooks permiten suscribirse a notificaciones sobre cambios en Wrike en lugar de sondear; se envía una carga útil al endpoint HTTP del cliente cuando ocurren cambios concretos (developers.wrike.com/docs/webhooks). El servicio inicia la entrega a un receptor controlado por el consumidor. Notificación de eventos.                                                               |
| Wrike MCP Server                                                                           | Agentic        | Servidor MCP (Streamable HTTP, OAuth/PAT)    | MCP da a los asistentes compatibles una forma estructurada de trabajar con el espacio de Wrike, con un conjunto fijo de herramientas que el cliente descubre y cachea al conectarse (developers.wrike.com/docs/wrike-mcp-server-overview). Descubrimiento y selección de capacidades forman parte del contrato: caso frontera MCP resuelto como Agentic, no Programmatic. Evidencia actual. |
| Wrike Copilot                                                                              | Conversational | Asistente de IA en el producto               | Wrike Copilot usa lenguaje natural para obtener respuestas e información en tiempo real sobre proyectos: en lugar de buscar, basta con preguntarle (wrike.com/ai; newsroom). Primitivo = el mensaje en lenguaje natural, con orquestación de herramientas interna al servicio. Caso frontera de asistente resuelto como Conversational, no Agentic.                                         |

## Registro de cobertura (coverage ledger)

| Mecanismo de acceso                         | Disposición                                                                                                                                                                                                      |
| ------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| API REST v4                                 | Interfaz: Wrike REST API v4 (Programmatic)                                                                                                                                                                       |
| DataHub Public API                          | Interfaz: Wrike DataHub Public API (Programmatic)                                                                                                                                                                |
| BI Export API                               | Excluido: no es interfaz aparte; se accede por el método /data-export de la API v4 (misma base y auth)                                                                                                           |
| Webhooks                                    | Interfaz: Wrike Webhooks (Event)                                                                                                                                                                                 |
| Servidor MCP                                | Interfaz: Wrike MCP Server (Agentic)                                                                                                                                                                             |
| Email entrante (wrike@wrike.com)            | Interfaz: Email-to-Wrike (Programmatic)                                                                                                                                                                          |
| Complementos Gmail / Outlook                | Excluido: integraciones de origen construidas sobre la API y la interfaz web, no una interfaz propia distinta                                                                                                    |
| Cloud Content Connector                     | Excluido: especificación que implementan los proveedores DAM externos para que Wrike los invoque; dirección inversa, no un modo de acceder a Wrike                                                               |
| Wrike Copilot                               | Interfaz: Wrike Copilot (Conversational)                                                                                                                                                                         |
| AI Agents / Conversational AI Agent Builder | Excluido: automatización interna y constructor dentro del Workspace, no una interfaz de acceso distinta                                                                                                          |
| Superficie web                              | Interfaz: Wrike Workspace (Interactive)                                                                                                                                                                          |
| Superficie de escritorio (Windows/Mac)      | Excluido como interfaz aparte: mismo contrato de manipulación de affordances que el Workspace web ("como lo usas ahora, con en gran medida las mismas funciones que en el navegador"); se pliega en el Workspace |
| Superficie móvil (iOS/Android)              | Interfaz: Wrike mobile app (Interactive)                                                                                                                                                                         |
| Superficie terminal / CLI                   | Excluido: no se halla CLI ni TUI de origen en las fuentes oficiales                                                                                                                                              |
| Comandos de voz en móvil                    | Excluido: modalidad de entrada de la app móvil / Copilot, sin contrato propio distinto                                                                                                                           |
| Herramienta Account Backup                  | Excluido: utilidad acotada de exportación que se apoya en la API de export, no una interfaz general de interacción                                                                                               |
| SDKs / librerías cliente (PHP, etc.)        | Excluido: implementan la API REST, no son interfaces                                                                                                                                                             |

## Tabla de cobertura por canal

| Canal          | Evidencia |
| -------------- | --------- |
| Interactive    | Observed  |
| Agentic        | Observed  |
| Conversational | Observed  |
| Event          | Observed  |
| Programmatic   | Observed  |

## Veredicto multicanal

`Multichannel` (5 paradigmas distintos observados)

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
  "generated_at": "2026-09-24T18:45:00Z",
  "evidence_checked_at": "2026-09-24T18:45:00Z",
  "saas": { "name": "Wrike" },
  "interfaces": [
    {
      "name": "Wrike Workspace (web application, also delivered as a Windows/Mac desktop client)",
      "technology": "Web application / desktop client",
      "channel": "Interactive",
      "classification_rationale": "Actions are expressed by manipulating views, menus and forms of a persistent, navigable representation of workspace state. The desktop client presents the same affordance-manipulation contract and is folded in.",
      "provenance": [
        {
          "url": "https://www.wrike.com/apps/mobile-and-desktop/",
          "evidence": "Wrike's product surfaces (browser, desktop, mobile) for accessing the workspace."
        },
        {
          "url": "https://www.wrike.com/apps/mobile-and-desktop/desktop-app/",
          "evidence": "Desktop app offers largely the same functionality as the browser, confirming the same interaction contract."
        }
      ]
    },
    {
      "name": "Wrike mobile app (iOS/Android)",
      "technology": "Native mobile application",
      "channel": "Interactive",
      "classification_rationale": "Native touch-based client whose interaction contract genuinely differs from the web workspace; actions are expressed by manipulating on-screen affordances.",
      "provenance": [
        {
          "url": "https://www.wrike.com/apps/mobile-and-desktop/",
          "evidence": "First-party native Android and iOS apps."
        },
        {
          "url": "https://www.wrike.com/try-mobile/",
          "evidence": "Mobile clients for phones and tablets to review and update work."
        }
      ]
    },
    {
      "name": "Wrike REST API v4",
      "technology": "HTTP REST API (OAuth 2.0)",
      "channel": "Programmatic",
      "classification_rationale": "The consumer explicitly invokes provider-defined operations via RESTful GET/POST/PUT/DELETE requests under a fixed base with OAuth 2.0.",
      "provenance": [
        {
          "url": "https://developers.wrike.com/docs/overview",
          "evidence": "RESTful methods with OAuth 2.0 authorization; base https://www.wrike.com/api/v4."
        }
      ]
    },
    {
      "name": "Wrike DataHub Public API",
      "technology": "HTTP REST API (OAuth 2.0), separate base",
      "channel": "Programmatic",
      "classification_rationale": "Distinct API surface (own OpenAPI, different base and control structure with requestId idempotency and session page tokens) through which the consumer invokes operations on DataHub databases, fields and records.",
      "provenance": [
        {
          "url": "https://developers.wrike.com/docs/datahub-overview",
          "evidence": "Separate DataHub public API with its own entities and operation set."
        },
        {
          "url": "https://developers.wrike.com/reference/finddatabases",
          "evidence": "OpenAPI servers under www.wrike.com/app/wrike_v2_web with /public/api/v1 paths."
        }
      ]
    },
    {
      "name": "Email-to-Wrike (inbound task creation/editing)",
      "technology": "Email (SMTP) submission to a Wrike address",
      "channel": "Programmatic",
      "classification_rationale": "The consumer invokes the create/edit-task operation by submitting a structured email (subject-line syntax for title, location, dates, status). Structured command via SMTP, not natural-language interpretation, so Programmatic rather than Conversational.",
      "provenance": [
        {
          "url": "https://help.wrike.com/hc/en-us/articles/1500005218562-Creating-a-Task-via-Email-Integration",
          "evidence": "Create tasks by emailing a Wrike address with bracketed subject-line parameters."
        },
        {
          "url": "https://www.wrike.com/apps/email-integration/email-app/",
          "evidence": "Send email to Wrike address to create/assign tasks; attachments become task files."
        }
      ]
    },
    {
      "name": "Wrike Webhooks",
      "technology": "Outbound HTTP event notifications",
      "channel": "Event",
      "classification_rationale": "The service initiates the interaction when subscribed events occur and delivers a payload to a consumer-controlled hookUrl, rather than the consumer polling.",
      "provenance": [
        {
          "url": "https://developers.wrike.com/docs/webhooks",
          "evidence": "Folder/space/account webhooks push payloads to the client endpoint on specific changes."
        }
      ]
    },
    {
      "name": "Wrike MCP Server",
      "technology": "MCP server (Streamable HTTP; OAuth or Permanent Access Token)",
      "channel": "Agentic",
      "classification_rationale": "A first-party MCP endpoint exposes a fixed, discoverable tool set that AI clients enumerate and select by goal as part of the interaction contract. Capability discovery and selection are part of the contract, so Agentic rather than Programmatic.",
      "provenance": [
        {
          "url": "https://developers.wrike.com/docs/wrike-mcp-server-overview",
          "evidence": "Wrike MCP server at https://mcp.wrike.com/v2 exposing a fixed tool set clients discover and cache."
        }
      ]
    },
    {
      "name": "Wrike Copilot",
      "technology": "In-product AI assistant",
      "channel": "Conversational",
      "classification_rationale": "The consumer interacts through natural-language questions interpreted by the service, with tool orchestration internal to Wrike. Message is the primitive, so Conversational rather than Agentic.",
      "provenance": [
        {
          "url": "https://www.wrike.com/ai/",
          "evidence": "Wrike Copilot is an AI assistant built into projects that answers questions and summarizes work on demand."
        },
        {
          "url": "https://www.wrike.com/newsroom/wrike-copilot-turning-ai-hype-into-everyday-productivity/",
          "evidence": "Copilot uses natural language to get answers and insights; the user simply asks."
        }
      ]
    }
  ],
  "access_mechanism_ledger": [
    {
      "mechanism": "REST API v4",
      "disposition": "interface",
      "detail": "Wrike REST API v4"
    },
    {
      "mechanism": "DataHub Public API",
      "disposition": "interface",
      "detail": "Wrike DataHub Public API"
    },
    {
      "mechanism": "BI Export API",
      "disposition": "excluded",
      "detail": "Accessed via the REST API v4 /data-export method (same base and auth); not a separate interface."
    },
    {
      "mechanism": "Webhooks",
      "disposition": "interface",
      "detail": "Wrike Webhooks"
    },
    {
      "mechanism": "MCP Server",
      "disposition": "interface",
      "detail": "Wrike MCP Server"
    },
    {
      "mechanism": "Inbound email (wrike@wrike.com)",
      "disposition": "interface",
      "detail": "Email-to-Wrike (inbound task creation/editing)"
    },
    {
      "mechanism": "Gmail/Outlook add-ins",
      "disposition": "excluded",
      "detail": "First-party integrations built on the API and web UI, not a distinct provider interface."
    },
    {
      "mechanism": "Cloud Content Connector",
      "disposition": "excluded",
      "detail": "Specification implemented by external DAM vendors so Wrike can call them; reverse direction, not a way to access Wrike."
    },
    {
      "mechanism": "Wrike Copilot (in-product AI assistant)",
      "disposition": "interface",
      "detail": "Wrike Copilot"
    },
    {
      "mechanism": "AI Agents / Conversational AI Agent Builder",
      "disposition": "excluded",
      "detail": "In-product automation and a builder inside the Workspace, not a distinct access interface."
    },
    {
      "mechanism": "Web client surface",
      "disposition": "interface",
      "detail": "Wrike Workspace"
    },
    {
      "mechanism": "Desktop client surface (Windows/Mac)",
      "disposition": "excluded",
      "detail": "Same affordance-manipulation contract as the web Workspace; folded into it."
    },
    {
      "mechanism": "Mobile client surface (iOS/Android)",
      "disposition": "interface",
      "detail": "Wrike mobile app"
    },
    {
      "mechanism": "Terminal/CLI surface",
      "disposition": "excluded",
      "detail": "No first-party CLI or TUI found in official sources."
    },
    {
      "mechanism": "Mobile voice commands",
      "disposition": "excluded",
      "detail": "Input modality of the mobile app / Copilot, not a distinct interaction contract."
    },
    {
      "mechanism": "Account Backup tool",
      "disposition": "excluded",
      "detail": "Narrow data-export utility riding on the export API, not a general interaction interface."
    },
    {
      "mechanism": "SDKs / client libraries",
      "disposition": "excluded",
      "detail": "Implement the REST API; not interfaces."
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
