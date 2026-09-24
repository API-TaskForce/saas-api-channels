## Clasificación de interfaces

| Interfaz               | Canal        | Tecnología de interacción                               | Procedencia                                                                                                                                                                                                                                                                                                  |
| ---------------------- | ------------ | ------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Aplicación web         | Interactive  | Web app en app.zenhub.com                               | Docs oficiales describen la web app como superficie autónoma de gestión con vistas dedicadas; el primitivo es manipulación de affordances (tableros, pipelines, formularios). El proveedor la presenta como interfaz separada de la extensión (support.zenhub.com, zenhub.com/faq).                          |
| Extensión de navegador | Interactive  | Zenhub for GitHub (Chrome, Firefox)                     | Inyecta los controles de Zenhub dentro de las páginas de GitHub; el consumidor actúa manipulando esos controles. Mismo paradigma que la web app pero superficie distinta, con estructura de control ligada a la navegación de GitHub (support.zenhub.com).                                                   |
| GraphQL API            | Programmatic | GraphQL sobre HTTP POST (api.zenhub.com/public/graphql) | El consumidor invoca operaciones definidas (queries y mutations) mediante peticiones estructuradas autenticadas con Personal API Key (developers.zenhub.com/graphql-api-docs/getting-started).                                                                                                               |
| REST API               | Programmatic | REST sobre HTTP (legacy)                                | Primera API pública de Zenhub, aún enlazada (github.com/ZenHubIO/API) aunque se recomienda GraphQL para proyectos nuevos. Base e invocación distintas de GraphQL, por lo que es una interfaz Programmatic separada (developers.zenhub.com).                                                                  |
| MCP Server             | Agentic      | Servidor Model Context Protocol (api.zenhub.com/mcp)    | Envuelve la GraphQL API y expone `tools` descritos semánticamente que un cliente de IA descubre y selecciona por objetivo ("¿en qué issue debería trabajar?"). El descubrimiento y la selección de capacidades estructuran el contrato, por lo que es Agentic y no Programmatic (developers.zenhub.com/mcp). |
| Webhooks               | Event        | POST HTTP salientes (destinos custom y preconfigurados) | Zenhub inicia la interacción cuando ocurren eventos del tablero (issue_transfer, estimate_set, estimate_cleared, issue_reprioritized) y hace POST a un receptor controlado por el consumidor (developers.zenhub.com/webhooks).                                                                               |

## Registro de cobertura

| Mecanismo de acceso                                      | Disposición                                                                                                                                                                |
| -------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| GraphQL API                                              | Interfaz: GraphQL API                                                                                                                                                      |
| REST API                                                 | Interfaz: REST API                                                                                                                                                         |
| MCP Server                                               | Interfaz: MCP Server                                                                                                                                                       |
| Webhooks                                                 | Interfaz: Webhooks                                                                                                                                                         |
| Superficie web de primera parte                          | Interfaz: Aplicación web                                                                                                                                                   |
| Extensión de navegador                                   | Interfaz: Extensión de navegador                                                                                                                                           |
| GraphQL Explorer (GraphiQL embebido)                     | Excluido: consola de pruebas en la documentación para construir y ejecutar llamadas GraphQL; materializa la GraphQL API, no es una interfaz de producción separada.        |
| Integraciones Slack / Gitter / Spark / HipChat           | Excluido: destinos preconfigurados dentro del mecanismo de Webhooks, no interfaces propias.                                                                                |
| Superficie móvil de primera parte                        | Excluido: no hay app móvil nativa; la web app se usa desde navegadores móviles (misma interfaz web Interactive). Las apps "ZenHub GFX" son de otro proveedor sin relación. |
| Superficie de escritorio de primera parte                | Excluido: no se documenta cliente de escritorio nativo; el acceso es vía web app.                                                                                          |
| Terminal / CLI / TUI de primera parte                    | Excluido: Zenhub no publica CLI ni TUI. Gemini CLI y Claude Code son clientes MCP de terceros, no interfaces de Zenhub.                                                    |
| SDKs / librerías cliente (pyzenhub, zenhub-client, etc.) | Excluido: librerías de terceros o comunidad que envuelven las APIs; los SDK no cuentan como interfaces.                                                                    |

