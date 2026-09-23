# Interface classification table

| Interface              | Channel      | Interaction technology                        | Provenance                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| ---------------------- | ------------ | --------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Web client             | Interactive  | Web application (trello.com)                  | Official product page (atlassian.com/software/trello) presents boards/lists/cards manipulated via drag-and-drop and menus in a persistent navigable representation of service state. Primitive is affordance manipulation. Current.                                                                                                                                                                                                                                                                                                   |
| Mobile client          | Interactive  | iOS + Android apps                            | Official support page "What browsers and platforms does Trello support?" and Atlassian's own app-store listings document first-party iOS/Android apps with the same board/card affordance-manipulation paradigm (touch drag-and-drop, widgets). Counted as one Interactive interface (same interaction contract across the two OSes). Current.                                                                                                                                                                                        |
| Desktop client         | Interactive  | macOS + Windows apps                          | Official support page "Trello desktop apps" documents first-party Mac/Windows apps distributed via the Mac App Store and Microsoft Store, presenting the navigable board UI in a dedicated window. Distinct first-party surface from web; same Interactive paradigm. Current.                                                                                                                                                                                                                                                         |
| REST API               | Programmatic | HTTP REST (api.trello.com/1)                  | Official REST reference (developer.atlassian.com/cloud/trello/rest). Consumer explicitly invokes provider-defined operations (GET/POST/PUT/DELETE on boards, cards, lists, etc.) through structured requests under one base and auth. Primitive is operation invocation. Batch endpoint shares base/auth, so it is part of this one interface. Current.                                                                                                                                                                               |
| Email-to-board / Inbox | Programmatic | Inbound email to a unique board/Inbox address | Official support "Create cards by email" documents that each board and the Inbox has a unique address; sending a structured email invokes the create-card operation (subject → title, body → description, `@user`/`#label` conventions). Primitive is operation invocation via message submission, analogous to SMTP submission. The optional AI summary is internal enrichment, not a consumer-facing conversational contract, so it does not reclassify this. Distinct primitive/base/auth from REST → separate interface. Current. |
| Webhooks               | Event        | HTTP callbacks to a consumer-controlled URL   | Official "Webhooks" guide and REST webhooks group. Trello initiates delivery to a subscriber-provided `callbackURL` when a watched model changes. Service-initiated delivery to a consumer-controlled receiver → Event, not an ordinary API read. Current.                                                                                                                                                                                                                                                                            |
| Trello MCP server      | Agentic      | Remote MCP (mcp.trello.com/v1)                | Official support "Connect Trello to AI Assistants with Trello MCP," trello.com/mcp, and the atlassian/trello-mcp-server repo. Exposes semantically described capabilities (view/create/update/move cards, checklists, search, Planner/Inbox) discoverable and selectable by an MCP client as part of the contract, over OAuth 2.0. Per the MCP boundary rule, capability discovery structuring the contract makes it Agentic, not Programmatic. Current (launched mid-2026).                                                          |

# Coverage ledger table

| Access mechanism                 | Disposition                                                                                                                                                                                                      |
| -------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Web app (web surface)            | Interface: Web client (Interactive)                                                                                                                                                                              |
| Mobile app (mobile surface)      | Interface: Mobile client (Interactive)                                                                                                                                                                           |
| Desktop app (desktop surface)    | Interface: Desktop client (Interactive)                                                                                                                                                                          |
| Terminal/CLI (terminal surface)  | Excluded: no first-party Trello CLI or TUI. The "Trello CLI"/ACLI on the Appfire/Bob Swift wiki and community tools (mheap/trello-cli) are third-party.                                                          |
| REST API                         | Interface: REST API (Programmatic)                                                                                                                                                                               |
| Batch API                        | Excluded as separate interface: same base/auth/invocation style as REST → part of the REST API interface.                                                                                                        |
| GraphQL API                      | Excluded: Trello exposes only REST (v1); no official GraphQL interface.                                                                                                                                          |
| Email-to-board / Inbox-by-email  | Interface: Email-to-board / Inbox (Programmatic)                                                                                                                                                                 |
| Webhooks                         | Interface: Webhooks (Event)                                                                                                                                                                                      |
| Trello MCP server                | Interface: Trello MCP server (Agentic)                                                                                                                                                                           |
| Atlassian Rovo MCP server        | Excluded: official docs state Rovo MCP does not currently reach Trello data (Trello-specific MCP only).                                                                                                          |
| Conversational AI assistant      | Excluded: no first-party natural-language assistant is the consumer-facing contract for Trello; email/Inbox "AI summary" is internal enrichment, and AI access is delivered through the MCP (Agentic) interface. |
| Power-Ups platform               | Excluded: third-party extension/plugin platform that augments the Interactive UI and consumes the REST API; not itself a distinct provider access interface (integrations/wrappers per the "do not count" list). |
| Butler automation                | Excluded: internal automation feature configured through the web UI; not a separate consumer-facing access interface.                                                                                            |
| client.js                        | Excluded: JavaScript client library/SDK wrapping the REST API.                                                                                                                                                   |
| Integrations / marketplace index | Excluded: catalog of third-party integrations, not a provider interface.                                                                                                                                         |

