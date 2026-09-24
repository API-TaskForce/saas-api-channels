# UserGuiding Access Channel Analysis

## SaaS summary

UserGuiding is a no-code product adoption and user onboarding platform (provider domain userguiding.com, panel at panel.userguiding.com, developer and help documentation at help.userguiding.com). The investigation identifies seven provider-defined logical interfaces, spanning five distinct access channels that each have at least one classified interface.

## Interface classification table

| Interface                       | Channel        | Interaction technology                                                                 | Provenance                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| ------------------------------- | -------------- | -------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Admin Panel                     | Interactive    | Hosted web dashboard (panel.userguiding.com)                                           | "Day 1: Intro to UserGuiding" states that after signup you land on panel.userguiding.com, the dashboard where you create and manage content by clicking through views and settings. Actions are expressed by manipulating presented affordances of a persistent, navigable state representation, so decision-tree step 1 (Affordance Manipulation) resolves it as Interactive. Current.                                                                                                                                                                                          |
| Chrome Extension visual builder | Interactive    | First-party browser extension with in-context step editor                              | The intro guide and the "Chrome Extension" / "Using the Step Editor in the Chrome Extension" articles describe downloading the extension to navigate your live product and click elements to attach tooltips and tour steps. Affordance Manipulation over a navigable representation, so Interactive. Counted separately from the Panel because its base (an extension injected into the customer's own live site) and interaction context (in-context element selection overlay) genuinely differ, though the paradigm is the same. Current.                                    |
| JavaScript API                  | Programmatic   | Client-side JS methods loaded via container code                                       | The JavaScript API article documents methods such as `userGuiding.previewGuide()`, `launchChecklist()`, and `launchSurvey()` that the customer's own front-end calls to invoke provider-defined operations. The consumer explicitly invokes named operations through structured commands, so decision-tree step 5 (Operation Invocation) resolves it as Programmatic. The in-page `userGuidingLayer` callbacks are part of this same embedded contract and fire in the loaded client, not to an out-of-band consumer-controlled receiver, so they do not make it Event. Current. |
| User API                        | Programmatic   | Server-side REST API (interactive docs at user.userguiding.com/docs), API access token | The User API article describes a server-side interface to create, update, delete, and list users, reset history, and track events, available once User Identification is enabled, with a separate API access token and interactive API documentation. Structured request/response operation invocation over its own base and auth, so Programmatic. Distinct from the JavaScript API by base, auth, and consumer (back-end rather than browser). Current.                                                                                                                        |
| Outgoing Webhooks               | Event          | Provider-initiated HTTP event delivery to a customer URL                               | The Webhook Integration article states that with UserGuiding as a source it pushes real-time event notifications to a webhook URL you control when events occur, with a documented event payload format and a selectable set of events to trigger. The service initiates on subscribed events and delivers to a consumer-controlled receiver, so decision-tree step 4 (Event Notification) resolves it as Event. Current.                                                                                                                                                        |
| MCP Server                      | Agentic        | Remote Model Context Protocol server (Streamable HTTP, JSON-RPC, OAuth)                | The UserGuiding MCP Server article describes 58 semantically described tools that an MCP-compatible assistant discovers and selects, stating explicitly that you never call tools by name, you ask a question and the assistant picks and chains them. Capability discovery and selection are part of the interaction contract, which is the MCP boundary case resolving to Agentic rather than Programmatic. Current, with legacy SSE endpoints retired (410 Gone) and API-key auth being retired in favor of OAuth.                                                            |
| Lighthouse AI                   | Conversational | In-panel natural-language AI analyst                                                   | The "What is Lighthouse AI?" article describes an AI analyst inside the panel that you ask in plain language, which interprets the message, runs the right analytics internally, and returns an answer. The consumer interacts through natural-language messages and tool orchestration is internal to the service, which is the assistant-with-internal-tools boundary case resolving to Conversational rather than Agentic. Current, in Beta.                                                                                                                                  |

## Coverage ledger

| Access mechanism                                                                                                                               | Disposition                                                                                                                                                               |
| ---------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Panel / dashboard (panel.userguiding.com)                                                                                                      | Admin Panel (Interactive)                                                                                                                                                 |
| Chrome Extension (step editor / visual builder)                                                                                                | Chrome Extension visual builder (Interactive)                                                                                                                             |
| JavaScript API                                                                                                                                 | JavaScript API (Programmatic)                                                                                                                                             |
| User API (REST, user.userguiding.com/docs)                                                                                                     | User API (Programmatic)                                                                                                                                                   |
| Webhook Integration / UserGuiding Event Payloads (outgoing)                                                                                    | Outgoing Webhooks (Event)                                                                                                                                                 |
| MCP Server                                                                                                                                     | MCP Server (Agentic)                                                                                                                                                      |
| Lighthouse AI (in-panel)                                                                                                                       | Lighthouse AI (Conversational)                                                                                                                                            |
| Container / snippet installation code                                                                                                          | Excluded: installation and transport mechanism that loads the widget runtime and JavaScript API, not itself an interaction interface                                      |
| npm package                                                                                                                                    | Excluded: client library / wrapper per the do-not-count rule                                                                                                              |
| Integrations index (HubSpot, Salesforce, Slack, Segment, Amplitude, Mixpanel, Woopra, Intercom, Google Analytics)                              | Excluded: third-party integrations per the do-not-count rule                                                                                                              |
| AI Assistant (support chatbot)                                                                                                                 | Excluded: an end-user support feature the customer configures and deploys on their own site, a product output rather than a channel for accessing the UserGuiding service |
| Rendered onboarding content (Guides, Hotspots, Checklists, Resource Center, Surveys, Banners, Knowledge Base, Product Updates, public Roadmap) | Excluded: product output and end-user content the customer deploys; programmatic control of it is already captured by the JavaScript API                                  |
| SSO / SAML2, OAuth, API keys                                                                                                                   | Excluded: authentication methods, not interfaces                                                                                                                          |
| Webhook inbound (UserGuiding as destination)                                                                                                   | Excluded: data ingestion of attributes and events into the service, covered by the attribute/event mechanisms rather than a distinct interface                            |
| Mobile client (first-party)                                                                                                                    | Excluded: no first-party mobile application for operating the service is documented; UserGuiding renders on mobile web but ships no mobile admin app or SDK               |
| Desktop client (first-party)                                                                                                                   | Excluded: none documented                                                                                                                                                 |
| Terminal / CLI and TUI (first-party)                                                                                                           | Excluded: no first-party command-line client is documented (Claude Code and Codex CLI appear only as third-party MCP clients, not a UserGuiding CLI)                      |

## Channel coverage

| Channel        | Evidence |
| -------------- | -------- |
| Interactive    | Observed |
| Agentic        | Observed |
| Conversational | Observed |
| Event          | Observed |
| Programmatic   | Observed |

## Classification notes

The Panel and the Chrome Extension are both Interactive and could reasonably be treated as one administration surface. They are reported as two interfaces because their bases and interaction contexts genuinely differ, and merging them does not change the channel count. Lighthouse AI and the MCP Server draw on the same underlying tool set, which the Lighthouse AI documentation states directly, yet they fall in different channels: the MCP Server exposes tool discovery and selection to an external assistant as part of its contract (Agentic), while Lighthouse AI takes plain-language messages and orchestrates those tools internally (Conversational).

## Multichannel verdict

Multichannel (5 distinct paradigms observed).

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
  "generated_at": "2026-09-24T00:00:00Z",
  "evidence_checked_at": "2026-09-24T00:00:00Z",
  "saas": { "name": "UserGuiding" },
  "interfaces": [
    {
      "name": "Admin Panel",
      "technology": "Hosted web dashboard (panel.userguiding.com)",
      "channel": "Interactive",
      "classification_rationale": "Content is created and managed by manipulating presented affordances (views, menus, settings) of a persistent, navigable dashboard, which is Affordance Manipulation.",
      "provenance": [
        {
          "url": "https://help.userguiding.com/en/articles/2540719-day-1-intro-to-userguiding",
          "evidence": "States that after signup you land on panel.userguiding.com, the dashboard where you create and manage content through its controls."
        }
      ]
    },
    {
      "name": "Chrome Extension visual builder",
      "technology": "First-party browser extension with in-context step editor",
      "channel": "Interactive",
      "classification_rationale": "The extension overlays the customer's live product so guides and hotspots are authored by clicking elements and manipulating a step editor, which is Affordance Manipulation. Its base and in-context interaction differ from the Panel, so it is counted separately.",
      "provenance": [
        {
          "url": "https://help.userguiding.com/en/articles/3624243-using-the-step-editor-in-the-chrome-extension",
          "evidence": "Documents downloading the extension and using its step editor to select elements on the live product and build steps."
        }
      ]
    },
    {
      "name": "JavaScript API",
      "technology": "Client-side JavaScript methods loaded via container code",
      "channel": "Programmatic",
      "classification_rationale": "The customer front-end explicitly invokes provider-defined operations such as previewGuide, launchChecklist and launchSurvey, which is Operation Invocation. In-page userGuidingLayer callbacks belong to the same embedded contract and are not out-of-band event delivery.",
      "provenance": [
        {
          "url": "https://help.userguiding.com/en/articles/3420081-userguiding-javascript-api",
          "evidence": "Documents methods and callbacks called from the customer's source code after the container code loads."
        }
      ]
    },
    {
      "name": "User API",
      "technology": "Server-side REST API with interactive docs (user.userguiding.com/docs), API access token",
      "channel": "Programmatic",
      "classification_rationale": "A server-side API where the consumer invokes structured operations to create, update, delete and list users, reset history and track events, which is Operation Invocation. Distinct base and auth from the JavaScript API.",
      "provenance": [
        {
          "url": "https://help.userguiding.com/en/articles/4493538-userguiding-user-api",
          "evidence": "Describes the User API operations, its API access token from the Installation section, and interactive API documentation at user.userguiding.com/docs."
        }
      ]
    },
    {
      "name": "Outgoing Webhooks",
      "technology": "Provider-initiated HTTP event delivery to a customer-configured URL",
      "channel": "Event",
      "classification_rationale": "With UserGuiding as a source it pushes real-time event notifications to a customer-controlled webhook URL when subscribed events occur, which is Event Notification.",
      "provenance": [
        {
          "url": "https://help.userguiding.com/en/articles/5377145-webhook-integration",
          "evidence": "States UserGuiding pushes real-time event notifications to a webhook URL you control when events occur, with a documented payload format and selectable trigger events."
        }
      ]
    },
    {
      "name": "MCP Server",
      "technology": "Remote Model Context Protocol server (Streamable HTTP, JSON-RPC, OAuth)",
      "channel": "Agentic",
      "classification_rationale": "Exposes 58 semantically described tools an assistant discovers and selects; the docs state you never call tools by name but ask a question and the assistant picks and chains them, so capability discovery and selection are part of the contract (MCP boundary case).",
      "provenance": [
        {
          "url": "https://help.userguiding.com/en/articles/20916-userguiding-mcp-server",
          "evidence": "Describes the MCP server, its 58 tools across nine areas, and that the assistant selects and chains tools from a natural-language request. Notes legacy SSE endpoints retired and API-key auth being retired in favor of OAuth."
        }
      ]
    },
    {
      "name": "Lighthouse AI",
      "technology": "In-panel natural-language AI analyst",
      "channel": "Conversational",
      "classification_rationale": "The consumer asks in plain language inside the panel and the service interprets the message and orchestrates its analytics tools internally, which is the assistant-with-internal-tools boundary case for Contextual Conversation.",
      "provenance": [
        {
          "url": "https://help.userguiding.com/en/articles/26132-what-is-lighthouse-ai",
          "evidence": "Describes an in-panel AI analyst you ask in plain language that reads the question, runs the right analytics internally, and writes up the result. Marked Beta."
        }
      ]
    }
  ],
  "access_mechanism_ledger": [
    {
      "mechanism": "Panel / dashboard (panel.userguiding.com)",
      "disposition": "interface",
      "detail": "Admin Panel (Interactive)"
    },
    {
      "mechanism": "Chrome Extension (step editor / visual builder)",
      "disposition": "interface",
      "detail": "Chrome Extension visual builder (Interactive)"
    },
    {
      "mechanism": "JavaScript API",
      "disposition": "interface",
      "detail": "JavaScript API (Programmatic)"
    },
    {
      "mechanism": "User API (REST)",
      "disposition": "interface",
      "detail": "User API (Programmatic)"
    },
    {
      "mechanism": "Webhook Integration / UserGuiding Event Payloads (outgoing)",
      "disposition": "interface",
      "detail": "Outgoing Webhooks (Event)"
    },
    {
      "mechanism": "MCP Server",
      "disposition": "interface",
      "detail": "MCP Server (Agentic)"
    },
    {
      "mechanism": "Lighthouse AI (in-panel)",
      "disposition": "interface",
      "detail": "Lighthouse AI (Conversational)"
    },
    {
      "mechanism": "Container / snippet installation code",
      "disposition": "excluded",
      "detail": "Installation and transport mechanism that loads the widget runtime and JavaScript API, not itself an interface"
    },
    {
      "mechanism": "npm package",
      "disposition": "excluded",
      "detail": "Client library / wrapper per the do-not-count rule"
    },
    {
      "mechanism": "Integrations index (HubSpot, Salesforce, Slack, Segment, Amplitude, Mixpanel, Woopra, Intercom, Google Analytics)",
      "disposition": "excluded",
      "detail": "Third-party integrations per the do-not-count rule"
    },
    {
      "mechanism": "AI Assistant (support chatbot)",
      "disposition": "excluded",
      "detail": "End-user support feature the customer configures and deploys, a product output rather than a channel to the service"
    },
    {
      "mechanism": "Rendered onboarding content (Guides, Hotspots, Checklists, Resource Center, Surveys, Banners, Knowledge Base, Product Updates, public Roadmap)",
      "disposition": "excluded",
      "detail": "Product output and end-user content; programmatic control is captured by the JavaScript API"
    },
    {
      "mechanism": "SSO / SAML2, OAuth, API keys",
      "disposition": "excluded",
      "detail": "Authentication methods, not interfaces"
    },
    {
      "mechanism": "Webhook inbound (UserGuiding as destination)",
      "disposition": "excluded",
      "detail": "Data ingestion of attributes and events into the service, not a distinct interface"
    },
    {
      "mechanism": "Mobile client (first-party)",
      "disposition": "excluded",
      "detail": "No first-party mobile admin app or SDK documented; renders on mobile web only"
    },
    {
      "mechanism": "Desktop client (first-party)",
      "disposition": "excluded",
      "detail": "None documented"
    },
    {
      "mechanism": "Terminal / CLI and TUI (first-party)",
      "disposition": "excluded",
      "detail": "No first-party command-line client documented"
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
