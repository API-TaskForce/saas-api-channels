## Resumen del SaaS

GitHub (Microsoft). Se identifican **11 interfaces lógicas** proveedor-definidas. Cada una queda clasificada en un único canal, cubriendo **5 canales distintos** con al menos una interfaz clasificada.

## Tabla de clasificación de interfaces

| Interfaz                                   | Canal          | Tecnología de interacción              | Procedencia                                                                                                                                                                                                                                                                                                                                                              |
| ------------------------------------------ | -------------- | -------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Aplicación web (github.com)                | Interactive    | Interfaz web navegable                 | Representación persistente y navegable del estado del servicio (repos, issues, pull requests, vista de código); las acciones se expresan manipulando vistas, menús y formularios. Documentada de forma transversal en docs.github.com (creación y gestión de repos, issues y PR desde el navegador). Vigente.                                                            |
| GitHub Mobile (iOS/Android)                | Interactive    | App nativa móvil de primera parte      | docs.github.com/en/get-started/using-github/github-mobile la describe como "trusted, first-party client application" para hacer triage, revisar y fusionar mediante affordances de UI. Superficie de cliente distinta (base propia). Vigente.                                                                                                                            |
| GitHub Desktop                             | Interactive    | App GUI de escritorio de primera parte | docs.github.com/en/desktop: permite interactuar con GitHub mediante una GUI en lugar de la línea de comandos o el navegador; operaciones Git con confirmación visual. Superficie de cliente distinta. Vigente.                                                                                                                                                           |
| REST API                                   | Programmatic   | API HTTP (verbos REST)                 | docs.github.com/en/rest: el consumidor invoca operaciones definidas por el proveedor mediante peticiones HTTP estructuradas. Vigente.                                                                                                                                                                                                                                    |
| GraphQL API                                | Programmatic   | API GraphQL (queries/mutations)        | docs.github.com/en/graphql: endpoint y esquema propios, distintos de REST (primitiva y base diferentes), por lo que cuenta como interfaz separada. Vigente.                                                                                                                                                                                                              |
| GitHub CLI (`gh`)                          | Programmatic   | Herramienta de línea de comandos       | cli.github.com y docs.github.com: invocación de operaciones de GitHub por comandos estructurados. Sus prompts interactivos recogen parámetros de la operación invocada, no constituyen un TUI navegable. Vigente.                                                                                                                                                        |
| Operaciones remotas Git (HTTPS/SSH)        | Programmatic   | Protocolo remoto Git                   | docs.github.com/en/get-started/git-basics/about-remote-repositories: clone, fetch, pull y push contra repos alojados; HTTPS y SSH son transportes del mismo conjunto de operaciones, por lo que forman una sola interfaz. Vigente.                                                                                                                                       |
| Correo entrante (respuesta a notificación) | Programmatic   | Envío por email a dirección con token  | docs.github.com/en/subscriptions-and-notifications/get-started/configuring-notifications: al responder al email se publica el cuerpo como comentario en el hilo identificado por la dirección reply-to. El texto se toma literal (se elimina lo citado), no se interpreta como lenguaje natural, de ahí que sea invocación de operación. Vigente.                        |
| Webhooks                                   | Event          | Entrega HTTP POST sobre eventos        | docs.github.com/en/webhooks/about-webhooks: el servicio inicia la interacción al ocurrir eventos suscritos y entrega la carga a una URL controlada por el consumidor. Vigente.                                                                                                                                                                                           |
| GitHub Copilot Chat                        | Conversational | Asistente de IA por mensajes           | docs.github.com/en/copilot/concepts/chat: la primitiva es el mensaje en lenguaje natural. La orquestación interna de herramientas (MCP integrado) no forma parte del contrato con el consumidor, por lo que es Conversational y no Agentic. Vigente.                                                                                                                     |
| Servidor GitHub MCP                        | Agentic        | Servidor Model Context Protocol        | github/github-mcp-server y docs.github.com/en/copilot/concepts/context/mcp: servidor de primera parte (endpoint remoto https://api.githubcopilot.com/mcp/) que expone toolsets descritos semánticamente, descubribles y seleccionables como parte del contrato por cualquier cliente MCP. El descubrimiento y la selección de capacidades definen el paradigma. Vigente. |

## Registro de cobertura

| Mecanismo de acceso                                        | Disposición                                                                                                                                                                      |
| ---------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Aplicación web (superficie web de primera parte)           | Interfaz: Aplicación web (Interactive)                                                                                                                                           |
| App móvil (superficie móvil de primera parte)              | Interfaz: GitHub Mobile (Interactive)                                                                                                                                            |
| App de escritorio (superficie escritorio de primera parte) | Interfaz: GitHub Desktop (Interactive)                                                                                                                                           |
| Superficie de terminal de primera parte (TUI de `gh`)      | Excluido: `gh` no expone un TUI navegable persistente; sus prompts son recogida de parámetros de la operación invocada                                                           |
| REST API                                                   | Interfaz: REST API (Programmatic)                                                                                                                                                |
| GraphQL API                                                | Interfaz: GraphQL API (Programmatic)                                                                                                                                             |
| GitHub CLI (`gh`)                                          | Interfaz: GitHub CLI (Programmatic)                                                                                                                                              |
| Operaciones remotas Git (HTTPS/SSH)                        | Interfaz: Operaciones remotas Git (Programmatic)                                                                                                                                 |
| Correo entrante (responder para comentar)                  | Interfaz: Correo entrante (Programmatic)                                                                                                                                         |
| Notificaciones por email (salientes)                       | Excluido como interfaz distinta: es la función de notificaciones renderizada a un buzón; la interfaz de entrega de eventos con receptor controlado por el consumidor es Webhooks |
| Webhooks                                                   | Interfaz: Webhooks (Event)                                                                                                                                                       |
| GitHub Copilot Chat (web, móvil, IDE, CLI)                 | Interfaz: GitHub Copilot Chat (Conversational); las distintas superficies comparten la misma primitiva de mensaje en lenguaje natural                                            |
| Copilot coding agent (asignar issue a Copilot)             | Excluido: capacidad de agente invocada a través de interfaces existentes (UI web, Copilot Chat, herramienta MCP), no un contrato de interacción propio                           |
| Servidor GitHub MCP                                        | Interfaz: Servidor GitHub MCP (Agentic)                                                                                                                                          |
| SDKs Octokit / librerías cliente                           | Excluido: envoltorios sobre REST/GraphQL, no son interfaces                                                                                                                      |
| GitHub Apps / OAuth apps                                   | Excluido: marco de autenticación e integración; consume REST/GraphQL/webhooks, no es un mecanismo de acceso en sí                                                                |
| Integraciones de terceros / Marketplace                    | Excluido: no son interfaces definidas por el proveedor                                                                                                                           |
| GitHub Actions                                             | Excluido: producto de CI/CD; se consume vía web/API/git, no es una interfaz de acceso distinta                                                                                   |
| GitHub Codespaces                                          | Excluido: entorno de desarrollo alojado; el acceso a GitHub desde él se hace por git/API/web                                                                                     |
| GitHub Pages                                               | Excluido: producto de alojamiento estático, no un mecanismo de acceso al servicio                                                                                                |

## Cobertura de canales

| Canal          | Evidencia |
| -------------- | --------- |
| Interactive    | Observed  |
| Agentic        | Observed  |
| Conversational | Observed  |
| Event          | Observed  |
| Programmatic   | Observed  |

## Veredicto multicanal

`Multichannel` (5 paradigmas distintos observados).

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
  "saas": { "name": "GitHub" },
  "interfaces": [
    {
      "name": "Web application (github.com)",
      "technology": "Navigable web interface",
      "channel": "Interactive",
      "classification_rationale": "Actions are expressed by manipulating views, menus and forms over a persistent, navigable representation of repository, issue and pull request state.",
      "provenance": [
        {
          "url": "https://docs.github.com/en/repositories",
          "evidence": "The web interface is documented throughout for creating and managing repositories, issues, pull requests and browsing code."
        }
      ]
    },
    {
      "name": "GitHub Mobile",
      "technology": "First-party native mobile app (iOS/Android)",
      "channel": "Interactive",
      "classification_rationale": "First-party client where users triage, review and merge by manipulating UI affordances; distinct client surface from web and desktop.",
      "provenance": [
        {
          "url": "https://docs.github.com/en/get-started/using-github/github-mobile",
          "evidence": "Described as a trusted, first-party client application for triaging, collaborating and managing work on GitHub."
        }
      ]
    },
    {
      "name": "GitHub Desktop",
      "technology": "First-party GUI desktop app",
      "channel": "Interactive",
      "classification_rationale": "Provider-shipped graphical client to perform Git and GitHub operations through a GUI rather than the command line, with visual confirmation of changes.",
      "provenance": [
        {
          "url": "https://docs.github.com/en/desktop",
          "evidence": "Lets you interact with GitHub using a GUI instead of the command line or a web browser."
        }
      ]
    },
    {
      "name": "REST API",
      "technology": "HTTP REST API",
      "channel": "Programmatic",
      "classification_rationale": "The consumer explicitly invokes provider-defined endpoints via structured HTTP requests.",
      "provenance": [
        {
          "url": "https://docs.github.com/en/rest",
          "evidence": "GitHub provides a REST API using standard HTTP verbs to extend and customize the GitHub experience."
        }
      ]
    },
    {
      "name": "GraphQL API",
      "technology": "GraphQL API",
      "channel": "Programmatic",
      "classification_rationale": "The consumer invokes queries and mutations against a typed schema through a separate endpoint from REST, so a distinct Programmatic interface.",
      "provenance": [
        {
          "url": "https://docs.github.com/en/graphql",
          "evidence": "Separate GraphQL endpoint and schema; all calls validated and executed against the schema."
        }
      ]
    },
    {
      "name": "GitHub CLI (gh)",
      "technology": "Command-line tool",
      "channel": "Programmatic",
      "classification_rationale": "Operation invocation through structured commands from the terminal; interactive prompts collect parameters for the invoked command and are not a persistent navigable TUI.",
      "provenance": [
        {
          "url": "https://cli.github.com/manual/",
          "evidence": "Official command line tool bringing pull requests, issues and other GitHub concepts to the terminal via commands."
        }
      ]
    },
    {
      "name": "Git remote operations (HTTPS/SSH)",
      "technology": "Git remote protocol",
      "channel": "Programmatic",
      "classification_rationale": "Structured Git operations (clone, fetch, pull, push) against hosted repositories; HTTPS and SSH are transports of one operation set, hence a single interface.",
      "provenance": [
        {
          "url": "https://docs.github.com/en/get-started/git-basics/about-remote-repositories",
          "evidence": "Push and pull to GitHub-hosted repositories via HTTPS and SSH remote URLs."
        }
      ]
    },
    {
      "name": "Inbound email (reply-to-comment)",
      "technology": "Email submission to a tokenized reply-to address",
      "channel": "Programmatic",
      "classification_rationale": "Replying to a notification email posts the body as a comment on the thread identified by the reply-to token; the body is taken verbatim (quoted text stripped), not interpreted as natural language, so it is operation invocation.",
      "provenance": [
        {
          "url": "https://docs.github.com/en/subscriptions-and-notifications/get-started/configuring-notifications",
          "evidence": "You can reply to email notifications and your reply is posted to the issue, pull request or discussion; the reply-to address identifies the thread and the account."
        }
      ]
    },
    {
      "name": "Webhooks",
      "technology": "HTTP POST event delivery",
      "channel": "Event",
      "classification_rationale": "The service initiates an HTTP POST to a consumer-configured URL when subscribed events occur, delivering to a consumer-controlled receiver.",
      "provenance": [
        {
          "url": "https://docs.github.com/en/webhooks/about-webhooks",
          "evidence": "On a subscribed event, GitHub sends an HTTP request with event data to the URL the consumer specified."
        }
      ]
    },
    {
      "name": "GitHub Copilot Chat",
      "technology": "AI chat assistant",
      "channel": "Conversational",
      "classification_rationale": "The consumer-facing primitive is the natural-language message; internal tool orchestration (built-in MCP) is not part of the consumer contract, so Conversational rather than Agentic.",
      "provenance": [
        {
          "url": "https://docs.github.com/en/copilot/concepts/chat",
          "evidence": "AI-powered chat interface for interacting with models in a conversational format; the GitHub MCP server is configured internally to perform a limited set of tasks on request."
        }
      ]
    },
    {
      "name": "GitHub MCP server",
      "technology": "Model Context Protocol server",
      "channel": "Agentic",
      "classification_rationale": "First-party server exposing semantically described toolsets that are discoverable and selectable as part of the interaction contract by any MCP client; capability discovery and selection define the paradigm.",
      "provenance": [
        {
          "url": "https://github.com/github/github-mcp-server",
          "evidence": "GitHub's official MCP server with a hosted remote endpoint (https://api.githubcopilot.com/mcp/) exposing selectable toolsets to AI clients."
        },
        {
          "url": "https://docs.github.com/en/copilot/concepts/context/mcp",
          "evidence": "The GitHub MCP server can run in any MCP-compatible editor and exposes toolsets controlling which GitHub capabilities are available to AI tools."
        }
      ]
    }
  ],
  "access_mechanism_ledger": [
    {
      "mechanism": "Web application (first-party web surface)",
      "disposition": "interface",
      "detail": "Web application (Interactive)"
    },
    {
      "mechanism": "Mobile app (first-party mobile surface)",
      "disposition": "interface",
      "detail": "GitHub Mobile (Interactive)"
    },
    {
      "mechanism": "Desktop app (first-party desktop surface)",
      "disposition": "interface",
      "detail": "GitHub Desktop (Interactive)"
    },
    {
      "mechanism": "First-party terminal surface (gh TUI)",
      "disposition": "excluded",
      "detail": "gh ships no persistent navigable TUI; its prompts are parameter collection for the invoked command"
    },
    {
      "mechanism": "REST API",
      "disposition": "interface",
      "detail": "REST API (Programmatic)"
    },
    {
      "mechanism": "GraphQL API",
      "disposition": "interface",
      "detail": "GraphQL API (Programmatic)"
    },
    {
      "mechanism": "GitHub CLI (gh)",
      "disposition": "interface",
      "detail": "GitHub CLI (Programmatic)"
    },
    {
      "mechanism": "Git remote operations (HTTPS/SSH)",
      "disposition": "interface",
      "detail": "Git remote operations (Programmatic)"
    },
    {
      "mechanism": "Inbound email (reply-to-comment)",
      "disposition": "interface",
      "detail": "Inbound email (Programmatic)"
    },
    {
      "mechanism": "Email notifications (outbound)",
      "disposition": "excluded",
      "detail": "Notifications feature delivered to a mailbox; the provider's event-delivery interface with a consumer-controlled receiver is Webhooks"
    },
    {
      "mechanism": "Webhooks",
      "disposition": "interface",
      "detail": "Webhooks (Event)"
    },
    {
      "mechanism": "GitHub Copilot Chat (web, mobile, IDE, CLI)",
      "disposition": "interface",
      "detail": "GitHub Copilot Chat (Conversational); surfaces share the natural-language message contract"
    },
    {
      "mechanism": "Copilot coding agent (assign issue to Copilot)",
      "disposition": "excluded",
      "detail": "Agent capability invoked through existing interfaces (web UI, Copilot Chat, MCP tool), not a separate interaction contract"
    },
    {
      "mechanism": "GitHub MCP server",
      "disposition": "interface",
      "detail": "GitHub MCP server (Agentic)"
    },
    {
      "mechanism": "Octokit SDKs / client libraries",
      "disposition": "excluded",
      "detail": "Wrappers over REST/GraphQL, not interfaces"
    },
    {
      "mechanism": "GitHub Apps / OAuth apps",
      "disposition": "excluded",
      "detail": "Authentication and integration framework consuming REST/GraphQL/webhooks, not an access interface itself"
    },
    {
      "mechanism": "Third-party integrations / Marketplace",
      "disposition": "excluded",
      "detail": "Not provider-defined interfaces"
    },
    {
      "mechanism": "GitHub Actions",
      "disposition": "excluded",
      "detail": "CI/CD product consumed via web/API/git, not a distinct provider access interface"
    },
    {
      "mechanism": "GitHub Codespaces",
      "disposition": "excluded",
      "detail": "Hosted dev environment; access to GitHub from it is via git/API/web"
    },
    {
      "mechanism": "GitHub Pages",
      "disposition": "excluded",
      "detail": "Static hosting product, not an access mechanism to the service"
    }
  ],
  "channel_evidence": {
    "Interactive": "observed",
    "Agentic": "observed",
    "Conversational": "observed",
    "Event": "observed",
    "Programmatic": "observed"
  },
  "number_of_interfaces": 11,
  "multi_interface": true,
  "number_of_channels": 5,
  "multi_channel": true
}
```