# Channel coverage table

| Channel        | Evidence             |
| -------------- | -------------------- |
| Interactive    | Observed             |
| Agentic        | Observed             |
| Conversational | No evidence observed |
| Event          | Observed             |
| Programmatic   | Observed             |

# Multichannel verdict

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
  "generated_at": "2026-09-22T00:00:00Z",
  "evidence_checked_at": "2026-09-22T00:00:00Z",
  "saas": { "name": "Trello" },
  "interfaces": [
    {
      "name": "Web client",
      "technology": "Web application (trello.com)",
      "channel": "Interactive",
      "classification_rationale": "Actions are expressed by manipulating presented affordances (boards, lists, cards, menus) of a persistent, navigable representation of service state.",
      "provenance": [
        {
          "url": "https://www.atlassian.com/software/trello",
          "evidence": "Official product page describing the board/card web UI available in the browser."
        }
      ]
    },
    {
      "name": "Mobile client",
      "technology": "iOS and Android apps",
      "channel": "Interactive",
      "classification_rationale": "First-party mobile apps present the same affordance-manipulation paradigm (touch drag-and-drop board UI); one Interactive interface across both OSes given the shared interaction contract.",
      "provenance": [
        {
          "url": "https://support.atlassian.com/trello/docs/apps/",
          "evidence": "Official support page listing the supported first-party mobile platforms."
        }
      ]
    },
    {
      "name": "Desktop client",
      "technology": "macOS and Windows apps",
      "channel": "Interactive",
      "classification_rationale": "First-party desktop apps present the navigable board UI in a dedicated window; distinct client surface, same Interactive paradigm.",
      "provenance": [
        {
          "url": "https://support.atlassian.com/trello/docs/trello-desktop-apps/",
          "evidence": "Official support page documenting the Mac and Windows desktop apps from the respective app stores."
        }
      ]
    },
    {
      "name": "REST API",
      "technology": "HTTP REST (api.trello.com/1)",
      "channel": "Programmatic",
      "classification_rationale": "Consumer explicitly invokes provider-defined operations through structured HTTP requests under one base and auth; primitive is operation invocation. Batch is part of this interface.",
      "provenance": [
        {
          "url": "https://developer.atlassian.com/cloud/trello/rest/",
          "evidence": "Official REST API reference enumerating operations across boards, cards, lists, webhooks, etc."
        }
      ]
    },
    {
      "name": "Email-to-board / Inbox",
      "technology": "Inbound email to a unique board/Inbox address",
      "channel": "Programmatic",
      "classification_rationale": "Sending a structured email to a provider-defined unique address invokes the create-card operation (subject to title, body to description, @user/#label conventions); message submission as operation invocation, analogous to SMTP submission. Optional AI summary is internal enrichment, not a consumer-facing conversational contract.",
      "provenance": [
        {
          "url": "https://support.atlassian.com/trello/docs/creating-cards-by-email/",
          "evidence": "Official support page documenting unique board/Inbox email addresses that create cards."
        }
      ]
    },
    {
      "name": "Webhooks",
      "technology": "HTTP callbacks to a consumer-controlled URL",
      "channel": "Event",
      "classification_rationale": "The service initiates delivery to a subscriber-provided callbackURL when a watched model changes; service-initiated notification to a consumer-controlled receiver.",
      "provenance": [
        {
          "url": "https://developer.atlassian.com/cloud/trello/guides/rest-api/webhooks/",
          "evidence": "Official webhooks guide describing change notifications delivered to a callback URL."
        }
      ]
    },
    {
      "name": "Trello MCP server",
      "technology": "Remote MCP (mcp.trello.com/v1)",
      "channel": "Agentic",
      "classification_rationale": "Exposes semantically described capabilities discoverable and selectable by an MCP client as part of the interaction contract over OAuth 2.0; capability discovery structures the contract, so Agentic rather than Programmatic.",
      "provenance": [
        {
          "url": "https://support.atlassian.com/trello/docs/connect-trello-to-ai-assistants-with-trello-mcp/",
          "evidence": "Official support page describing the Trello MCP server as the connection layer letting AI assistants read/write/search Trello via approved permissions."
        },
        {
          "url": "https://github.com/atlassian/trello-mcp-server",
          "evidence": "Official Atlassian repository for the remote Trello MCP server."
        }
      ]
    }
  ],
  "access_mechanism_ledger": [
    {
      "mechanism": "Web app (web surface)",
      "disposition": "interface",
      "detail": "Web client"
    },
    {
      "mechanism": "Mobile app (mobile surface)",
      "disposition": "interface",
      "detail": "Mobile client"
    },
    {
      "mechanism": "Desktop app (desktop surface)",
      "disposition": "interface",
      "detail": "Desktop client"
    },
    {
      "mechanism": "Terminal/CLI (terminal surface)",
      "disposition": "excluded",
      "detail": "No first-party Trello CLI or TUI; the ACLI/'Trello CLI' and community CLIs are third-party."
    },
    {
      "mechanism": "REST API",
      "disposition": "interface",
      "detail": "REST API"
    },
    {
      "mechanism": "Batch API",
      "disposition": "excluded",
      "detail": "Same base/auth/invocation style as REST; part of the REST API interface."
    },
    {
      "mechanism": "GraphQL API",
      "disposition": "excluded",
      "detail": "Trello exposes only REST v1; no official GraphQL."
    },
    {
      "mechanism": "Email-to-board / Inbox-by-email",
      "disposition": "interface",
      "detail": "Email-to-board / Inbox"
    },
    {
      "mechanism": "Webhooks",
      "disposition": "interface",
      "detail": "Webhooks"
    },
    {
      "mechanism": "Trello MCP server",
      "disposition": "interface",
      "detail": "Trello MCP server"
    },
    {
      "mechanism": "Atlassian Rovo MCP server",
      "disposition": "excluded",
      "detail": "Official docs state Rovo MCP does not currently reach Trello data."
    },
    {
      "mechanism": "Conversational AI assistant",
      "disposition": "excluded",
      "detail": "No first-party natural-language assistant is the consumer-facing contract; AI access is via the MCP interface, and email/Inbox AI summary is internal enrichment."
    },
    {
      "mechanism": "Power-Ups platform",
      "disposition": "excluded",
      "detail": "Third-party extension/plugin platform augmenting the UI and consuming REST; not a distinct provider access interface."
    },
    {
      "mechanism": "Butler automation",
      "disposition": "excluded",
      "detail": "Internal automation feature configured through the web UI; not a separate access interface."
    },
    {
      "mechanism": "client.js",
      "disposition": "excluded",
      "detail": "JavaScript client library/SDK wrapping the REST API."
    },
    {
      "mechanism": "Integrations / marketplace index",
      "disposition": "excluded",
      "detail": "Catalog of third-party integrations, not a provider interface."
    }
  ],
  "channel_evidence": {
    "Interactive": "observed",
    "Agentic": "observed",
    "Conversational": "no_evidence_observed",
    "Event": "observed",
    "Programmatic": "observed"
  },
  "number_of_interfaces": 7,
  "multi_interface": true,
  "number_of_channels": 4,
  "multi_channel": true
}
```
