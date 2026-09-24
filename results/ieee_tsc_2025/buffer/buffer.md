## SaaS summary

Buffer is a social media management platform (buffer.com). Its official documentation supports six provider-defined logical interfaces, spread across three distinct access channels.

## Interface classification table

| Interface                     | Channel      | Interaction technology                 | Provenance                                                                                                                                                                                                                                                                                                                                              |
| ----------------------------- | ------------ | -------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Web application               | Interactive  | Web app (publish.buffer.com)           | The Publish, Create and Insights feature pages describe planning, scheduling and analytics done by working a navigable dashboard, and the site's "Open Buffer" control opens the signed-in web client. Actions are affordance manipulation over a persistent representation of account state. Current.                                                  |
| Mobile apps (iOS and Android) | Interactive  | Native mobile apps                     | The footer links a first-party iOS app (App Store id 490474324) and Android app (org.buffer.android), and the apple-itunes-app meta tag advertises the same iOS app. Same affordance-manipulation paradigm on the mobile surface; the two OS builds share one interaction contract, so they count as one interface. Current.                            |
| Browser extension             | Interactive  | Chrome browser extension               | The official extensions page describes a first-party extension that opens a composer to share links, images and videos from any web page without returning to the dashboard. Its own surface, primitive is affordance manipulation. Current.                                                                                                            |
| GraphQL API                   | Programmatic | GraphQL API (api.buffer.com)           | The developer portal documents a single GraphQL endpoint with an Account, Organizations, Channels, Posts and Ideas reference plus guides and examples. The consumer explicitly invokes provider-defined queries and mutations. Current.                                                                                                                 |
| Command-line interface        | Programmatic | Buffer CLI (@bufferapp/cli)            | The CLI guide documents commands of the form `buffer <group> <command> [flags]` with structured JSON output generated from the schema. The only interactive step is a setup wizard that collects parameters, and no persistent navigable TUI exists, so it is one Programmatic interface. Current.                                                      |
| MCP server                    | Agentic      | Remote MCP server (mcp.buffer.com/mcp) | The MCP guide documents named tools (get_account, list_channels, create_post and others), an introspect_schema tool, a `buffer://schema` resource and a prompt. Capability discovery and selection are part of the contract, which resolves the MCP boundary case to Agentic rather than Programmatic even though it ultimately calls GraphQL. Current. |

## Coverage ledger table

| Access mechanism                                                                                                       | Disposition                                                                                                                                                                                                       |
| ---------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Web client (web surface)                                                                                               | Web application                                                                                                                                                                                                   |
| Mobile client (mobile surface)                                                                                         | Mobile apps (iOS and Android)                                                                                                                                                                                     |
| Desktop client (desktop surface)                                                                                       | Excluded: no first-party desktop application found in official product or footer listings (only web, mobile and browser-extension clients).                                                                       |
| Browser extension                                                                                                      | Browser extension                                                                                                                                                                                                 |
| CLI / terminal (terminal surface)                                                                                      | Command-line interface; checked for a TUI, none present (only a setup wizard).                                                                                                                                    |
| GraphQL API                                                                                                            | GraphQL API                                                                                                                                                                                                       |
| Legacy REST API (api.bufferapp.com)                                                                                    | Excluded: deprecated and superseded by the GraphQL API (docs carry a REST-migration guide and a Legacy Apps page). Historically Programmatic, not the present-day interface.                                      |
| MCP server                                                                                                             | MCP server                                                                                                                                                                                                        |
| AI Assistant                                                                                                           | Excluded: an in-composer content feature of the web app (generate, rephrase, shorten, expand, tone in the post composer and Create space), not a separate access mechanism or a conversational service interface. |
| Webhooks / events / subscriptions                                                                                      | Excluded: no provider-defined event, webhook or subscription mechanism found in current developer docs. No evidence is not absence.                                                                               |
| API Explorer (explorer.html)                                                                                           | Excluded: an interactive documentation and testing console for the GraphQL API, not a distinct production interface.                                                                                              |
| Third-party integrations (Zapier, n8n, Notion, Manus, Grok, Cursor, Antigravity, Raycast, Perplexity, Claude, ChatGPT) | Excluded: third-party consumers. The AI-assistant integrations consume the MCP server already counted; Zapier and n8n consume the GraphQL API.                                                                    |
| Docs AI helper                                                                                                         | Excluded: a documentation assistant for debugging queries, not a way to access service state.                                                                                                                     |
| SDKs / client libraries (Node, Ruby wrappers)                                                                          | Excluded: client libraries are not interfaces; those located are third-party or legacy.                                                                                                                           |
| OAuth / API keys                                                                                                       | Excluded: authentication methods supporting the API and MCP interfaces, not interfaces.                                                                                                                           |
| Start Page (link-in-bio)                                                                                               | Excluded: an end-product and publishing target, not an access mechanism for managing Buffer.                                                                                                                      |

