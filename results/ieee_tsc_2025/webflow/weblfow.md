# Tabla de clasificación de interfaces

| Interfaz         | Canal        | Tecnología de interacción                             | Procedencia                                                                                                                                                                                                                                                                                                                                                                                                                 |
| ---------------- | ------------ | ----------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Webflow Designer | Interactive  | Aplicación web (lienzo visual en navegador)           | developers.webflow.com/reference y /mcp/reference/how-it-works describen el Designer como el entorno visual donde se manipulan elementos, estilos y paneles ("an agent can do through the MCP server only what you can do in the Webflow Designer"). El primitivo es la manipulación de affordances presentadas sobre una representación navegable del estado del sitio. Fuente vigente.                                    |
| Data API         | Programmatic | API REST sobre HTTPS                                  | developers.webflow.com/data documenta endpoints RESTful para gestionar CMS, sites, ecommerce, forms, assets, custom code y configuración Enterprise. El consumidor invoca operaciones definidas por el proveedor mediante peticiones estructuradas. Fuente vigente.                                                                                                                                                         |
| Designer API     | Programmatic | API JavaScript del lado cliente (Designer Extensions) | developers.webflow.com/designer la describe como una API JavaScript que las Designer Extensions usan para leer y escribir elementos, estilos, componentes, variables, páginas y assets. El código de la extensión invoca operaciones; el primitivo es la llamada a operación, no la manipulación de affordances. Fuente vigente.                                                                                            |
| Browser API      | Programmatic | API JavaScript del lado cliente (sitios publicados)   | developers.webflow.com/browser la describe como una API cliente que corre en sitios publicados para fijar atributos personalizados, registrar variaciones de optimización y enviar eventos de objetivo. Invocación de operaciones contra el backend de Webflow. Contexto y base distintos de Data y Designer. Fuente vigente.                                                                                               |
| Webflow CLI      | Programmatic | Cliente de línea de comandos                          | developers.webflow.com/cli documenta grupos de comandos (auth, sites, forms, assets, cms, devlink, cloud, extension). El primitivo es el comando estructurado. No se documenta una TUI persistente y navegable. Fuente vigente.                                                                                                                                                                                             |
| Webhooks         | Event        | Entrega HTTP iniciada por el servicio                 | developers.webflow.com/data ("Working with Webhooks" / "Get real-time updates when events occur on your site"). El servicio inicia la interacción al ocurrir eventos suscritos y entrega a un receptor controlado por el consumidor. Fuente vigente.                                                                                                                                                                        |
| MCP server       | Agentic      | Servidor Model Context Protocol                       | developers.webflow.com/mcp y /mcp/reference/how-it-works describen el servidor oficial en mcp.webflow.com/mcp que expone las APIs de Webflow como herramientas que un agente descubre y selecciona, con descripciones semánticas y recursos referenciables. El descubrimiento y la selección de capacidades estructuran el contrato, por lo que es Agentic según la regla de frontera MCP, no Programmatic. Fuente vigente. |

# Registro de cobertura (coverage ledger)

| Mecanismo de acceso                        | Disposición                                                                                                                                  |
| ------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------- |
| Data API                                   | Interfaz: Data API (Programmatic)                                                                                                            |
| Designer API                               | Interfaz: Designer API (Programmatic)                                                                                                        |
| Browser API                                | Interfaz: Browser API (Programmatic)                                                                                                         |
| Webflow CLI                                | Interfaz: Webflow CLI (Programmatic)                                                                                                         |
| TUI del CLI                                | Excluido: el CLI es basado en comandos; no se documenta una TUI persistente y navegable                                                      |
| Webhooks / eventos                         | Interfaz: Webhooks (Event)                                                                                                                   |
| MCP server y AI tools                      | Interfaz: MCP server (Agentic)                                                                                                               |
| Cliente web (Designer + dashboard)         | Interfaz: Webflow Designer (Interactive)                                                                                                     |
| Cliente móvil de primera parte             | Excluido: no existe cliente móvil propio; el Designer es de navegador y no está optimizado para móvil                                        |
| Cliente de escritorio de primera parte     | Excluido: no existe cliente de escritorio propio; el Designer corre en el navegador                                                          |
| JavaScript SDK                             | Excluido: librería cliente que implementa la Data API, no una interfaz                                                                       |
| Python SDK                                 | Excluido: librería cliente que implementa la Data API, no una interfaz                                                                       |
| Flowkit CSS                                | Excluido: framework CSS, no un mecanismo de acceso                                                                                           |
| Webflow Cloud                              | Excluido: producto de hosting/despliegue; se accede vía CLI (Programmatic) y dashboard web (Interactive), no es una interfaz lógica distinta |
| DevLink (import/export de React)           | Excluido: función del CLI, no una interfaz distinta                                                                                          |
| App Marketplace / índice de integraciones  | Excluido: directorio de integraciones de terceros, no una interfaz de acceso del proveedor                                                   |
| llms.txt / MCP de documentación / "Ask AI" | Excluido: ayudas de documentación, no interfaces de acceso al servicio                                                                       |

