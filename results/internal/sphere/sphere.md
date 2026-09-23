# Análisis de canales de acceso: SPHERE

## Resumen del SaaS

SPHERE (SaaS Pricing Holistic Evaluation and Regulation Environment) es la plataforma multi-tenant de ISA Group (Universidad de Sevilla) para modelar, versionar y analizar pricings de SaaS. Se identifican **4 interfaces lógicas** repartidas en **4 canales distintos**.

## Clasificación de interfaces

| Interfaz                               | Canal          | Tecnología                                          | Procedencia                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| -------------------------------------- | -------------- | --------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Aplicación web SPHERE                  | Interactive    | SPA web en React                                    | La sección de arquitectura de "What is SPHERE?" indica que el frontend es una SPA de React servida por Nginx; la guía de usuario describe manipular menús, tarjetas de pricing, el editor visual Pricing2Yaml y el explorador del espacio de configuración. El primitivo es la manipulación de affordances. Vigente (v2.0.1).                                                                                                                         |
| API REST de SPHERE                     | Programmatic   | API REST descrita con OpenAPI sobre HTTPS           | La referencia de API declara un contrato OpenAPI que expone capacidades de pricing, colecciones, organizaciones, membresías, permisos, analítica, notificaciones y autenticación a integraciones, con bearer token o cabecera `x-api-key`; el YAML canónico enumera operaciones sobre rutas como `/pricings`, `/orgs`, `/collections`, `/users`. El consumidor invoca operaciones definidas por el proveedor. Vigente.                                |
| Asistente HARVEY                       | Conversational | Asistente conversacional integrado en la web        | La guía de HARVEY muestra que el usuario escribe una pregunta en lenguaje natural y recibe una respuesta en streaming; la arquitectura indica que HARVEY usa A-MINT y PRIME como herramientas internas. El primitivo es el mensaje, y la orquestación de herramientas no forma parte del contrato con el consumidor: caso frontera de asistente en lenguaje natural con herramientas internas, que resuelve a Conversational y no a Agentic. Vigente. |
| Flujo de notificaciones en tiempo real | Event          | Endpoint Server-Sent Events `/notifications/stream` | El OpenAPI define `/notifications/stream` como un "SSE stream for real-time notifications" que establece una conexión Server-Sent Events para la entrega en tiempo real (`text/event-stream`); la arquitectura confirma que los server-sent events entregan notificaciones de plataforma. Tras la suscripción, el servicio inicia la entrega cuando ocurren eventos y la empuja por la conexión persistente: Event Notification. Vigente.             |

## Registro de cobertura

| Mecanismo de acceso                                               | Disposición                                                                                                                                                            |
| ----------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Aplicación web (SPA React)                                        | Interfaz: Aplicación web SPHERE                                                                                                                                        |
| API REST / referencia OpenAPI                                     | Interfaz: API REST de SPHERE                                                                                                                                           |
| Asistente conversacional HARVEY                                   | Interfaz: Asistente HARVEY                                                                                                                                             |
| Flujo SSE de notificaciones (`/notifications/stream`)             | Interfaz: Flujo de notificaciones en tiempo real                                                                                                                       |
| Editor Pricing2Yaml (visual/código) y explorador de configuración | Excluido: vistas y controles dentro de la web app; se integran en la interfaz web, sin contrato propio                                                                 |
| Páginas públicas de pricing y URLs estables de Pricing2Yaml       | Excluido: las páginas públicas forman parte de la web app; la descarga estable de YAML es un GET no autenticado sobre la misma superficie HTTP, no una interfaz aparte |
| SDKs y clientes (librerías Node.js, React)                        | Excluido: librerías cliente que consumen la API; los SDK no cuentan como interfaz                                                                                      |
| Pricing4SaaS Suite (Pricing4Java, Pricing4React, Pricing4TS)      | Excluido: librerías embebibles del ecosistema, no mecanismos de acceso de la plataforma SPHERE                                                                         |
| SPACE (Subscription and Pricing Access Control Engine)            | Excluido: producto desplegable independiente con su propio OpenAPI, SDKs e integraciones; no es un canal de acceso de la plataforma SPHERE analizada                   |
| App móvil (superficie de cliente propia)                          | Excluido: no se documenta cliente móvil propio; SPHERE se entrega como plataforma web                                                                                  |
| App de escritorio (superficie de cliente propia)                  | Excluido: no se documenta cliente de escritorio propio                                                                                                                 |
| CLI / terminal (superficie de cliente propia)                     | Excluido: no se documenta cliente de línea de comandos en la documentación ni en el repositorio                                                                        |
| Dashboard TUI                                                     | Excluido: no existe CLI, por tanto no existe interfaz de terminal navegable                                                                                            |
| Webhooks / callbacks salientes                                    | Excluido: no se documenta mecanismo de webhook registrado por el consumidor; la entrega de eventos es vía SSE, contada aparte                                          |
| MCP / protocolo de agente                                         | Excluido: no se documenta servidor MCP ni contrato de descubrimiento de capacidades                                                                                    |
| Índice de integraciones                                           | Excluido: no hay directorio de integraciones de terceros; la integración se logra llamando a la API REST, ya contada                                                   |

