## SaaS summary

**Clockify** (by CAKE.com Inc., official domain `clockify.me`). Identified logical interfaces: **8**. Distinct channels with at least one classified interface: **4**.

## Interface classification table

| Interface           | Channel      | Interaction technology                                               | Provenance                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| ------------------- | ------------ | -------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Web application     | Interactive  | Web app at `app.clockify.me`                                         | `clockify.me/apps` and `clockify.me/help/apps` document a first-party web client; the user manipulates views, forms, and controls over a persistent workspace representation. Actions are expressed by affordance manipulation, so decision-tree step 1 fires. Current.                                                                                                                                                                         |
| Desktop application | Interactive  | Windows, macOS, Linux native apps                                    | `clockify.me/apps` lists Windows/Mac/Linux clients; Mac App Store listing is published by CAKE.com Inc. Same affordance-manipulation primitive over a navigable local client with offline mode and auto tracker. Current.                                                                                                                                                                                                                       |
| Mobile application  | Interactive  | iOS and Android native apps                                          | Google Play listing by Cake.com Inc. and `clockify.me/apps` document first-party mobile clients. Affordance manipulation on a touch client. Current.                                                                                                                                                                                                                                                                                            |
| Browser extension   | Interactive  | Chrome, Firefox, Edge extensions                                     | `clockify.me/help/apps/chrome-extension` documents a first-party extension exposing a popup and an injected timer control the user operates directly. The primitive is manipulation of presented controls, not structured operation invocation, so it resolves at step 1. Current.                                                                                                                                                              |
| Kiosk               | Interactive  | Browser-delivered shared-device clock-in                             | `clockify.me/free-time-clock-kiosk-app` documents a shared-device surface where limited users clock in via PIN, QR code, or photo capture. Distinct interaction contract (shared device, limited-user model) but the same affordance-manipulation primitive. Current.                                                                                                                                                                           |
| REST API            | Programmatic | HTTP REST, base `api.clockify.me/api/v1`, `X-Api-Key` header         | `docs.clockify.me` documents provider-defined operations over workspaces, projects, tasks, time entries, reports, and webhook management, invoked as structured HTTP requests. The consumer explicitly invokes named operations, so it resolves at step 5. Report endpoints share the same REST style and auth and are treated as the same interface. Current.                                                                                  |
| Webhooks            | Event        | Provider-initiated HTTP callbacks to a subscriber endpoint           | `docs.clockify.me` (webhooks) states Clockify sends real-time notifications to a consumer-controlled endpoint when events such as starting a timer or deleting an entry occur. The service initiates the interaction on subscribed events, so it resolves at step 4. Current.                                                                                                                                                                   |
| MCP server          | Agentic      | Model Context Protocol over HTTP at `api.clockify.me/mcp-server/mcp` | `clockify.me/help/integrations-and-add-ons/use-clockify-mcp-server-to-connect-to-ai-agent` documents a first-party MCP endpoint exposing discoverable tools, prompts, and resources that an AI agent selects by goal. Capability discovery and selection are part of the contract, so the MCP boundary case classifies it Agentic rather than Programmatic. Officially documented but labeled "COMING SOON" as of 2026-09-22 (preview/rollout). |

## Coverage ledger table

| Access mechanism                                                                  | Disposition                                                                                                                                                                                   |
| --------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Web app (first-party web surface)                                                 | Web application (Interactive)                                                                                                                                                                 |
| Desktop app (first-party desktop surface)                                         | Desktop application (Interactive)                                                                                                                                                             |
| Mobile app (first-party mobile surface)                                           | Mobile application (Interactive)                                                                                                                                                              |
| Terminal/CLI (first-party terminal surface)                                       | Excluded: no provider-shipped Clockify CLI or TUI found. The Claude/Gemini/Codex CLIs in the MCP docs are third-party AI agents used to reach the MCP server, not a Clockify terminal client. |
| Browser extension                                                                 | Browser extension (Interactive)                                                                                                                                                               |
| Kiosk mode                                                                        | Kiosk (Interactive)                                                                                                                                                                           |
| REST API / API reference                                                          | REST API (Programmatic)                                                                                                                                                                       |
| Reports API endpoints                                                             | Folded into REST API (same REST style and `X-Api-Key` auth).                                                                                                                                  |
| Webhooks / events                                                                 | Webhooks (Event)                                                                                                                                                                              |
| MCP server / AI agent                                                             | MCP server (Agentic)                                                                                                                                                                          |
| Conversational / chat AI assistant (first-party)                                  | Excluded: no first-party natural-language assistant inside Clockify. Natural-language interaction occurs in external AI agents that consume the MCP interface (counted as Agentic).           |
| Integrations index (Jira, QuickBooks, Xero, Zapier, Make, Pipedream, 2,900+ apps) | Excluded: third-party integrations and connectors that consume the REST API, webhooks, or the extension; not provider-defined interfaces.                                                     |
| Pumble chat time updates                                                          | Excluded: cross-product integration delivered through the API/webhooks, not a distinct Clockify interface.                                                                                    |
| SDKs / client libraries (e.g. `clockify-ts`)                                      | Excluded: SDKs and wrappers are not interfaces; also unofficial.                                                                                                                              |

