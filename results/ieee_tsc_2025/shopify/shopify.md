## Resumen del SaaS

Shopify es una plataforma de comercio operada por Shopify Inc. (dominio oficial `shopify.com`, portal de desarrollo `shopify.dev`). A partir de la documentación oficial se reconstruyeron **12 interfaces lógicas** provistas por el proveedor, repartidas en **5 canales distintos** con al menos una interfaz clasificada.

## Tabla de clasificación de interfaces

| Interfaz                                    | Canal          | Tecnología de interacción                                     | Procedencia                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| ------------------------------------------- | -------------- | ------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Shopify admin (web y app móvil de comercio) | Interactive    | Aplicación web (`shopify.com/admin`) y app nativa iOS/Android | `help.shopify.com/manual/shopify-admin` describe el admin como back office accesible en escritorio (navegador) y mediante la app móvil de primera parte para gestionar pedidos, productos y analítica. Las acciones se expresan manipulando vistas, controles y formularios de una representación persistente y navegable del estado de la tienda: Affordance Manipulation. Vigente.                                                                                     |
| Shopify POS                                 | Interactive    | App nativa iOS/Android de punto de venta                      | `shopify.com/pos` y `help.shopify.com/manual/sell-in-person` documentan la app POS de primera parte para venta en persona (caja, carrito, cobro, inventario). Contrato de interacción minorista propio, manipulado por afordancias presentadas en la app: Interactive. Vigente.                                                                                                                                                                                          |
| Admin GraphQL API                           | Programmatic   | GraphQL sobre HTTPS                                           | `shopify.dev/docs/api/admin-graphql`: el consumidor formula queries y mutations explícitas contra `admin/api/{version}/graphql.json` con token de acceso. Invocación explícita de operaciones definidas por el proveedor: Operation Invocation. Vigente y recomendada.                                                                                                                                                                                                   |
| Admin REST API                              | Programmatic   | REST sobre HTTPS                                              | `shopify.dev/docs/api/admin-rest`: endpoints por recurso `admin/api/{version}/{recurso}.json`. Invocación explícita de operaciones: Programmatic. Frescura: heredada (legacy) desde el 1 de octubre de 2024; desde el 1 de abril de 2025 las nuevas apps públicas deben usar GraphQL. Contrato distinto (REST) del de la GraphQL Admin, por lo que cuenta como interfaz separada.                                                                                        |
| Storefront API                              | Programmatic   | GraphQL sobre HTTPS                                           | `shopify.dev/docs/api/storefront`: único endpoint GraphQL `/{version}/graphql.json` (solo POST) con token de storefront, base y autenticación distintas del Admin API. Invocación explícita de operaciones: Programmatic. Vigente.                                                                                                                                                                                                                                       |
| Partner API                                 | Programmatic   | GraphQL sobre HTTPS                                           | `shopify.dev/docs/api/partner`: acceso a los datos del Partner Dashboard (organizaciones, apps, pagos) con autenticación de partner, base y credenciales propias. Invocación explícita de operaciones: Programmatic. Vigente.                                                                                                                                                                                                                                            |
| Shopify CLI                                 | Programmatic   | Interfaz de línea de comandos                                 | `shopify.dev/docs/api/shopify-cli` y `github.com/Shopify/cli`: herramienta basada en comandos (`shopify app`, `shopify theme`, etc.) para scaffolding, despliegue y desarrollo. El consumidor invoca comandos definidos por el proveedor: Operation Invocation. Los prompts interactivos recogen parámetros del comando que se invoca y no constituyen un TUI navegable persistente. Vigente.                                                                            |
| Webhooks / Events                           | Event          | Entrega HTTPS a receptor (URL, EventBridge, Pub/Sub)          | `shopify.dev/docs/apps/build/webhooks/subscribe` y `.../events`: ante un evento de un topic suscrito, el servicio inicia la interacción y envía la carga a un receptor controlado por el consumidor. Notificación iniciada por el servicio hacia un receptor del consumidor: Event Notification. Webhooks clásicos vigentes; Events es el sucesor de nueva generación en developer preview (versión `unstable`), mismo paradigma.                                        |
| Sidekick                                    | Conversational | Asistente de IA embebido en el admin                          | `help.shopify.com/manual/shopify-admin/productivity-tools/sidekick`: asistente de comercio con IA; el consumidor expresa la intención mediante mensajes en lenguaje natural (texto, voz, pantalla compartida) y el asistente planifica, ejecuta y presenta los cambios para revisión. El primitivo es el mensaje y la orquestación interna de herramientas no forma parte del contrato de cara al consumidor: Contextual Conversation. Vigente.                          |
| Storefront MCP                              | Agentic        | Servidor MCP por tienda                                       | `shopify.dev/docs/apps/build/storefront-mcp` y `.../agents/catalog/storefront-mcp`: endpoint por tienda `https://{shop}.myshopify.com/api/mcp` (y `/api/ucp/mcp`) que expone herramientas descubribles (búsqueda de catálogo, carrito, políticas) que un agente lista y selecciona. El descubrimiento y la selección de capacidades forman parte del contrato: Capability Discovery and Invocation. Caso frontera MCP resuelto como Agentic. Vigente; sin autenticación. |
| Catalog MCP (Global)                        | Agentic        | Servidor MCP entre tiendas                                    | `shopify.dev/docs/agents/catalog/mcp`: MCP de descubrimiento a través de todo el ecosistema (`search_global_products` y similares) con autenticación JWT, base y credenciales distintas del Storefront MCP. Descubrimiento e invocación de capacidades: Agentic. Vigente.                                                                                                                                                                                                |
| Shopify Dev MCP                             | Agentic        | Servidor MCP de documentación y esquema                       | `npmjs.com/package/@shopify/dev-mcp` y `github.com/Shopify/dev-mcp`: servidor MCP oficial que expone herramientas (buscar documentación, introspección del esquema Admin GraphQL, validación de GraphQL) que un cliente descubre y selecciona. Descubrimiento e invocación de capacidades: Agentic. Vigente.                                                                                                                                                             |

