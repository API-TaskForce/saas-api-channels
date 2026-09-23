I'll investigate Zapier's official documentation to reconstruct its logical interfaces and classify each by access channel.Zapier is a large platform with many surfaces. Let me build the worklist by examining the official developer docs and product pages.I have the developer surfaces. Now let me examine the API reference, MCP, mobile/desktop clients, and AI assistant surfaces.The Partner/Workflow API is a REST API. Now let me verify the first-party client surfaces (mobile, desktop) and the AI-native surfaces (MCP, Copilot, Agents).No first-party mobile or desktop app exists (only a Chrome extension). Let me confirm the MCP, SDK/CLI, and AI assistant surfaces.I have the developer surfaces mapped. Let me confirm the natural-language surfaces (Copilot, Agents) since those determine whether a Conversational channel is observed.I have strong evidence across all surfaces. Let me do one final check on the status of AI Actions (NLA) to record freshness accurately.I now have complete coverage across Zapier's surfaces, with freshness confirmed (AI Actions is deprecated in favor of MCP). Let me validate my JSON structure against the skill's checker before finalizing.The validator expects a newer schema version than the SKILL text. Let me inspect it to align exactly.Structural invariants pass. Here is the analysis.

## SaaS summary

**Zapier** exposes **7 logical interfaces** spanning **4 distinct access channels**. The service can be reached through its web application and Chrome extension, a REST API and two command-line tools, a Model Context Protocol server, and an in-product natural-language assistant. Zapier ships no first-party consumer mobile or desktop client, and no provider-level event interface was found in official documentation.

## Interface classification table

| Interface                                   | Channel        | Interaction technology                                                                                                                   | Provenance                                                                                                                                                                                                                                                                                                                         |
| ------------------------------------------- | -------------- | ---------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Zapier web application                      | Interactive    | Web GUI: Zap editor, dashboard, Tables, Interfaces, Canvas, Agents and Chatbots consoles, and the Platform UI visual integration builder | Help docs describe the Zap editor as a navigable canvas whose steps users configure, test, publish and turn on through on-screen controls; Platform UI is documented as a visual form editor in the browser. Actions are expressed by affordance manipulation on a persistent representation of state. Current.                    |
| Zapier Chrome extension                     | Interactive    | First-party browser toolbar extension with its own panel                                                                                 | Official help doc: the extension lets users select a Zap, fill input fields, click Send, and view replies rendered in the panel. Same affordance-manipulation primitive on a distinct first-party client surface. Current.                                                                                                         |
| Partner API / Workflow API                  | Programmatic   | REST over HTTPS at `api.zapier.com` (v1/v2), OAuth scopes                                                                                | Official OpenAPI titled "Partner API" defines discrete operations such as `POST /v2/action-runs`, `GET /v2/zap-runs`, and `GET /v1/profiles/me`. The consumer invokes provider-defined operations through structured requests under one base and auth, so it is one Programmatic interface. Current.                               |
| Zapier Platform CLI                         | Programmatic   | Command-line tool (`zapier-platform-cli`: `login`, `deploy`, `convert`)                                                                  | Official docs present it as a terminal toolset to build, test and manage integrations. Command invocation with no navigable view. Distinct from the SDK CLI by package, deploy-key auth and integration-building purpose. Current.                                                                                                 |
| Zapier SDK CLI                              | Programmatic   | Command-line tool (`@zapier/zapier-sdk-cli`: `list-apps`, `list-actions`, `run-action`, `curl`)                                          | Official SDK docs list terminal commands to inspect and run authenticated actions across apps. Command invocation, no persistent TUI. Distinct from the Platform CLI by package, connection-based auth and action-execution purpose. Current.                                                                                      |
| Zapier MCP                                  | Agentic        | Model Context Protocol server (hosted at `mcp.zapier.com`; local server via `@zapier/zapier-sdk-mcp`)                                    | Official docs: one MCP server gives any MCP client governed access to your apps and actions, with tools discovered and selected by the client then invoked. Capability discovery and selection are part of the contract, which fixes it as Agentic rather than Programmatic. Current.                                              |
| Zapier Copilot (natural-language assistant) | Conversational | In-product AI assistant chat in the Zap editor, home page and Agents; the Agents natural-language chat shares this paradigm              | Official help docs: Copilot is an assistant you chat with in a prompt box to build, configure and refine Zaps, agents, tables, interfaces and actions. The primitive is the natural-language message and tool orchestration is internal to the service, which fixes it as Conversational rather than Agentic. Current (open beta). |

## Coverage ledger

