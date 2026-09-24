## SaaS summary

**OpenPhone** (rebranded **Quo** in 2026) is a business phone and team-communication platform. Investigation of its official documentation identifies **6 logical interfaces** spread across **4 distinct access channels**.

## Interface classification

| Interface         | Channel      | Interaction technology                      | Provenance                                                                                                                                                                                                                                                                                                                                                                                        |
| ----------------- | ------------ | ------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Web app           | Interactive  | Browser web application                     | Official install page states Quo runs in the browser with no installation; the product presents a navigable shared-inbox workspace. Actions are affordance manipulation over persistent service state. Current.                                                                                                                                                                                   |
| Mobile app        | Interactive  | Native iOS and Android apps                 | Install page offers iPhone/iPad and Android downloads; first-party App Store listing is published by OpenPhone Technologies Inc. Same touch-client paradigm across both platforms, so one interface. Current.                                                                                                                                                                                     |
| Desktop app       | Interactive  | Native macOS and Windows apps               | Install page offers Mac and PC downloads; provider blog documents the native Windows client. Same navigable workspace presented on the desktop. Current.                                                                                                                                                                                                                                          |
| REST API          | Programmatic | HTTPS REST API (JSON), API-key auth         | Provider states the API is built around REST, returns JSON, and authenticates with API keys. The consumer explicitly invokes provider-defined operations (messages, calls, contacts, conversations, tasks, numbers, users, webhook management) at a fixed base under one auth scheme. Current.                                                                                                    |
| Webhooks          | Event        | HTTP event callbacks                        | Official docs describe real-time notifications for call, message, and transcript events delivered to developer endpoints. The service initiates delivery on subscribed events to a consumer-controlled receiver. App-created and API-created webhooks share this push paradigm, so one interface. Current.                                                                                        |
| Quo MCP connector | Agentic      | Model Context Protocol server (remote, SSE) | Provider docs describe an official MCP connector giving Claude and ChatGPT direct access to the workspace via mcp.quo.com/sse. Semantically described capabilities are discovered and selected by the assistant, which structures the contract as capability discovery rather than fixed operation invocation. It began as an experimental beta and is now a certified native connector. Current. |

## Coverage ledger

| Access mechanism                                                                                           | Disposition                                                                                                                                                                                        |
| ---------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Web client (browser)                                                                                       | Web app                                                                                                                                                                                            |
| Mobile app (iOS / iPad)                                                                                    | Mobile app                                                                                                                                                                                         |
| Mobile app (Android / tablet)                                                                              | Mobile app                                                                                                                                                                                         |
| Desktop app (macOS)                                                                                        | Desktop app                                                                                                                                                                                        |
| Desktop app (Windows)                                                                                      | Desktop app                                                                                                                                                                                        |
| REST API                                                                                                   | REST API                                                                                                                                                                                           |
| Webhooks (API-created and app-created)                                                                     | Webhooks                                                                                                                                                                                           |
| Quo MCP connector (mcp.quo.com)                                                                            | Quo MCP connector                                                                                                                                                                                  |
| CLI                                                                                                        | Excluded: no first-party command-line interface found in official documentation.                                                                                                                   |
| TUI dashboard                                                                                              | Excluded: no CLI exists, so no persistent navigable terminal interface.                                                                                                                            |
| GraphQL API                                                                                                | Excluded: only a REST API is offered; no separate GraphQL endpoint documented.                                                                                                                     |
| SMTP / email relay                                                                                         | Excluded: Quo is a voice and SMS/MMS platform; no email-submission interface is offered.                                                                                                           |
| Sona AI agent / AI receptionist / auto attendant / call flows                                              | Excluded: service functionality that answers and routes the customer's own callers, configured through the GUI; not a provider-defined interface for a consumer to access and operate the service. |
| Inbound calling and SMS to Quo numbers (PSTN)                                                              | Excluded: the delivered product function; account holders access and handle these communications through the GUI, API, and webhooks classified above.                                              |
| Third-party integrations index (Slack, HubSpot, Salesforce, Pipedrive, Zapier, Make, Pipedream, viaSocket) | Excluded: third-party integrations and connectors, not provider-defined interfaces; built on the REST API and webhooks.                                                                            |
| SDKs / client libraries                                                                                    | Excluded: wrappers over the REST API, not interfaces in their own right.                                                                                                                           |

