# Interface classification table

| Interface                       | Channel        | Interaction technology                       | Provenance                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| ------------------------------- | -------------- | -------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Web application                 | Interactive    | Browser web client                           | ClickUp's help center documents a first-party web client, and the product pages describe navigable views (List, Board, Gantt, Calendar, Table). Actions are expressed by manipulating presented affordances of persistent workspace state, so the primitive is affordance manipulation. Current. (help.clickup.com, "ClickUp Apps across all devices"; clickup.com)                                                                                                                                               |
| Desktop application             | Interactive    | Native Mac / Windows / Linux client          | The help center documents a first-party desktop app for macOS, Windows, and Linux that renders the same navigable workspace on a separate surface. Same affordance-manipulation paradigm as the web client, distinct surface. Current. (help.clickup.com, "Use the ClickUp desktop app")                                                                                                                                                                                                                          |
| Mobile application              | Interactive    | Native iOS / Android client                  | The help center and the provider's app-store listings document first-party iOS and Android clients presenting a navigable representation of workspace state. Affordance manipulation on the mobile surface. Current. (help.clickup.com, "ClickUp Apps across all devices"; App Store listing)                                                                                                                                                                                                                     |
| REST API (v2 / v3)              | Programmatic   | HTTP REST over `api.clickup.com`             | The developer portal exposes provider-defined endpoints for Tasks, Chat, Docs, Comments, Views, Time Tracking, and webhook management under one base and one auth scheme (personal token or OAuth). The consumer explicitly invokes named operations through structured requests, so the primitive is operation invocation. Current. (developer.clickup.com/reference)                                                                                                                                            |
| Inbound email to task / comment | Programmatic   | Email submission to a ClickUp-issued address | The Email ClickApp issues a unique address per task and per List; sending or forwarding a message to that address invokes a create-task or create-comment operation, with the address encoding the target. The primitive is operation invocation by message submission (analogous to SMTP submission), not natural-language interpretation. Current. (help.clickup.com, "Create tasks and comments via email"; "Use Email in ClickUp")                                                                            |
| Webhooks                        | Event          | HTTP callbacks to a subscriber URL           | The developer portal documents webhook creation where ClickUp initiates delivery to a consumer-controlled receiver when subscribed events occur. The service starts the interaction on an event, which is event notification, not consumer-invoked retrieval. Current. (developer.clickup.com, "Webhooks"; "Create Webhook")                                                                                                                                                                                      |
| MCP Server                      | Agentic        | Model Context Protocol server                | The developer portal documents an official ClickUp MCP server with a set of supported tools, and the Brain help page confirms it is first-party. Capabilities are semantically described and selectable as part of the interaction contract, so discovery and selection structure the contract. That places it in Agentic rather than Programmatic despite tools ultimately being invoked. Current. (developer.clickup.com, "ClickUp's MCP Server", "Supported Tools"; help.clickup.com, "What is ClickUp Brain") |
| ClickUp Brain                   | Conversational | Natural-language AI assistant                | The help center describes Brain as a natural-language assistant you chat with, which answers and takes actions such as creating tasks or summarizing. The consumer-facing primitive is the message; tool orchestration is internal to the service and not exposed as a discovery contract, so it is Conversational rather than Agentic. Current. (help.clickup.com, "Chat with Brain"; "What is ClickUp Brain")                                                                                                   |

# Coverage ledger table

| Access mechanism                                  | Disposition                                                                                                                                      |
| ------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| API / API Reference (REST v2 and v3)              | REST API (v2 / v3)                                                                                                                               |
| Chat API                                          | Folded into REST API (same base and auth)                                                                                                        |
| Docs API                                          | Folded into REST API (same base and auth)                                                                                                        |
| Comments API                                      | Folded into REST API (same base and auth)                                                                                                        |
| Webhooks                                          | Webhooks                                                                                                                                         |
| MCP Server                                        | MCP Server                                                                                                                                       |
| ClickUp Brain / AI assistant                      | ClickUp Brain                                                                                                                                    |
| Web client                                        | Web application                                                                                                                                  |
| Desktop client (Mac / Windows / Linux)            | Desktop application                                                                                                                              |
| Mobile client (iOS / Android)                     | Mobile application                                                                                                                               |
| Terminal / CLI surface                            | Excluded: no first-party CLI documented on the developer portal or product pages                                                                 |
| Email ClickApp (create tasks / comments by email) | Inbound email to task / comment                                                                                                                  |
| Outlook Add-In, Chrome extension, email add-on    | Excluded: first-party add-ons embedded inside third-party clients that drive the existing web/API interfaces, not standalone provider interfaces |
| Forms                                             | Excluded: a view type inside the web application surface, not a separate interaction contract                                                    |
| Autopilot / Super / Ambient Agents                | Excluded: configurable in-workspace automation features, built and run through Brain and the UI, not a consumer access channel                   |
| Talk to Text, AI Notetaker                        | Excluded: input modalities and features within Brain, not separate access interfaces                                                             |
| Integrations directory                            | Excluded: third-party integrations, not provider-defined interfaces                                                                              |
| SDKs, OpenAPI spec, OAuth, API keys               | Excluded per counting rules: these implement or support an interface without being one                                                           |

