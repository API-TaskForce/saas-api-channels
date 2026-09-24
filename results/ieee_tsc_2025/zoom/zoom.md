# Zoom — Interface and Access-Channel Analysis

## SaaS summary

Zoom (Zoom Communications, official developer portal at developers.zoom.us) resolves to a single provider. This analysis identifies **8 logical interfaces** distributed across **5 distinct access channels**. The provider ships first-party clients on web, desktop, and mobile, a proprietary HTTPS REST API, a standards-based SCIM2 provisioning API, an SSH command interface for Zoom Rooms, two event-delivery mechanisms, an official MCP server, and a natural-language assistant embedded in the product.

## Interface classification table

| Interface                                    | Channel        | Interaction technology                                                                                   | Provenance                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| -------------------------------------------- | -------------- | -------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Zoom Workplace client (web, desktop, mobile) | Interactive    | Browser web client and native desktop/mobile GUI apps                                                    | Zoom's official download center distributes the Zoom Workplace app for mobile, desktop, web browsers, and operating systems. The desktop client, mobile app, and web client are distinct clients with different feature sets. Actions are expressed by manipulating presented affordances of a persistent navigable representation of the user's Zoom state, which fixes the primitive as affordance manipulation. Current.                                                  |
| REST API v2                                  | Programmatic   | HTTPS/JSON, base `https://api.zoom.us/v2/`, OAuth 2.0                                                    | Requests are sent to the base URL https://api.zoom.us/v2/ with an access token, using GET, POST, PATCH, PUT, or DELETE methods against documented endpoints. The consumer explicitly invokes provider-defined operations through structured requests. One base and one auth model cover Meetings, Phone, Chat, Mail, Calendar, Users, Accounts and other resource groups, so this is one interface. Current.                                                                 |
| SCIM2 provisioning API                       | Programmatic   | HTTPS, base `https://api.zoom.us`, paths under `/scim2/`, `application/scim+json`, OAuth (`scim2` scope) | The Zoom SCIM2 API supports user and group provisioning through User and Group resources, uses HTTP methods compatible with REST, requires the Accept header application/scim+json, and authenticates via OAuth with the scim2 scope against server https://api.zoom.us. Operation invocation, but a distinct base path and a distinct standardized contract separate it from REST v2. Current.                                                                              |
| Zoom Rooms Control System API (ZR-CSAPI)     | Programmatic   | SSH terminal, port 2244, plain-text CLI commands                                                         | The ZR-CSAPI exposes an SSH interface on port 2244 that accepts CLI terminal commands from an external automation controller and translates them to a proprietary Zoom Room API. The consumer invokes provider-defined operations through structured CLI commands, which is operation invocation. Command-line editing keys support input editing and do not constitute a navigable state representation, so this is not Interactive. Current.                               |
| Webhooks                                     | Event          | Provider-initiated HTTPS POST to a consumer-hosted endpoint                                              | Zoom sends real-time notifications to a consumer-specified HTTPS endpoint that accepts POST requests with JSON payloads when subscribed events occur. The service initiates the interaction on events and delivers to a consumer-controlled receiver. Current.                                                                                                                                                                                                               |
| WebSockets                                   | Event          | Persistent socket the consumer holds to receive pushed events                                            | Zoom offers WebSockets as an alternative method for real-time event notifications, currently in public beta. Same event-notification primitive as webhooks, but a different delivery contract (consumer-held connection rather than a consumer-hosted receiver), so it is a separate Event interface. Freshness: public beta.                                                                                                                                                |
| MCP Server                                   | Agentic        | Remote MCP over streamable HTTP, gateway `https://mcp.zoom.us/` and regional URLs                        | Zoom's MCP servers follow the Model Context Protocol and provide a consistent way for AI agents to discover, authenticate, and use tools dynamically without custom integration per system. Capability discovery and selection are part of the interaction contract, which places it in Agentic rather than Programmatic. Current, expanded May 2026.                                                                                                                        |
| AI Companion assistant (ZoomMate)            | Conversational | Natural-language side panel across Workplace and a web surface                                           | Zoom's online AI chat, powered by AI Companion, is a conversational interface where the user asks questions in natural language and receives answers, connecting to meetings, documents, and conversations. It can also execute tasks and workflows described in plain language. The primitive is the natural-language message interpreted by the service, and tool orchestration is internal to the product, which fixes it as Conversational rather than Agentic. Current. |

