# Clasificación de interfaces

| Interfaz                       | Canal              | Tecnología de interacción                                              | Procedencia y razonamiento                                                                                                                                                                                                                                                                                                                               |
| ------------------------------ | ------------------ | ---------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Aplicación web de Box          | **Interactive**    | Cliente web propietario (app.box.com)                                  | developer.box.com y support.box.com describen una app web donde el usuario opera sobre archivos y carpetas mediante vistas, menús y formularios. Primitiva: manipulación de affordances de una representación navegable del estado del servicio. Vigente.                                                                                                |
| Aplicación móvil de Box        | **Interactive**    | Apps iOS/Android propietarias                                          | box.com/resources/downloads y la ficha oficial de la App Store confirman clientes móviles de primera parte. Mismo paradigma que la web sobre superficie móvil. Contada como interfaz aparte según la regla de superficies de cliente. Vigente.                                                                                                           |
| Box Drive                      | **Interactive**    | Cliente de escritorio (Windows/macOS) que monta Box en Finder/Explorer | box.com/resources/downloads y docs.box.com/en/box-drive: presenta el contenido como volumen navegable del sistema de archivos, donde el usuario manipula elementos como affordances. Vigente (sustituye a Box Sync, retirado).                                                                                                                           |
| API REST de Box                | **Programmatic**   | REST sobre HTTPS, base api.box.com/2.0, OAuth 2.0                      | developer.box.com/reference. Primitiva: invocación explícita de operaciones definidas por el proveedor. La Box AI API (POST /2.0/ai/ask) y la Sign API comparten base, autenticación y estilo de invocación, por lo que pertenecen a esta misma interfaz. Vigente.                                                                                       |
| Box CLI                        | **Programmatic**   | Interfaz de comandos de terminal (@box/cli)                            | developer.box.com/guides/cli. Primitiva: comandos explícitos como `box folders:get 0`. No expone un TUI navegable persistente, así que es una sola interfaz de comandos. Vigente.                                                                                                                                                                        |
| FTPS                           | **Programmatic**   | Servicio FTPS/FTPES en ftp.box.com                                     | support.box.com «Using Box with FTPS». Primitiva: operaciones de transferencia mediante el conjunto de comandos FTP sobre TLS. Base, protocolo y autenticación distintos de la API REST. Vigente.                                                                                                                                                        |
| Box SFTP                       | **Programmatic**   | Servicio SFTP en sftp.services.box.com (puerto 22)                     | support.box.com «Introducing Box SFTP» (GA sept. 2025). Primitiva: operaciones de archivo sobre SSH. Protocolo, endpoint y autenticación distintos tanto de FTPS como de REST, de ahí que sea una interfaz separada. Vigente; supera a comunicados antiguos que declaraban SFTP no soportado.                                                            |
| Webhooks (V1/V2)               | **Event**          | Notificaciones HTTP salientes a una URL del consumidor                 | developer.box.com/guides/webhooks. Estructura de control: el servicio inicia la interacción cuando ocurren eventos sobre archivos o carpetas y entrega la carga a un receptor controlado por el consumidor. Vigente.                                                                                                                                     |
| Box AI (asistente en producto) | **Conversational** | Panel de chat en la web y el móvil (Box AI / Box Agent / AI Home)      | support.box.com «What is Box AI» y «Box AI for Documents»: caja «Message Box AI», preguntas y repreguntas en lenguaje natural, historial de conversación. Primitiva: el mensaje interpretado por el servicio, con orquestación de herramientas interna y no expuesta como contrato de descubrimiento. Caso límite resuelto como Conversational. Vigente. |
| Servidor MCP remoto de Box     | **Agentic**        | Endpoint MCP alojado por Box (mcp.box.com)                             | developer.box.com/guides/box-mcp/remote y comunicado de GA (ago. 2025). El contrato ofrece capacidades descritas semánticamente, descubribles y seleccionables por el agente consumidor. Caso límite MCP: el descubrimiento estructura el contrato, luego Agentic y no Programmatic. Vigente.                                                            |

# Registro de cobertura