| Access mechanism                                                                 | Disposition                                                                                                                                             |
| -------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Web application (Zap editor, dashboard, Tables, Interfaces, Canvas, Platform UI) | Zapier web application (Interactive)                                                                                                                    |
| Chrome extension                                                                 | Zapier Chrome extension (Interactive)                                                                                                                   |
| First-party mobile client (surface check)                                        | Excluded: no first-party consumer mobile app. An iOS beta from 2020 was never released; the only store apps are internal Zapier event apps.             |
| First-party desktop client (surface check)                                       | Excluded: no native desktop application; the browser client is the Chrome extension, already counted.                                                   |
| Terminal TUI (surface check on each CLI)                                         | Excluded: neither CLI exposes a persistent navigable TUI dashboard; both are command interfaces counted as Programmatic.                                |
| Partner API / Workflow API (`api.zapier.com`)                                    | Partner API / Workflow API (Programmatic)                                                                                                               |
| Zapier Platform CLI                                                              | Zapier Platform CLI (Programmatic)                                                                                                                      |
| Zapier SDK CLI                                                                   | Zapier SDK CLI (Programmatic)                                                                                                                           |
| Zapier SDK (TypeScript/Python library)                                           | Excluded: client library that wraps the API and materializes as the SDK CLI and a local MCP server; SDKs are not counted as logical interfaces.         |
| Zapier MCP (hosted and local)                                                    | Zapier MCP (Agentic)                                                                                                                                    |
| Zapier Copilot                                                                   | Zapier Copilot (Conversational)                                                                                                                         |
| Zapier Agents                                                                    | Folded into the Conversational interface: the agent chat shares the natural-language-message primitive with Copilot (same channel).                     |
| Zapier Chatbots                                                                  | Excluded: a customer-facing chatbot product built and embedded for a user's own end-users; an output artifact, not a way to access the Zapier platform. |
| Webhooks by Zapier / Email by Zapier                                             | Excluded: built-in trigger apps configured inside a Zap, not a standalone provider-wide access interface.                                               |
| AI Actions (Natural Language Actions / NLA)                                      | Excluded: deprecated and no longer developed or supported, officially superseded by Zapier MCP.                                                         |
| Powered by Zapier / Embed / White Label                                          | Excluded: a distribution of existing interfaces (the Partner/Workflow API plus the embedded web editor), not a new logical interface.                   |
| SDKs, client libraries, OAuth, API keys, npm packages, App Directory             | Excluded: support or implement interfaces without being logical interfaces per the counting rules.                                                      |

## Channel coverage

| Channel        | Evidence             |
| -------------- | -------------------- |
| Interactive    | Observed             |
| Agentic        | Observed             |
| Conversational | Observed             |
| Event          | No evidence observed |
| Programmatic   | Observed             |

## Classification notes

The two command-line tools are kept as separate Programmatic interfaces rather than merged, because their interaction contracts genuinely differ: the Platform CLI authenticates with a deploy key and manages integration publishing, while the SDK CLI authenticates through app connections and runs actions. The same granularity rule keeps them distinct from the REST Partner/Workflow API, which uses a different primitive (HTTP request rather than shell command).

The Event channel is recorded as "no evidence observed" rather than absent. Zapier reacts to events pervasively, but that orchestration is internal. The one candidate found, the optional `callback_url` on the Partner API action-run endpoint, is a callback within a Programmatic operation rather than a standalone provider-initiated subscription interface, so it does not establish the Event paradigm.

## Multichannel verdict