# Channel coverage table

| Channel        | Evidence |
| -------------- | -------- |
| Interactive    | Observed |
| Agentic        | Observed |
| Conversational | Observed |
| Event          | Observed |
| Programmatic   | Observed |

# Multichannel verdict

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
  "generated_at": "2026-09-24T00:00:00Z",
  "evidence_checked_at": "2026-09-24T00:00:00Z",
  "saas": {
    "name": "ClickUp"
  },
  "interfaces": [
    {
      "name": "Web application",
      "technology": "Browser web client",
      "channel": "Interactive",
      "classification_rationale": "Actions are expressed by manipulating presented affordances (List, Board, Gantt, Calendar and other views) of a persistent, navigable representation of workspace state.",
      "provenance": [
        {
          "url": "https://help.clickup.com/hc/en-us/articles/6311182548887-ClickUp-Apps-across-all-devices",
          "evidence": "Documents a first-party web client alongside desktop and mobile."
        },
        {
          "url": "https://clickup.com/",
          "evidence": "Product page lists navigable views and workspace surfaces."
        }
      ]
    },
    {
      "name": "Desktop application",
      "technology": "Native macOS / Windows / Linux client",
      "channel": "Interactive",
      "classification_rationale": "A first-party desktop client renders the same navigable workspace on a distinct surface; the primitive remains affordance manipulation.",
      "provenance": [
        {
          "url": "https://help.clickup.com/hc/en-us/articles/6311884486423-Use-the-ClickUp-desktop-app",
          "evidence": "Documents native desktop apps for Mac, Windows, and Linux."
        }
      ]
    },
    {
      "name": "Mobile application",
      "technology": "Native iOS / Android client",
      "channel": "Interactive",
      "classification_rationale": "First-party mobile clients present a navigable representation of workspace state; actions are expressed by manipulating on-screen affordances.",
      "provenance": [
        {
          "url": "https://help.clickup.com/hc/en-us/articles/6311182548887-ClickUp-Apps-across-all-devices",
          "evidence": "Documents first-party iOS and Android apps."
        },
        {
          "url": "https://apps.apple.com/us/app/clickup-manage-teams-tasks/id1535098836",
          "evidence": "Provider's App Store listing for the mobile client."
        }
      ]
    },
    {
      "name": "REST API (v2 / v3)",
      "technology": "HTTP REST over api.clickup.com",
      "channel": "Programmatic",
      "classification_rationale": "The consumer explicitly invokes provider-defined operations (Tasks, Chat, Docs, Comments, Views, Time Tracking, webhook management) through structured requests under one base and one auth scheme.",
      "provenance": [
        {
          "url": "https://developer.clickup.com/reference",
          "evidence": "API reference exposing named endpoints under api.clickup.com/api/v2 and /v3 with personal token or OAuth auth."
        },
        {
          "url": "https://developer.clickup.com/llms.txt",
          "evidence": "Index of endpoints across Tasks, Chat, Docs, and webhook management sharing the same base and auth."
        }
      ]
    },
    {
      "name": "Inbound email to task / comment",
      "technology": "Email submission to a ClickUp-issued address",
      "channel": "Programmatic",
      "classification_rationale": "Sending a message to a unique ClickUp-issued task or List address invokes a create-task or create-comment operation encoded by the address; the primitive is operation invocation by message submission, not natural-language interpretation.",
      "provenance": [
        {
          "url": "https://help.clickup.com/hc/en-us/articles/6309707288599-Create-tasks-and-comments-via-email",
          "evidence": "Unique addresses per task and List; sending an email creates a task or comment."
        },
        {
          "url": "https://help.clickup.com/hc/en-us/articles/6303747270807-Use-Email-in-ClickUp",
          "evidence": "Email ClickApp enabling task and comment creation by email."
        }
      ]
    },
    {
      "name": "Webhooks",
      "technology": "HTTP callbacks to a subscriber URL",
      "channel": "Event",
      "classification_rationale": "ClickUp initiates the interaction when subscribed events occur and delivers to a consumer-controlled receiver URL, which is event notification rather than consumer-invoked retrieval.",
      "provenance": [
        {
          "url": "https://developer.clickup.com/docs/webhooks.md",
          "evidence": "Documents subscribing to events and delivery to a receiver."
        },
        {
          "url": "https://developer.clickup.com/reference/createwebhook.md",
          "evidence": "Create Webhook endpoint monitoring events and posting to a URL."
        }
      ]
    },
    {
      "name": "MCP Server",
      "technology": "Model Context Protocol server",
      "channel": "Agentic",
      "classification_rationale": "The official MCP server exposes semantically described tools that are discoverable and selectable as part of the interaction contract, so discovery and selection structure the contract rather than mere operation invocation.",
      "provenance": [
        {
          "url": "https://developer.clickup.com/docs/connect-an-ai-assistant-to-clickups-mcp-server.md",
          "evidence": "Documents ClickUp's official MCP server for AI assistants."
        },
        {
          "url": "https://developer.clickup.com/docs/mcp-tools.md",
          "evidence": "Lists the supported tools the MCP server advertises for selection."
        }
      ]
    },
    {
      "name": "ClickUp Brain",
      "technology": "Natural-language AI assistant",
      "channel": "Conversational",
      "classification_rationale": "The consumer interacts through natural-language messages the service interprets; task creation, search, and summarization are orchestrated internally and are not exposed as a discovery contract, so it is Conversational rather than Agentic.",
      "provenance": [
        {
          "url": "https://help.clickup.com/hc/en-us/articles/28401383762455-Chat-with-Brain",
          "evidence": "Brain is chatted with using natural language and asks for clarification."
        },
        {
          "url": "https://help.clickup.com/hc/en-us/articles/12578085238039-What-is-ClickUp-Brain",
          "evidence": "Describes Brain as a native AI assistant acting across the workspace."
        }
      ]
    }
  ],
  "access_mechanism_ledger": [
    {
      "mechanism": "API / API Reference (REST v2 and v3)",
      "disposition": "interface",
      "detail": "REST API (v2 / v3)"
    },
    {
      "mechanism": "Chat API",
      "disposition": "interface",
      "detail": "REST API (v2 / v3) (same base and auth)"
    },
    {
      "mechanism": "Docs API",
      "disposition": "interface",
      "detail": "REST API (v2 / v3) (same base and auth)"
    },
    {
      "mechanism": "Comments API",
      "disposition": "interface",
      "detail": "REST API (v2 / v3) (same base and auth)"
    },
    {
      "mechanism": "Webhooks",
      "disposition": "interface",
      "detail": "Webhooks"
    },
    {
      "mechanism": "MCP Server",
      "disposition": "interface",
      "detail": "MCP Server"
    },
    {
      "mechanism": "ClickUp Brain / AI assistant",
      "disposition": "interface",
      "detail": "ClickUp Brain"
    },
    {
      "mechanism": "Web client",
      "disposition": "interface",
      "detail": "Web application"
    },
    {
      "mechanism": "Desktop client (Mac / Windows / Linux)",
      "disposition": "interface",
      "detail": "Desktop application"
    },
    {
      "mechanism": "Mobile client (iOS / Android)",
      "disposition": "interface",
      "detail": "Mobile application"
    },
    {
      "mechanism": "Email ClickApp (create tasks / comments by email)",
      "disposition": "interface",
      "detail": "Inbound email to task / comment"
    },
    {
      "mechanism": "Terminal / CLI surface",
      "disposition": "excluded",
      "detail": "No first-party CLI documented on the developer portal or product pages"
    },
    {
      "mechanism": "Outlook Add-In, Chrome extension, email add-on",
      "disposition": "excluded",
      "detail": "First-party add-ons embedded inside third-party clients that drive the existing web and API interfaces, not standalone provider interfaces"
    },
    {
      "mechanism": "Forms",
      "disposition": "excluded",
      "detail": "A view type inside the web application surface, not a separate interaction contract"
    },
    {
      "mechanism": "Autopilot / Super / Ambient Agents",
      "disposition": "excluded",
      "detail": "In-workspace automation features built and run through Brain and the UI, not a consumer access channel"
    },
    {
      "mechanism": "Talk to Text, AI Notetaker",
      "disposition": "excluded",
      "detail": "Input modalities and features within Brain, not separate access interfaces"
    },
    {
      "mechanism": "Integrations directory",
      "disposition": "excluded",
      "detail": "Third-party integrations, not provider-defined interfaces"
    },
    {
      "mechanism": "SDKs, OpenAPI spec, OAuth, API keys",
      "disposition": "excluded",
      "detail": "Implement or support an interface without being one"
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
