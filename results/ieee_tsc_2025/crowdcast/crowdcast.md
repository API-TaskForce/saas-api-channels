## Resumen del SaaS

Crowdcast (Crowdcast Inc.) es una plataforma de vídeo en directo para webinars, cursos, Q&A, shows y cumbres online, basada en navegador. Del examen de sus fuentes oficiales se reconstruyen **3 interfaces lógicas provider-defined**, repartidas en **2 canales distintos** con al menos una interfaz clasificada.

## Tabla de clasificación de interfaces

| Interfaz                          | Canal        | Tecnología de interacción                        | Procedencia                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| --------------------------------- | ------------ | ------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Aplicación web (host y asistente) | Interactive  | SPA en navegador (WebRTC/HLS)                    | La guía oficial describe una plataforma en navegador donde el usuario opera afdordances de una representación navegable del evento: registro, chat, Q&A estructurado, encuestas, CTA, compartir pantalla y el control "Go Live". El primitivo es la manipulación de controles presentados; el control lo lleva el usuario sobre una vista persistente. Fuente actual (docs.crowdcast.io, "How to Run Webinars", y "Which browsers and devices", act. ago. 2026).                                                                          |
| Aplicación móvil (iOS/Android)    | Interactive  | Cliente nativo móvil                             | Ficha oficial de la App Store de Crowdcast Inc. ("Crowdcast Mobile") y la documentación de compatibilidad confirman un cliente nativo de primera parte para unirse al evento e interactuar (chat, encuestas, upvote de preguntas). Mismo paradigma de manipulación de affordances que la web, sobre una superficie y runtime distintos, por lo que se contabiliza como interfaz separada según el checklist de superficies cliente. Fuente actual (App Store id1119071572; docs.crowdcast.io, act. ago. 2026).                            |
| Ingesta RTMP (RTMP Mode)          | Programmatic | Publicación RTMP/RTMPS a Server URL + Stream Key | La documentación oficial de RTMP Mode indica que el consumidor obtiene una Server URL y una Stream Key y publica un flujo desde un encoder externo (OBS, Wirecast, Ecamm, vMix). Es una invocación estructurada de una operación de publicación contra un endpoint provider-defined, análoga a la submission SMTP o al push a un remoto Git. El primitivo es la operación de publicación; el consumidor la inicia explícitamente. Fuente actual (docs.crowdcast.io, "Connecting Live Streaming Software With RTMP Mode", act. jun. 2026). |

## Ledger de cobertura

| Mecanismo de acceso                                                       | Disposición                                                                                                                                                                                                                                                                                             |
| ------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Aplicación web en navegador                                               | Interfaz: Aplicación web (Interactive)                                                                                                                                                                                                                                                                  |
| App móvil iOS/Android (primera parte)                                     | Interfaz: Aplicación móvil (Interactive)                                                                                                                                                                                                                                                                |
| RTMP Mode (ingesta de encoders externos)                                  | Interfaz: Ingesta RTMP (Programmatic)                                                                                                                                                                                                                                                                   |
| Cliente de escritorio de primera parte                                    | Excluido: no se encuentra app de escritorio nativa; el hosting y la asistencia se realizan por navegador.                                                                                                                                                                                               |
| CLI / TUI                                                                 | Excluido: no existe interfaz de línea de comandos ni panel TUI documentado.                                                                                                                                                                                                                             |
| Asistente conversacional / IA de Crowdcast                                | Excluido: no se documenta ningún asistente de lenguaje natural propio de la plataforma.                                                                                                                                                                                                                 |
| Integración con Zapier (con API key generada en Settings)                 | Excluido: plataforma de integración de terceros. La API subyacente es de alcance partner y se documenta solo para conectar Zapier, sin referencia pública de operaciones, base y autenticación que permita reconstruir una interfaz Programmatic directamente consumible.                               |
| API nativa / webhooks (triggers de registro, pregunta, sesión finalizada) | Excluido: solo se exponen a través de Zapier. Las fuentes provider-controlled no establecen si Crowdcast envía estos eventos por webhooks nativos push o si Zapier hace polling de la API, de modo que no se establece una interfaz Event nativa. La ausencia de evidencia no es evidencia de ausencia. |
| Integraciones directas Stripe y Patreon                                   | Excluido: integraciones de terceros para pagos y acceso por membresía; no son un mecanismo de acceso al propio servicio.                                                                                                                                                                                |
| Embed del evento en sitios externos                                       | Excluido: instancia embebida de la aplicación web; mismo contrato de interacción, no una interfaz distinta.                                                                                                                                                                                             |
| Multistreaming a YouTube/Facebook (RTMP saliente)                         | Excluido: función de retransmisión saliente desde Crowdcast hacia terceros; no es una vía para acceder a Crowdcast.                                                                                                                                                                                     |

## Cobertura por canal

