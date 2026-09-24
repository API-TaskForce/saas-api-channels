## SaaS summary

**Deskera** exposes **4 provider-defined logical interfaces** across **3 distinct access channels**. Deskera is a cloud business platform (deskera.com) whose product suite (Books, Sales, CRM+, People, and the broader ERP/MRP offering) is reached through browser and mobile clients, a single REST API, and a first-party conversational AI assistant.

## Interface classification table

| Interface                                                    | Channel        | Interaction technology       | Provenance                                                                                                                                                                                                                                                                                                                                                                                                                      |
| ------------------------------------------------------------ | -------------- | ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Deskera Web Application (BooksPlus, CRMPlus, PeoplePlus, Go) | Interactive    | Browser-based web UI         | The developer documentation "Production Environment" page lists the product UI URLs (booksplus.deskera.com, crmplus.deskera.com, peopleplus.deskera.com, go.deskera.com). These are persistent, navigable representations of service state where actions are expressed by manipulating presented affordances (views, forms, menus). Current.                                                                                    |
| Deskera Mobile App                                           | Interactive    | Native iOS and Android app   | Official product page deskera.com/deskera-mobile plus App Store (Deskera Holdings Ltd., id1463523833) and Google Play (com.deskera.desk) listings confirm a first-party mobile client. Same affordance-manipulation paradigm on a mobile surface, distinct client technology from the web app. Current.                                                                                                                         |
| Deskera REST API (Books, Sales, CRM+, People)                | Programmatic   | HTTP REST API                | Official developer docs at deskera.github.io/Developer-Documentation. All four product APIs share one production base (bifrost-us.deskera.com) and one token/OAuth auth scheme (x-access-token), so they form one logical interface. The consumer explicitly invokes provider-defined operations through structured HTTP requests (Operation Invocation). Current.                                                              |
| Deskera AI assistant ("David")                               | Conversational | In-product AI chat assistant | Official product page deskera.com/ai. Users act by chatting in natural language ("chatting with your AI", "Ask AI to create bills and invoices", "AI-powered chat"). The primitive is the natural-language message interpreted by the service, with tool orchestration internal to the service. This is the natural-language-assistant-with-internal-tools case, which resolves to Conversational rather than Agentic. Current. |

## Coverage ledger table

| Access mechanism                                        | Disposition                                                                                                                                                                              |
| ------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| REST API (Books / Sales / CRM+ / People)                | Deskera REST API (Programmatic)                                                                                                                                                          |
| Web application surface                                 | Deskera Web Application (Interactive)                                                                                                                                                    |
| Mobile application surface                              | Deskera Mobile App (Interactive)                                                                                                                                                         |
| Conversational AI assistant ("David")                   | Deskera AI assistant (Conversational)                                                                                                                                                    |
| OAuth endpoints (oauth.deskera.com, token)              | Excluded: authentication mechanism, not a logical interface                                                                                                                              |
| Desktop application surface                             | Excluded: no first-party native desktop client observed; desktop use is the web application in a browser                                                                                 |
| Terminal / CLI surface                                  | Excluded: only a community sample ("deskera-cli-node-sample", a Node.js API client) exists; no provider-shipped CLI product. It is a sample wrapper over the REST API                    |
| CLI TUI                                                 | Excluded: no CLI product exists, so no persistent navigable TUI                                                                                                                          |
| Webhooks / events                                       | Excluded: no provider-defined webhook or event mechanism in the official developer docs; third-party platforms (Zapier, Make, Integrately) build webhooks externally around the REST API |
| MCP / agent protocol                                    | Excluded: no official Deskera-shipped MCP server; only a generic conceptual mention of MCP in a Deskera blog post, which is not a shipped interface                                      |
| Java SDK                                                | Excluded: SDK, not a logical interface (it implements the REST API)                                                                                                                      |
| Third-party integrations (Make, Zapier, Integrately)    | Excluded: third-party connectors, not provider-defined interfaces                                                                                                                        |
| Helpdesk email-to-ticket ("connect your support email") | Excluded: an internal CRM helpdesk feature, not a provider-defined access interface to operate the service                                                                               |

## Channel coverage table

| Channel        | Evidence             |
| -------------- | -------------------- |
| Interactive    | Observed             |
| Agentic        | No evidence observed |
| Conversational | Observed             |
| Event          | No evidence observed |
| Programmatic   | Observed             |

## Classification notes

The AI assistant "David" was placed in Conversational rather than Agentic because the consumer-facing contract is natural-language messaging. The assistant creates transactions and retrieves data by orchestrating tools internally, and that orchestration is not exposed as a discoverable, selectable capability set in the interaction contract, so the Agentic test is not met.

The community "deskera-cli-node-sample" repository is a sample API client, not a provider-shipped CLI product, so it does not add a Programmatic interface beyond the REST API it calls, and it introduces no TUI.

## Multichannel verdict

