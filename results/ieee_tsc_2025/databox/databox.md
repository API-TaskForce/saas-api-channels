## SaaS summary

Databox is a cloud business-analytics and KPI-dashboard platform (databox.com). Investigation of its official documentation identifies **5 provider-defined logical interfaces** spread across **4 distinct access channels** with at least one classified interface.

## Interface classification

| Interface                                         | Channel        | Interaction technology                             | Provenance                                                                                                                                                                                                                                                                                                                                                                        |
| ------------------------------------------------- | -------------- | -------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Web application (Databoards / Dashboard Designer) | Interactive    | Browser-based web app                              | Official product and data-visualization pages describe a drag-and-drop Designer and navigable, responsive dashboards that run from the browser with no download. Actions are expressed by manipulating on-screen affordances of account state (affordance manipulation). Current.                                                                                                 |
| Mobile app (iOS / Android, incl. Apple Watch)     | Interactive    | Native mobile client                               | Official help doc and product page confirm first-party native apps for viewing, editing, annotating, and reordering dashboards on device. Same paradigm as web but a distinct provider-shipped client surface. Current.                                                                                                                                                           |
| Genie AI Analyst (in-app Agentic Analytics chat)  | Conversational | In-product natural-language assistant              | Official help and product pages: reached via Data > Agentic Analytics > New chat, the user types plain-language prompts and Genie interprets them, formulates queries an internal engine executes, then summarizes. Tool orchestration is internal to the service, so the primitive is the message. Current.                                                                      |
| REST API (Push / Dataset API, v1)                 | Programmatic   | REST/HTTP API                                      | Official developer docs and help articles: resource-oriented URLs at api.databox.com/v1, JSON bodies, standard HTTP verbs, x-api-key auth. The consumer explicitly invokes provider-defined operations (operation invocation). Current.                                                                                                                                           |
| Databox MCP server                                | Agentic        | Model Context Protocol server (JSON-RPC over HTTP) | Official MCP docs and the databox-owned repo: server at mcp.databox.com/mcp, OAuth 2.0, exposing semantically described tools (ingest_data, query_dataset_with_ai, and others) that an AI client discovers and selects as part of the contract. Capability discovery structures the contract, making it Agentic rather than Programmatic. Documented as an evolving/beta feature. |

## Coverage ledger

| Access mechanism                            | Disposition                                                                                                                                                                                                                  |
| ------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| API / API reference                         | Interface: REST API (Push / Dataset API, v1)                                                                                                                                                                                 |
| MCP / agent / protocol                      | Interface: Databox MCP server                                                                                                                                                                                                |
| Conversational / chat / AI assistant        | Interface: Genie AI Analyst                                                                                                                                                                                                  |
| First-party web client                      | Interface: Web application (Databoards / Dashboard Designer)                                                                                                                                                                 |
| First-party mobile client                   | Interface: Mobile app (iOS / Android, incl. Apple Watch)                                                                                                                                                                     |
| First-party desktop client                  | Excluded: the "desktop app" / desktop Designer is the same browser-based web app on desktop (no download); the Mac App Store listing is the iOS app on Apple Silicon, not a separate native desktop client.                  |
| Terminal client / CLI / TUI                 | Excluded: no first-party CLI or TUI found in official docs; Databox ships SDKs, not a command-line client.                                                                                                                   |
| Webhooks / events / inbound routing         | Excluded: no official provider-defined outbound webhook/event interface delivering to a consumer-controlled receiver was found. Alerts and Scorecards are UI-configured notifications sent to email, Slack, and mobile push. |
| SMTP / email relay                          | Excluded: not offered as an access or data-submission interface.                                                                                                                                                             |
| SDKs (Java, PHP, Ruby, Node.js, Go, Python) | Excluded: client libraries wrapping the REST API; they implement an interface rather than being one.                                                                                                                         |
| Integrations index (130+ connectors)        | Excluded: third-party inbound data-source connectors, not interfaces for accessing Databox itself.                                                                                                                           |
| SSO / OAuth / authentication                | Excluded: authentication methods, not logical interfaces.                                                                                                                                                                    |

## Channel coverage

| Channel        | Evidence             |
| -------------- | -------------------- |
| Interactive    | Observed             |
| Agentic        | Observed             |
| Conversational | Observed             |
| Event          | No evidence observed |
| Programmatic   | Observed             |