## Tabla del registro de cobertura

| Mecanismo de acceso                                   | Disposición                                                                                                                                                                                                         |
| ----------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Shopify admin (web)                                   | Interfaz: Shopify admin (Interactive)                                                                                                                                                                               |
| App móvil de comercio (iOS/Android)                   | Interfaz: Shopify admin (Interactive), superficie móvil del mismo contrato                                                                                                                                          |
| Cliente de escritorio                                 | Excluido: no existe app de escritorio de primera parte dedicada; el admin es de navegador                                                                                                                           |
| Terminal / Shopify CLI                                | Interfaz: Shopify CLI (Programmatic); sin TUI navegable persistente, solo prompts de comando                                                                                                                        |
| Shopify POS                                           | Interfaz: Shopify POS (Interactive)                                                                                                                                                                                 |
| Escaparate hosteado (Online Store)                    | Excluido: superficie de comercio configurada por el comerciante (sitio de cara al comprador), no una interfaz del proveedor para operar el servicio; el acceso programático de compra ya lo cubre la Storefront API |
| App de consumidor Shop                                | Excluido: app de descubrimiento y checkout entre comerciantes de Shopify; capa de mercado para compradores, no una interfaz hacia el servicio Shopify de un comerciante concreto                                    |
| Admin GraphQL API                                     | Interfaz: Admin GraphQL API (Programmatic)                                                                                                                                                                          |
| Admin REST API                                        | Interfaz: Admin REST API (Programmatic, legacy)                                                                                                                                                                     |
| Storefront API                                        | Interfaz: Storefront API (Programmatic)                                                                                                                                                                             |
| Partner API                                           | Interfaz: Partner API (Programmatic)                                                                                                                                                                                |
| Webhooks / Events                                     | Interfaz: Webhooks / Events (Event)                                                                                                                                                                                 |
| Sidekick (asistente IA)                               | Interfaz: Sidekick (Conversational)                                                                                                                                                                                 |
| Storefront MCP                                        | Interfaz: Storefront MCP (Agentic)                                                                                                                                                                                  |
| Catalog MCP (Global)                                  | Interfaz: Catalog MCP (Agentic)                                                                                                                                                                                     |
| Shopify Dev MCP                                       | Interfaz: Shopify Dev MCP (Agentic)                                                                                                                                                                                 |
| Shopify Functions                                     | Excluido: mecanismo de extensión de backend (lógica personalizada dentro de Shopify), no una interfaz de acceso de cara al consumidor                                                                               |
| App extensions / UI extensions (admin, POS, checkout) | Excluido: renderizan UI de apps dentro de superficies Shopify existentes; extienden esas interfaces Interactive en lugar de constituir una nueva                                                                    |
| Shopify Flow                                          | Excluido: producto de automatización configurado dentro del admin, no un canal de acceso externo distinto                                                                                                           |
| Liquid / temas                                        | Excluido: capa de plantillas del escaparate, no una interfaz de acceso                                                                                                                                              |
| GraphiQL / explorador de API                          | Excluido: utilidad de desarrollo para componer y ejecutar llamadas; da soporte a las APIs GraphQL, no es una interfaz distinta                                                                                      |
| Customer Account API / Customer Account MCP           | Excluido: superficies adicionales de cuenta de cliente (Programmatic y Agentic respectivamente); sus canales ya están Observados, no se enumeran por separado para evitar recuentos poco inspeccionados             |
| Checkout MCP                                          | Excluido: en preview para socios seleccionados; superficie Agentic emergente cuyo canal (Agentic) ya está Observado                                                                                                 |

