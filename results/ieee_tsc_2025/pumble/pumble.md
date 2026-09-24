# Interface classification table

| Interface                                  | Channel        | Interaction technology                                                                                                                       | Provenance                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| ------------------------------------------ | -------------- | -------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Pumble client                              | Interactive    | Web app plus native desktop (Windows, macOS, Linux) and mobile (iOS, Android) clients                                                        | pumble.com/apps and the desktop help article establish first-party clients on web, desktop, and mobile. The desktop article states these clients perform the same messaging, administration, and user actions as the web app. The primitive is affordance manipulation of a persistent, navigable representation of workspace state (channels, threads, menus, forms), so all surfaces instantiate one Interactive paradigm and count as one interface. Current.                                                                                                                               |
| Pumble REST API                            | Programmatic   | HTTP REST API (api.pumble.com / docs.pumble.com), reachable with an API-Key-addon key or with OAuth2 app and bot tokens                      | The API Keys addon help page describes generating a key to send messages, reactions, and more via HTTP requests against the Swagger-documented action set. The Node SDK API Client reference lists the same operation families (messages, channels, users, workspace, calls, files) and points to docs.pumble.com. The consumer explicitly invokes provider-defined operations through structured requests, which is Operation Invocation. The two credential paths are authentication mechanisms over the same operation set, base, and invocation style, so they are one interface. Current. |
| Incoming Webhooks                          | Programmatic   | HTTP POST of a JSON or form payload to a unique per-webhook URL (api.pumble.com/workspaces/{id}/incomingWebhooks/postMessage/{code})         | The Incoming Webhooks help page documents posting a message by issuing an HTTP POST with a text or attachments payload to a Pumble-generated URL. The consumer explicitly invokes a single provider-defined post-message operation through a structured request, which is Operation Invocation. It is a separate interface from the REST API because the base, credential model (URL-embedded secret rather than API key or OAuth token), and operation scope genuinely differ. Current.                                                                                                       |
| Pumble Apps event and interaction delivery | Event          | Signed HTTPS callbacks to a developer-hosted endpoint (event subscriptions, slash commands, shortcuts, block interactions, view submissions) | The Node SDK getting-started guide shows an app registering `events` (for example NEW_MESSAGE, APP_UNINSTALLED) and `eventSubscriptions.url`, plus slash-command, shortcut, block-interaction, and view-action handlers, all delivered to an `eventsPath` endpoint and signed with the app signing secret. Pumble initiates the interaction when subscribed or user-triggered events occur and delivers to a consumer-controlled receiver, which is Event Notification. The shared delivery contract makes this one interface rather than several. Current.                                    |
| Pumble AI Assistant addon                  | Conversational | In-workspace AI assistant messaged directly or by @mention, backed by a connected LLM provider                                               | The AI Assistant addon help page states that once connected to an AI provider, users communicate with it inside Pumble by direct message or by mentioning it in a channel or group DM, and it responds in a thread. The primitive is the natural-language message interpreted by the service, and any internal orchestration (for example summarizing a thread) is not part of the consumer-facing contract, which places it in Conversational rather than Agentic. Current.                                                                                                                   |
| Pumble native MCP server                   | Agentic        | Model Context Protocol server hosted at pumble.com, exposing tools and built-in prompts to external AI agents                                | The Pumble AI and automation guide states that Pumble maintains a native MCP server hosted at pumble.com to connect a workspace to an AI agent, listing available tools and built-in prompts. Capability discovery and selection structure the interaction contract, which is the defining feature of Capability Discovery and Invocation, so per the MCP boundary rule this is Agentic rather than Programmatic. Current.                                                                                                                                                                     |

# Coverage ledger

