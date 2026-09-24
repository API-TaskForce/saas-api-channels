## SaaS summary

Canva, the visual design platform by Canva Pty Ltd. This analysis identifies **7 provider-defined logical interfaces** across **5 distinct access channels** with at least one classified interface each.

## Interface classification table

| Interface                                         | Channel        | Interaction technology                                        | Provenance                                                                                                                                                                                                                                                                                         |
| ------------------------------------------------- | -------------- | ------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Canva web editor                                  | Interactive    | Browser-based web app (canva.com)                             | Official product at canva.com presents a drag-and-drop design suite. Actions are affordance manipulation (canvas, menus, panels) over a persistent navigable workspace. Current.                                                                                                                   |
| Canva desktop app                                 | Interactive    | Native Windows/macOS client                                   | Canva Help Center and the Microsoft Store list an official desktop client with the same editor, native tabs, and offline mode. A distinct first-party client surface. Current.                                                                                                                     |
| Canva mobile app                                  | Interactive    | Native iOS/iPadOS/Android client                              | Canva download pages list official mobile apps alongside web and desktop. A touch GUI on a navigable representation of designs; a separate client surface. Current.                                                                                                                                |
| Canva AI assistant (Canva AI / Magic Studio chat) | Conversational | Conversational assistant with dedicated chat (text and voice) | canva.com/ai-assistant describes a conversational assistant with its own chat interface. The consumer-facing primitive is the natural-language message. Internal tool orchestration does not expose a discovery contract, so it is Conversational, not Agentic. Current.                           |
| Canva Connect REST API                            | Programmatic   | REST over HTTPS, OAuth 2.0 (PKCE)                             | canva.dev/docs/connect documents REST APIs to create and sync assets, designs, comments, exports, and templates via structured HTTP requests. Explicit operation invocation under one base and auth. Current.                                                                                      |
| Canva Connect webhooks                            | Event          | Outgoing HTTP webhooks                                        | canva.dev/docs/connect/webhooks: Canva initiates delivery of event data (comments, access requests, approvals, suggestions) as POST requests to a consumer-registered URL. Service-initiated, not polled. Marked preview.                                                                          |
| Canva remote MCP server (AI Connector)            | Agentic        | Remote Model Context Protocol server (mcp.canva.com)          | canva.dev/docs/mcp: a provider-hosted MCP server exposing design creation/editing, asset and brand management, search, export, and commenting as discoverable MCP tools an assistant selects by goal. Capability discovery structures the contract, so Agentic per the MCP boundary rule. Current. |

## Coverage ledger

| Access mechanism                                             | Disposition                                                                                                                                            |
| ------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Web client surface                                           | Interface: Canva web editor                                                                                                                            |
| Desktop client surface                                       | Interface: Canva desktop app                                                                                                                           |
| Mobile client surface                                        | Interface: Canva mobile app                                                                                                                            |
| Terminal / CLI client surface                                | Excluded: no first-party Canva CLI or navigable TUI found in official sources                                                                          |
| Connect REST API                                             | Interface: Canva Connect REST API                                                                                                                      |
| Webhooks / events                                            | Interface: Canva Connect webhooks                                                                                                                      |
| Canva remote MCP server / AI Connector                       | Interface: Canva remote MCP server (AI Connector)                                                                                                      |
| Canva AI / Magic Studio conversational assistant             | Interface: Canva AI assistant                                                                                                                          |
| Apps SDK (extensions / app platform)                         | Excluded: SDK/framework for building apps that run inside the editor; do-not-count list, not itself an access interface                                |
| Canva Dev MCP server                                         | Excluded: local developer tool exposing Canva's docs, examples, and helper tooling to coding agents; does not access the service's design capabilities |
| Canva Button (China only)                                    | Excluded: embeds the Interactive web editor into third-party sites (same paradigm); region-limited, not a distinct logical interface                   |
| SDKs / client libraries / OpenAPI-generated clients          | Excluded: do-not-count list; they support an interface without being one                                                                               |
| Third-party integrations (Zapier, Make, n8n, Composio, etc.) | Excluded: third-party automations and wrappers built on the Connect API or MCP; not provider-defined interfaces                                        |