## Coverage ledger

| Access mechanism                                                        | Disposition                                                                                                                        |
| ----------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| Web client                                                              | Zoom Workplace client (Interactive)                                                                                                |
| Desktop client                                                          | Zoom Workplace client (Interactive)                                                                                                |
| Mobile app                                                              | Zoom Workplace client (Interactive)                                                                                                |
| Terminal / TUI (first-party)                                            | No navigable TUI dashboard exists; the only terminal-accessible official interface is ZR-CSAPI (Programmatic). No Interactive TUI. |
| REST API (Meetings, Phone, Chat, Mail, Calendar, Users, Accounts, etc.) | REST API v2 (Programmatic)                                                                                                         |
| SCIM2 API                                                               | SCIM2 provisioning API (Programmatic)                                                                                              |
| Zoom Rooms Control System API (SSH CLI)                                 | ZR-CSAPI (Programmatic)                                                                                                            |
| Webhooks                                                                | Webhooks (Event)                                                                                                                   |
| WebSockets                                                              | WebSockets (Event)                                                                                                                 |
| MCP server                                                              | MCP Server (Agentic)                                                                                                               |
| AI Companion / ZoomMate assistant                                       | AI Companion assistant (Conversational)                                                                                            |
| AI Companion API                                                        | Excluded: retired per the developer API index; the live assistant is captured as the Conversational interface.                     |
| Chatbot API / Team Chat apps (Rivet)                                    | Excluded: a build platform for developers to create bots, not a provider interface to Zoom's own service.                          |
| Video SDK, Meeting SDK, Cobrowse SDK, Zoom Apps SDK                     | Excluded: SDKs and client libraries, which implement or embed interfaces without being one.                                        |
| OAuth 2.0 / server-to-server OAuth                                      | Excluded: authentication method.                                                                                                   |
| Marketplace / integrations index                                        | Excluded: third-party app distribution and integrations.                                                                           |
| Postman public workspace                                                | Excluded: a collection of prepared REST requests, not a distinct interface.                                                        |
| Community / third-party CLIs and MCP servers                            | Excluded: not provider-controlled.                                                                                                 |
| Developer CLI announced 2021                                            | Excluded: announced as a prototyping tool with no confirmed current status as an official general access interface.                |

## Channel coverage

| Channel        | Evidence |
| -------------- | -------- |
| Interactive    | Observed |
| Agentic        | Observed |
| Conversational | Observed |
| Event          | Observed |
| Programmatic   | Observed |

## Classification notes

The three Programmatic interfaces are split rather than folded because their interaction contracts genuinely differ: REST v2 uses base `/v2/` with JSON, SCIM2 uses base `/scim2/` with the SCIM standard schema and `application/scim+json`, and ZR-CSAPI uses SSH transport with a plain-text command primitive. The two Event interfaces are split on the same basis, since webhooks push to a consumer-hosted receiver while WebSockets deliver over a consumer-held connection. None of these splits affects the channel count, since each pair or group shares one paradigm.

## Multichannel verdict