| Access mechanism                                                                                              | Disposition                                                                                                                   |
| ------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| Web application                                                                                               | Pumble client (Interactive)                                                                                                   |
| Desktop application (Windows, macOS, Linux)                                                                   | Pumble client (Interactive), same contract as web                                                                             |
| Mobile application (iOS, Android)                                                                             | Pumble client (Interactive), same contract as web                                                                             |
| Terminal / TUI client                                                                                         | Excluded: no first-party navigable TUI is documented; pumble-cli is app-development tooling, not a service TUI                |
| REST API via API Keys addon                                                                                   | Pumble REST API (Programmatic)                                                                                                |
| OAuth2 app and bot token API access (SDK API Client)                                                          | Pumble REST API (Programmatic), same operation set and base, different credential path                                        |
| Incoming Webhooks                                                                                             | Incoming Webhooks (Programmatic)                                                                                              |
| Pumble Apps event subscriptions and events                                                                    | Pumble Apps event and interaction delivery (Event)                                                                            |
| Slash commands, shortcuts, block interactions, view actions (Apps)                                            | Pumble Apps event and interaction delivery (Event), same signed-callback contract                                             |
| AI Assistant addon                                                                                            | Pumble AI Assistant addon (Conversational)                                                                                    |
| Native MCP server                                                                                             | Pumble native MCP server (Agentic)                                                                                            |
| pumble-cli                                                                                                    | Excluded: developer scaffolding and deployment tool for building Pumble Apps; not a service access channel and exposes no TUI |
| SDKs (pumble-sdk / pumble-node-sdk, third-party Python SDK)                                                   | Excluded: client libraries that implement or support interfaces without being one                                             |
| Native partner integrations (Clockify, Plaky, Google Drive, GitHub, GitLab, Zendesk, RSS, Zoom)               | Excluded: third-party or partner integrations, not access channels to Pumble itself                                           |
| Third-party automation and MCP wrappers (Zapier, Make, Pipedream, viaSocket, Composio, community MCP servers) | Excluded: not provider-defined                                                                                                |
| Email / SMTP message ingestion                                                                                | Excluded: no official provider mechanism to post into Pumble by email was found                                               |

# Channel coverage

| Channel        | Evidence |
| -------------- | -------- |
| Interactive    | Observed |
| Agentic        | Observed |
| Conversational | Observed |
| Event          | Observed |
| Programmatic   | Observed |