# Cobertura por canal

| Canal          | Evidencia            |
| -------------- | -------------------- |
| Interactive    | Observed             |
| Agentic        | Observed             |
| Conversational | No evidence observed |
| Event          | Observed             |
| Programmatic   | Observed             |

# Notas de clasificación

El servidor MCP podría confundirse con Conversational porque se usa desde agentes de lenguaje natural, pero el lenguaje natural vive en el agente externo, no en el contrato de Webflow. El contrato del servidor consiste en herramientas descubribles e invocables, lo que lo sitúa en Agentic. No se observó una interfaz conversacional propia de Webflow (por ejemplo, un asistente de lenguaje natural que interprete mensajes como primitivo de acceso al servicio); ausencia de evidencia no equivale a evidencia de ausencia.

# Veredicto multicanal

`Multichannel` (4 paradigmas distintos: Interactive, Agentic, Event, Programmatic).

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
    "name": "Webflow"
  },
  "interfaces": [
    {
      "name": "Webflow Designer",
      "technology": "Web application (visual canvas in browser)",
      "channel": "Interactive",
      "classification_rationale": "Actions are expressed by manipulating presented affordances (canvas, panels, controls) over a persistent, navigable representation of site state.",
      "provenance": [
        {
          "url": "https://developers.webflow.com/reference",
          "evidence": "Docs describe extending the Webflow Designer, the visual editing environment."
        },
        {
          "url": "https://developers.webflow.com/mcp/reference/how-it-works",
          "evidence": "States an agent can do through the MCP server only what a user can do in the Webflow Designer, framing the Designer as the interactive control surface."
        }
      ]
    },
    {
      "name": "Data API",
      "technology": "REST API over HTTPS",
      "channel": "Programmatic",
      "classification_rationale": "The consumer explicitly invokes provider-defined operations through structured HTTP requests over one base and auth.",
      "provenance": [
        {
          "url": "https://developers.webflow.com/data",
          "evidence": "RESTful endpoints to manage CMS, sites, ecommerce, forms, assets, custom code, webhooks and Enterprise configuration."
        }
      ]
    },
    {
      "name": "Designer API",
      "technology": "Client-side JavaScript API (Designer Extensions)",
      "channel": "Programmatic",
      "classification_rationale": "Extension code invokes provider-defined operations to read and write elements, styles, components and variables; the primitive is operation invocation, not affordance manipulation.",
      "provenance": [
        {
          "url": "https://developers.webflow.com/reference",
          "evidence": "Designer API described as a JavaScript API that Designer Extensions use to read and write elements, styles, components, variables, pages, folders and assets."
        }
      ]
    },
    {
      "name": "Browser API",
      "technology": "Client-side JavaScript API (published sites)",
      "channel": "Programmatic",
      "classification_rationale": "Code on published sites invokes provider-defined operations to set custom attributes, record optimization variations and send custom goal events.",
      "provenance": [
        {
          "url": "https://developers.webflow.com/reference",
          "evidence": "Browser API described as a client-side JavaScript API running on published sites to set attributes, record optimization variations and send goal events."
        }
      ]
    },
    {
      "name": "Webflow CLI",
      "technology": "Command-line client",
      "channel": "Programmatic",
      "classification_rationale": "The consumer invokes provider-defined operations through structured commands (auth, sites, forms, assets, cms, devlink, cloud, extension); no persistent navigable TUI is documented.",
      "provenance": [
        {
          "url": "https://developers.webflow.com/cli/reference/webflow-cli",
          "evidence": "Command-based CLI to manage sites, CMS, forms and assets and to build, share and deploy code from the terminal."
        }
      ]
    },
    {
      "name": "Webhooks",
      "technology": "Service-initiated HTTP delivery to a subscriber receiver",
      "channel": "Event",
      "classification_rationale": "The service initiates the interaction when subscribed events occur and delivers to a consumer-controlled receiver URL.",
      "provenance": [
        {
          "url": "https://developers.webflow.com/data",
          "evidence": "Working with Webhooks; get real-time updates when events occur on a site."
        }
      ]
    },
    {
      "name": "MCP server",
      "technology": "Model Context Protocol server",
      "channel": "Agentic",
      "classification_rationale": "The official server exposes Webflow APIs as semantically described tools that an agent discovers and selects; capability discovery and selection structure the interaction contract.",
      "provenance": [
        {
          "url": "https://developers.webflow.com/mcp/reference/overview",
          "evidence": "Official MCP server exposing Webflow APIs as tools an AI agent can use to create and manage site objects."
        },
        {
          "url": "https://developers.webflow.com/mcp/reference/how-it-works",
          "evidence": "Server at mcp.webflow.com/mcp translates intent into API calls, exposes tools and referenceable resources, and reports mode-aware tool availability."
        }
      ]
    }
  ],
  "access_mechanism_ledger": [
    {
      "mechanism": "Data API",
      "disposition": "interface",
      "detail": "Data API"
    },
    {
      "mechanism": "Designer API",
      "disposition": "interface",
      "detail": "Designer API"
    },
    {
      "mechanism": "Browser API",
      "disposition": "interface",
      "detail": "Browser API"
    },
    {
      "mechanism": "Webflow CLI",
      "disposition": "interface",
      "detail": "Webflow CLI"
    },
    {
      "mechanism": "CLI TUI",
      "disposition": "excluded",
      "detail": "Command-based CLI; no persistent navigable TUI documented."
    },
    {
      "mechanism": "Webhooks / events",
      "disposition": "interface",
      "detail": "Webhooks"
    },
    {
      "mechanism": "MCP server and AI tools",
      "disposition": "interface",
      "detail": "MCP server"
    },
    {
      "mechanism": "Web client (Designer + dashboard)",
      "disposition": "interface",
      "detail": "Webflow Designer"
    },
    {
      "mechanism": "First-party mobile client",
      "disposition": "excluded",
      "detail": "No first-party mobile client; the Designer is browser-based and not optimized for mobile."
    },
    {
      "mechanism": "First-party desktop client",
      "disposition": "excluded",
      "detail": "No first-party desktop client; the Designer runs in the browser."
    },
    {
      "mechanism": "JavaScript SDK",
      "disposition": "excluded",
      "detail": "Client library implementing the Data API, not an interface."
    },
    {
      "mechanism": "Python SDK",
      "disposition": "excluded",
      "detail": "Client library implementing the Data API, not an interface."
    },
    {
      "mechanism": "Flowkit CSS",
      "disposition": "excluded",
      "detail": "CSS framework, not an access mechanism."
    },
    {
      "mechanism": "Webflow Cloud",
      "disposition": "excluded",
      "detail": "Hosting/deployment product accessed via CLI and web dashboard; not a distinct logical interface."
    },
    {
      "mechanism": "DevLink (React import/export)",
      "disposition": "excluded",
      "detail": "Feature of the CLI, not a distinct interface."
    },
    {
      "mechanism": "App Marketplace / integrations index",
      "disposition": "excluded",
      "detail": "Third-party integrations directory, not a provider access interface."
    },
    {
      "mechanism": "llms.txt / documentation MCP / Ask AI",
      "disposition": "excluded",
      "detail": "Documentation aids, not service-access interfaces."
    }
  ],
  "channel_evidence": {
    "Interactive": "observed",
    "Agentic": "observed",
    "Conversational": "no_evidence_observed",
    "Event": "observed",
    "Programmatic": "observed"
  },
  "number_of_interfaces": 7,
  "multi_interface": true,
  "number_of_channels": 4,
  "multi_channel": true
}
```