## Channel coverage table

| Channel        | Evidence             |
| -------------- | -------------------- |
| Interactive    | Observed             |
| Agentic        | Observed             |
| Conversational | No evidence observed |
| Event          | No evidence observed |
| Programmatic   | Observed             |

## Multichannel verdict

Multichannel (3 distinct paradigms).

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
  "saas": { "name": "Buffer" },
  "interfaces": [
    {
      "name": "Web application",
      "technology": "Web app (publish.buffer.com)",
      "channel": "Interactive",
      "classification_rationale": "Actions are expressed by manipulating affordances (calendar, queue, post composer, menus, insights views) of a persistent, navigable representation of account state.",
      "provenance": [
        {
          "url": "https://buffer.com/publish",
          "evidence": "Publish/Create/Insights feature pages describe planning, scheduling and analytics performed by manipulating a navigable dashboard; the site's 'Open Buffer' control opens publish.buffer.com, the signed-in web client."
        }
      ]
    },
    {
      "name": "Mobile apps (iOS and Android)",
      "technology": "Native mobile apps",
      "channel": "Interactive",
      "classification_rationale": "First-party mobile client on the mobile surface; the primitive is affordance manipulation of the same account state, distinct from the web client only by surface. iOS and Android builds share one interaction contract, so they count as one logical interface.",
      "provenance": [
        {
          "url": "https://buffer.com/extensions",
          "evidence": "Site footer links a first-party iOS App (App Store id 490474324) and Android App (org.buffer.android); the apple-itunes-app meta tag on Buffer pages advertises the same iOS app."
        }
      ]
    },
    {
      "name": "Browser extension",
      "technology": "Chrome browser extension",
      "channel": "Interactive",
      "classification_rationale": "A first-party client on its own surface that presents a composer popup (text field, media, channel and schedule controls) to add content to the queue from any web page. The primitive is affordance manipulation, distinct from the web app by surface.",
      "provenance": [
        {
          "url": "https://buffer.com/extensions",
          "evidence": "Official extensions page describes the Buffer browser extension for sharing links, images and videos from anywhere on the web without returning to the dashboard, installed from the Chrome Web Store."
        }
      ]
    },
    {
      "name": "GraphQL API",
      "technology": "GraphQL API (api.buffer.com)",
      "channel": "Programmatic",
      "classification_rationale": "The consumer explicitly invokes provider-defined queries and mutations through structured requests against a single GraphQL endpoint. The primitive is explicit operation invocation.",
      "provenance": [
        {
          "url": "https://developers.buffer.com/index.html",
          "evidence": "Developer portal documents a single GraphQL endpoint with an Account/Organizations/Channels/Posts/Ideas API reference, guides and examples; the developers page describes 'a single GraphQL endpoint'."
        }
      ]
    },
    {
      "name": "Command-line interface (CLI)",
      "technology": "Buffer CLI (@bufferapp/cli, npm)",
      "channel": "Programmatic",
      "classification_rationale": "Actions are expressed as explicit commands of the shape 'buffer <group> <command> [flags]' with structured JSON output. The interactive 'buffer init' step only collects setup parameters and there is no persistent navigable TUI dashboard, so it is a single Programmatic interface.",
      "provenance": [
        {
          "url": "https://developers.buffer.com/guides/cli.html",
          "evidence": "CLI guide documents command groups (account, channels, posts, ideas, schema), flags, exit codes and JSON output generated from the GraphQL schema; the only interactive element is a setup wizard, not a navigable dashboard."
        }
      ]
    },
    {
      "name": "MCP server",
      "technology": "Remote Model Context Protocol server (mcp.buffer.com/mcp)",
      "channel": "Agentic",
      "classification_rationale": "The server exposes semantically described tools plus schema introspection and a 'buffer://schema' resource, so capability discovery and selection are part of the interaction contract. Although it ultimately invokes GraphQL, the discovery-structured contract makes it Agentic rather than Programmatic (MCP boundary case).",
      "provenance": [
        {
          "url": "https://developers.buffer.com/guides/integrations/mcp.html",
          "evidence": "Buffer runs a remote MCP server exposing named tools (get_account, list_channels, create_post, etc.), an 'introspect_schema' tool, a 'buffer://schema' resource and a prompt, enabling assistants to discover and select capabilities as part of the contract."
        }
      ]
    }
  ],
  "access_mechanism_ledger": [
    {
      "mechanism": "Web client (web surface)",
      "disposition": "interface",
      "detail": "Web application"
    },
    {
      "mechanism": "Mobile client (mobile surface)",
      "disposition": "interface",
      "detail": "Mobile apps (iOS and Android)"
    },
    {
      "mechanism": "Desktop client (desktop surface)",
      "disposition": "excluded",
      "detail": "Excluded: no first-party desktop application found in official product or footer listings (web, mobile and browser-extension clients only)."
    },
    {
      "mechanism": "Browser extension",
      "disposition": "interface",
      "detail": "Browser extension"
    },
    {
      "mechanism": "CLI / terminal (terminal surface)",
      "disposition": "interface",
      "detail": "Command-line interface (CLI); checked for a TUI, none present (only a setup wizard)."
    },
    {
      "mechanism": "GraphQL API",
      "disposition": "interface",
      "detail": "GraphQL API"
    },
    {
      "mechanism": "Legacy REST API (api.bufferapp.com)",
      "disposition": "excluded",
      "detail": "Excluded: deprecated and superseded by the current GraphQL API (docs provide a REST-migration guide and a Legacy Apps page). Historically Programmatic; not the present-day interface."
    },
    {
      "mechanism": "MCP server",
      "disposition": "interface",
      "detail": "MCP server"
    },
    {
      "mechanism": "AI Assistant",
      "disposition": "excluded",
      "detail": "Excluded: an in-composer content-generation feature of the web app (generate, rephrase, shorten, expand, tone within the post composer and Create space), not a distinct access mechanism or a conversational service interface."
    },
    {
      "mechanism": "Webhooks / events / subscriptions",
      "disposition": "excluded",
      "detail": "Excluded: no provider-defined event, webhook or subscription mechanism found in current developer docs (API reference exposes account, organizations, channels, posts, ideas and other, with no events). No evidence is not evidence of absence."
    },
    {
      "mechanism": "API Explorer (developers.buffer.com/explorer.html)",
      "disposition": "excluded",
      "detail": "Excluded: an interactive documentation and testing console for the GraphQL API, not a distinct production interface."
    },
    {
      "mechanism": "Third-party integrations (Zapier, n8n, Notion, Manus, Grok, Cursor, Antigravity, Raycast, Perplexity, Claude, ChatGPT)",
      "disposition": "excluded",
      "detail": "Excluded: third-party integrations/consumers. The AI-assistant integrations consume the already-counted MCP server; Zapier and n8n consume the GraphQL API. None is a provider-defined interface of its own."
    },
    {
      "mechanism": "Docs AI helper",
      "disposition": "excluded",
      "detail": "Excluded: a documentation assistant that helps debug queries, not a mechanism for accessing service state."
    },
    {
      "mechanism": "SDKs / client libraries (Node, Ruby wrappers)",
      "disposition": "excluded",
      "detail": "Excluded: client libraries are not interfaces; the wrappers located are third-party and/or legacy."
    },
    {
      "mechanism": "OAuth / API keys",
      "disposition": "excluded",
      "detail": "Excluded: authentication methods that support the API and MCP interfaces rather than being interfaces themselves."
    },
    {
      "mechanism": "Start Page (link-in-bio)",
      "disposition": "excluded",
      "detail": "Excluded: an end-product/publishing feature (a hosted bio page and a posting target), not an access mechanism for managing the Buffer service."
    }
  ],
  "channel_evidence": {
    "Interactive": "observed",
    "Agentic": "observed",
    "Conversational": "no_evidence_observed",
    "Event": "no_evidence_observed",
    "Programmatic": "observed"
  },
  "number_of_interfaces": 6,
  "multi_interface": true,
  "number_of_channels": 3,
  "multi_channel": true
}
```
