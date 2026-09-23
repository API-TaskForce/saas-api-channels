# Resumen del SaaS

**Notion** (Notion Labs, Inc.). Interfaces lógicas identificadas: **6**. Canales distintos con al menos una interfaz clasificada: **5**.

Notion materializa varias interfaces lógicas sobre pocas tecnologías. Sus clientes de primera parte (web, escritorio y móvil) comparten el mismo contrato de manipulación de affordances y colapsan en una sola interfaz Interactive; su API REST y su CLI `ntn` son dos interfaces Programmatic separadas por estilo de invocación; el servidor MCP remoto, el asistente Notion AI y las suscripciones de webhooks aportan un canal cada uno.

# Tabla de clasificación de interfaces

| Interfaz                                                           | Canal          | Tecnología de interacción                                     | Procedencia                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| ------------------------------------------------------------------ | -------------- | ------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Clientes Notion (web, escritorio macOS/Windows, móvil iOS/Android) | Interactive    | Aplicación web y apps nativas de escritorio y móvil           | notion.com/desktop y notion.com/mobile documentan las apps de primera parte; el centro de ayuda "Notion for desktop" confirma cliente descargable (sin app Linux, solo navegador). Las acciones se expresan manipulando affordances (páginas, bloques, bases de datos, menús) sobre una representación persistente y navegable del estado del workspace: Affordance Manipulation. Evidencia actual.                                         |
| API REST de Notion                                                 | Programmatic   | API REST HTTP (base `api.notion.com`, token bearer)           | developers.notion.com/reference/intro establece endpoints GET/POST/PATCH/DELETE sobre páginas, bases de datos y usuarios con cuerpos JSON. El consumidor invoca operaciones definidas por el proveedor mediante peticiones estructuradas: Operation Invocation. Evidencia actual (versión 2026-03-11).                                                                                                                                      |
| CLI de Notion (`ntn`)                                              | Programmatic   | Interfaz de comandos de terminal (OAuth en keychain o PAT)    | developers.notion.com/cli documenta `ntn login`, `ntn api`, `ntn pages`, `ntn datasources`, `ntn files`, `ntn workers`. El primitivo es el comando de terminal y el control es invocación explícita de operaciones, distinto en estilo de invocación, base y autenticación respecto a la API REST, por lo que cuenta como interfaz aparte: Operation Invocation. Sin TUI navegable persistente. Evidencia actual (beta, lanzada mayo 2026). |
| Notion MCP (servidor remoto)                                       | Agentic        | Servidor MCP alojado en `mcp.notion.com/mcp`, OAuth           | developers.notion.com/guides/mcp/overview describe un servidor MCP remoto que expone herramientas descubribles con descripciones semánticas para clientes como Claude Code, Cursor o Codex. El descubrimiento y la selección de capacidades forman parte del contrato de interacción: Capability Discovery and Invocation, caso límite MCP resuelto como Agentic. Evidencia actual.                                                         |
| Notion AI / Notion Agent                                           | Conversational | Asistente de chat en lenguaje natural embebido en el producto | notion.com/product/ai y el centro de ayuda describen un asistente con el que se conversa en lenguaje natural para consultar y actuar sobre el workspace; la orquestación de herramientas es interna al servicio. El primitivo es el mensaje: Contextual Conversation, caso límite del asistente con herramientas internas resuelto como Conversational, no Agentic. Evidencia actual.                                                       |
| Webhooks de Notion                                                 | Event          | Suscripciones de webhook con entrega HTTP POST saliente       | developers.notion.com/reference/webhooks documenta suscripciones a eventos (por ejemplo `page.content_updated`); Notion inicia la interacción cuando ocurre el evento y entrega a un endpoint HTTPS controlado por el consumidor: Event Notification. Evidencia actual (webhooks v2).                                                                                                                                                       |

# Registro de cobertura

