# Análisis de canales de acceso: OpenBinding

## Resumen del SaaS

**OpenBinding** (ISA Group, Universidad de Sevilla) es una pasarela de composición de servicios con conciencia de QoS y un marco de motores solucionadores. Se identifican **2 interfaces lógicas** provistas por el proveedor, repartidas en **2 canales distintos**.

## Tabla de clasificación de interfaces

| Interfaz                                     | Canal        | Tecnología de interacción                          | Procedencia                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| -------------------------------------------- | ------------ | -------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Frontend web (SPA)                           | Interactive  | React + Vite, servido en `openbinding.score.us.es` | README oficial (isa-group/OpenBinding): describe el frontend como una SPA multipágina con Home, Playground (editor JSON, selector de motor, visualización de resultados), Engines Explorer y Schema Explorer. El primitivo es la manipulación de affordances (vistas, editores, selectores) sobre una representación navegable y persistente del estado del servicio, lo que satisface el primer nodo del árbol de decisión. Evidencia actual.              |
| API del Gateway (`/v1/solve`, `/v1/analyze`) | Programmatic | Servicio Python FastAPI sobre HTTP/JSON            | README oficial: el Gateway es el punto de entrada que valida esquemas, enruta a los motores y responde de forma síncrona (`HTTP 200`, o `422` en fallo de validación). El ejemplo de uso muestra `POST /v1/solve` con cuerpo JSON estructurado. El consumidor invoca explícitamente operaciones definidas por el proveedor mediante peticiones estructuradas, sin descubrimiento de capacidades ni contrato basado en eventos o mensajes. Evidencia actual. |

## Tabla del registro de cobertura

| Mecanismo de acceso                                                  | Disposición                                                                                                                                                     |
| -------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Frontend web (React/Vite SPA)                                        | Interfaz: Frontend web (Interactive)                                                                                                                            |
| API del Gateway (FastAPI, `/v1/solve`, `/v1/analyze`)                | Interfaz: API del Gateway (Programmatic)                                                                                                                        |
| Documentación interactiva de la API (`/docs`, Swagger UI de FastAPI) | Excluido: página de documentación autogenerada del API programático, no una interfaz lógica con contrato propio                                                 |
| Motores solucionadores (MiniZinc CSP, Random Search, Many-Heuristic) | Excluido: componentes internos enrutados por el Gateway; no son mecanismos de acceso orientados al consumidor                                                   |
| Ejemplos con `curl` en el README                                     | Excluido: no es una CLI de primera parte, solo ilustra llamadas HTTP a la API programática                                                                      |
| Cliente móvil de primera parte                                       | Excluido: sin evidencia en fuentes oficiales                                                                                                                    |
| Cliente de escritorio de primera parte                               | Excluido: sin evidencia en fuentes oficiales                                                                                                                    |
| CLI / TUI de primera parte                                           | Excluido: sin evidencia de una CLI propia; los comandos `docker`, `npm`, `mvn`, `uvicorn` son herramientas de desarrollo, no una interfaz de acceso al servicio |
| Webhooks / eventos / entrega inbound                                 | Excluido: sin evidencia; el Gateway responde de forma síncrona, no inicia entregas por eventos                                                                  |
| Interfaz conversacional / chat / asistente IA                        | Excluido: sin evidencia en fuentes oficiales                                                                                                                    |
| MCP / protocolo de agente                                            | Excluido: sin evidencia en fuentes oficiales                                                                                                                    |

## Tabla de cobertura de canales

| Canal          | Evidencia               |
| -------------- | ----------------------- |
| Interactive    | Observado               |
| Agentic        | Sin evidencia observada |
| Conversational | Sin evidencia observada |
| Event          | Sin evidencia observada |
| Programmatic   | Observado               |

## Veredicto multicanal

`Multicanal` (2 paradigmas distintos observados: Interactive y Programmatic).

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
  "saas": {
    "name": "OpenBinding"
  },
  "interfaces": [
    {
      "name": "Web frontend (SPA)",
      "technology": "React + Vite single-page web application",
      "channel": "Interactive",
      "classification_rationale": "Actions are expressed by manipulating presented affordances (JSON editor, engine selector, schema explorer, result views) over a persistent, navigable representation of service state.",
      "provenance": [
        {
          "url": "https://github.com/isa-group/OpenBinding",
          "evidence": "Official README describes the frontend as a React + Vite multi-page SPA with Home, Playground, Engines Explorer and Schema Explorer, served at openbinding.score.us.es."
        }
      ]
    },
    {
      "name": "Gateway API (/v1/solve, /v1/analyze)",
      "technology": "Python FastAPI service over HTTP/JSON",
      "channel": "Programmatic",
      "classification_rationale": "The consumer explicitly invokes provider-defined operations through structured HTTP/JSON requests; the gateway validates, routes and returns synchronous results, with no capability discovery, message interpretation or event-driven contract.",
      "provenance": [
        {
          "url": "https://github.com/isa-group/OpenBinding",
          "evidence": "Official README documents the FastAPI gateway as the entry point and shows a POST /v1/solve example with a structured JSON body; enhanced validation responses cover /v1/analyze and /v1/solve."
        }
      ]
    }
  ],
  "access_mechanism_ledger": [
    {
      "mechanism": "Web frontend (React/Vite SPA)",
      "disposition": "interface",
      "detail": "Web frontend (SPA)"
    },
    {
      "mechanism": "Gateway API (FastAPI, /v1/solve, /v1/analyze)",
      "disposition": "interface",
      "detail": "Gateway API (/v1/solve, /v1/analyze)"
    },
    {
      "mechanism": "Interactive API docs (/docs, FastAPI Swagger UI)",
      "disposition": "excluded",
      "detail": "Auto-generated documentation page for the programmatic API, not a distinct logical interface with its own contract."
    },
    {
      "mechanism": "Solver engines (MiniZinc CSP, Random Search, Many-Heuristic)",
      "disposition": "excluded",
      "detail": "Internal components routed by the gateway; not consumer-facing access mechanisms."
    },
    {
      "mechanism": "curl examples in README",
      "disposition": "excluded",
      "detail": "Not a first-party CLI; only illustrates HTTP calls to the programmatic API."
    },
    {
      "mechanism": "First-party mobile client",
      "disposition": "excluded",
      "detail": "No evidence in official sources."
    },
    {
      "mechanism": "First-party desktop client",
      "disposition": "excluded",
      "detail": "No evidence in official sources."
    },
    {
      "mechanism": "First-party CLI / TUI",
      "disposition": "excluded",
      "detail": "No provider CLI; docker/npm/mvn/uvicorn commands are development tooling, not a service access interface."
    },
    {
      "mechanism": "Webhooks / events / inbound delivery",
      "disposition": "excluded",
      "detail": "No evidence; the gateway responds synchronously and does not initiate event-driven delivery."
    },
    {
      "mechanism": "Conversational / chat / AI assistant",
      "disposition": "excluded",
      "detail": "No evidence in official sources."
    },
    {
      "mechanism": "MCP / agent protocol",
      "disposition": "excluded",
      "detail": "No evidence in official sources."
    }
  ],
  "channel_evidence": {
    "Interactive": "observed",
    "Agentic": "no_evidence_observed",
    "Conversational": "no_evidence_observed",
    "Event": "no_evidence_observed",
    "Programmatic": "observed"
  },
  "number_of_interfaces": 2,
  "multi_interface": true,
  "number_of_channels": 2,
  "multi_channel": true
}
```
