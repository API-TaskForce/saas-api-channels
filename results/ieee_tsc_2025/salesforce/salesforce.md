## SaaS summary

**Salesforce** (Salesforce Platform, provider Salesforce, Inc., official docs at developer.salesforce.com and help.salesforce.com). This analysis identifies **14 logical interfaces** spread across **5 distinct access channels**. Salesforce follows an explicitly API-first design, so most platform capabilities are exposed through more than one interaction paradigm.

## Interface classification table

| Interface                                          | Channel        | Interaction technology               | Provenance                                                                                                                                                                                                                                                                                                         |
| -------------------------------------------------- | -------------- | ------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Web UI (Lightning Experience / Salesforce Classic) | Interactive    | Browser-based web application        | help.salesforce.com supported-browsers and Lightning Experience docs. Users act by manipulating presented views, records, list views, and forms of a persistent navigable representation of org state. Affordance Manipulation. Current.                                                                           |
| Salesforce mobile app                              | Interactive    | Native iOS / Android client          | salesforce.com/products/mobile and help.salesforce.com mobile-app article: downloadable client included with all orgs, distinct from the web client, same affordance-manipulation paradigm on a mobile surface. Current.                                                                                           |
| REST API                                           | Programmatic   | REST over HTTP (JSON/XML), OAuth     | developer.salesforce.com REST guide and help "Which API Do I Use". Consumer explicitly invokes provider-defined resource operations. Operation Invocation. Folds in Connect REST, User Interface API, Composite, Apex REST, and Tooling REST (same REST style, /services/data base, and auth). Current.            |
| SOAP API                                           | Programmatic   | SOAP/WSDL over HTTP (XML)            | developer.salesforce.com API guide and Trailhead API basics: WSDL defines a formal operation contract; consumer invokes named calls synchronously. Operation Invocation, distinct SOAP primitive from REST. Folds in Apex SOAP. Current.                                                                           |
| GraphQL API                                        | Programmatic   | GraphQL single endpoint              | help.salesforce.com and developer GraphQL guide (GA Winter '23). Distinct query-language contract on one endpoint; consumer explicitly invokes queries/mutations. Operation Invocation, split from REST on primitive. Current.                                                                                     |
| Bulk API 2.0                                       | Programmatic   | REST-framework asynchronous jobs     | help "Which API Do I Use" and Bulk API guide: asynchronous job lifecycle (create job, upload, close, poll, retrieve). Operation Invocation, split from REST on control structure (async). Current.                                                                                                                 |
| Metadata API                                       | Programmatic   | SOAP-based deploy/retrieve           | help "Which API Do I Use" and Metadata API guide: retrieve, deploy, create, update, delete org customizations via asynchronous deploy/retrieve. Operation Invocation, split from SOAP API on async control structure. Current.                                                                                     |
| Salesforce CLI command interface                   | Programmatic   | `sf` command-line tool               | developer.salesforce.com CLI Command Reference (sf v2, GA July 2023). Actions expressed as explicit commands and flags. Operation Invocation. No persistent navigable TUI dashboard observed, so the CLI hosts only this command interface. Current.                                                               |
| Pub/Sub API                                        | Event          | gRPC over HTTP/2, Avro payloads      | developer.salesforce.com pub-sub-api guide: on Subscribe, the service delivers platform-event, CDC, and event-monitoring messages to a consumer-held stream. Service-initiated delivery to a consumer-controlled receiver. Event Notification. Current (the actively invested streaming path).                     |
| Streaming API (CometD)                             | Event          | CometD/Bayeux long-polling           | developer.salesforce.com platform_events CometD subscribe docs: service pushes event notifications (PushTopic, generic, platform events, CDC) to subscribed clients. Event Notification. Current but legacy; superseded by Pub/Sub API.                                                                            |
| Outbound Messages                                  | Event          | Workflow/flow-triggered SOAP callout | developer.salesforce.com API guide "Understanding Outbound Messaging": on a record field-change event, the service sends a SOAP message over HTTP(S) to a designated endpoint. Service-initiated delivery to a consumer-controlled receiver. Event Notification. Current.                                          |
| Agentforce agents (Agent API)                      | Conversational | REST Agent API / in-app agent panel  | developer.salesforce.com Agentforce references and Conversation Client API: consumer sends natural-language utterances/messages to an AI agent that interprets them; topic/action orchestration is internal to the service. Message primitive, internal tools. Contextual Conversation. Current.                   |
| Salesforce Hosted MCP Server                       | Agentic        | Model Context Protocol endpoint      | developer.salesforce.com blog "Hosted MCP Servers Now GA" (Apr 2026): Salesforce-managed MCP endpoint exposing org data, Flows, Apex actions, and queries as discoverable tools to any MCP client. Capability discovery and selection are part of the contract. Capability Discovery and Invocation. Current (GA). |
| Salesforce DX MCP Server                           | Agentic        | Model Context Protocol (local dev)   | developer.salesforce.com DX MCP docs and Summer '26 release blog: MCP server exposing DX/development tools (deploy, metadata context, etc.) as discoverable tools to agentic IDEs. Capability Discovery and Invocation. Beta / Developer Preview.                                                                  |

## Coverage ledger

| Access mechanism                                | Disposition                                                                                                                                                                                                                       |
| ----------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| REST API                                        | Interface: REST API                                                                                                                                                                                                               |
| Connect REST API (Chatter/Experience)           | Folded into REST API (same REST style, base, auth)                                                                                                                                                                                |
| User Interface (UI) API                         | Folded into REST API                                                                                                                                                                                                              |
| Composite API                                   | Folded into REST API                                                                                                                                                                                                              |
| Apex REST                                       | Folded into REST API                                                                                                                                                                                                              |
| Tooling API (REST/SOAP)                         | Folded into REST API and SOAP API (resource group, same styles/auth)                                                                                                                                                              |
| SOAP API                                        | Interface: SOAP API                                                                                                                                                                                                               |
| Apex SOAP                                       | Folded into SOAP API                                                                                                                                                                                                              |
| GraphQL API                                     | Interface: GraphQL API                                                                                                                                                                                                            |
| Bulk API 2.0                                    | Interface: Bulk API 2.0                                                                                                                                                                                                           |
| Metadata API                                    | Interface: Metadata API                                                                                                                                                                                                           |
| Salesforce CLI (`sf`)                           | Interface: Salesforce CLI command interface                                                                                                                                                                                       |
| CLI TUI check                                   | Excluded: no persistent navigable TUI; `sf` is command-based only                                                                                                                                                                 |
| Pub/Sub API                                     | Interface: Pub/Sub API                                                                                                                                                                                                            |
| Streaming API (CometD)                          | Interface: Streaming API (Event)                                                                                                                                                                                                  |
| Outbound Messages                               | Interface: Outbound Messages (Event)                                                                                                                                                                                              |
| Web UI surface (Lightning Experience / Classic) | Interface: Web UI                                                                                                                                                                                                                 |
| Mobile client surface                           | Interface: Salesforce mobile app                                                                                                                                                                                                  |
| Desktop client surface                          | Excluded: no first-party standalone desktop CRM client; desktop use is the browser-based Web UI. Salesforce for Outlook is retired; Outlook/Gmail integrations are add-ins embedding the web experience, not a distinct interface |
| Agentforce / Agent API (conversational)         | Interface: Agentforce agents (Conversational)                                                                                                                                                                                     |
| Salesforce Hosted MCP Server                    | Interface: Salesforce Hosted MCP Server (Agentic)                                                                                                                                                                                 |
| Salesforce DX MCP Server                        | Interface: Salesforce DX MCP Server (Agentic)                                                                                                                                                                                     |
| Models API                                      | Excluded: LLM-access feature reached through Apex classes and REST endpoints; folds into REST/Apex programmatic access, not a distinct access contract                                                                            |
| Email Services / Email-to-Case (inbound email)  | Excluded: feature-level inbound data ingestion configured per handler, not a general-purpose provider access interface                                                                                                            |
| SDKs (Mobile SDK, Agentforce Python SDK, etc.)  | Excluded: client libraries, not interfaces                                                                                                                                                                                        |
| AppExchange / third-party integrations          | Excluded: partner marketplace, not a provider interface                                                                                                                                                                           |
| Apex                                            | Excluded: server-side programming language, not an access interface                                                                                                                                                               |
| OAuth / Connected Apps                          | Excluded: authentication mechanism                                                                                                                                                                                                |

## Channel coverage table

| Channel        | Evidence |
| -------------- | -------- |
| Interactive    | Observed |
| Agentic        | Observed |
| Conversational | Observed |
| Event          | Observed |
| Programmatic   | Observed |

## Classification notes

Streaming API (CometD) is current but explicitly positioned by Salesforce as the older path, with Pub/Sub API named as the sole actively invested streaming interface; both remain officially documented and are classified as Event. The Salesforce DX MCP Server is a Beta / Developer Preview, whereas the Hosted MCP Server reached GA in April 2026; both are Agentic, and the Agentic channel is Observed on the strength of the GA hosted server. No interface required an Unclassified verdict, and no genuine evidence conflict was found.

## Multichannel verdict

**Multichannel** (5 distinct paradigms).

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
  "generated_at": "2026-09-22T12:00:00Z",
  "evidence_checked_at": "2026-09-22T12:00:00Z",
  "saas": { "name": "Salesforce" },
  "interfaces": [
    {
      "name": "Web UI (Lightning Experience / Salesforce Classic)",
      "technology": "Browser-based web application",
      "channel": "Interactive",
      "classification_rationale": "Actions are expressed by manipulating views, records, list views, and forms of a persistent navigable representation of org state.",
      "provenance": [
        {
          "url": "https://help.salesforce.com/s/articleView?language=en_US&id=getstart_browsers_sfx.htm&type=5",
          "evidence": "Lightning Experience is delivered through supported browsers as an interactive UI."
        }
      ]
    },
    {
      "name": "Salesforce mobile app",
      "technology": "Native iOS / Android client",
      "channel": "Interactive",
      "classification_rationale": "Downloadable first-party client whose actions are affordance manipulation of records and views on a mobile surface.",
      "provenance": [
        {
          "url": "https://help.salesforce.com/s/articleView?language=en_US&id=xcloud.salesforce_app.htm&type=5",
          "evidence": "Salesforce for iOS and Android is downloadable and included with all orgs."
        }
      ]
    },
    {
      "name": "REST API",
      "technology": "REST over HTTP (JSON/XML), OAuth",
      "channel": "Programmatic",
      "classification_rationale": "Consumer explicitly invokes provider-defined resource operations; synchronous request/response. Folds in Connect REST, UI API, Composite, Apex REST, Tooling REST.",
      "provenance": [
        {
          "url": "https://help.salesforce.com/s/articleView?language=en_US&id=sf.integrate_what_is_api.htm&type=5",
          "evidence": "REST API provides synchronous REST-based operations for interacting with Salesforce data."
        }
      ]
    },
    {
      "name": "SOAP API",
      "technology": "SOAP/WSDL over HTTP (XML)",
      "channel": "Programmatic",
      "classification_rationale": "WSDL defines a formal operation contract; consumer invokes named calls. Distinct SOAP primitive from REST.",
      "provenance": [
        {
          "url": "https://developer.salesforce.com/docs/atlas.en-us.api.meta/api",
          "evidence": "SOAP API exposes 20+ WSDL-defined calls for operation invocation."
        }
      ]
    },
    {
      "name": "GraphQL API",
      "technology": "GraphQL single endpoint",
      "channel": "Programmatic",
      "classification_rationale": "Distinct query-language contract on one endpoint; consumer explicitly invokes queries/mutations.",
      "provenance": [
        {
          "url": "https://help.salesforce.com/s/articleView?language=en_US&id=sf.integrate_what_is_api.htm&type=5",
          "evidence": "GraphQL API is a separate documented API (GA Winter '23) for precise data requests."
        }
      ]
    },
    {
      "name": "Bulk API 2.0",
      "technology": "REST-framework asynchronous jobs",
      "channel": "Programmatic",
      "classification_rationale": "Explicit operation invocation with an asynchronous job lifecycle; split from REST on control structure.",
      "provenance": [
        {
          "url": "https://help.salesforce.com/s/articleView?language=en_US&id=sf.integrate_what_is_api.htm&type=5",
          "evidence": "Bulk API 2.0 asynchronously queries/inserts/updates/deletes large record volumes via jobs."
        }
      ]
    },
    {
      "name": "Metadata API",
      "technology": "SOAP-based deploy/retrieve",
      "channel": "Programmatic",
      "classification_rationale": "Explicit retrieve/deploy/create/update/delete of org customizations with an asynchronous deploy control structure; split from SOAP API.",
      "provenance": [
        {
          "url": "https://help.salesforce.com/s/articleView?language=en_US&id=sf.integrate_what_is_api.htm&type=5",
          "evidence": "Metadata API retrieves and deploys org customizations, commonly to migrate between environments."
        }
      ]
    },
    {
      "name": "Salesforce CLI command interface",
      "technology": "sf command-line tool",
      "channel": "Programmatic",
      "classification_rationale": "Actions expressed as explicit commands and flags; no persistent navigable TUI observed.",
      "provenance": [
        {
          "url": "https://developer.salesforce.com/docs/atlas.en-us.sfdx_cli_reference.meta/sfdx_cli_reference/cli_reference_unified.htm",
          "evidence": "sf commands invoke discrete operations against orgs; command reference is command-based."
        }
      ]
    },
    {
      "name": "Pub/Sub API",
      "technology": "gRPC over HTTP/2, Avro payloads",
      "channel": "Event",
      "classification_rationale": "On Subscribe the service delivers platform-event, CDC, and event-monitoring messages to a consumer-held stream; service-initiated delivery to a consumer-controlled receiver.",
      "provenance": [
        {
          "url": "https://developer.salesforce.com/docs/platform/pub-sub-api/guide/intro.html",
          "evidence": "Pub/Sub API publishes and delivers binary event messages over gRPC/HTTP2 to subscribers."
        }
      ]
    },
    {
      "name": "Streaming API (CometD)",
      "technology": "CometD/Bayeux long-polling",
      "channel": "Event",
      "classification_rationale": "Service pushes event notifications to subscribed clients; Event Notification. Legacy but still documented.",
      "provenance": [
        {
          "url": "https://developer.salesforce.com/docs/atlas.en-us.264.0.platform_events.meta/platform_events/platform_events_subscribe_cometd.htm",
          "evidence": "CometD subscription delivers platform-event notifications to external clients; Pub/Sub API is the newer path."
        }
      ]
    },
    {
      "name": "Outbound Messages",
      "technology": "Workflow/flow-triggered SOAP callout",
      "channel": "Event",
      "classification_rationale": "On a record field-change event, the service sends a SOAP message to a designated endpoint; service-initiated delivery to a consumer-controlled receiver.",
      "provenance": [
        {
          "url": "https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_om_outboundmessaging_understanding.htm",
          "evidence": "Outbound messaging sends SOAP messages over HTTP(S) to a designated endpoint when triggered by a workflow rule."
        }
      ]
    },
    {
      "name": "Agentforce agents (Agent API)",
      "technology": "REST Agent API / in-app agent panel",
      "channel": "Conversational",
      "classification_rationale": "Consumer sends natural-language utterances to an AI agent that interprets them; topic/action orchestration is internal to the service. Message primitive with internal tools.",
      "provenance": [
        {
          "url": "https://developer.salesforce.com/docs/ai/agentforce/references/about",
          "evidence": "Agent API communicates with AI agents by sending messages; agents use topics and actions internally."
        }
      ]
    },
    {
      "name": "Salesforce Hosted MCP Server",
      "technology": "Model Context Protocol endpoint",
      "channel": "Agentic",
      "classification_rationale": "Salesforce-managed MCP endpoint exposing org data, Flows, Apex actions, and queries as discoverable tools; capability discovery and selection are part of the contract.",
      "provenance": [
        {
          "url": "https://developer.salesforce.com/blogs/2026/04/salesforce-hosted-mcp-servers-are-now-generally-available",
          "evidence": "Hosted MCP servers (GA Apr 2026) let any MCP client discover and call approved org tools."
        }
      ]
    },
    {
      "name": "Salesforce DX MCP Server",
      "technology": "Model Context Protocol (local dev)",
      "channel": "Agentic",
      "classification_rationale": "MCP server exposing DX/development tools as discoverable tools to agentic IDEs; capability discovery structures the contract. Beta/Developer Preview.",
      "provenance": [
        {
          "url": "https://developer.salesforce.com/blogs/2025/06/introducing-mcp-support-across-salesforce",
          "evidence": "The DX MCP Server runs development tasks via natural language through discoverable MCP tools."
        }
      ]
    }
  ],
  "access_mechanism_ledger": [
    {
      "mechanism": "REST API",
      "disposition": "interface",
      "detail": "REST API"
    },
    {
      "mechanism": "Connect REST API",
      "disposition": "excluded",
      "detail": "Folded into REST API (same style, base, auth)"
    },
    {
      "mechanism": "User Interface API",
      "disposition": "excluded",
      "detail": "Folded into REST API"
    },
    {
      "mechanism": "Composite API",
      "disposition": "excluded",
      "detail": "Folded into REST API"
    },
    {
      "mechanism": "Apex REST",
      "disposition": "excluded",
      "detail": "Folded into REST API"
    },
    {
      "mechanism": "Tooling API",
      "disposition": "excluded",
      "detail": "Folded into REST API and SOAP API"
    },
    {
      "mechanism": "SOAP API",
      "disposition": "interface",
      "detail": "SOAP API"
    },
    {
      "mechanism": "Apex SOAP",
      "disposition": "excluded",
      "detail": "Folded into SOAP API"
    },
    {
      "mechanism": "GraphQL API",
      "disposition": "interface",
      "detail": "GraphQL API"
    },
    {
      "mechanism": "Bulk API 2.0",
      "disposition": "interface",
      "detail": "Bulk API 2.0"
    },
    {
      "mechanism": "Metadata API",
      "disposition": "interface",
      "detail": "Metadata API"
    },
    {
      "mechanism": "Salesforce CLI (sf)",
      "disposition": "interface",
      "detail": "Salesforce CLI command interface"
    },
    {
      "mechanism": "CLI TUI check",
      "disposition": "excluded",
      "detail": "No persistent navigable TUI; command-based only"
    },
    {
      "mechanism": "Pub/Sub API",
      "disposition": "interface",
      "detail": "Pub/Sub API"
    },
    {
      "mechanism": "Streaming API (CometD)",
      "disposition": "interface",
      "detail": "Streaming API (CometD)"
    },
    {
      "mechanism": "Outbound Messages",
      "disposition": "interface",
      "detail": "Outbound Messages"
    },
    {
      "mechanism": "Web UI surface",
      "disposition": "interface",
      "detail": "Web UI (Lightning Experience / Salesforce Classic)"
    },
    {
      "mechanism": "Mobile client surface",
      "disposition": "interface",
      "detail": "Salesforce mobile app"
    },
    {
      "mechanism": "Desktop client surface",
      "disposition": "excluded",
      "detail": "No first-party standalone desktop client; desktop use is the browser-based Web UI; Outlook/Gmail integrations are add-ins"
    },
    {
      "mechanism": "Agentforce / Agent API",
      "disposition": "interface",
      "detail": "Agentforce agents (Agent API)"
    },
    {
      "mechanism": "Salesforce Hosted MCP Server",
      "disposition": "interface",
      "detail": "Salesforce Hosted MCP Server"
    },
    {
      "mechanism": "Salesforce DX MCP Server",
      "disposition": "interface",
      "detail": "Salesforce DX MCP Server"
    },
    {
      "mechanism": "Models API",
      "disposition": "excluded",
      "detail": "LLM-access feature via Apex/REST; folds into programmatic access"
    },
    {
      "mechanism": "Email Services / Email-to-Case",
      "disposition": "excluded",
      "detail": "Feature-level inbound ingestion, not a general access interface"
    },
    {
      "mechanism": "SDKs (Mobile SDK, Agentforce Python SDK, etc.)",
      "disposition": "excluded",
      "detail": "Client libraries, not interfaces"
    },
    {
      "mechanism": "AppExchange / third-party integrations",
      "disposition": "excluded",
      "detail": "Partner marketplace, not a provider interface"
    },
    {
      "mechanism": "Apex",
      "disposition": "excluded",
      "detail": "Server-side programming language, not an access interface"
    },
    {
      "mechanism": "OAuth / Connected Apps",
      "disposition": "excluded",
      "detail": "Authentication mechanism"
    }
  ],
  "channel_evidence": {
    "Interactive": "observed",
    "Agentic": "observed",
    "Conversational": "observed",
    "Event": "observed",
    "Programmatic": "observed"
  },
  "number_of_interfaces": 14,
  "multi_interface": true,
  "number_of_channels": 5,
  "multi_channel": true
}
```