| Mecanismo de acceso                               | Disposición                                                                                                                                                                                                                            |
| ------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| App web                                           | Interfaz: Clientes Notion (Interactive)                                                                                                                                                                                                |
| App de escritorio (macOS/Windows)                 | Interfaz: Clientes Notion (Interactive); mismo contrato que web                                                                                                                                                                        |
| App móvil (iOS/Android)                           | Interfaz: Clientes Notion (Interactive); mismo contrato que web                                                                                                                                                                        |
| Terminal / CLI `ntn`                              | Interfaz: CLI de Notion (Programmatic). Comprobación de TUS/TUI: no expone panel navegable persistente, solo comandos                                                                                                                  |
| API REST                                          | Interfaz: API REST de Notion (Programmatic)                                                                                                                                                                                            |
| Notion MCP (remoto)                               | Interfaz: Notion MCP (Agentic)                                                                                                                                                                                                         |
| Notion MCP (open source autoalojado)              | Excluido: misma interfaz Agentic (variante autoalojada, en desuso y sin soporte activo según el repo `makenotion/notion-mcp-server`)                                                                                                   |
| Notion AI / Notion Agent                          | Interfaz: Notion AI (Conversational)                                                                                                                                                                                                   |
| Webhooks (suscripciones de integración)           | Interfaz: Webhooks (Event)                                                                                                                                                                                                             |
| Notion Workers (runtime alojado)                  | Excluido: entorno de ejecución para código personalizado, se opera a través del CLI ya contado; no es un canal de acceso propio. Su capacidad `worker.webhook` ingiere eventos externos hacia Notion, dirección inversa al canal Event |
| Agent SDK                                         | Excluido: SDK/biblioteca cliente, no es interfaz lógica                                                                                                                                                                                |
| SDKs (por ejemplo notion-sdk-js)                  | Excluido: SDK/biblioteca cliente                                                                                                                                                                                                       |
| Link previews                                     | Excluido: funcionalidad de renderizado de contenido externo, no un canal de acceso al servicio                                                                                                                                         |
| Galería de integraciones / conectores de terceros | Excluido: integraciones de terceros                                                                                                                                                                                                    |
| OAuth / PAT / tokens                              | Excluido: método de autenticación                                                                                                                                                                                                      |

# Cobertura por canal

| Canal          | Evidencia |
| -------------- | --------- |
| Interactive    | Observed  |
| Agentic        | Observed  |
| Conversational | Observed  |
| Event          | Observed  |
| Programmatic   | Observed  |