| Mecanismo de acceso                                                                              | Disposición                                                                                                                                              |
| ------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| API / API reference                                                                              | Interfaz: API REST de Box (Programmatic)                                                                                                                 |
| Box AI API                                                                                       | Excluido: misma base, autenticación y estilo de invocación que la API REST; forma parte de ella, no es una interfaz aparte                               |
| Box Sign API                                                                                     | Excluido: parte de la API REST                                                                                                                           |
| Box CLI                                                                                          | Interfaz: Box CLI (Programmatic)                                                                                                                         |
| TUI del CLI (chequeo de superficie de terminal)                                                  | Excluido: el CLI es solo de comandos; no presenta un TUI navegable persistente                                                                           |
| Webhooks (V1/V2)                                                                                 | Interfaz: Webhooks (Event)                                                                                                                               |
| Servidor MCP remoto (mcp.box.com)                                                                | Interfaz: Servidor MCP remoto de Box (Agentic)                                                                                                           |
| Servidor MCP autoalojado (box-community)                                                         | Excluido: proyecto open source de comunidad, desplegado por el consumidor; no es un endpoint operado por el proveedor; mismo paradigma que el MCP remoto |
| Box AI (asistente en producto)                                                                   | Interfaz: Box AI (Conversational)                                                                                                                        |
| FTPS / FTPES (ftp.box.com)                                                                       | Interfaz: FTPS (Programmatic)                                                                                                                            |
| Box SFTP (sftp.services.box.com)                                                                 | Interfaz: Box SFTP (Programmatic)                                                                                                                        |
| Cliente web (superficie de primera parte)                                                        | Interfaz: Aplicación web de Box (Interactive)                                                                                                            |
| Cliente móvil (iOS/Android)                                                                      | Interfaz: Aplicación móvil de Box (Interactive)                                                                                                          |
| Cliente de escritorio (Box Drive)                                                                | Interfaz: Box Drive (Interactive)                                                                                                                        |
| SDKs (Python, Java, Node, .NET, Swift/iOS, etc.)                                                 | Excluido: bibliotecas cliente, no interfaces                                                                                                             |
| UI Elements (box-ui-elements)                                                                    | Excluido: biblioteca de componentes front-end para construir UIs, no una interfaz del proveedor                                                          |
| Colección de Postman                                                                             | Excluido: forma de invocar la API REST, no una interfaz aparte                                                                                           |
| Box Notes, Box Sign, Box Hubs, Doc Gen, AI Studio                                                | Excluido: funcionalidades o productos dentro de la app web o la API REST, no mecanismos de acceso distintos                                              |
| Integraciones de terceros (Salesforce, Teams, Slack, complementos de Office, Snowflake, Airbyte) | Excluido: integraciones de terceros                                                                                                                      |

# Cobertura por canal

| Canal          | Evidencia |
| -------------- | --------- |
| Interactive    | Observed  |
| Agentic        | Observed  |
| Conversational | Observed  |
| Event          | Observed  |
| Programmatic   | Observed  |

# Notas de clasificación

Box SFTP alcanzó disponibilidad general en septiembre de 2025 con endpoint y autenticación propios, de modo que las publicaciones anteriores de la comunidad que lo daban por no soportado quedan superadas por la evidencia actual. FTPS y SFTP se cuentan como dos interfaces porque difieren en protocolo, endpoint y autenticación, aunque ambas caen en el mismo canal. El servidor MCP remoto (operado por Box) es la interfaz Agentic; su variante autoalojada de comunidad se excluye por no ser un endpoint del proveedor.