## Classification notes

Two calls rest on the skill's boundary rules and are worth stating explicitly. Genie is classified **Conversational** rather than Agentic because the consumer-facing primitive is the natural-language message and the tool/query orchestration happens inside the service (the AI formulates, the engine executes, the AI summarizes), not as a contract the consumer drives. The **MCP server** is classified Agentic rather than Programmatic because tool discovery and selection are part of its interaction contract, which is the defining feature of the Agentic channel even though tools are ultimately invoked underneath.

The **Event** channel is marked "no evidence observed," not absent. Databox clearly initiates Alerts and Scorecards on threshold and schedule events, but the documented delivery targets are email, Slack, and mobile push configured in the UI. No official outbound-webhook interface delivering to a consumer-controlled HTTP receiver was found. If Databox documents such a webhook contract elsewhere, it would add a Programmatic-adjacent Event interface; the conservative reading on current official evidence leaves the channel unobserved.

## Multichannel verdict

**Multichannel** (4 distinct paradigms observed: Interactive, Conversational, Programmatic, Agentic).

```json
{
  "schema_version": "2.1",
  "generator": {
    "platform": "Claude",
    "provider": "Anthropic",
    "model": "claude-opus-4-8",
    "skill": "saas-interface-channel-analyzer",
    "skill_version": "1.0"
  },
  "generated_at": "2026-09-24T12:00:00Z",
  "evidence_checked_at": "2026-09-24T12:00:00Z",
  "saas": { "name": "Databox" },
  "interfaces": [
    {
      "name": "Web application (Databoards / Dashboard Designer)",
      "technology": "Browser-based web app",
      "channel": "Interactive",
      "classification_rationale": "Actions are expressed by manipulating presented affordances (drag-and-drop Designer, navigable dashboards, menus, filters) of a persistent representation of account state. The primitive is affordance manipulation.",
      "provenance": [
        {
          "url": "https://databox.com/product/designer",
          "evidence": "Official product page describing the drag-and-drop Dashboard Designer used to build and edit navigable dashboards."
        },
        {
          "url": "https://databox.com/data-visualization",
          "evidence": "States the Designer runs from the browser with no downloads and dashboards are fully interactive/responsive across desktop, mobile, TV."
        }
      ]
    },
    {
      "name": "Mobile app (iOS / Android, incl. Apple Watch)",
      "technology": "Native mobile client",
      "channel": "Interactive",
      "classification_rationale": "A first-party native client on the mobile surface where the user manipulates on-screen affordances (dashboards, favorites, Insights/Pulse, drag-to-reorder) of service state. Same paradigm as web but a distinct provider-shipped client surface.",
      "provenance": [
        {
          "url": "https://help.databox.com/overview-mobile-app",
          "evidence": "Official help doc detailing navigation of Databoards, Metrics, Goals, Notifications pages and reordering within the app."
        },
        {
          "url": "https://databox.com/product/mobile",
          "evidence": "Official page confirming first-party iOS and Android apps for viewing, editing, and annotating dashboards on device."
        }
      ]
    },
    {
      "name": "Genie AI Analyst (in-app Agentic Analytics chat)",
      "technology": "In-product natural-language assistant",
      "channel": "Conversational",
      "classification_rationale": "The consumer interacts through plain-language messages that the service interprets; the AI formulates queries that an internal engine executes and then summarizes. Tool orchestration is internal to the service, so the primitive is the message (Conversational, not Agentic).",
      "provenance": [
        {
          "url": "https://help.databox.com/get-started-with-genie-the-databox-ai-assistant",
          "evidence": "Official help doc: Genie is reached via Data > Agentic Analytics > New chat; user enters prompts and Genie responds in the prompt's language."
        },
        {
          "url": "https://databox.com/ai-analyst",
          "evidence": "Official page describing Genie as an in-product AI Analyst answering plain-language performance questions from connected data."
        }
      ]
    },
    {
      "name": "REST API (Push / Dataset API, v1)",
      "technology": "REST/HTTP API",
      "channel": "Programmatic",
      "classification_rationale": "The consumer explicitly invokes provider-defined operations via resource-oriented URLs, JSON bodies, and standard HTTP verbs authenticated with an API key. The primitive is structured operation invocation.",
      "provenance": [
        {
          "url": "https://developers.databox.com/docs/api/overview",
          "evidence": "Official developer docs: REST conventions, resource-oriented URLs, JSON, standard HTTP verbs/status codes, versioned in the URL. Current."
        },
        {
          "url": "https://help.databox.com/article/171-how-to-push-data-via-api-to-databox",
          "evidence": "Official help article showing GET/POST calls to api.databox.com/v1 endpoints with x-api-key header."
        }
      ]
    },
    {
      "name": "Databox MCP server",
      "technology": "Model Context Protocol server (JSON-RPC over HTTP)",
      "channel": "Agentic",
      "classification_rationale": "Exposes semantically described tools (e.g. ingest_data, query_dataset_with_ai, current-datetime) that an AI client discovers and selects as part of the interaction contract, authorized via OAuth 2.0. Capability discovery/selection structures the contract, so it is Agentic rather than Programmatic.",
      "provenance": [
        {
          "url": "https://developers.databox.com/docs/mcp/overview",
          "evidence": "Official MCP docs: server at mcp.databox.com/mcp, JSON-RPC over HTTP, OAuth 2.0, tools such as ingest_data and query_dataset_with_ai. Marked as an evolving/beta feature."
        },
        {
          "url": "https://github.com/databox/databox-mcp",
          "evidence": "Databox-owned repository documenting the MCP server, its tool set, and three-layer query architecture for AI clients."
        }
      ]
    }
  ],
  "access_mechanism_ledger": [
    {
      "mechanism": "API / API reference",
      "disposition": "interface",
      "detail": "REST API (Push / Dataset API, v1)"
    },
    {
      "mechanism": "MCP / agent / protocol",
      "disposition": "interface",
      "detail": "Databox MCP server"
    },
    {
      "mechanism": "Conversational / chat / AI assistant",
      "disposition": "interface",
      "detail": "Genie AI Analyst (in-app Agentic Analytics chat)"
    },
    {
      "mechanism": "First-party web client",
      "disposition": "interface",
      "detail": "Web application (Databoards / Dashboard Designer)"
    },
    {
      "mechanism": "First-party mobile client",
      "disposition": "interface",
      "detail": "Mobile app (iOS / Android, incl. Apple Watch)"
    },
    {
      "mechanism": "First-party desktop client",
      "disposition": "excluded",
      "detail": "Excluded: the 'desktop app' / desktop Designer is the same browser-based web application on desktop (no download required); the Mac App Store listing is the iOS app on Apple Silicon, not a separate native desktop client."
    },
    {
      "mechanism": "Terminal client / CLI / TUI",
      "disposition": "excluded",
      "detail": "Excluded: no first-party CLI or TUI found in official Databox documentation; Databox ships SDKs, not a command-line client."
    },
    {
      "mechanism": "Webhooks / events / inbound routing",
      "disposition": "excluded",
      "detail": "Excluded: no official provider-defined outbound webhook/event interface delivering to a consumer-controlled receiver was found. Alerts and Scorecards are UI-configured notifications delivered to email, Slack, and mobile push, not a distinct event interface."
    },
    {
      "mechanism": "SMTP / email relay",
      "disposition": "excluded",
      "detail": "Excluded: not offered by Databox as an inbound data-submission or access interface."
    },
    {
      "mechanism": "SDKs / client libraries (Java, PHP, Ruby, Node.js, Go, Python)",
      "disposition": "excluded",
      "detail": "Excluded per counting rules: client libraries that wrap the REST API; they implement an interface rather than being one."
    },
    {
      "mechanism": "Integrations index (130+ connectors)",
      "disposition": "excluded",
      "detail": "Excluded: third-party inbound data-source connectors, not provider-defined interfaces for accessing Databox itself."
    },
    {
      "mechanism": "SSO / OAuth / authentication",
      "disposition": "excluded",
      "detail": "Excluded per counting rules: authentication methods, not logical interfaces."
    }
  ],
  "channel_evidence": {
    "Interactive": "observed",
    "Agentic": "observed",
    "Conversational": "observed",
    "Event": "no_evidence_observed",
    "Programmatic": "observed"
  },
  "number_of_interfaces": 5,
  "multi_interface": true,
  "number_of_channels": 4,
  "multi_channel": true
}
```
