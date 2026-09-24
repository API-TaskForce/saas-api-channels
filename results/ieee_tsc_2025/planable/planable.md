## SaaS summary

Planable (planable.io) is a social media content collaboration, approval, and scheduling platform operated by Planable Inc. The investigation identifies **four logical interfaces** across **three distinct access channels**.

## Interface classification table

| Interface          | Channel      | Interaction technology                   | Provenance                                                                                                                                                                                                                                                                                                         |
| ------------------ | ------------ | ---------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Web application    | Interactive  | Web app at app.planable.io               | Provider product page presents the workspace as navigable views and controls (calendar, composer, approval queues, social inbox, analytics). Primitive is affordance manipulation over a persistent representation of workspace state. Current.                                                                    |
| Mobile application | Interactive  | Native iOS and Android apps              | Planable Inc. store listings, linked from planable.io, describe creating, scheduling, previewing, and approving content through calendar, list, and feed views. Same affordance-manipulation paradigm on a separate first-party client surface. Current.                                                           |
| Public API         | Programmatic | REST API at api.planable.io/api/v1       | Provider guide documents a versioned REST API, Bearer-token auth, and an OpenAPI 3.1 spec covering workspaces, pages, posts, media, labels, and stories. The consumer explicitly invokes provider-defined operations, which is Operation Invocation. Current.                                                      |
| MCP connector      | Agentic      | Remote MCP server at mcp.planable.io/mcp | Provider help article and guide describe a single MCP server URL that any MCP-compatible AI tool authorizes and then uses to act on account data. Capability discovery and selection structure the contract, so the channel is Agentic rather than Programmatic even though tools are ultimately invoked. Current. |

## Coverage ledger table

| Access mechanism                                                                                                                      | Disposition                                                                                                                                                                                                                                                         |
| ------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Web app (app.planable.io)                                                                                                             | Interface: Web application (Interactive)                                                                                                                                                                                                                            |
| Mobile apps (iOS + Android)                                                                                                           | Interface: Mobile application (Interactive)                                                                                                                                                                                                                         |
| Public REST API (api.planable.io/api/v1)                                                                                              | Interface: Public API (Programmatic)                                                                                                                                                                                                                                |
| MCP connector (mcp.planable.io/mcp)                                                                                                   | Interface: MCP connector (Agentic)                                                                                                                                                                                                                                  |
| Planable AI (composer and social inbox assistant)                                                                                     | Excluded: embedded AI generation feature triggered by UI affordances such as "Generate with AI" and "Answer with AI" inside the composer and social inbox. It folds into the web and mobile Interactive interfaces and is not a separate consumer-facing interface. |
| Public API interactive docs / OpenAPI console (api.planable.io/api/v1/docs)                                                           | Excluded: an API explorer and documentation surface that issues the same REST operations. It belongs to the Public API Programmatic interface, not a separate navigable representation of service state.                                                            |
| Zapier connector and Zapier Integration API (app.planable.io/api/integrations/zapier), including its webhooks                         | Excluded: third-party integration. The provider-hosted API and its webhooks exist to power the Zapier connector through an OAuth app pairing, not as a general-purpose provider interface. The general-purpose Public API has no webhooks in v1.                    |
| Desktop client (surface check)                                                                                                        | Excluded: no first-party desktop application found. Only third-party Android emulators such as BlueStacks run the mobile app on PC or Mac.                                                                                                                          |
| CLI / TUI (terminal surface check)                                                                                                    | Excluded: no provider command-line tool or terminal dashboard found in official documentation.                                                                                                                                                                      |
| SDKs / client libraries                                                                                                               | Excluded: none offered as distinct interfaces. The OpenAPI spec imports into third-party API clients, which are not provider interfaces.                                                                                                                            |
| Outbound social-network integrations (Facebook, Instagram, LinkedIn, TikTok, YouTube, Pinterest, X, Threads, Google Business Profile) | Excluded: these are Planable publishing outward to social platforms, not access mechanisms into Planable.                                                                                                                                                           |
| Third-party app integrations (Canva, Slack, and similar)                                                                              | Excluded: third-party integrations, not provider-defined access interfaces.                                                                                                                                                                                         |