## Cobertura de canales

| Canal          | Evidencia               |
| -------------- | ----------------------- |
| Interactive    | Observado               |
| Agentic        | Observado               |
| Conversational | Sin evidencia observada |
| Event          | Observado               |
| Programmatic   | Observado               |

## Notas de clasificación

La web app y la extensión de navegador se cuentan como dos interfaces Interactive separadas, no como una. Comparten primitivo (manipulación de affordances) y autenticación, pero el propio proveedor las presenta como "ambas interfaces" y difieren en superficie y estructura de control: una es una aplicación autónoma en app.zenhub.com y la otra un overlay inyectado en el DOM de github.com. Esta decisión afecta al recuento de interfaces, no al de canales, ya que ambas caen en Interactive.

No se observó ninguna interfaz Conversational de primera parte. El servidor MCP es Agentic, no Conversational: el consumidor no dialoga en lenguaje natural con un asistente interpretado por Zenhub, sino que un cliente de IA externo descubre e invoca tools. La ausencia de evidencia no implica ausencia del canal.

## Veredicto multicanal

**Multichannel** (4 paradigmas distintos: Interactive, Agentic, Event, Programmatic).

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
  "generated_at": "2026-09-24T21:42:19+02:00",
  "evidence_checked_at": "2026-09-24T21:42:19+02:00",
  "saas": {
    "name": "Zenhub"
  },
  "interfaces": [
    {
      "name": "Web application",
      "technology": "Web app (app.zenhub.com)",
      "channel": "Interactive",
      "classification_rationale": "A persistent, navigable representation of workspace state where actions are expressed by manipulating boards, menus, and forms (drag-and-drop pipelines, issue editing). Primitive is affordance manipulation.",
      "provenance": [
        {
          "url": "https://support.zenhub.com/article/how-do-i-use-zenhubs-browser-extension-for-git-hub",
          "evidence": "Provider states the web application at app.zenhub.com is a standalone project-management surface with dedicated views, presented as an interface distinct from the extension."
        },
        {
          "url": "https://www.zenhub.com/faq",
          "evidence": "Provider describes Zenhub as available 'as a full featured standalone web app', also available for Safari and mobile browsers."
        }
      ]
    },
    {
      "name": "Browser extension",
      "technology": "Zenhub for GitHub extension (Chrome, Firefox)",
      "channel": "Interactive",
      "classification_rationale": "Injects Zenhub affordances (boards, pipelines, controls) into GitHub's own pages; the consumer acts by manipulating those presented controls. Same paradigm as the web app but a distinct surface with a control structure bound to GitHub's page navigation.",
      "provenance": [
        {
          "url": "https://support.zenhub.com/article/how-do-i-use-zenhubs-browser-extension-for-git-hub",
          "evidence": "Provider documents the extension as adding project-management features directly within GitHub's interface, calling extension and web app 'both interfaces' with identical functionality."
        }
      ]
    },
    {
      "name": "GraphQL API",
      "technology": "GraphQL over HTTP POST (api.zenhub.com/public/graphql)",
      "channel": "Programmatic",
      "classification_rationale": "Consumer explicitly invokes provider-defined operations (queries and mutations) through structured requests to a fixed endpoint with a personal API key. Primitive is operation invocation.",
      "provenance": [
        {
          "url": "https://developers.zenhub.com/graphql-api-docs/getting-started",
          "evidence": "Official docs: POST requests to api.zenhub.com/public/graphql, authenticated by a Personal API Key, invoking GraphQL queries and mutations."
        }
      ]
    },
    {
      "name": "REST API",
      "technology": "REST over HTTP (legacy)",
      "channel": "Programmatic",
      "classification_rationale": "Consumer explicitly invokes provider-defined REST operations through structured requests. Distinct base and invocation style from GraphQL, so a separate Programmatic interface. Documented but legacy (GraphQL recommended for new projects).",
      "provenance": [
        {
          "url": "https://developers.zenhub.com/",
          "evidence": "Official overview lists the REST API as Zenhub's first public API offering, still linked (github.com/ZenHubIO/API), with GraphQL recommended for new work."
        }
      ]
    },
    {
      "name": "MCP Server",
      "technology": "Model Context Protocol server (api.zenhub.com/mcp)",
      "channel": "Agentic",
      "classification_rationale": "Exposes semantically described tools that an AI client discovers and selects by goal ('which issue should I work on'). Capability discovery and selection structure the interaction contract, so Agentic rather than Programmatic despite wrapping the GraphQL API.",
      "provenance": [
        {
          "url": "https://developers.zenhub.com/mcp",
          "evidence": "Official docs: the MCP server wraps the GraphQL API and exposes tools to search and modify issues and understand the sprint; the LLM figures out which tools to call to answer a goal."
        }
      ]
    },
    {
      "name": "Webhooks",
      "technology": "Outbound HTTP POST webhooks (custom and preset targets)",
      "channel": "Event",
      "classification_rationale": "Zenhub initiates the interaction when board events occur (issue_transfer, estimate_set, estimate_cleared, issue_reprioritized) and POSTs to a consumer-controlled receiver URL. Primitive is event notification.",
      "provenance": [
        {
          "url": "https://developers.zenhub.com/webhooks",
          "evidence": "Official docs: the custom webhook sends a POST request to your endpoint for multiple events occurring on your Zenhub board, configurable to Slack, Gitter, Spark, HipChat, or a custom receiver."
        }
      ]
    }
  ],
  "access_mechanism_ledger": [
    {
      "mechanism": "GraphQL API",
      "disposition": "interface",
      "detail": "GraphQL API"
    },
    {
      "mechanism": "REST API",
      "disposition": "interface",
      "detail": "REST API"
    },
    {
      "mechanism": "MCP Server",
      "disposition": "interface",
      "detail": "MCP Server"
    },
    {
      "mechanism": "Webhooks",
      "disposition": "interface",
      "detail": "Webhooks"
    },
    {
      "mechanism": "Web app (first-party web surface)",
      "disposition": "interface",
      "detail": "Web application"
    },
    {
      "mechanism": "Browser extension",
      "disposition": "interface",
      "detail": "Browser extension"
    },
    {
      "mechanism": "GraphQL Explorer (embedded GraphiQL)",
      "disposition": "excluded",
      "detail": "In-docs testing console for constructing and running GraphQL calls; it materializes the GraphQL API rather than being a separate production interface."
    },
    {
      "mechanism": "Slack / Gitter / Spark / HipChat integrations",
      "disposition": "excluded",
      "detail": "Preset destinations configured through the Webhooks mechanism, not distinct provider interfaces."
    },
    {
      "mechanism": "Mobile (first-party mobile surface)",
      "disposition": "excluded",
      "detail": "No native mobile app; the web app is reached through mobile browsers, which is the same web Interactive interface. (Unrelated 'ZenHub GFX' mobile apps are a different vendor.)"
    },
    {
      "mechanism": "Desktop (first-party desktop surface)",
      "disposition": "excluded",
      "detail": "No native desktop client documented; access is via the web app."
    },
    {
      "mechanism": "Terminal / CLI / TUI (first-party terminal surface)",
      "disposition": "excluded",
      "detail": "Zenhub ships no CLI or TUI. Gemini CLI / Claude Code are third-party MCP clients, not Zenhub interfaces."
    },
    {
      "mechanism": "SDKs / client libraries (pyzenhub, zenhub-client, etc.)",
      "disposition": "excluded",
      "detail": "Third-party/community libraries wrapping the APIs; SDKs are not counted as interfaces."
    }
  ],
  "channel_evidence": {
    "Interactive": "observed",
    "Agentic": "observed",
    "Conversational": "no_evidence_observed",
    "Event": "observed",
    "Programmatic": "observed"
  },
  "number_of_interfaces": 6,
  "multi_interface": true,
  "number_of_channels": 4,
  "multi_channel": true
}
```
