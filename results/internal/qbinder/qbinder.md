## Resumen del SaaS

QRB (Quantum Resource Binder) es un _binder_ declarativo de recursos cuánticos: dado un circuito OpenQASM 3 y unas preferencias declaradas, resuelve el recurso cuántico óptimo (IBM Quantum o Amazon Braket) sin llegar a enviar el trabajo. Interfaces lógicas identificadas: **3**. Canales distintos con al menos una interfaz clasificada: **2**.

## Tabla de clasificación de interfaces

| Interfaz                                                 | Canal        | Tecnología de interacción                      | Procedencia                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| -------------------------------------------------------- | ------------ | ---------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Frontend web (catálogo / playground / referencia de API) | Interactive  | Aplicación web Next.js                         | README: "apps/web: Next.js catalog / playground / API-docs frontend". El árbol `apps/web/app` expone páginas navegables (`page.tsx`, `catalog`, `catalog/resource`, `playground`, `api`) y componentes de manipulación (editor de circuito, tarjetas de recurso, panel de resultado, paleta de comandos). El primitivo es la manipulación de affordances sobre una representación persistente del estado; consume `apps/api` y no define operaciones propias. |
| API HTTP (REST)                                          | Programmatic | API FastAPI (OpenAPI, referencia en `/scalar`) | `apps/api/src/qrb_api/main.py` declara rutas REST `POST /select`, `POST /instance`, `GET /catalog`, `GET /catalog/{candidate_id}`, `GET /engines`, `GET /presets`, `GET /health` y una página de referencia OpenAPI en `/scalar`. Docstring: "HTTP mirror of the CLI surface ... exposed as JSON". El primitivo es la invocación explícita de operaciones. Vigente (rama main).                                                                               |
| Interfaz de línea de comandos (`qrb`)                    | Programmatic | Aplicación CLI basada en Typer                 | `apps/cli/src/qrb_cli/main.py`: `typer.Typer("qrb")` con subcomandos (`select`, `instance`, `catalog`, `engines`, `preset`) y salida por `typer.echo`. Sin `textual`, `curses` ni `prompt_toolkit`. El primitivo es la invocación de operaciones mediante comandos estructurados con flags.                                                                                                                                                                   |

## Ledger de cobertura

| Mecanismo de acceso                                                | Disposición                                                                                                                                                                                                                          |
| ------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| API HTTP/REST (`apps/api`, FastAPI) + referencia OpenAPI `/scalar` | Interfaz: API HTTP (REST)                                                                                                                                                                                                            |
| CLI (`apps/cli`, `qrb`)                                            | Interfaz: Interfaz de línea de comandos (`qrb`)                                                                                                                                                                                      |
| Superficie de cliente web (`apps/web`, Next.js)                    | Interfaz: Frontend web                                                                                                                                                                                                               |
| Superficie de terminal / TUI del CLI                               | Excluido: el CLI es una app Typer con salida impresa; no expone una TUI persistente y navegable, así que no hay una segunda interfaz Interactive.                                                                                    |
| Superficie de cliente móvil                                        | Excluido: no hay app móvil de primera parte documentada en el repositorio ni en páginas de producto o listados de tienda.                                                                                                            |
| Superficie de cliente de escritorio                                | Excluido: no se distribuye una GUI de escritorio; las vías de escritorio son el CLI y la app web en navegador.                                                                                                                       |
| Webhooks / eventos / inbound routing                               | Excluido: el esquema OpenAPI generado declara `webhooks` vacío (`Record<string, never>`); la API es petición/respuesta, sin SSE, websocket ni entrega de eventos a un receptor controlado por el consumidor.                         |
| Conversacional / chat / asistente IA                               | Excluido: no hay interfaz de mensajes en lenguaje natural; el Playground web es un formulario/editor, no un chat.                                                                                                                    |
| Interfaz MCP / agente / protocolo                                  | Excluido: no existe servidor MCP ni contrato de descubrimiento y selección de capacidades. (`apps/web/AGENTS.md` y `CLAUDE.md` son instrucciones para agentes de codificación sobre el repo, no un mecanismo de acceso al servicio.) |
| Integraciones (IBM Quantum, Amazon Braket)                         | Excluido: son proveedores aguas arriba cuyo catálogo lee QRB; son integraciones salientes, no vías de acceso a QRB. README: "QRB never submits jobs, selection only".                                                                |
| `openbinding` (cliente Python del gateway OpenBinding)             | Excluido: librería cliente, no una interfaz del proveedor; además apunta a un gateway externo distinto.                                                                                                                              |
| `qrb` (librería núcleo / SDK)                                      | Excluido: librería Python consumida por el CLI y la API; las librerías no cuentan como interfaces.                                                                                                                                   |
| `qrb-store` (persistencia Postgres)                                | Excluido: almacén de datos de decisiones y telemetría; no es un mecanismo de acceso de cara al consumidor.                                                                                                                           |
| `poller` (muestreador de telemetría del catálogo)                  | Excluido: proceso interno de fondo que muestrea el catálogo y escribe en `qrb-store`; no expone interfaz alguna.                                                                                                                     |