## Cobertura de canales

| Canal          | Evidencia               |
| -------------- | ----------------------- |
| Interactive    | Observado               |
| Agentic        | Sin evidencia observada |
| Conversational | Observado               |
| Event          | Observado               |
| Programmatic   | Observado               |

## Notas de clasificación

La clasificación del flujo SSE `/notifications/stream` como Event, y no como parte de la API Programmatic, se apoya en su estructura de control: es un canal de empuje persistente que el servicio inicia cuando ocurren eventos de plataforma, distinto de los endpoints de sondeo ordinarios como `GET /notifications` o `/notifications/unread-count`. La documentación describe al navegador como receptor, pero el endpoint figura en el OpenAPI público, de modo que un consumidor externo también puede suscribirse; el receptor es la conexión que el consumidor abre y controla. Bajo el criterio de "el servicio inicia la interacción al producirse eventos", corresponde a Event Notification.

No se observa el canal Agentic. HARVEY es conversacional porque la orquestación de A-MINT y PRIME es interna y no un contrato de descubrimiento y selección de capacidades expuesto al consumidor, y no se documenta ningún servidor MCP ni protocolo de agente.

## Veredicto multicanal

**Multicanal** (4 paradigmas distintos: Interactive, Programmatic, Conversational, Event).

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
  "generated_at": "2026-09-22T13:36:02Z",
  "evidence_checked_at": "2026-09-22T13:36:02Z",
  "saas": {
    "name": "SPHERE"
  },
  "interfaces": [
    {
      "name": "SPHERE web application",
      "technology": "React single-page web application",
      "channel": "Interactive",
      "classification_rationale": "Users act on the service by manipulating a persistent, navigable representation of state (avatar menu, pricing cards, collections, the Pricing2Yaml visual editor, the configuration-space explorer), which is Affordance Manipulation.",
      "provenance": [
        {
          "url": "https://sphere-docs.vercel.app/docs/2.0.1/api/sphere/introduction",
          "evidence": "Architecture section states the frontend is a React single-page application served by Nginx, communicating with the API over HTTP(S)."
        },
        {
          "url": "https://sphere-docs.vercel.app/docs/2.0.1/category/-user-guide",
          "evidence": "User guide describes UI workflows: managing organizations, members, collections, analysing pricings, visual editor, and the account/avatar menu."
        }
      ]
    },
    {
      "name": "SPHERE REST API",
      "technology": "REST API described by OpenAPI over HTTPS",
      "channel": "Programmatic",
      "classification_rationale": "External consumers explicitly invoke provider-defined operations through structured HTTP requests against resource paths, authenticated by bearer token or x-api-key, which is Operation Invocation.",
      "provenance": [
        {
          "url": "https://sphere-docs.vercel.app/docs/2.0.1/api/sphere/sphere-api",
          "evidence": "API reference states the OpenAPI-generated contract exposes pricing, collection, organization, membership, permission, analytics, notification and authentication capabilities to integrations, using bearer token or x-api-key."
        },
        {
          "url": "https://raw.githubusercontent.com/Alex-GF/SPHERE/refs/heads/main/api/docs/sphere-api-docs.yaml",
          "evidence": "Canonical OpenAPI document enumerates request/response operations over resource paths such as /pricings, /orgs, /collections, /users and /notifications."
        }
      ]
    },
    {
      "name": "HARVEY pricing-intelligence assistant",
      "technology": "In-app conversational assistant",
      "channel": "Conversational",
      "classification_rationale": "The consumer expresses actions through natural-language questions that the service interprets and answers as a streamed reply; tool orchestration (A-MINT extraction, PRIME optimization) is internal to the service and not part of the consumer contract, so it is Contextual Conversation, not Agentic.",
      "provenance": [
        {
          "url": "https://sphere-docs.vercel.app/docs/2.0.1/api/sphere/user-guides/use-harvey",
          "evidence": "Guide shows the consumer types a natural-language question and reviews a streamed answer; context is attached from a stored pricing, an external URL, or the active pricing card."
        },
        {
          "url": "https://sphere-docs.vercel.app/docs/2.0.1/api/sphere/introduction",
          "evidence": "Architecture states HARVEY uses PRIME and A-MINT as internal tools, delegating extraction and optimization behind the conversational surface."
        }
      ]
    },
    {
      "name": "SPHERE real-time notification stream",
      "technology": "Server-Sent Events (SSE) endpoint /notifications/stream",
      "channel": "Event",
      "classification_rationale": "After the consumer subscribes by opening the stream, the service initiates delivery of notifications when platform events occur, pushing them over the persistent connection. This service-initiated, event-triggered push is Event Notification and differs from the ordinary polling endpoints such as GET /notifications.",
      "provenance": [
        {
          "url": "https://raw.githubusercontent.com/Alex-GF/SPHERE/refs/heads/main/api/docs/sphere-api-docs.yaml",
          "evidence": "OpenAPI defines /notifications/stream as an SSE stream for real-time notifications that establishes a Server-Sent Events connection for real-time notification delivery (text/event-stream)."
        },
        {
          "url": "https://sphere-docs.vercel.app/docs/2.0.1/api/sphere/introduction",
          "evidence": "Integration section states server-sent events deliver platform notifications to the browser."
        }
      ]
    }
  ],
  "access_mechanism_ledger": [
    {
      "mechanism": "Web application (React SPA) surface",
      "disposition": "interface",
      "detail": "SPHERE web application"
    },
    {
      "mechanism": "REST API / OpenAPI reference",
      "disposition": "interface",
      "detail": "SPHERE REST API"
    },
    {
      "mechanism": "HARVEY conversational assistant",
      "disposition": "interface",
      "detail": "HARVEY pricing-intelligence assistant"
    },
    {
      "mechanism": "SSE notifications stream (/notifications/stream)",
      "disposition": "interface",
      "detail": "SPHERE real-time notification stream"
    },
    {
      "mechanism": "Pricing2Yaml visual/code editor and configuration-space explorer",
      "disposition": "excluded",
      "detail": "Views and controls within the web application; folded into the SPHERE web application interface, not a distinct contract."
    },
    {
      "mechanism": "Public pricing pages and stable Pricing2Yaml URLs",
      "disposition": "excluded",
      "detail": "Public discovery pages are part of the web application; stable YAML retrieval is an unauthenticated GET on the same HTTP surface, not a separate interface."
    },
    {
      "mechanism": "SDKs and clients (Node.js, React libraries)",
      "disposition": "excluded",
      "detail": "Client libraries that consume the API; SDKs are not counted as interfaces."
    },
    {
      "mechanism": "Pricing4SaaS Suite (Pricing4Java, Pricing4React, Pricing4TS)",
      "disposition": "excluded",
      "detail": "Separate embeddable libraries in the wider ecosystem, not access mechanisms of the SPHERE platform."
    },
    {
      "mechanism": "SPACE (Subscription and Pricing Access Control Engine)",
      "disposition": "excluded",
      "detail": "Separate deployable product with its own OpenAPI, SDKs and integrations; not an access channel of the SPHERE platform under analysis."
    },
    {
      "mechanism": "Mobile app (first-party client surface)",
      "disposition": "excluded",
      "detail": "No first-party mobile client documented; SPHERE is delivered as a web platform."
    },
    {
      "mechanism": "Desktop app (first-party client surface)",
      "disposition": "excluded",
      "detail": "No first-party desktop client documented."
    },
    {
      "mechanism": "CLI / terminal (first-party client surface)",
      "disposition": "excluded",
      "detail": "No command-line client documented in the docs or the SPHERE repository."
    },
    {
      "mechanism": "TUI dashboard",
      "disposition": "excluded",
      "detail": "No CLI exists, so no persistent navigable terminal interface exists."
    },
    {
      "mechanism": "Webhooks / outbound callbacks",
      "disposition": "excluded",
      "detail": "No consumer-registered webhook mechanism documented; event delivery is via the SSE stream, counted separately."
    },
    {
      "mechanism": "MCP / agent protocol",
      "disposition": "excluded",
      "detail": "No Model Context Protocol server or agent-capability discovery contract documented."
    },
    {
      "mechanism": "Integrations index",
      "disposition": "excluded",
      "detail": "No third-party integrations directory; integration is achieved by calling the REST API, already counted."
    }
  ],
  "channel_evidence": {
    "Interactive": "observed",
    "Agentic": "no_evidence_observed",
    "Conversational": "observed",
    "Event": "observed",
    "Programmatic": "observed"
  },
  "number_of_interfaces": 4,
  "multi_interface": true,
  "number_of_channels": 4,
  "multi_channel": true
}
```
