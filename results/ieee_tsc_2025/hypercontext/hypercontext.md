## Clasificación de interfaces

| Interfaz                         | Canal        | Tecnología de interacción                                                                           | Procedencia                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| -------------------------------- | ------------ | --------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Cliente gráfico de la aplicación | Interactive  | App web, apps móviles iOS/iPadOS y Android, app de escritorio macOS y extensión de navegador Chrome | La ficha de la tienda del propio proveedor (SoapBox Innovations) describe la app iOS/iPad y la "Hypercontext Mac App" con vistas navegables, agendas, calendario y notas: manipulación de affordances sobre el estado de la cuenta. El acceso web ("Continue with Google / Email / Microsoft") confirma el cliente web. Todas estas superficies comparten el mismo primitivo (manipulación de affordances), la misma base de estado de cuenta y la misma autenticación, por lo que constituyen una única interfaz lógica materializada en varias tecnologías. Frescura: clientes documentados en la etapa Hypercontext; proveedor ahora Spinach AI. |
| API HTTP de la cuenta            | Programmatic | Endpoint HTTP autenticado con una API key privada por cuenta                                        | El centro de ayuda del proveedor documenta la generación de una "private API KEY that will allow Zapier access to your Hypercontext account" y un formato de cuerpo estructurado (`next_step_id: ##`) para invocar operaciones como cerrar o crear next steps desde otra aplicación. El consumidor invoca operaciones definidas por el proveedor mediante solicitudes estructuradas, lo que fija el paradigma como Programmatic. El tipo de consumidor (Zapier) no determina el canal. Frescura/alcance: no se localizó una referencia de API pública independiente; la documentación se limita al contexto de la integración con Zapier.           |

## Cobertura de mecanismos de acceso

| Mecanismo de acceso                                                                                                                 | Disposición                                                                                                                                                                                                                     |
| ----------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Cliente web                                                                                                                         | Interfaz: Cliente gráfico de la aplicación (Interactive)                                                                                                                                                                        |
| App móvil (iOS/iPadOS, Android)                                                                                                     | Interfaz: Cliente gráfico de la aplicación (Interactive)                                                                                                                                                                        |
| App de escritorio (macOS)                                                                                                           | Interfaz: Cliente gráfico de la aplicación (Interactive)                                                                                                                                                                        |
| Extensión de Chrome                                                                                                                 | Interfaz: Cliente gráfico de la aplicación (Interactive)                                                                                                                                                                        |
| Cliente de terminal / CLI                                                                                                           | Excluido: no se encontró cliente de terminal de primera parte                                                                                                                                                                   |
| API HTTP / API key de cuenta                                                                                                        | Interfaz: API HTTP de la cuenta (Programmatic)                                                                                                                                                                                  |
| Webhooks / eventos / triggers salientes                                                                                             | Excluido: sin evidencia oficial de una interfaz nativa de eventos con receptor controlado por el consumidor; la entrega tipo evento está mediada por la integración de terceros Zapier                                          |
| Asistente conversacional / IA / comandos de voz                                                                                     | Excluido: sin evidencia oficial de una interfaz de lenguaje natural dentro del contrato del producto Hypercontext; los comandos de voz se documentan en el asistente de reuniones de Spinach, fuera del alcance de Hypercontext |
| Envío por SMTP / correo                                                                                                             | Excluido: el envío automático de notas es una función de notificación saliente, no una interfaz invocable por el consumidor                                                                                                     |
| Integraciones de terceros (Slack, Teams, Google Calendar/Meet, Outlook, Zoom, Jira, Asana, Linear, Airtable, Zapier con 3000+ apps) | Excluido: integraciones de terceros, no interfaces lógicas definidas por el proveedor                                                                                                                                           |
| Paquete "hypercontext" en PyPI / framework de agentes                                                                               | Excluido: colisión de nombres, proyecto distinto y sin relación                                                                                                                                                                 |

## Cobertura por canal

| Canal          | Evidencia               |
| -------------- | ----------------------- |
| Interactive    | Observado               |
| Agentic        | Sin evidencia observada |
| Conversational | Sin evidencia observada |
| Event          | Sin evidencia observada |
| Programmatic   | Observado               |

## Notas de clasificación