## Cobertura por canal

| Canal          | Evidencia               |
| -------------- | ----------------------- |
| Interactive    | Observado               |
| Agentic        | Sin evidencia observada |
| Conversational | Sin evidencia observada |
| Event          | Sin evidencia observada |
| Programmatic   | Observado               |

## Notas de clasificación

El CLI y la API son dos interfaces separadas (base e invocación distintas: comandos de terminal frente a peticiones HTTP) pero ambas del mismo canal Programmatic, por lo que suman dos interfaces y un solo canal. La página `/scalar` es documentación OpenAPI de la propia API, no una interfaz independiente. Como se indicó arriba, el despliegue por IP no se pudo inspeccionar, así que la evidencia de frescura procede de la rama `main` del repositorio.

## Veredicto multicanal

`Multichannel` (2 paradigmas distintos: Interactive y Programmatic).

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
  "generated_at": "2026-09-22T14:56:00Z",
  "evidence_checked_at": "2026-09-22T14:56:00Z",
  "saas": { "name": "QRB (Quantum Resource Binder)" },
  "interfaces": [
    {
      "name": "Web frontend (catalog / playground / API reference)",
      "technology": "Next.js web application",
      "channel": "Interactive",
      "classification_rationale": "A persistent, navigable representation of catalog and binding state whose actions are expressed by manipulating presented affordances (pages, resource cards, circuit editor, preference controls, command palette). Primitive is affordance manipulation.",
      "provenance": [
        {
          "url": "https://github.com/qrb-maker/qrb",
          "evidence": "README: 'apps/web: Next.js catalog / playground / API-docs frontend'; task web:dev serves it at http://localhost:3000."
        },
        {
          "url": "https://github.com/qrb-maker/qrb/tree/main/apps/web/app",
          "evidence": "Source tree shows navigable pages app/page.tsx, app/catalog, app/catalog/resource, app/playground, app/api plus interactive components (circuit-editor, resource-card, binding-result-panel, command-palette); consumes apps/api, defines no service operations of its own."
        }
      ]
    },
    {
      "name": "HTTP (REST) API",
      "technology": "FastAPI HTTP API (OpenAPI, /scalar reference)",
      "channel": "Programmatic",
      "classification_rationale": "The consumer explicitly invokes provider-defined operations via structured HTTP requests (POST /select, POST /instance, GET /catalog, GET /catalog/{id}, GET /engines, GET /presets). Primitive is operation invocation.",
      "provenance": [
        {
          "url": "https://github.com/qrb-maker/qrb/blob/main/apps/api/src/qrb_api/main.py",
          "evidence": "FastAPI app declares REST routes /select, /instance, /catalog, /catalog/{candidate_id}, /engines, /presets, /health and a /scalar OpenAPI reference page; module docstring: 'HTTP mirror of the CLI surface ... exposed as JSON'. Current (main branch)."
        }
      ]
    },
    {
      "name": "Command-line interface (qrb)",
      "technology": "Typer command-line application",
      "channel": "Programmatic",
      "classification_rationale": "The consumer explicitly invokes provider-defined subcommands (select, instance, catalog, engines, preset) with flags. Primitive is operation invocation via structured commands; output is printed, not a navigable representation.",
      "provenance": [
        {
          "url": "https://github.com/qrb-maker/qrb/blob/main/apps/cli/src/qrb_cli/main.py",
          "evidence": "typer.Typer app 'qrb' with subcommands and typer.echo output; no textual/curses/prompt_toolkit or persistent TUI. README documents 'uv run qrb select|catalog|instance|engines|preset list'."
        }
      ]
    }
  ],
  "access_mechanism_ledger": [
    {
      "mechanism": "HTTP/REST API (apps/api, FastAPI) + /scalar OpenAPI reference",
      "disposition": "interface",
      "detail": "HTTP (REST) API"
    },
    {
      "mechanism": "Command-line interface (apps/cli, qrb)",
      "disposition": "interface",
      "detail": "Command-line interface (qrb)"
    },
    {
      "mechanism": "Web client surface (apps/web, Next.js)",
      "disposition": "interface",
      "detail": "Web frontend (catalog / playground / API reference)"
    },
    {
      "mechanism": "Terminal client surface / CLI TUI",
      "disposition": "excluded",
      "detail": "CLI is a Typer command app with printed output; no persistent navigable TUI is exposed, so no separate Interactive interface."
    },
    {
      "mechanism": "Mobile client surface",
      "disposition": "excluded",
      "detail": "No first-party mobile app documented in the repo, product pages, or app-store listing."
    },
    {
      "mechanism": "Desktop client surface",
      "disposition": "excluded",
      "detail": "No first-party desktop GUI application shipped; the desktop entry points are the CLI and the browser-based web app."
    },
    {
      "mechanism": "Webhooks / events / inbound routing",
      "disposition": "excluded",
      "detail": "Generated OpenAPI schema declares webhooks as empty (Record<string, never>); API is request/response only, with no SSE, websocket, or event delivery to a consumer-controlled receiver."
    },
    {
      "mechanism": "Conversational / chat / AI assistant",
      "disposition": "excluded",
      "detail": "No natural-language message interface; the web Playground is a form/editor, not a chat surface."
    },
    {
      "mechanism": "MCP / agent / protocol interface",
      "disposition": "excluded",
      "detail": "No MCP server or capability-discovery-and-selection contract exists. (apps/web/AGENTS.md and CLAUDE.md are coding-agent instructions for repo development, not an access mechanism into the service.)"
    },
    {
      "mechanism": "Integrations (IBM Quantum, Amazon Braket)",
      "disposition": "excluded",
      "detail": "These are upstream providers whose catalogs QRB reads; they are outbound integrations, not ways of accessing QRB. README: 'QRB never submits jobs — selection only.'"
    },
    {
      "mechanism": "openbinding (typed Python client for the OpenBinding gateway)",
      "disposition": "excluded",
      "detail": "Client library, not a provider-defined interface; also a client to a separate external gateway service."
    },
    {
      "mechanism": "qrb (core library / SDK)",
      "disposition": "excluded",
      "detail": "Python library consumed by the CLI and API; libraries are not counted as interfaces."
    },
    {
      "mechanism": "qrb-store (Postgres persistence)",
      "disposition": "excluded",
      "detail": "Data store for binding decisions and telemetry; not a consumer-facing access mechanism."
    },
    {
      "mechanism": "poller (catalog telemetry sampler)",
      "disposition": "excluded",
      "detail": "Internal long-running background job that samples the catalog and writes to qrb-store; exposes no consumer-facing interface."
    }
  ],
  "channel_evidence": {
    "Interactive": "observed",
    "Agentic": "no_evidence_observed",
    "Conversational": "no_evidence_observed",
    "Event": "no_evidence_observed",
    "Programmatic": "observed"
  },
  "number_of_interfaces": 3,
  "multi_interface": true,
  "number_of_channels": 2,
  "multi_channel": true
}
```