**Multichannel** (3 distinct paradigms: Interactive, Programmatic, Conversational).

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
    "name": "Deskera"
  },
  "interfaces": [
    {
      "name": "Deskera Web Application (BooksPlus, CRMPlus, PeoplePlus, Go)",
      "technology": "Browser-based web UI",
      "channel": "Interactive",
      "classification_rationale": "Persistent, navigable product UIs where the consumer expresses actions by manipulating presented affordances (views, forms, menus). Affordance Manipulation.",
      "provenance": [
        {
          "url": "https://deskera.github.io/Developer-Documentation/docs/environment/prod",
          "evidence": "Official developer docs 'Production Environment' page lists UI URLs booksplus.deskera.com, crmplus.deskera.com, peopleplus.deskera.com, go.deskera.com."
        }
      ]
    },
    {
      "name": "Deskera Mobile App",
      "technology": "Native iOS and Android application",
      "channel": "Interactive",
      "classification_rationale": "First-party mobile client using the same affordance-manipulation paradigm on a distinct mobile surface.",
      "provenance": [
        {
          "url": "https://www.deskera.com/deskera-mobile",
          "evidence": "Official product page describing the Deskera mobile application for the workforce, syncing with the desktop backend."
        },
        {
          "url": "https://apps.apple.com/us/app/deskera-business-accounting/id1463523833",
          "evidence": "App Store listing published by Deskera Holdings Ltd., confirming a first-party iOS client."
        },
        {
          "url": "https://play.google.com/store/apps/details?id=com.deskera.desk",
          "evidence": "Google Play listing (com.deskera.desk) confirming a first-party Android client."
        }
      ]
    },
    {
      "name": "Deskera REST API (Books, Sales, CRM+, People)",
      "technology": "HTTP REST API",
      "channel": "Programmatic",
      "classification_rationale": "The consumer explicitly invokes provider-defined operations through structured HTTP requests. All product APIs share one production base and one token/OAuth auth scheme, so they form one logical interface. Operation Invocation.",
      "provenance": [
        {
          "url": "https://deskera.github.io/Developer-Documentation/",
          "evidence": "Official developer documentation portal covering Books, Sales, CRM+, and People API references."
        },
        {
          "url": "https://deskera.github.io/Developer-Documentation/docs/books/started/",
          "evidence": "Establishes token authentication (x-access-token) and REST request/response structure common to the Deskera APIs."
        },
        {
          "url": "https://deskera.github.io/Developer-Documentation/docs/environment/prod",
          "evidence": "Establishes a single production API base (bifrost-us.deskera.com) and OAuth token flow shared across the products."
        }
      ]
    },
    {
      "name": "Deskera AI assistant (\"David\")",
      "technology": "In-product conversational AI assistant",
      "channel": "Conversational",
      "classification_rationale": "Actions are expressed through natural-language messages interpreted by the service (chat to retrieve financials, create transactions, get support). Tool orchestration is internal to the service and not part of the consumer-facing contract, so Conversational rather than Agentic.",
      "provenance": [
        {
          "url": "https://www.deskera.com/ai",
          "evidence": "Official AI product page describing chat-based interaction ('chatting with your AI', 'Ask AI to create bills and invoices', 'AI-powered chat') and the assistant 'David'."
        }
      ]
    }
  ],
  "access_mechanism_ledger": [
    {
      "mechanism": "REST API (Books / Sales / CRM+ / People)",
      "disposition": "interface",
      "detail": "Deskera REST API"
    },
    {
      "mechanism": "Web application surface",
      "disposition": "interface",
      "detail": "Deskera Web Application"
    },
    {
      "mechanism": "Mobile application surface",
      "disposition": "interface",
      "detail": "Deskera Mobile App"
    },
    {
      "mechanism": "Conversational AI assistant (David)",
      "disposition": "interface",
      "detail": "Deskera AI assistant"
    },
    {
      "mechanism": "OAuth endpoints",
      "disposition": "excluded",
      "detail": "Authentication mechanism, not a logical interface"
    },
    {
      "mechanism": "Desktop application surface",
      "disposition": "excluded",
      "detail": "No first-party native desktop client observed; desktop use is the web application in a browser"
    },
    {
      "mechanism": "Terminal / CLI surface",
      "disposition": "excluded",
      "detail": "Only a community sample (deskera-cli-node-sample, a Node.js API client) exists; no provider-shipped CLI product. It wraps the REST API"
    },
    {
      "mechanism": "CLI TUI",
      "disposition": "excluded",
      "detail": "No CLI product exists, so no persistent navigable TUI"
    },
    {
      "mechanism": "Webhooks / events",
      "disposition": "excluded",
      "detail": "No provider-defined webhook or event mechanism in the official developer docs; third-party platforms build webhooks externally around the REST API"
    },
    {
      "mechanism": "MCP / agent protocol",
      "disposition": "excluded",
      "detail": "No official Deskera-shipped MCP server; only a generic conceptual mention in a blog post"
    },
    {
      "mechanism": "Java SDK",
      "disposition": "excluded",
      "detail": "SDK that implements the REST API, not a logical interface"
    },
    {
      "mechanism": "Third-party integrations (Make, Zapier, Integrately)",
      "disposition": "excluded",
      "detail": "Third-party connectors, not provider-defined interfaces"
    },
    {
      "mechanism": "Helpdesk email-to-ticket",
      "disposition": "excluded",
      "detail": "Internal CRM helpdesk feature, not a provider-defined service access interface"
    }
  ],
  "channel_evidence": {
    "Interactive": "observed",
    "Agentic": "no_evidence_observed",
    "Conversational": "observed",
    "Event": "no_evidence_observed",
    "Programmatic": "observed"
  },
  "number_of_interfaces": 4,
  "multi_interface": true,
  "number_of_channels": 3,
  "multi_channel": true
}
```