# Veredicto multicanal

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
  "generated_at": "2026-09-24T12:00:00Z",
  "evidence_checked_at": "2026-09-24T12:00:00Z",
  "saas": { "name": "Box" },
  "interfaces": [
    {
      "name": "Box web application",
      "technology": "First-party web client (app.box.com)",
      "channel": "Interactive",
      "classification_rationale": "Actions are expressed by manipulating views, menus and forms of a persistent, navigable representation of Box content.",
      "provenance": [
        {
          "url": "https://support.box.com/hc/en-us/articles/44814498431379-What-is-Box-AI",
          "evidence": "References the Box Web App as the surface where users work with content."
        }
      ]
    },
    {
      "name": "Box mobile app",
      "technology": "First-party iOS/Android clients",
      "channel": "Interactive",
      "classification_rationale": "A first-party mobile client whose actions are affordance manipulation on a mobile UI; counted separately from the web client per the surface checklist.",
      "provenance": [
        {
          "url": "https://www.box.com/resources/downloads",
          "evidence": "Box lists first-party desktop and mobile app downloads."
        },
        {
          "url": "https://apps.apple.com/us/app/box-the-power-of-content-ai/id290853822",
          "evidence": "Box's own App Store listing for the mobile client."
        }
      ]
    },
    {
      "name": "Box Drive desktop client",
      "technology": "Windows/macOS desktop app mounting Box in Finder/Explorer",
      "channel": "Interactive",
      "classification_rationale": "Content is presented as a navigable file-system volume whose items the user manipulates as affordances of the OS explorer.",
      "provenance": [
        {
          "url": "https://docs.box.com/en/box-drive/getting-started-with-box-drive/using-box-drive-basics",
          "evidence": "Box Drive streams Box content into Finder/File Explorer for direct manipulation."
        },
        {
          "url": "https://www.box.com/resources/downloads",
          "evidence": "Official Box Drive desktop downloads for Mac and Windows."
        }
      ]
    },
    {
      "name": "Box REST API",
      "technology": "REST over HTTPS, base api.box.com/2.0, OAuth 2.0",
      "channel": "Programmatic",
      "classification_rationale": "The consumer explicitly invokes provider-defined operations via structured HTTPS requests; Box AI and Sign APIs share the same base, auth and invocation style and fold in here.",
      "provenance": [
        {
          "url": "https://developer.box.com/reference",
          "evidence": "API reference covering every Box resource under api.box.com/2.0 with OAuth 2.0."
        }
      ]
    },
    {
      "name": "Box CLI command interface",
      "technology": "Terminal command-line tool (@box/cli)",
      "channel": "Programmatic",
      "classification_rationale": "Actions are expressed as explicit commands (e.g. box folders:get 0); no persistent navigable TUI is exposed, so it is a single command interface.",
      "provenance": [
        {
          "url": "https://developer.box.com/guides/cli",
          "evidence": "Box CLI for managing Box content from the terminal via commands."
        }
      ]
    },
    {
      "name": "Box FTPS service",
      "technology": "FTPS/FTPES service at ftp.box.com over TLS",
      "channel": "Programmatic",
      "classification_rationale": "The consumer invokes file-transfer operations through the FTP command set over TLS; distinct base and auth from the REST API.",
      "provenance": [
        {
          "url": "https://support.box.com/hc/en-us/articles/360043697414-Using-Box-with-FTPS",
          "evidence": "Box supports FTPS/FTPES for bulk upload/download via ftp.box.com."
        }
      ]
    },
    {
      "name": "Box SFTP service",
      "technology": "SFTP service at sftp.services.box.com, port 22",
      "channel": "Programmatic",
      "classification_rationale": "The consumer invokes file operations over the SSH File Transfer Protocol; protocol, endpoint and auth differ from FTPS and from REST, so it is a separate interface.",
      "provenance": [
        {
          "url": "https://support.box.com/hc/en-us/articles/44855616735891-Introducing-Box-SFTP-Sept-2025",
          "evidence": "RFC-compliant SFTP service via sftp.services.box.com:22; GA Sept 2025 (current), superseding older 'not supported' posts."
        }
      ]
    },
    {
      "name": "Box Webhooks (V1/V2)",
      "technology": "Outbound HTTPS event notifications",
      "channel": "Event",
      "classification_rationale": "Box initiates the interaction on file/folder events and delivers the payload to a consumer-controlled receiver URL.",
      "provenance": [
        {
          "url": "https://developer.box.com/guides/webhooks/",
          "evidence": "Webhooks monitor Box content for events and notify a URL of the consumer's choice."
        }
      ]
    },
    {
      "name": "Box AI in-product assistant",
      "technology": "Natural-language chat panel in web/mobile (Box AI, Box Agent, AI Home)",
      "channel": "Conversational",
      "classification_rationale": "The consumer interacts through natural-language messages interpreted by the service, with tool orchestration internal and not exposed as a discovery contract.",
      "provenance": [
        {
          "url": "https://support.box.com/hc/en-us/articles/22158484213267-Box-AI-for-Documents",
          "evidence": "Message box, Ask, follow-up questions and conversation history in the Box AI panel."
        }
      ]
    },
    {
      "name": "Box remote MCP server",
      "technology": "Provider-hosted MCP endpoint (mcp.box.com)",
      "channel": "Agentic",
      "classification_rationale": "The interaction contract exposes semantically described tools that agent consumers discover and select; discovery/selection structure the contract, so Agentic rather than Programmatic.",
      "provenance": [
        {
          "url": "https://developer.box.com/guides/box-mcp/remote/",
          "evidence": "Box-hosted remote MCP server at mcp.box.com exposing content and AI tools to agents (GA Aug 2025)."
        }
      ]
    }
  ],
  "access_mechanism_ledger": [
    {
      "mechanism": "API / API reference",
      "disposition": "interface",
      "detail": "Box REST API"
    },
    {
      "mechanism": "Box AI API",
      "disposition": "excluded",
      "detail": "Same base/auth/invocation as REST API; part of it, not a separate interface"
    },
    {
      "mechanism": "Box Sign API",
      "disposition": "excluded",
      "detail": "Part of the REST API"
    },
    {
      "mechanism": "Box CLI",
      "disposition": "interface",
      "detail": "Box CLI command interface"
    },
    {
      "mechanism": "CLI TUI (terminal surface check)",
      "disposition": "excluded",
      "detail": "No persistent navigable TUI; CLI is command-only"
    },
    {
      "mechanism": "Webhooks (V1/V2)",
      "disposition": "interface",
      "detail": "Box Webhooks (V1/V2)"
    },
    {
      "mechanism": "Remote MCP server (mcp.box.com)",
      "disposition": "interface",
      "detail": "Box remote MCP server"
    },
    {
      "mechanism": "Self-hosted MCP server (box-community)",
      "disposition": "excluded",
      "detail": "Open-source community project self-hosted by the consumer; not a provider-operated endpoint; same paradigm as the remote server"
    },
    {
      "mechanism": "Box AI in-product assistant",
      "disposition": "interface",
      "detail": "Box AI in-product assistant"
    },
    {
      "mechanism": "FTPS/FTPES (ftp.box.com)",
      "disposition": "interface",
      "detail": "Box FTPS service"
    },
    {
      "mechanism": "Box SFTP (sftp.services.box.com)",
      "disposition": "interface",
      "detail": "Box SFTP service"
    },
    {
      "mechanism": "Web client (first-party surface)",
      "disposition": "interface",
      "detail": "Box web application"
    },
    {
      "mechanism": "Mobile client (iOS/Android)",
      "disposition": "interface",
      "detail": "Box mobile app"
    },
    {
      "mechanism": "Desktop client (Box Drive)",
      "disposition": "interface",
      "detail": "Box Drive desktop client"
    },
    {
      "mechanism": "SDKs (Python, Java, Node, .NET, Swift/iOS, etc.)",
      "disposition": "excluded",
      "detail": "Client libraries, not interfaces"
    },
    {
      "mechanism": "UI Elements (box-ui-elements)",
      "disposition": "excluded",
      "detail": "Front-end component library for building UIs, not a provider interface"
    },
    {
      "mechanism": "Postman collection",
      "disposition": "excluded",
      "detail": "A way to call the REST API, not a separate interface"
    },
    {
      "mechanism": "Box Notes / Sign / Hubs / Doc Gen / AI Studio",
      "disposition": "excluded",
      "detail": "Features/products within the web app or REST API, not distinct access mechanisms"
    },
    {
      "mechanism": "Third-party integrations (Salesforce, Teams, Slack, Office add-ins, Snowflake, Airbyte)",
      "disposition": "excluded",
      "detail": "Third-party integrations"
    }
  ],
  "channel_evidence": {
    "Interactive": "observed",
    "Agentic": "observed",
    "Conversational": "observed",
    "Event": "observed",
    "Programmatic": "observed"
  },
  "number_of_interfaces": 10,
  "multi_interface": true,
  "number_of_channels": 5,
  "multi_channel": true
}
```