## Channel coverage table

| Channel        | Evidence             |
| -------------- | -------------------- |
| Interactive    | Observed             |
| Agentic        | Observed             |
| Conversational | No evidence observed |
| Event          | Observed             |
| Programmatic   | Observed             |

## Classification notes

Two counting judgments affect reproducibility. First, the web, desktop, mobile, browser-extension, and kiosk clients are treated as five distinct Interactive interfaces because each is a separate provider-defined client surface with a genuinely different interaction contract, even though they share the affordance-manipulation paradigm; folding them together would not change the channel count. Second, the MCP server is a first-party endpoint but its help page is marked "COMING SOON," so its Agentic classification rests on current official documentation of a preview feature rather than a stable release.

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
  "generated_at": "2026-09-24T00:00:00Z",
  "evidence_checked_at": "2026-09-24T00:00:00Z",
  "saas": { "name": "Clockify" },
  "interfaces": [
    {
      "name": "Web application",
      "technology": "Web app (app.clockify.me)",
      "channel": "Interactive",
      "classification_rationale": "Actions are expressed by manipulating views, forms, and controls of a persistent, navigable workspace representation.",
      "provenance": [
        {
          "url": "https://clockify.me/apps",
          "evidence": "First-party web client listed among Clockify apps."
        },
        {
          "url": "https://clockify.me/help/apps",
          "evidence": "Help center documents web/app surfaces for tracking time."
        }
      ]
    },
    {
      "name": "Desktop application",
      "technology": "Windows, macOS, Linux native apps",
      "channel": "Interactive",
      "classification_rationale": "Native desktop client operated through affordance manipulation over a navigable local representation, with offline mode and auto tracker.",
      "provenance": [
        {
          "url": "https://clockify.me/apps",
          "evidence": "Windows, Mac, and Linux clients listed as first-party apps."
        },
        {
          "url": "https://apps.apple.com/us/app/clockify-desktop/id1364502317",
          "evidence": "Mac desktop app published by CAKE.com Inc."
        }
      ]
    },
    {
      "name": "Mobile application",
      "technology": "iOS and Android native apps",
      "channel": "Interactive",
      "classification_rationale": "Native mobile client operated through affordance manipulation of the Clockify workspace.",
      "provenance": [
        {
          "url": "https://clockify.me/apps",
          "evidence": "Android and iOS clients listed as first-party apps."
        },
        {
          "url": "https://play.google.com/store/apps/details?id=me.clockify.android",
          "evidence": "Android app published by Cake.com Inc."
        }
      ]
    },
    {
      "name": "Browser extension",
      "technology": "Chrome, Firefox, Edge extensions",
      "channel": "Interactive",
      "classification_rationale": "First-party extension exposing a popup and an injected timer control the user operates directly; the primitive is manipulation of presented controls, not structured operation invocation.",
      "provenance": [
        {
          "url": "https://clockify.me/help/apps/chrome-extension",
          "evidence": "Documents the first-party browser extension, its timer controls, reminders, and settings."
        }
      ]
    },
    {
      "name": "Kiosk",
      "technology": "Browser-delivered shared-device clock-in",
      "channel": "Interactive",
      "classification_rationale": "Shared-device surface where limited users clock in via PIN, QR code, or photo capture; distinct contract but the same affordance-manipulation primitive.",
      "provenance": [
        {
          "url": "https://clockify.me/free-time-clock-kiosk-app",
          "evidence": "Documents the kiosk opened via a browser link with PIN/QR/photo clock-in for limited members."
        }
      ]
    },
    {
      "name": "REST API",
      "technology": "HTTP REST, base api.clockify.me/api/v1, X-Api-Key",
      "channel": "Programmatic",
      "classification_rationale": "The consumer explicitly invokes provider-defined operations over resources through structured HTTP requests; report endpoints share the same style and auth and are the same interface.",
      "provenance": [
        {
          "url": "https://docs.clockify.me/",
          "evidence": "Official API docs: base URL api.clockify.me/api/v1, X-Api-Key auth, operations over workspaces, projects, time entries, reports, and webhook management."
        }
      ]
    },
    {
      "name": "Webhooks",
      "technology": "Provider-initiated HTTP callbacks to a subscriber endpoint",
      "channel": "Event",
      "classification_rationale": "The service initiates the interaction when subscribed events occur and delivers to a consumer-controlled endpoint.",
      "provenance": [
        {
          "url": "https://docs.clockify.me/",
          "evidence": "Webhooks section: real-time notifications sent to your endpoint on events such as starting a timer or deleting a time entry."
        }
      ]
    },
    {
      "name": "MCP server",
      "technology": "Model Context Protocol over HTTP (api.clockify.me/mcp-server/mcp)",
      "channel": "Agentic",
      "classification_rationale": "First-party MCP endpoint exposing discoverable tools, prompts, and resources selected by an AI agent by goal; capability discovery and selection are part of the contract, so the MCP boundary case makes it Agentic rather than Programmatic.",
      "provenance": [
        {
          "url": "https://clockify.me/help/integrations-and-add-ons/use-clockify-mcp-server-to-connect-to-ai-agent",
          "evidence": "Official help page documenting the Clockify MCP endpoint, its tools, prompts, and resources; labeled COMING SOON as of 2026-09-22 (preview)."
        }
      ]
    }
  ],
  "access_mechanism_ledger": [
    {
      "mechanism": "Web app (first-party web surface)",
      "disposition": "interface",
      "detail": "Web application"
    },
    {
      "mechanism": "Desktop app (first-party desktop surface)",
      "disposition": "interface",
      "detail": "Desktop application"
    },
    {
      "mechanism": "Mobile app (first-party mobile surface)",
      "disposition": "interface",
      "detail": "Mobile application"
    },
    {
      "mechanism": "Terminal/CLI (first-party terminal surface)",
      "disposition": "excluded",
      "detail": "No provider-shipped Clockify CLI or TUI; the CLIs in the MCP docs are third-party AI agents used to reach the MCP server."
    },
    {
      "mechanism": "Browser extension",
      "disposition": "interface",
      "detail": "Browser extension"
    },
    {
      "mechanism": "Kiosk mode",
      "disposition": "interface",
      "detail": "Kiosk"
    },
    {
      "mechanism": "REST API / API reference",
      "disposition": "interface",
      "detail": "REST API"
    },
    {
      "mechanism": "Reports API endpoints",
      "disposition": "excluded",
      "detail": "Folded into REST API: same REST style and X-Api-Key auth."
    },
    {
      "mechanism": "Webhooks / events",
      "disposition": "interface",
      "detail": "Webhooks"
    },
    {
      "mechanism": "MCP server / AI agent",
      "disposition": "interface",
      "detail": "MCP server"
    },
    {
      "mechanism": "Conversational / chat AI assistant (first-party)",
      "disposition": "excluded",
      "detail": "No first-party natural-language assistant inside Clockify; NL interaction occurs in external agents consuming the MCP interface."
    },
    {
      "mechanism": "Integrations index (Jira, QuickBooks, Xero, Zapier, Make, Pipedream, 2,900+ apps)",
      "disposition": "excluded",
      "detail": "Third-party integrations/connectors that consume the REST API, webhooks, or the extension."
    },
    {
      "mechanism": "Pumble chat time updates",
      "disposition": "excluded",
      "detail": "Cross-product integration delivered via API/webhooks, not a distinct Clockify interface."
    },
    {
      "mechanism": "SDKs / client libraries (e.g. clockify-ts)",
      "disposition": "excluded",
      "detail": "SDKs and wrappers are not interfaces; also unofficial."
    }
  ],
  "channel_evidence": {
    "Interactive": "observed",
    "Agentic": "observed",
    "Conversational": "no_evidence_observed",
    "Event": "observed",
    "Programmatic": "observed"
  },
  "number_of_interfaces": 8,
  "multi_interface": true,
  "number_of_channels": 4,
  "multi_channel": true
}
```