## Channel coverage table

| Channel        | Evidence             |
| -------------- | -------------------- |
| Interactive    | Observed             |
| Agentic        | Observed             |
| Conversational | No evidence observed |
| Event          | No evidence observed |
| Programmatic   | Observed             |

## Classification notes

Two calls are worth stating explicitly, since they turn on the boundary rules rather than on the provenance alone.

Planable AI reads like a conversational feature but is not a Conversational interface. It appears as affordance-triggered generation embedded in the composer and the social inbox, where a prompt field collects parameters for a "generate" operation the user invokes through UI controls. That parameter collection stays part of the invoking Interactive interface and does not establish a separate message-primitive contract. The natural-language surfaces that do talk to Planable, namely Claude, ChatGPT, and Gemini, reach it through the Agentic MCP connector and are themselves third-party consumers, not a Planable-provided conversational interface.

The Event channel shows no evidence at present. The Public API guide states plainly that webhooks are not available in v1 and that integrations must poll, with webhooks listed as a roadmap item. The only webhook mechanism found sits inside the Zapier Integration API, which is excluded as third-party integration plumbing. Absence of a current provider-general event interface is treated as no evidence observed, not as a positive claim of absence for any future version.

## Multichannel verdict

**Multichannel** (3 distinct paradigms: Interactive, Programmatic, Agentic).