## Tabla de cobertura por canal

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
  "generated_at": "2026-09-23T12:00:00Z",
  "evidence_checked_at": "2026-09-23T12:00:00Z",
  "saas": { "name": "Shopify" },
  "interfaces": [
    {
      "name": "Shopify admin (web and mobile app)",
      "technology": "Web application and native iOS/Android app",
      "channel": "Interactive",
      "classification_rationale": "Actions are expressed by manipulating presented views, controls and forms of a persistent, navigable representation of store state (Affordance Manipulation). Delivered on both web and the first-party mobile app under the same primitive, state and authentication.",
      "provenance": [
        {
          "url": "https://help.shopify.com/en/manual/shopify-admin",
          "evidence": "Admin is the back office accessed on desktop via browser and on mobile via the first-party Shopify app to manage orders, products and analytics."
        },
        {
          "url": "https://help.shopify.com/en/manual/shopify-admin/shopify-app",
          "evidence": "First-party iOS/Android app to run the store: view performance, manage orders, update catalog, capture payments."
        }
      ]
    },
    {
      "name": "Shopify POS",
      "technology": "Native iOS/Android point-of-sale app",
      "channel": "Interactive",
      "classification_rationale": "In-person retail selling through affordances presented in the POS app (register, cart, tender, inventory); a distinct interaction contract manipulated by the operator.",
      "provenance": [
        {
          "url": "https://www.shopify.com/pos",
          "evidence": "First-party POS app installed on a smartphone or tablet for in-person sales, synced with the store back office."
        },
        {
          "url": "https://help.shopify.com/en/manual/sell-in-person",
          "evidence": "Shopify POS available on iOS and Android; syncs orders and inventory across retail locations and the online store."
        }
      ]
    },
    {
      "name": "Admin GraphQL API",
      "technology": "GraphQL over HTTPS",
      "channel": "Programmatic",
      "classification_rationale": "Consumer explicitly issues GraphQL queries and mutations against a provider-defined endpoint with an access token (Operation Invocation).",
      "provenance": [
        {
          "url": "https://shopify.dev/docs/api/admin-graphql",
          "evidence": "GraphQL Admin API at admin/api/{version}/graphql.json for products, customers, orders, inventory; recommended API for new apps."
        }
      ]
    },
    {
      "name": "Admin REST API",
      "technology": "REST over HTTPS",
      "channel": "Programmatic",
      "classification_rationale": "Consumer explicitly invokes resource endpoints (Operation Invocation). Separate interface from the GraphQL Admin API because the invocation style differs.",
      "provenance": [
        {
          "url": "https://shopify.dev/docs/api/admin-rest",
          "evidence": "Resource endpoints admin/api/{version}/{resource}.json; legacy as of Oct 1 2024, GraphQL required for new public apps from Apr 1 2025."
        }
      ]
    },
    {
      "name": "Storefront API",
      "technology": "GraphQL over HTTPS",
      "channel": "Programmatic",
      "classification_rationale": "Consumer explicitly issues GraphQL operations against a single POST endpoint with a storefront token (Operation Invocation). Distinct base and auth from the Admin API.",
      "provenance": [
        {
          "url": "https://shopify.dev/docs/api/storefront",
          "evidence": "Single GraphQL endpoint /{version}/graphql.json (POST only); no REST equivalent for storefronts."
        }
      ]
    },
    {
      "name": "Partner API",
      "technology": "GraphQL over HTTPS",
      "channel": "Programmatic",
      "classification_rationale": "Consumer explicitly invokes GraphQL operations against Partner Dashboard data with partner authentication (Operation Invocation). Distinct base and auth from the Admin and Storefront APIs.",
      "provenance": [
        {
          "url": "https://shopify.dev/docs/api/partner",
          "evidence": "Partner API exposes Partner Dashboard data to automate front and back-office operations."
        }
      ]
    },
    {
      "name": "Shopify CLI",
      "technology": "Command-line interface",
      "channel": "Programmatic",
      "classification_rationale": "Consumer invokes provider-defined commands to scaffold, deploy and run apps and themes (Operation Invocation). Interactive prompts collect parameters for the invoked command and are not a persistent navigable TUI.",
      "provenance": [
        {
          "url": "https://shopify.dev/docs/api/shopify-cli",
          "evidence": "Command-line tool (shopify app/theme commands) to build apps, themes and Hydrogen storefronts and automate development tasks."
        }
      ]
    },
    {
      "name": "Webhooks / Events",
      "technology": "Service-initiated HTTPS delivery to a consumer receiver (URL, EventBridge, Pub/Sub)",
      "channel": "Event",
      "classification_rationale": "On a subscribed topic event, the service initiates the interaction and delivers a payload to a consumer-controlled receiver (Event Notification).",
      "provenance": [
        {
          "url": "https://shopify.dev/docs/apps/build/webhooks/subscribe",
          "evidence": "A webhook subscription describes a topic and a destination; Shopify sends a payload to the destination when the event occurs."
        },
        {
          "url": "https://shopify.dev/docs/apps/build/events",
          "evidence": "Events is the next-generation subscription mechanism in developer preview; same subscribe-and-deliver workflow as webhooks."
        }
      ]
    },
    {
      "name": "Sidekick",
      "technology": "Embedded AI commerce assistant",
      "channel": "Conversational",
      "classification_rationale": "Consumer interacts through natural-language messages (text, voice, screen share); the assistant plans and executes and surfaces changes for review. The primitive is the message and internal tool orchestration is not part of the consumer-facing contract (Contextual Conversation).",
      "provenance": [
        {
          "url": "https://help.shopify.com/en/manual/shopify-admin/productivity-tools/sidekick",
          "evidence": "AI-enabled commerce assistant in the admin; chat by text or voice from any page to get guidance and complete tasks, presented for review before applying."
        }
      ]
    },
    {
      "name": "Storefront MCP",
      "technology": "Per-store Model Context Protocol server",
      "channel": "Agentic",
      "classification_rationale": "Per-store MCP endpoint exposes discoverable tools (catalog search, cart, policies) that an agent lists and selects; discovery and selection are part of the interaction contract (Capability Discovery and Invocation). MCP boundary case resolved as Agentic.",
      "provenance": [
        {
          "url": "https://shopify.dev/docs/apps/build/storefront-mcp",
          "evidence": "Per-store endpoint https://{shop}.myshopify.com/api/mcp exposing structured tools for search, cart and orders that an AI agent connects to and selects."
        }
      ]
    },
    {
      "name": "Catalog MCP (Global)",
      "technology": "Cross-merchant Model Context Protocol server",
      "channel": "Agentic",
      "classification_rationale": "Cross-merchant discovery MCP whose tools (search_global_products and similar) an agent discovers and selects; distinct base and JWT auth from the Storefront MCP (Capability Discovery and Invocation).",
      "provenance": [
        {
          "url": "https://shopify.dev/docs/agents/catalog/mcp",
          "evidence": "Catalog MCP provides search across all Shopify products with authentication via JWT tokens, as the primary discovery toolkit for agentic commerce."
        }
      ]
    },
    {
      "name": "Shopify Dev MCP",
      "technology": "Model Context Protocol server for docs and schema",
      "channel": "Agentic",
      "classification_rationale": "Official MCP server exposing tools (search docs, introspect Admin GraphQL schema, validate GraphQL) that a client discovers and selects (Capability Discovery and Invocation).",
      "provenance": [
        {
          "url": "https://www.npmjs.com/package/@shopify/dev-mcp",
          "evidence": "Official @shopify/dev-mcp server provides tools such as search_dev_docs and introspect_admin_schema for AI clients."
        }
      ]
    }
  ],
  "access_mechanism_ledger": [
    {
      "mechanism": "Shopify admin (web)",
      "disposition": "interface",
      "detail": "Shopify admin (web and mobile app)"
    },
    {
      "mechanism": "Merchant mobile app (iOS/Android)",
      "disposition": "interface",
      "detail": "Shopify admin (web and mobile app) — mobile surface"
    },
    {
      "mechanism": "Desktop client",
      "disposition": "excluded",
      "detail": "No dedicated first-party desktop app; admin is browser-based"
    },
    {
      "mechanism": "Terminal / Shopify CLI",
      "disposition": "interface",
      "detail": "Shopify CLI; no persistent navigable TUI"
    },
    {
      "mechanism": "Shopify POS",
      "disposition": "interface",
      "detail": "Shopify POS"
    },
    {
      "mechanism": "Online Store hosted storefront",
      "disposition": "excluded",
      "detail": "Merchant-configured buyer-facing commerce output, not a provider interface for operating the service; programmatic buyer access covered by Storefront API"
    },
    {
      "mechanism": "Shop consumer app",
      "disposition": "excluded",
      "detail": "Cross-merchant consumer discovery/checkout app; buyer marketplace layer, not an interface into a single merchant's service"
    },
    {
      "mechanism": "Admin GraphQL API",
      "disposition": "interface",
      "detail": "Admin GraphQL API"
    },
    {
      "mechanism": "Admin REST API",
      "disposition": "interface",
      "detail": "Admin REST API (legacy)"
    },
    {
      "mechanism": "Storefront API",
      "disposition": "interface",
      "detail": "Storefront API"
    },
    {
      "mechanism": "Partner API",
      "disposition": "interface",
      "detail": "Partner API"
    },
    {
      "mechanism": "Webhooks / Events",
      "disposition": "interface",
      "detail": "Webhooks / Events"
    },
    {
      "mechanism": "Sidekick AI assistant",
      "disposition": "interface",
      "detail": "Sidekick"
    },
    {
      "mechanism": "Storefront MCP",
      "disposition": "interface",
      "detail": "Storefront MCP"
    },
    {
      "mechanism": "Catalog MCP (Global)",
      "disposition": "interface",
      "detail": "Catalog MCP (Global)"
    },
    {
      "mechanism": "Shopify Dev MCP",
      "disposition": "interface",
      "detail": "Shopify Dev MCP"
    },
    {
      "mechanism": "Shopify Functions",
      "disposition": "excluded",
      "detail": "Backend extension mechanism, not a consumer-facing access interface"
    },
    {
      "mechanism": "App extensions / UI extensions",
      "disposition": "excluded",
      "detail": "Render app UI inside existing Shopify surfaces; extend Interactive interfaces rather than constitute a new one"
    },
    {
      "mechanism": "Shopify Flow",
      "disposition": "excluded",
      "detail": "Automation product configured within the admin, not a distinct external access channel"
    },
    {
      "mechanism": "Liquid / themes",
      "disposition": "excluded",
      "detail": "Templating layer for the storefront, not an access interface"
    },
    {
      "mechanism": "GraphiQL / API explorer",
      "disposition": "excluded",
      "detail": "Developer utility for composing and running API calls; supports the GraphQL APIs"
    },
    {
      "mechanism": "Customer Account API / Customer Account MCP",
      "disposition": "excluded",
      "detail": "Additional customer-account surfaces (Programmatic / Agentic); channels already Observed, not separately enumerated"
    },
    {
      "mechanism": "Checkout MCP",
      "disposition": "excluded",
      "detail": "Preview for select partners; emerging Agentic surface, channel already Observed"
    }
  ],
  "channel_evidence": {
    "Interactive": "observed",
    "Agentic": "observed",
    "Conversational": "observed",
    "Event": "observed",
    "Programmatic": "observed"
  },
  "number_of_interfaces": 12,
  "multi_interface": true,
  "number_of_channels": 5,
  "multi_channel": true
}
```