`Multichannel` (5 distinct paradigms observed)

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
    "name": "Zoom"
  },
  "interfaces": [
    {
      "name": "Zoom Workplace client (web, desktop, mobile)",
      "technology": "Browser web client and native desktop/mobile GUI apps",
      "channel": "Interactive",
      "classification_rationale": "Actions are expressed by manipulating presented affordances of a persistent, navigable representation of the user's Zoom state; the three surfaces share this primitive and control structure, so they form one logical Interactive interface.",
      "provenance": [
        {
          "url": "https://www.zoom.us/download",
          "evidence": "Official download center distributes the first-party Zoom Workplace app for web, desktop, and mobile."
        },
        {
          "url": "https://support.zoom.com/hc/en/article?id=zm_kb&sysparm_article=KB0060928",
          "evidence": "Support documentation on downloading the Zoom Workplace desktop and mobile app."
        }
      ]
    },
    {
      "name": "REST API v2",
      "technology": "HTTPS/JSON REST, base https://api.zoom.us/v2/, OAuth 2.0",
      "channel": "Programmatic",
      "classification_rationale": "The consumer explicitly invokes provider-defined operations through structured HTTP requests; one base and auth cover many resource groups, so it is one interface.",
      "provenance": [
        {
          "url": "https://developers.zoom.us/docs/api/",
          "evidence": "Requests go to https://api.zoom.us/v2/ with an access token using standard HTTP methods against documented endpoints."
        }
      ]
    },
    {
      "name": "SCIM2 provisioning API",
      "technology": "HTTPS, base https://api.zoom.us, paths under /scim2/, application/scim+json, OAuth (scim2 scope)",
      "channel": "Programmatic",
      "classification_rationale": "Operation invocation over HTTP, but a distinct base path and standardized SCIM contract and content type separate it from REST v2, so it is counted separately.",
      "provenance": [
        {
          "url": "https://developers.zoom.us/docs/api/scim2/",
          "evidence": "Zoom SCIM2 API provides user and group provisioning via User and Group resources using REST-compatible HTTP methods, application/scim+json, and OAuth with the scim2 scope against server https://api.zoom.us."
        }
      ]
    },
    {
      "name": "Zoom Rooms Control System API (ZR-CSAPI)",
      "technology": "SSH terminal on port 2244, plain-text CLI commands",
      "channel": "Programmatic",
      "classification_rationale": "The consumer invokes provider-defined operations through structured CLI commands over SSH; command-line editing is input handling, not a navigable state representation, so it is Programmatic and not Interactive.",
      "provenance": [
        {
          "url": "https://developers.zoom.us/docs/rooms/cli/",
          "evidence": "ZR-CSAPI exposes an SSH interface on port 2244 that accepts CLI terminal commands and translates them to a proprietary Zoom Room API."
        }
      ]
    },
    {
      "name": "Webhooks",
      "technology": "Provider-initiated HTTPS POST to a consumer-hosted endpoint",
      "channel": "Event",
      "classification_rationale": "The service initiates the interaction when subscribed events occur and delivers JSON payloads to a consumer-controlled HTTPS receiver.",
      "provenance": [
        {
          "url": "https://developers.zoom.us/docs/api/webhooks",
          "evidence": "Real-time notifications are sent to a consumer-specified HTTPS endpoint that accepts POST requests when subscribed events occur."
        }
      ]
    },
    {
      "name": "WebSockets",
      "technology": "Persistent socket held by the consumer to receive pushed events",
      "channel": "Event",
      "classification_rationale": "Same event-notification primitive as webhooks but a different delivery contract (consumer-held connection rather than consumer-hosted receiver), so it is a separate Event interface. Public beta.",
      "provenance": [
        {
          "url": "https://developers.zoom.us/docs/api/websockets",
          "evidence": "Zoom offers WebSockets as an alternative method for real-time event notifications, currently in public beta."
        }
      ]
    },
    {
      "name": "MCP Server",
      "technology": "Remote MCP over streamable HTTP, gateway https://mcp.zoom.us/ and regional URLs",
      "channel": "Agentic",
      "classification_rationale": "Capability discovery, authentication, and dynamic tool use are part of the interaction contract, which places it in Agentic rather than Programmatic.",
      "provenance": [
        {
          "url": "https://developers.zoom.us/docs/mcp/",
          "evidence": "Zoom's MCP servers follow the Model Context Protocol and let AI agents discover, authenticate, and use tools dynamically without custom integration per system; regional gateway URLs under mcp.zoom.us are listed."
        }
      ]
    },
    {
      "name": "AI Companion assistant (ZoomMate)",
      "technology": "Natural-language assistant panel across Workplace and a web surface",
      "channel": "Conversational",
      "classification_rationale": "The consumer expresses actions through natural-language messages interpreted by the service, and tool orchestration is internal to the product, which fixes it as Conversational rather than Agentic.",
      "provenance": [
        {
          "url": "https://www.zoom.com/en/products/ai-assistant/features/web-surface/",
          "evidence": "Zoom's online AI chat, powered by AI Companion, is a conversational interface where the user asks questions in natural language and receives context-aware answers."
        },
        {
          "url": "https://www.zoom.com/en/products/ai-assistant/",
          "evidence": "ZoomMate, the AI Companion assistant, answers natural-language questions and can execute tasks and workflows described in plain language across Zoom Workplace."
        }
      ]
    }
  ],
  "access_mechanism_ledger": [
    {
      "mechanism": "Web client",
      "disposition": "interface",
      "detail": "Zoom Workplace client (Interactive)"
    },
    {
      "mechanism": "Desktop client",
      "disposition": "interface",
      "detail": "Zoom Workplace client (Interactive)"
    },
    {
      "mechanism": "Mobile app",
      "disposition": "interface",
      "detail": "Zoom Workplace client (Interactive)"
    },
    {
      "mechanism": "Terminal / first-party TUI",
      "disposition": "excluded",
      "detail": "No navigable TUI dashboard exists; the only terminal-accessible official interface is ZR-CSAPI (Programmatic)."
    },
    {
      "mechanism": "REST API v2",
      "disposition": "interface",
      "detail": "REST API v2 (Programmatic)"
    },
    {
      "mechanism": "SCIM2 API",
      "disposition": "interface",
      "detail": "SCIM2 provisioning API (Programmatic)"
    },
    {
      "mechanism": "Zoom Rooms Control System API (SSH CLI)",
      "disposition": "interface",
      "detail": "ZR-CSAPI (Programmatic)"
    },
    {
      "mechanism": "Webhooks",
      "disposition": "interface",
      "detail": "Webhooks (Event)"
    },
    {
      "mechanism": "WebSockets",
      "disposition": "interface",
      "detail": "WebSockets (Event)"
    },
    {
      "mechanism": "MCP server",
      "disposition": "interface",
      "detail": "MCP Server (Agentic)"
    },
    {
      "mechanism": "AI Companion / ZoomMate assistant",
      "disposition": "interface",
      "detail": "AI Companion assistant (Conversational)"
    },
    {
      "mechanism": "AI Companion API",
      "disposition": "excluded",
      "detail": "Retired per the developer API index; the live assistant is captured as the Conversational interface."
    },
    {
      "mechanism": "Chatbot API / Team Chat apps (Rivet)",
      "disposition": "excluded",
      "detail": "Build platform for developers to create bots, not a provider interface to Zoom's own service."
    },
    {
      "mechanism": "Video SDK, Meeting SDK, Cobrowse SDK, Zoom Apps SDK",
      "disposition": "excluded",
      "detail": "SDKs and client libraries, which implement or embed interfaces without being one."
    },
    {
      "mechanism": "OAuth 2.0 / server-to-server OAuth",
      "disposition": "excluded",
      "detail": "Authentication method."
    },
    {
      "mechanism": "Marketplace / integrations index",
      "disposition": "excluded",
      "detail": "Third-party app distribution and integrations."
    },
    {
      "mechanism": "Postman public workspace",
      "disposition": "excluded",
      "detail": "A collection of prepared REST requests, not a distinct interface."
    },
    {
      "mechanism": "Community / third-party CLIs and MCP servers",
      "disposition": "excluded",
      "detail": "Not provider-controlled."
    },
    {
      "mechanism": "Developer CLI announced 2021",
      "disposition": "excluded",
      "detail": "Announced as a prototyping tool with no confirmed current status as an official general access interface."
    }
  ],
  "channel_evidence": {
    "Interactive": "observed",
    "Agentic": "observed",
    "Conversational": "observed",
    "Event": "observed",
    "Programmatic": "observed"
  },
  "number_of_interfaces": 8,
  "multi_interface": true,
  "number_of_channels": 5,
  "multi_channel": true
}
```