## Channel coverage

| Channel        | Evidence |
| -------------- | -------- |
| Interactive    | Observed |
| Agentic        | Observed |
| Conversational | Observed |
| Event          | Observed |
| Programmatic   | Observed |

## Classification notes

Canva markets "Canva AI 2.0" (announced April 2026) using the word _agentic_ to describe internal autonomy, where the assistant interprets a brief and coordinates multiple tools. This does not change the channel. The classification turns on the consumer-facing interaction contract, whose primitive is the natural-language message and whose tool orchestration is internal to the service. Under the decision tree and the natural-language-assistant boundary rule, that is Conversational. The Agentic classification here belongs to the separate remote MCP server, where capability discovery and selection are exposed as part of the contract.

The Apps SDK, the Connect REST API, and the remote MCP server were recently unified under a single "Canva Developers SDK" umbrella. That is a documentation and packaging change, not a merge of interaction contracts. The REST API (operation invocation) and the MCP server (capability discovery) remain distinct logical interfaces in distinct channels.

## Multichannel verdict

`Multichannel` (5 distinct paradigms observed).

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
  "generated_at": "2026-09-23T00:00:00Z",
  "evidence_checked_at": "2026-09-23T00:00:00Z",
  "saas": { "name": "Canva" },
  "interfaces": [
    {
      "name": "Canva web editor",
      "technology": "Browser-based web application (canva.com)",
      "channel": "Interactive",
      "classification_rationale": "Actions are expressed by manipulating presented affordances (drag-and-drop canvas, menus, panels, forms) over a persistent navigable representation of the user's designs and assets.",
      "provenance": [
        {
          "url": "https://www.canva.com/",
          "evidence": "Official product describes a drag-and-drop design suite accessed at canva.com in the browser; affordance-manipulation editor."
        }
      ]
    },
    {
      "name": "Canva desktop app",
      "technology": "Native desktop client (Windows, macOS)",
      "channel": "Interactive",
      "classification_rationale": "A first-party native GUI presenting the same affordance-manipulation editor as a persistent navigable workspace, with native tabs and offline mode.",
      "provenance": [
        {
          "url": "https://www.canva.com/es_us/help/canva-desktop-app/",
          "evidence": "Canva Help Center documents an official desktop app for Windows and Mac."
        },
        {
          "url": "https://apps.microsoft.com/detail/xp8k17rnmm8mtn",
          "evidence": "Official Canva Windows app listing on the Microsoft Store."
        }
      ]
    },
    {
      "name": "Canva mobile app",
      "technology": "Native mobile client (iOS, iPadOS, Android)",
      "channel": "Interactive",
      "classification_rationale": "A first-party touch GUI whose actions are affordance manipulation on a navigable representation of designs; a distinct client surface from web and desktop.",
      "provenance": [
        {
          "url": "https://www.canva.com/es_us/descargar/windows/",
          "evidence": "Canva download pages list official iOS and Android apps alongside desktop."
        }
      ]
    },
    {
      "name": "Canva AI assistant (Canva AI / Magic Studio chat)",
      "technology": "Conversational assistant with dedicated chat interface (text and voice)",
      "channel": "Conversational",
      "classification_rationale": "The consumer-facing primitive is the natural-language message interpreted by the service; tool orchestration is internal to the service and not exposed as a discovery contract, so it is Conversational rather than Agentic.",
      "provenance": [
        {
          "url": "https://www.canva.com/ai-assistant/",
          "evidence": "Official page describes a conversational AI creative assistant with its own dedicated chat interface on the Canva home page, accepting text, voice, or image input."
        }
      ]
    },
    {
      "name": "Canva Connect REST API",
      "technology": "REST API over HTTPS, OAuth 2.0 (PKCE)",
      "channel": "Programmatic",
      "classification_rationale": "The consumer explicitly invokes provider-defined operations (designs, assets, templates, autofill, exports, comments) through structured HTTP requests under one base and auth.",
      "provenance": [
        {
          "url": "https://www.canva.dev/docs/connect/",
          "evidence": "Official docs: REST APIs to create and sync assets, designs, comments and more via HTTP requests."
        }
      ]
    },
    {
      "name": "Canva Connect webhooks",
      "technology": "Outgoing HTTP webhooks to a consumer-controlled receiver",
      "channel": "Event",
      "classification_rationale": "Canva initiates the interaction when subscribed events occur (comments, access requests, approvals, suggestions) and delivers a POST to a consumer-registered URL; service-initiated delivery, not consumer polling.",
      "provenance": [
        {
          "url": "https://www.canva.dev/docs/connect/webhooks/",
          "evidence": "Official docs: Canva sends real-time event information to your integration as POST requests; Canva only supports outgoing webhooks."
        }
      ]
    },
    {
      "name": "Canva remote MCP server (AI Connector)",
      "technology": "Remote Model Context Protocol server (mcp.canva.com)",
      "channel": "Agentic",
      "classification_rationale": "Provider-hosted MCP server that exposes Canva's design capabilities as semantically described, discoverable MCP tools an AI assistant selects by goal or context; capability discovery and selection structure the interaction contract, so it is Agentic rather than Programmatic.",
      "provenance": [
        {
          "url": "https://www.canva.dev/docs/mcp/",
          "evidence": "Official docs: the Canva MCP server exposes design creation/editing, asset and brand management, search, export, and commenting as MCP-compatible tools for AI assistants."
        }
      ]
    }
  ],
  "access_mechanism_ledger": [
    {
      "mechanism": "Web client surface",
      "disposition": "interface",
      "detail": "Canva web editor"
    },
    {
      "mechanism": "Desktop client surface",
      "disposition": "interface",
      "detail": "Canva desktop app"
    },
    {
      "mechanism": "Mobile client surface",
      "disposition": "interface",
      "detail": "Canva mobile app"
    },
    {
      "mechanism": "Terminal / CLI client surface",
      "disposition": "excluded",
      "detail": "No first-party Canva CLI or navigable TUI found in official sources."
    },
    {
      "mechanism": "Connect REST API",
      "disposition": "interface",
      "detail": "Canva Connect REST API"
    },
    {
      "mechanism": "Webhooks / events",
      "disposition": "interface",
      "detail": "Canva Connect webhooks"
    },
    {
      "mechanism": "Canva remote MCP server / AI Connector",
      "disposition": "interface",
      "detail": "Canva remote MCP server (AI Connector)"
    },
    {
      "mechanism": "Canva AI / Magic Studio conversational assistant",
      "disposition": "interface",
      "detail": "Canva AI assistant (Canva AI / Magic Studio chat)"
    },
    {
      "mechanism": "Apps SDK (extensions/app platform)",
      "disposition": "excluded",
      "detail": "An SDK/framework for building apps that run inside the Canva editor; on the do-not-count list, not itself an access interface to the service."
    },
    {
      "mechanism": "Canva Dev MCP server",
      "disposition": "excluded",
      "detail": "Local developer tool exposing Canva's docs, examples and helper tooling to coding agents; aids building integrations, does not access the service's design capabilities."
    },
    {
      "mechanism": "Canva Button (China only)",
      "disposition": "excluded",
      "detail": "Embeds the Interactive web editor into a third-party site (same affordance-manipulation paradigm); region-limited to China, not a distinct logical interface."
    },
    {
      "mechanism": "SDKs / client libraries / OpenAPI-generated clients",
      "disposition": "excluded",
      "detail": "Do-not-count list: libraries and generated clients implement or support an interface without being one."
    },
    {
      "mechanism": "Third-party integrations (Zapier, Make, n8n, Composio, etc.)",
      "disposition": "excluded",
      "detail": "Third-party automation/wrappers built on the Connect API or MCP; not provider-defined interfaces."
    }
  ],
  "channel_evidence": {
    "Interactive": "observed",
    "Agentic": "observed",
    "Conversational": "observed",
    "Event": "observed",
    "Programmatic": "observed"
  },
  "number_of_interfaces": 7,
  "multi_interface": true,
  "number_of_channels": 5,
  "multi_channel": true
}
```