## Channel coverage

| Channel        | Evidence             |
| -------------- | -------------------- |
| Interactive    | Observed             |
| Agentic        | Observed             |
| Conversational | No evidence observed |
| Event          | Observed             |
| Programmatic   | Observed             |

## Classification notes

The Quo MCP connector is the one call worth flagging. It resolves to **Agentic** rather than **Conversational** because the natural-language layer lives in the third-party assistant (Claude or ChatGPT), while the contract Quo itself exposes is a set of discoverable, selectable capabilities. It resolves to Agentic rather than **Programmatic** because capability discovery and selection are part of that contract, not fixed endpoint invocation. Its status has shifted from experimental beta to a certified native connector, so the present-day classification rests on current official sources.

## Multichannel verdict

**Multichannel** (4 distinct paradigms observed).

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
    "name": "OpenPhone (Quo)"
  },
  "interfaces": [
    {
      "name": "Web app",
      "technology": "Browser web application",
      "channel": "Interactive",
      "classification_rationale": "Actions are expressed by manipulating presented affordances (shared inbox, conversations, contacts, settings) over a persistent, navigable representation of workspace state.",
      "provenance": [
        {
          "url": "https://support.quo.com/getting-started/install-apps",
          "evidence": "Official install page: 'Use Quo on your browser - no installation needed', establishing a first-party web client. Current."
        },
        {
          "url": "https://www.quo.com/",
          "evidence": "Product site lists availability on Web alongside a shared-inbox workspace UI. Current."
        }
      ]
    },
    {
      "name": "Mobile app",
      "technology": "Native iOS and Android apps",
      "channel": "Interactive",
      "classification_rationale": "A first-party touch client where the consumer operates the service by manipulating on-screen affordances of the same navigable workspace; same interaction paradigm across iOS and Android, so one logical interface.",
      "provenance": [
        {
          "url": "https://support.quo.com/getting-started/install-apps",
          "evidence": "Official install page offers iPhone/iPad and Android downloads. Current."
        },
        {
          "url": "https://apps.apple.com/us/app/quo-formerly-openphone/id1241817309",
          "evidence": "First-party App Store listing published by OpenPhone Technologies Inc. Current."
        }
      ]
    },
    {
      "name": "Desktop app",
      "technology": "Native macOS and Windows apps",
      "channel": "Interactive",
      "classification_rationale": "A first-party desktop client presenting the same navigable workspace; actions are affordance manipulation. One logical interface across macOS and Windows.",
      "provenance": [
        {
          "url": "https://support.quo.com/getting-started/install-apps",
          "evidence": "Official install page offers Mac and PC downloads. Current."
        },
        {
          "url": "https://www.quo.com/blog/openphone-update-december-2021",
          "evidence": "Provider blog documents the native Windows desktop app running in its own process. Historical announcement, client remains current per install page."
        }
      ]
    },
    {
      "name": "REST API",
      "technology": "HTTPS REST API (JSON), API-key auth",
      "channel": "Programmatic",
      "classification_rationale": "The consumer explicitly invokes provider-defined operations (send messages, list/retrieve calls, manage contacts, conversations, tasks, phone numbers, users, webhooks) through structured HTTP requests against a fixed base and single auth scheme.",
      "provenance": [
        {
          "url": "https://www.openphone.com/product/api",
          "evidence": "Provider states the API is built around REST, returns JSON, and uses API keys for authentication. Current."
        },
        {
          "url": "https://www.openphone.com/docs/guides/webhooks",
          "evidence": "Official developer docs describe the versioned API surface and payloads. Current."
        }
      ]
    },
    {
      "name": "Webhooks",
      "technology": "HTTP event callbacks",
      "channel": "Event",
      "classification_rationale": "The service initiates the interaction when subscribed events occur (call.ringing, call.completed, message and transcript events) and pushes structured payloads to a consumer-controlled receiver.",
      "provenance": [
        {
          "url": "https://www.openphone.com/docs/guides/webhooks",
          "evidence": "Official docs: webhooks deliver real-time notifications for calls, messages, and transcripts to developer endpoints; both app-created and API-created webhooks exist, sharing the same push-delivery paradigm. Current."
        }
      ]
    },
    {
      "name": "Quo MCP connector",
      "technology": "Model Context Protocol server (remote, SSE)",
      "channel": "Agentic",
      "classification_rationale": "An official MCP server exposes semantically described capabilities (send messages, pull transcripts, look up and update contacts) that an AI assistant discovers and selects by goal; capability discovery and selection structure the interaction contract, so Agentic rather than Programmatic. Natural-language interpretation happens in the third-party assistant, not in Quo's contract.",
      "provenance": [
        {
          "url": "https://www.quo.com/docs/2026-03-30/ai-agents",
          "evidence": "Provider docs: 'Quo ships an official MCP (Model Context Protocol) connector ... that gives Claude and ChatGPT direct access to your workspace.' Current."
        },
        {
          "url": "https://support.quo.com/core-concepts/integrations/mcp",
          "evidence": "Resource center: Quo is an official connector for Claude and ChatGPT; capabilities invoked in plain language. Began as an experimental beta and is now a certified native connector. Current."
        },
        {
          "url": "https://mcp.quo.com/",
          "evidence": "First-party MCP endpoint https://mcp.quo.com/sse with Quo API-key/OAuth authentication. Current."
        }
      ]
    }
  ],
  "access_mechanism_ledger": [
    {
      "mechanism": "Web client (browser)",
      "disposition": "interface",
      "detail": "Web app"
    },
    {
      "mechanism": "Mobile app (iOS / iPad)",
      "disposition": "interface",
      "detail": "Mobile app"
    },
    {
      "mechanism": "Mobile app (Android / tablet)",
      "disposition": "interface",
      "detail": "Mobile app"
    },
    {
      "mechanism": "Desktop app (macOS)",
      "disposition": "interface",
      "detail": "Desktop app"
    },
    {
      "mechanism": "Desktop app (Windows)",
      "disposition": "interface",
      "detail": "Desktop app"
    },
    {
      "mechanism": "REST API",
      "disposition": "interface",
      "detail": "REST API"
    },
    {
      "mechanism": "Webhooks (API-created and app-created)",
      "disposition": "interface",
      "detail": "Webhooks"
    },
    {
      "mechanism": "Quo MCP connector (mcp.quo.com)",
      "disposition": "interface",
      "detail": "Quo MCP connector"
    },
    {
      "mechanism": "CLI",
      "disposition": "excluded",
      "detail": "No first-party command-line interface found in official documentation."
    },
    {
      "mechanism": "TUI dashboard",
      "disposition": "excluded",
      "detail": "No CLI exists, so no persistent navigable terminal interface."
    },
    {
      "mechanism": "GraphQL API",
      "disposition": "excluded",
      "detail": "Only a REST API is offered; no separate GraphQL endpoint documented."
    },
    {
      "mechanism": "SMTP / email relay",
      "disposition": "excluded",
      "detail": "Quo is a voice and SMS/MMS platform; no email-submission interface is offered."
    },
    {
      "mechanism": "Sona AI agent / AI receptionist / auto attendant / call flows",
      "disposition": "excluded",
      "detail": "Service functionality that answers and routes the customer's own callers, configured through the GUI; not a provider-defined interface for a consumer to access and operate the Quo service."
    },
    {
      "mechanism": "Inbound calling and SMS to Quo numbers (PSTN)",
      "disposition": "excluded",
      "detail": "This is the delivered product function (the business's contacts reaching it); account holders access and handle these communications through the GUI, API, and webhooks, which are the interfaces classified above."
    },
    {
      "mechanism": "Third-party integrations index (Slack, HubSpot, Salesforce, Pipedrive, Zapier, Make, Pipedream, viaSocket, etc.)",
      "disposition": "excluded",
      "detail": "Third-party integrations and connectors, not provider-defined interfaces; they are built on the REST API and webhooks."
    },
    {
      "mechanism": "SDKs / client libraries",
      "disposition": "excluded",
      "detail": "Wrappers over the REST API, not interfaces in their own right."
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