**Multichannel** (4 distinct paradigms observed).

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
  "generated_at": "2026-09-23T12:00:00Z",
  "evidence_checked_at": "2026-09-23T12:00:00Z",
  "saas": {
    "name": "Zapier"
  },
  "interfaces": [
    {
      "name": "Zapier web application",
      "technology": "Web GUI (Zap editor, dashboard, Tables, Interfaces, Canvas, Agents/Chatbots consoles, and the Platform UI visual integration builder)",
      "channel": "Interactive",
      "classification_rationale": "Actions are expressed by manipulating presented affordances (views, forms, menus, buttons) of a persistent, navigable representation of account and workflow state. The primitive is affordance manipulation, not command or message.",
      "provenance": [
        {
          "url": "https://help.zapier.com/hc/en-us/articles/15703650952077-Use-the-power-of-AI-to-generate-Zaps",
          "evidence": "Official help docs describe the Zap editor as a navigable canvas of steps that users configure, test, publish and turn on through on-screen controls. Current."
        },
        {
          "url": "https://docs.zapier.com/integrations/manage/export-cli.md",
          "evidence": "Official docs describe Platform UI as a visual form editor to build integrations in the browser, confirming a web GUI surface under the same account. Current."
        }
      ]
    },
    {
      "name": "Zapier Chrome extension",
      "technology": "Browser toolbar extension panel",
      "channel": "Interactive",
      "classification_rationale": "A first-party browser client presenting its own panel where the user selects a Zap, fills fields and clicks Send, then sees results rendered in the panel. Interaction is affordance manipulation on a presented view, so it is Interactive despite the different surface.",
      "provenance": [
        {
          "url": "https://help.zapier.com/hc/en-us/articles/8496306654349-Use-the-Zapier-Chrome-extension",
          "evidence": "Official help doc: the extension lets users create, send, retrieve information and run Zap workflows from a toolbar panel with input fields and a Send button. Current."
        }
      ]
    },
    {
      "name": "Partner API / Workflow API",
      "technology": "REST API over HTTPS (api.zapier.com, v1/v2, OAuth scopes)",
      "channel": "Programmatic",
      "classification_rationale": "The consumer explicitly invokes provider-defined operations through structured HTTP requests to fixed endpoints (for example POST /v2/action-runs, GET /v2/zap-runs, GET /v1/profiles/me). The primitive is operation invocation under a fixed base and OAuth authentication, so it is one logical interface.",
      "provenance": [
        {
          "url": "https://docs.zapier.com/api-reference/workflow/experimental/create-an-action-run.md",
          "evidence": "Official OpenAPI titled 'Partner API' at base https://api.zapier.com defines discrete operations with OAuth scopes, for example action-runs, action test, zap-runs, accounts. Current."
        }
      ]
    },
    {
      "name": "Zapier Platform CLI",
      "technology": "Command-line tool (zapier-platform-cli; commands such as zapier login, deploy, convert)",
      "channel": "Programmatic",
      "classification_rationale": "The consumer explicitly invokes provider-defined commands to build, test, deploy and manage integrations. The primitive is command invocation with no persistent navigable view, so it is Programmatic rather than Interactive. It is a distinct interface from the SDK CLI (different package, deploy-key authentication and purpose).",
      "provenance": [
        {
          "url": "https://docs.zapier.com/integrations/manage/export-cli.md",
          "evidence": "Official docs describe the Platform CLI as a terminal toolset to build, test and manage integrations with commands like zapier convert. Current."
        }
      ]
    },
    {
      "name": "Zapier SDK CLI",
      "technology": "Command-line tool (@zapier/zapier-sdk-cli; commands such as list-apps, list-actions, run-action, curl)",
      "channel": "Programmatic",
      "classification_rationale": "The consumer explicitly invokes provider-defined commands from the terminal to inspect and run actions across connected apps. The primitive is command invocation; there is no persistent navigable TUI. It is distinct from the Platform CLI (different package, connection-based authentication and action-execution purpose).",
      "provenance": [
        {
          "url": "https://docs.zapier.com/sdk/using-the-cli",
          "evidence": "Official SDK docs list the CLI commands (list-apps, list-actions, run-action, curl) used to explore and run authenticated actions from the terminal. Current."
        },
        {
          "url": "https://docs.zapier.com/install.md",
          "evidence": "Official install router: 'Zapier CLI. Drive Zapier from the terminal', installed via @zapier/zapier-sdk-cli. Current."
        }
      ]
    },
    {
      "name": "Zapier MCP",
      "technology": "Model Context Protocol server (hosted at mcp.zapier.com; also a local server via @zapier/zapier-sdk-mcp)",
      "channel": "Agentic",
      "classification_rationale": "The interface exposes semantically described tools that an MCP client discovers and selects by goal as part of the interaction contract, then invokes. Capability discovery and selection are part of the contract, which is the defining feature of the Agentic paradigm, so it is Agentic rather than Programmatic.",
      "provenance": [
        {
          "url": "https://docs.zapier.com/",
          "evidence": "Official docs home: one MCP server gives any MCP client governed access to your apps and actions, i.e. discoverable tools selected and invoked by the client. Current."
        },
        {
          "url": "https://docs.zapier.com/install.md",
          "evidence": "Official install router: create an MCP server at mcp.zapier.com, add the tools you need, and paste the server URL into the client's MCP settings. Current."
        }
      ]
    },
    {
      "name": "Zapier Copilot (natural-language assistant)",
      "technology": "In-product AI assistant chat (Copilot in the Zap editor, home page and Agents; the Agents natural-language chat surface shares this paradigm)",
      "channel": "Conversational",
      "classification_rationale": "The consumer expresses intent through natural-language messages that the service interprets to build and edit Zaps, agents, tables, interfaces and actions. The primitive is the message and tool orchestration is internal to the service, so it is Conversational rather than Agentic.",
      "provenance": [
        {
          "url": "https://help.zapier.com/hc/en-us/articles/15703650952077-Use-the-power-of-AI-to-generate-Zaps",
          "evidence": "Official help doc: Copilot is an AI assistant you chat with in a prompt box; you describe the workflow and it creates, configures and refines the Zap. Current (open beta)."
        },
        {
          "url": "https://help.zapier.com/hc/en-us/articles/24393442652557-Build-an-agent-in-Zapier-Agents",
          "evidence": "Official help doc: you instruct and refine Agents through a natural-language chat field, confirming a message-primitive surface. Current."
        }
      ]
    }
  ],
  "access_mechanism_ledger": [
    {
      "mechanism": "Web application (Zap editor, dashboard, Tables, Interfaces, Canvas, Platform UI visual builder)",
      "disposition": "interface",
      "detail": "Zapier web application (Interactive)"
    },
    {
      "mechanism": "Chrome extension",
      "disposition": "interface",
      "detail": "Zapier Chrome extension (Interactive)"
    },
    {
      "mechanism": "First-party mobile client (web/mobile/desktop/terminal surface check)",
      "disposition": "excluded",
      "detail": "No first-party consumer mobile app. Zapier tested an iOS beta in 2020 that was never released; the only store apps are internal event apps."
    },
    {
      "mechanism": "First-party desktop client (surface check)",
      "disposition": "excluded",
      "detail": "No native desktop application. The browser-based client is the Chrome extension, already counted."
    },
    {
      "mechanism": "Terminal / CLI TUI (surface check for each CLI)",
      "disposition": "excluded",
      "detail": "Neither the Platform CLI nor the SDK CLI exposes a persistent navigable TUI dashboard; both are command interfaces, counted as Programmatic."
    },
    {
      "mechanism": "Partner API / Workflow API (api.zapier.com)",
      "disposition": "interface",
      "detail": "Partner API / Workflow API (Programmatic)"
    },
    {
      "mechanism": "Zapier Platform CLI",
      "disposition": "interface",
      "detail": "Zapier Platform CLI (Programmatic)"
    },
    {
      "mechanism": "Zapier SDK CLI",
      "disposition": "interface",
      "detail": "Zapier SDK CLI (Programmatic)"
    },
    {
      "mechanism": "Zapier SDK (TypeScript/Python library, @zapier/zapier-sdk)",
      "disposition": "excluded",
      "detail": "Client library that wraps Zapier's API and materializes as the SDK CLI and a local MCP server; SDKs are not counted as logical interfaces."
    },
    {
      "mechanism": "Zapier MCP (hosted mcp.zapier.com and local @zapier/zapier-sdk-mcp)",
      "disposition": "interface",
      "detail": "Zapier MCP (Agentic)"
    },
    {
      "mechanism": "Zapier Copilot (natural-language assistant)",
      "disposition": "interface",
      "detail": "Zapier Copilot (Conversational)"
    },
    {
      "mechanism": "Zapier Agents",
      "disposition": "interface",
      "detail": "Folded into the Conversational interface: the agent chat shares the natural-language-message primitive with Copilot (same channel)."
    },
    {
      "mechanism": "Zapier Chatbots",
      "disposition": "excluded",
      "detail": "A customer-facing chatbot product that users build and embed for their own end-users; it is an output artifact, not an interface for accessing the Zapier platform."
    },
    {
      "mechanism": "Webhooks by Zapier / Email by Zapier (inbound catch hooks and email triggers)",
      "disposition": "excluded",
      "detail": "Built-in trigger apps configured inside a Zap, not a standalone provider-wide access interface."
    },
    {
      "mechanism": "AI Actions (Natural Language Actions / NLA)",
      "disposition": "excluded",
      "detail": "Deprecated and no longer developed or supported; officially superseded by Zapier MCP."
    },
    {
      "mechanism": "Powered by Zapier / Embed / White Label",
      "disposition": "excluded",
      "detail": "A distribution of existing interfaces (the Partner/Workflow API plus the embedded web Zap editor), not a new logical interface."
    },
    {
      "mechanism": "SDKs, client libraries, OAuth, API keys, npm packages, App Directory",
      "disposition": "excluded",
      "detail": "Support or implement interfaces but are not themselves logical interfaces per the counting rules."
    }
  ],
  "channel_evidence": {
    "Interactive": "observed",
    "Agentic": "observed",
    "Conversational": "observed",
    "Event": "no_evidence_observed",
    "Programmatic": "observed"
  },
  "number_of_interfaces": 7,
  "multi_interface": true,
  "number_of_channels": 4,
  "multi_channel": true
}
```