La procedencia de la interfaz Programmatic es limitada: la API con clave por cuenta está descrita solo en el contexto de la integración con Zapier, sin una referencia de API pública localizable. El paradigma es claro (invocación de operaciones mediante solicitudes estructuradas), por lo que se clasifica como Programmatic en lugar de Unclassified, con la salvedad de alcance anotada. Además, la migración de Hypercontext hacia Spinach AI introduce incertidumbre de frescura sobre la vigencia de los clientes móviles, de escritorio y de extensión documentados en la etapa Hypercontext. No hay conflicto de evidencia que impida una clasificación confiable en ninguna de las dos interfaces.

## Veredicto multicanal

**Multichannel** (2 paradigmas distintos observados: Interactive y Programmatic).

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
  "saas": {
    "name": "Hypercontext"
  },
  "interfaces": [
    {
      "name": "Graphical application client",
      "technology": "Web app, iOS/iPadOS and Android mobile apps, macOS desktop app, Chrome browser extension",
      "channel": "Interactive",
      "classification_rationale": "Actions are expressed by manipulating presented affordances (agendas, notes, calendar views, controls) of a persistent, navigable representation of the account's service state. All client surfaces share the same primitive, base state, and authentication, so they form one logical interface materialized across technologies.",
      "provenance": [
        {
          "url": "https://apps.apple.com/us/app/hypercontext/id1572485643",
          "evidence": "Provider (SoapBox Innovations) app-store listing describing the iOS/iPad app and the 'Hypercontext Mac App' with navigable menu-bar calendar, agendas, notes and next steps: affordance-manipulation UI. Freshness: Hypercontext-era clients; provider now Spinach AI."
        },
        {
          "url": "https://www.spinach.ai/hypercontext",
          "evidence": "Provider web login ('Hypercontext is now Spinach AI', Continue with Google/Email/Microsoft) confirms the web application client."
        }
      ]
    },
    {
      "name": "Account HTTP API",
      "technology": "HTTP endpoint authenticated with a private per-account API key",
      "channel": "Programmatic",
      "classification_rationale": "The consumer explicitly invokes provider-defined operations (create/close next steps) through structured HTTP requests authenticated by a per-account API key. Operation invocation via structured requests fixes the paradigm as Programmatic; the consumer type (Zapier) does not determine the channel.",
      "provenance": [
        {
          "url": "https://help.hypercontext.com/en/articles/4211687-common-problems-with-hypercontext-app-integration-with-zapier",
          "evidence": "Provider help center documents generating a private account API key and a structured request body format (next_step_id: ##) to invoke next-step operations from another application. Scope/freshness: no standalone public API reference located; documentation confined to the Zapier integration context."
        }
      ]
    }
  ],
  "access_mechanism_ledger": [
    {
      "mechanism": "Web client",
      "disposition": "interface",
      "detail": "Graphical application client"
    },
    {
      "mechanism": "Mobile app (iOS/iPadOS, Android)",
      "disposition": "interface",
      "detail": "Graphical application client"
    },
    {
      "mechanism": "Desktop app (macOS)",
      "disposition": "interface",
      "detail": "Graphical application client"
    },
    {
      "mechanism": "Chrome extension",
      "disposition": "interface",
      "detail": "Graphical application client"
    },
    {
      "mechanism": "Terminal / CLI client",
      "disposition": "excluded",
      "detail": "No first-party terminal client found"
    },
    {
      "mechanism": "Account HTTP API / API key",
      "disposition": "interface",
      "detail": "Account HTTP API"
    },
    {
      "mechanism": "Webhooks / events / outbound triggers",
      "disposition": "excluded",
      "detail": "No official evidence of a native event/webhook interface with a consumer-controlled receiver; event-like delivery is mediated by the third-party Zapier integration"
    },
    {
      "mechanism": "Conversational / AI assistant / voice commands",
      "disposition": "excluded",
      "detail": "No official evidence of a natural-language interface within the Hypercontext product contract; voice commands are documented under Spinach's meeting assistant, out of Hypercontext scope"
    },
    {
      "mechanism": "SMTP / email submission",
      "disposition": "excluded",
      "detail": "Automated note emails are an outbound notification feature, not a consumer-invocable interface"
    },
    {
      "mechanism": "Third-party integrations (Slack, Teams, Google Calendar/Meet, Outlook, Zoom, Jira, Asana, Linear, Airtable, Zapier 3000+ apps)",
      "disposition": "excluded",
      "detail": "Third-party integrations, not provider-defined logical interfaces"
    },
    {
      "mechanism": "PyPI 'hypercontext' package / agent framework",
      "disposition": "excluded",
      "detail": "Name collision; unrelated project"
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