## JSON block

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
  "saas": { "name": "Planable" },
  "interfaces": [
    {
      "name": "Web application",
      "technology": "Web app (app.planable.io)",
      "channel": "Interactive",
      "classification_rationale": "Actions are expressed by manipulating presented affordances (content calendar, composer, approval queues, social inbox, analytics views) of a persistent, navigable representation of workspace state. Affordance Manipulation.",
      "provenance": [
        {
          "url": "https://planable.io/product/",
          "evidence": "Provider product page describes the web workspace: create, plan, collaborate, approve, schedule, analyze, and a social inbox, navigated as views and controls."
        },
        {
          "url": "https://app.planable.io/login",
          "evidence": "Provider-hosted web application entry point (login/register), confirming a first-party browser client."
        }
      ]
    },
    {
      "name": "Mobile application",
      "technology": "Native mobile apps (iOS, Android)",
      "channel": "Interactive",
      "classification_rationale": "First-party mobile client that presents the same affordance-driven navigable representation (calendar, feed, grid, previews, approvals) on the mobile surface. Separate Interactive interface from the web client per the surface checklist.",
      "provenance": [
        {
          "url": "https://play.google.com/store/apps/details?id=com.planable",
          "evidence": "Provider (Planable Inc.) Google Play listing: create, schedule, preview, and approve content; calendar/list/feed views on mobile."
        },
        {
          "url": "https://apps.apple.com/us/app/planable-social-media-planner/id1437715174",
          "evidence": "Provider App Store listing linked from planable.io, confirming a first-party iOS client."
        }
      ]
    },
    {
      "name": "Public API",
      "technology": "REST API (https://api.planable.io/api/v1)",
      "channel": "Programmatic",
      "classification_rationale": "The consumer explicitly invokes provider-defined REST operations (workspaces, pages, posts, media, labels, stories) via structured HTTP requests with Bearer-token auth and an OpenAPI 3.1 spec. Operation Invocation.",
      "provenance": [
        {
          "url": "https://planable.io/guides/planable-public-api/",
          "evidence": "Provider guide: versioned REST API under /api/v1, Bearer token auth, OpenAPI 3.1 at /api/v1/openapi.json; explicitly states webhooks are not available in v1 (poll instead)."
        },
        {
          "url": "https://help.planable.io/hc/en-us/articles/27638359236508-How-to-connect-and-use-the-Planable-Public-API",
          "evidence": "Provider help article describing token generation, scopes, and programmatic read/write access without logging into the app."
        }
      ]
    },
    {
      "name": "MCP connector",
      "technology": "Remote MCP server (https://mcp.planable.io/mcp)",
      "channel": "Agentic",
      "classification_rationale": "Exposes semantically described Planable capabilities (create/update drafts, review approval queues, pull analytics, audit calendars, approve posts) that MCP-compatible AI tools discover and select as part of the interaction contract. Capability Discovery and Invocation, so Agentic rather than Programmatic despite tools ultimately being invoked.",
      "provenance": [
        {
          "url": "https://help.planable.io/hc/en-us/articles/27538577098780-How-to-connect-Planable-MCP-to-your-AI-tools",
          "evidence": "Provider help article: single MCP server URL (mcp.planable.io/mcp) that any MCP-compatible AI tool connects to and authorizes to interact with Planable content."
        },
        {
          "url": "https://planable.io/guides/planable-mcp/",
          "evidence": "Provider guide describes the connector giving compatible AI tools authorized access to act on real account data across the content workflow via MCP capabilities."
        }
      ]
    }
  ],
  "access_mechanism_ledger": [
    {
      "mechanism": "Web app (app.planable.io)",
      "disposition": "interface",
      "detail": "Web application (Interactive)"
    },
    {
      "mechanism": "Mobile apps (iOS + Android)",
      "disposition": "interface",
      "detail": "Mobile application (Interactive)"
    },
    {
      "mechanism": "Public REST API (api.planable.io/api/v1)",
      "disposition": "interface",
      "detail": "Public API (Programmatic)"
    },
    {
      "mechanism": "MCP connector (mcp.planable.io/mcp)",
      "disposition": "interface",
      "detail": "MCP connector (Agentic)"
    },
    {
      "mechanism": "Planable AI (composer + social inbox assistant)",
      "disposition": "excluded",
      "detail": "Embedded AI generation feature invoked via UI affordances (Generate with AI, Answer with AI) inside the web/mobile composer and social inbox; folds into those Interactive interfaces, not a separate consumer-facing interface."
    },
    {
      "mechanism": "Public API interactive docs / OpenAPI console (api.planable.io/api/v1/docs)",
      "disposition": "excluded",
      "detail": "API explorer and documentation surface that issues the same REST operations; part of the Public API Programmatic interface, not a distinct navigable representation of service state."
    },
    {
      "mechanism": "Zapier connector and Zapier Integration API (app.planable.io/api/integrations/zapier), including its webhooks",
      "disposition": "excluded",
      "detail": "Third-party integration; the provider-hosted API and its webhooks exist solely to power the Zapier connector (OAuth app pairing) and are not offered as a general-purpose provider interface. The general-purpose Public API has no webhooks in v1."
    },
    {
      "mechanism": "Desktop client (web/mobile/desktop/terminal surface check)",
      "disposition": "excluded",
      "detail": "No first-party desktop application found; only third-party Android emulators (e.g., BlueStacks) run the mobile app on PC/Mac."
    },
    {
      "mechanism": "CLI / TUI (terminal surface check)",
      "disposition": "excluded",
      "detail": "No provider command-line tool or terminal dashboard found in official documentation."
    },
    {
      "mechanism": "SDKs / client libraries",
      "disposition": "excluded",
      "detail": "None offered as distinct interfaces; the OpenAPI spec imports into third-party API clients (Postman/Insomnia), which are not provider interfaces."
    },
    {
      "mechanism": "Outbound social-network integrations (Facebook, Instagram, LinkedIn, TikTok, YouTube, Pinterest, X, Threads, Google Business Profile)",
      "disposition": "excluded",
      "detail": "These are Planable publishing outward to social platforms, not access mechanisms into Planable."
    },
    {
      "mechanism": "Third-party app integrations (Canva, Slack, etc.)",
      "disposition": "excluded",
      "detail": "Third-party integrations, not provider-defined access interfaces."
    }
  ],
  "channel_evidence": {
    "Interactive": "observed",
    "Agentic": "observed",
    "Conversational": "no_evidence_observed",
    "Event": "no_evidence_observed",
    "Programmatic": "observed"
  },
  "number_of_interfaces": 4,
  "multi_interface": true,
  "number_of_channels": 3,
  "multi_channel": true
}
```