# Veredicto multicanal

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
  "generated_at": "2026-09-22T12:00:00Z",
  "evidence_checked_at": "2026-09-22T12:00:00Z",
  "saas": { "name": "Notion" },
  "interfaces": [
    {
      "name": "Notion client apps (web, desktop, mobile)",
      "technology": "Web application and native desktop (macOS/Windows) and mobile (iOS/Android) apps",
      "channel": "Interactive",
      "classification_rationale": "Actions are expressed by manipulating presented affordances (pages, blocks, databases, menus) of a persistent, navigable representation of workspace state (Affordance Manipulation). Web, desktop, and mobile share the same interaction contract and count as one interface.",
      "provenance": [
        {
          "url": "https://www.notion.com/desktop",
          "evidence": "Official first-party desktop app downloads for macOS and Windows."
        },
        {
          "url": "https://www.notion.com/mobile",
          "evidence": "Official first-party mobile app for iOS and Android."
        },
        {
          "url": "https://www.notion.com/help/notion-for-desktop",
          "evidence": "Confirms downloadable desktop client; no Linux app, browser only."
        }
      ]
    },
    {
      "name": "Notion REST API",
      "technology": "HTTP REST API (base api.notion.com, bearer token)",
      "channel": "Programmatic",
      "classification_rationale": "The consumer explicitly invokes provider-defined operations via structured HTTP requests with JSON bodies (Operation Invocation).",
      "provenance": [
        {
          "url": "https://developers.notion.com/reference/intro",
          "evidence": "RESTful GET/POST/PATCH/DELETE operations on page and database resources over api.notion.com with bearer auth."
        }
      ]
    },
    {
      "name": "Notion CLI (ntn)",
      "technology": "Command-based terminal CLI (OAuth keychain or PAT)",
      "channel": "Programmatic",
      "classification_rationale": "First-party command interface whose primitive is the terminal command and whose control structure is explicit operation invocation; differs from the REST API in invocation style, base, and auth, so it is a separate Programmatic interface. No persistent navigable TUI.",
      "provenance": [
        {
          "url": "https://developers.notion.com/cli/get-started/overview",
          "evidence": "Official ntn CLI for authentication, Workers, API requests, and data sources from the terminal."
        },
        {
          "url": "https://developers.notion.com/cli/get-started/authentication",
          "evidence": "ntn login/logout/doctor and PAT-based ntn api commands; credentials in OS keychain."
        }
      ]
    },
    {
      "name": "Notion MCP (remote server)",
      "technology": "Hosted remote MCP server at mcp.notion.com/mcp, OAuth",
      "channel": "Agentic",
      "classification_rationale": "Exposes semantically described tools that MCP clients discover and select as part of the interaction contract (Capability Discovery and Invocation); MCP boundary case resolved to Agentic.",
      "provenance": [
        {
          "url": "https://developers.notion.com/guides/mcp/overview",
          "evidence": "Remote MCP server hosted by Notion; MCP clients connect via OAuth and use discoverable tools to read and update content."
        },
        {
          "url": "https://developers.notion.com/guides/mcp/hosting-open-source-mcp",
          "evidence": "Recommends the remote MCP at mcp.notion.com/mcp; open-source self-hosted server is the deprecated variant."
        }
      ]
    },
    {
      "name": "Notion AI / Notion Agent",
      "technology": "In-product natural-language chat assistant",
      "channel": "Conversational",
      "classification_rationale": "The consumer expresses intent through natural-language messages interpreted by the service; tool orchestration is internal to Notion (Contextual Conversation). Natural-language-assistant boundary case resolved to Conversational, not Agentic.",
      "provenance": [
        {
          "url": "https://www.notion.com/product/ai",
          "evidence": "Notion Agent is chatted with to take on tasks using workspace context, creating and editing pages and databases."
        },
        {
          "url": "https://www.notion.com/help/guides/everything-you-can-do-with-notion-ai",
          "evidence": "Notion AI chat accepts natural-language prompts and file/image inputs to act within the workspace."
        }
      ]
    },
    {
      "name": "Notion Webhooks",
      "technology": "Integration webhook subscriptions (outbound HTTP POST)",
      "channel": "Event",
      "classification_rationale": "The service initiates delivery when subscribed events occur, sending HTTP POST to a consumer-controlled HTTPS endpoint (Event Notification).",
      "provenance": [
        {
          "url": "https://developers.notion.com/reference/webhooks",
          "evidence": "Connections subscribe to event types; Notion sends signed HTTP POST requests to the configured public endpoint on workspace changes."
        }
      ]
    }
  ],
  "access_mechanism_ledger": [
    {
      "mechanism": "Web app",
      "disposition": "interface",
      "detail": "Notion client apps (web, desktop, mobile)"
    },
    {
      "mechanism": "Desktop app (macOS/Windows)",
      "disposition": "interface",
      "detail": "Notion client apps (web, desktop, mobile)"
    },
    {
      "mechanism": "Mobile app (iOS/Android)",
      "disposition": "interface",
      "detail": "Notion client apps (web, desktop, mobile)"
    },
    {
      "mechanism": "Terminal / CLI (ntn)",
      "disposition": "interface",
      "detail": "Notion CLI (ntn); no persistent navigable TUI found"
    },
    {
      "mechanism": "REST API",
      "disposition": "interface",
      "detail": "Notion REST API"
    },
    {
      "mechanism": "MCP (remote)",
      "disposition": "interface",
      "detail": "Notion MCP (remote server)"
    },
    {
      "mechanism": "MCP (open-source self-hosted)",
      "disposition": "excluded",
      "detail": "Same Agentic interface as remote MCP; deprecated, unsupported self-hosted variant"
    },
    {
      "mechanism": "Notion AI / Notion Agent",
      "disposition": "interface",
      "detail": "Notion AI / Notion Agent"
    },
    {
      "mechanism": "Webhooks (integration subscriptions)",
      "disposition": "interface",
      "detail": "Notion Webhooks"
    },
    {
      "mechanism": "Notion Workers (hosted runtime)",
      "disposition": "excluded",
      "detail": "Execution/extension runtime operated via the already-counted CLI; not a distinct access channel; its worker.webhook ingests external events into Notion (inverse of the Event channel)"
    },
    {
      "mechanism": "Agent SDK",
      "disposition": "excluded",
      "detail": "SDK / client library, not a logical interface"
    },
    {
      "mechanism": "SDKs (e.g. notion-sdk-js)",
      "disposition": "excluded",
      "detail": "SDK / client library, not a logical interface"
    },
    {
      "mechanism": "Link previews",
      "disposition": "excluded",
      "detail": "External-content rendering feature, not an access channel to the service"
    },
    {
      "mechanism": "Integrations gallery / third-party connectors",
      "disposition": "excluded",
      "detail": "Third-party integrations"
    },
    {
      "mechanism": "OAuth / PAT / tokens",
      "disposition": "excluded",
      "detail": "Authentication method"
    }
  ],
  "channel_evidence": {
    "Interactive": "observed",
    "Agentic": "observed",
    "Conversational": "observed",
    "Event": "observed",
    "Programmatic": "observed"
  },
  "number_of_interfaces": 6,
  "multi_interface": true,
  "number_of_channels": 5,
  "multi_channel": true
}
```