# Multichannel verdict

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
  "generated_at": "2026-09-24T00:00:00Z",
  "evidence_checked_at": "2026-09-24T00:00:00Z",
  "saas": { "name": "Pumble" },
  "interfaces": [
    {
      "name": "Pumble client",
      "technology": "Web app plus native desktop (Windows, macOS, Linux) and mobile (iOS, Android) clients",
      "channel": "Interactive",
      "classification_rationale": "The primitive is affordance manipulation of a persistent, navigable representation of workspace state; web, desktop, and mobile share this paradigm, base, and auth, so they form one Interactive interface.",
      "provenance": [
        {
          "url": "https://pumble.com/apps",
          "evidence": "Lists first-party apps for iOS, Android, Mac, Windows, Linux, and web."
        },
        {
          "url": "https://pumble.com/help/getting-started/pumble-apps/pumble-for-desktop/",
          "evidence": "Desktop app performs the same messaging, administration, and invite actions as the web application."
        }
      ]
    },
    {
      "name": "Pumble REST API",
      "technology": "HTTP REST API (api.pumble.com / docs.pumble.com), API-key or OAuth2 token auth",
      "channel": "Programmatic",
      "classification_rationale": "The consumer explicitly invokes provider-defined operations (messages, channels, users, workspace, calls, files) through structured HTTP requests. The two credential paths share one operation set and base, so they are one interface.",
      "provenance": [
        {
          "url": "https://pumble.com/help/integrations/automation-workflow-integrations/api-keys-integration/",
          "evidence": "API Keys addon generates a key to send messages, reactions, and more via HTTP requests, with the full action list in Swagger."
        },
        {
          "url": "https://cake-com.github.io/pumble-node-sdk/api-client.html",
          "evidence": "API Client lists the same REST operation families and references the Pumble API docs at docs.pumble.com."
        }
      ]
    },
    {
      "name": "Incoming Webhooks",
      "technology": "HTTP POST of JSON or form payload to a unique per-webhook URL",
      "channel": "Programmatic",
      "classification_rationale": "The consumer explicitly invokes a single provider-defined post-message operation by POSTing a payload to a Pumble-generated URL; distinct base and credential model make it a separate Programmatic interface from the REST API.",
      "provenance": [
        {
          "url": "https://pumble.com/help/integrations/add-pumble-apps/incoming-webhooks-for-pumble/",
          "evidence": "Documents posting a message by HTTP POST with a text or attachments payload to a unique incoming-webhook URL under api.pumble.com."
        }
      ]
    },
    {
      "name": "Pumble Apps event and interaction delivery",
      "technology": "Signed HTTPS callbacks to a developer-hosted endpoint (events, slash commands, shortcuts, block interactions, view actions)",
      "channel": "Event",
      "classification_rationale": "Pumble initiates the interaction on subscribed or user-triggered events and delivers signed payloads to a consumer-controlled receiver; the shared delivery contract makes this one Event interface.",
      "provenance": [
        {
          "url": "https://cake-com.github.io/pumble-node-sdk/getting-started",
          "evidence": "Apps register events and eventSubscriptions.url plus command, shortcut, block-interaction, and view handlers, delivered to an eventsPath endpoint and signed with the app signing secret."
        }
      ]
    },
    {
      "name": "Pumble AI Assistant addon",
      "technology": "In-workspace AI assistant messaged directly or by @mention, backed by a connected LLM provider",
      "channel": "Conversational",
      "classification_rationale": "The consumer interacts through natural-language messages interpreted by the service, and internal orchestration is not part of the consumer-facing contract, so it is Conversational rather than Agentic.",
      "provenance": [
        {
          "url": "https://pumble.com/help/integrations/automation-workflow-integrations/pumble-ai-assistant-addon/",
          "evidence": "Users communicate with the assistant inside Pumble by direct message or by mentioning it in a channel or group DM, and it responds in a thread."
        }
      ]
    },
    {
      "name": "Pumble native MCP server",
      "technology": "Model Context Protocol server hosted at pumble.com, exposing tools and built-in prompts",
      "channel": "Agentic",
      "classification_rationale": "Capability discovery and selection structure the interaction contract, which is Capability Discovery and Invocation; per the MCP boundary rule this is Agentic rather than Programmatic.",
      "provenance": [
        {
          "url": "https://pumble.com/learn/pumble/ai-automation-guide/",
          "evidence": "States Pumble maintains a native MCP server hosted at pumble.com to connect a workspace to an AI agent, listing available tools and built-in prompts."
        }
      ]
    }
  ],
  "access_mechanism_ledger": [
    {
      "mechanism": "Web application",
      "disposition": "interface",
      "detail": "Pumble client"
    },
    {
      "mechanism": "Desktop application (Windows, macOS, Linux)",
      "disposition": "interface",
      "detail": "Pumble client"
    },
    {
      "mechanism": "Mobile application (iOS, Android)",
      "disposition": "interface",
      "detail": "Pumble client"
    },
    {
      "mechanism": "Terminal / TUI client",
      "disposition": "excluded",
      "detail": "No first-party navigable TUI documented; pumble-cli is app-development tooling, not a service TUI."
    },
    {
      "mechanism": "REST API via API Keys addon",
      "disposition": "interface",
      "detail": "Pumble REST API"
    },
    {
      "mechanism": "OAuth2 app and bot token API access (SDK API Client)",
      "disposition": "interface",
      "detail": "Pumble REST API (same operation set, different credential path)"
    },
    {
      "mechanism": "Incoming Webhooks",
      "disposition": "interface",
      "detail": "Incoming Webhooks"
    },
    {
      "mechanism": "Pumble Apps event subscriptions and events",
      "disposition": "interface",
      "detail": "Pumble Apps event and interaction delivery"
    },
    {
      "mechanism": "Slash commands, shortcuts, block interactions, view actions (Apps)",
      "disposition": "interface",
      "detail": "Pumble Apps event and interaction delivery (same signed-callback contract)"
    },
    {
      "mechanism": "AI Assistant addon",
      "disposition": "interface",
      "detail": "Pumble AI Assistant addon"
    },
    {
      "mechanism": "Native MCP server",
      "disposition": "interface",
      "detail": "Pumble native MCP server"
    },
    {
      "mechanism": "pumble-cli",
      "disposition": "excluded",
      "detail": "Developer scaffolding and deployment tool for building Pumble Apps; not a service access channel and exposes no TUI."
    },
    {
      "mechanism": "SDKs (pumble-sdk / pumble-node-sdk, third-party Python SDK)",
      "disposition": "excluded",
      "detail": "Client libraries that implement or support interfaces without being one."
    },
    {
      "mechanism": "Native partner integrations (Clockify, Plaky, Google Drive, GitHub, GitLab, Zendesk, RSS, Zoom)",
      "disposition": "excluded",
      "detail": "Third-party or partner integrations, not access channels to Pumble itself."
    },
    {
      "mechanism": "Third-party automation and MCP wrappers (Zapier, Make, Pipedream, viaSocket, Composio, community MCP servers)",
      "disposition": "excluded",
      "detail": "Not provider-defined."
    },
    {
      "mechanism": "Email / SMTP message ingestion",
      "disposition": "excluded",
      "detail": "No official provider mechanism to post into Pumble by email was found."
    }
  ],
  "channel_evidence": {
    "Interactive": "observed",
    "Agentic": "observed",
    "Conversational": "observed",
    "Event": "observed",
    "Programmatic": "observed"
  },
  "number_of_interfaces": 6,
  "multi_interface": true,
  "number_of_channels": 5,
  "multi_channel": true
}
```