| Canal          | Evidencia            |
| -------------- | -------------------- |
| Interactive    | Observed             |
| Agentic        | No evidence observed |
| Conversational | No evidence observed |
| Event          | No evidence observed |
| Programmatic   | Observed             |

## Veredicto multicanal

`Multichannel` (2 paradigmas distintos observados: Interactive y Programmatic).

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
    "name": "Crowdcast"
  },
  "interfaces": [
    {
      "name": "Web application",
      "technology": "Browser-based SPA (WebRTC/HLS)",
      "channel": "Interactive",
      "classification_rationale": "Actions are expressed by manipulating presented affordances (registration, chat, Q&A, polls, CTA, screen share, Go Live) of a persistent navigable representation of the event; primitive is affordance manipulation with consumer-driven control.",
      "provenance": [
        {
          "url": "https://docs.crowdcast.io/en/articles/10622496-how-to-run-webinars-on-crowdcast",
          "evidence": "Official guide describing the browser-based hosting UI and its interactive engagement controls."
        },
        {
          "url": "https://docs.crowdcast.io/en/articles/7257749-which-browsers-and-devices-are-compatible-with-crowdcast",
          "evidence": "Current (Aug 2026) provider doc confirming browser-based access for hosts and attendees."
        }
      ]
    },
    {
      "name": "Mobile app",
      "technology": "Native iOS/Android client",
      "channel": "Interactive",
      "classification_rationale": "First-party native client where the consumer manipulates on-screen affordances (chat, polls, upvote questions) of the event representation; same paradigm as web on a distinct client surface and runtime.",
      "provenance": [
        {
          "url": "https://apps.apple.com/us/app/crowdcast-mobile/id1119071572",
          "evidence": "Provider (Crowdcast Inc.) App Store listing for the first-party mobile client."
        },
        {
          "url": "https://docs.crowdcast.io/en/articles/7257749-which-browsers-and-devices-are-compatible-with-crowdcast",
          "evidence": "Current provider doc stating attendees can use the Crowdcast app for Android or iOS."
        }
      ]
    },
    {
      "name": "RTMP ingest (RTMP Mode)",
      "technology": "RTMP/RTMPS publish to Server URL + Stream Key",
      "channel": "Programmatic",
      "classification_rationale": "The consumer explicitly invokes a provider-defined publish operation, pushing a stream from an external encoder to a provider ingest endpoint identified by Server URL and Stream Key, analogous to SMTP submission or Git remote push.",
      "provenance": [
        {
          "url": "https://docs.crowdcast.io/en/articles/7260494-connecting-live-streaming-software-with-rtmp-mode",
          "evidence": "Current (Jun 2026) official RTMP Mode doc defining the ingest endpoint and stream key publishing flow from OBS, Wirecast, Ecamm, vMix."
        }
      ]
    }
  ],
  "access_mechanism_ledger": [
    {
      "mechanism": "Web application (browser)",
      "disposition": "interface",
      "detail": "Web application (Interactive)"
    },
    {
      "mechanism": "Mobile app (iOS/Android, first-party)",
      "disposition": "interface",
      "detail": "Mobile app (Interactive)"
    },
    {
      "mechanism": "RTMP Mode ingest",
      "disposition": "interface",
      "detail": "RTMP ingest (Programmatic)"
    },
    {
      "mechanism": "First-party desktop client",
      "disposition": "excluded",
      "detail": "No native desktop app found; hosting and attending are done via browser."
    },
    {
      "mechanism": "CLI / TUI",
      "disposition": "excluded",
      "detail": "No command-line interface or TUI dashboard documented."
    },
    {
      "mechanism": "Conversational / AI assistant",
      "disposition": "excluded",
      "detail": "No first-party natural-language assistant documented."
    },
    {
      "mechanism": "Zapier integration (with generated API key)",
      "disposition": "excluded",
      "detail": "Third-party integration platform; underlying API is partner-scoped and documented only for Zapier, with no public operation/base/auth reference to reconstruct a directly consumable Programmatic interface."
    },
    {
      "mechanism": "Native API / event webhooks (registration, question, session-ended triggers)",
      "disposition": "excluded",
      "detail": "Surfaced only through Zapier; provider sources do not establish native push webhooks versus Zapier polling, so no Event interface is established. No evidence is not absence."
    },
    {
      "mechanism": "Stripe and Patreon direct integrations",
      "disposition": "excluded",
      "detail": "Third-party integrations for payments and membership access; not a mechanism for accessing the service."
    },
    {
      "mechanism": "Event embed on external sites",
      "disposition": "excluded",
      "detail": "Embedded instance of the web application; same interaction contract, not a distinct interface."
    },
    {
      "mechanism": "Multistreaming to YouTube/Facebook (outbound RTMP)",
      "disposition": "excluded",
      "detail": "Outbound restream feature from Crowdcast to third parties; not a way to access Crowdcast."
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
