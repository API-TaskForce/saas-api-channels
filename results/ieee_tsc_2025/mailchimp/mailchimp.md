## SaaS summary

Mailchimp (Intuit Mailchimp, operated by The Rocket Science Group / Intuit) is a marketing and transactional messaging platform. This analysis identifies **10 provider-defined logical interfaces** spanning **5 distinct access channels** with at least one classified interface each. Mailchimp Transactional (formerly Mandrill) is treated as part of the same provider service. The self-hostable open-source Open Commerce project is treated as a separate product (see the coverage ledger).

## Interface classification table

| Interface                                                                      | Channel        | Interaction technology                                     | Provenance                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| ------------------------------------------------------------------------------ | -------------- | ---------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Web application                                                                | Interactive    | Browser-based web client                                   | Help docs repeatedly direct users to "the full version of Mailchimp in a web browser" for anything the mobile app cannot do, and the product is operated at login.mailchimp.com. Actions are expressed by manipulating views, menus, and forms over persistent account state (Affordance Manipulation). Current.                                                                                                                                                                                                                                                 |
| Mobile app (iOS and Android)                                                   | Interactive    | Native iOS and Android clients                             | mailchimp.com/features/mailchimp-mobile and the iOS/Android help articles document first-party apps with Home, Audience, Campaigns, and Analytics tabs and a Quick Actions menu. The consumer manipulates on-screen affordances of account state, so this is Interactive, not the Marketing API that the Mobile SDK wraps. Current.                                                                                                                                                                                                                              |
| Marketing API (v3.0)                                                           | Programmatic   | REST over HTTPS                                            | developer/marketing/docs/fundamentals and the API reference define REST resources (campaigns, lists, reports, ecommerce) under one datacenter-suffixed base (us\*.api.mailchimp.com/3.0) with API key or OAuth 2. The consumer explicitly invokes provider-defined operations (Operation Invocation). Current; some resources such as the Audiences Endpoints are marked BETA.                                                                                                                                                                                   |
| Transactional API (Mandrill)                                                   | Programmatic   | REST over HTTPS                                            | mandrillapp.com/docs and the Transactional developer docs define a distinct API at mandrillapp.com/api/1.0 with its own API key, covering transactional email and Transactional SMS. Different base and authentication from the Marketing API, so it is a separate Programmatic interface. Current.                                                                                                                                                                                                                                                              |
| Transactional SMTP relay                                                       | Programmatic   | SMTP submission                                            | developer/transactional/docs/smtp-integration documents message submission to smtp.mandrillapp.com over ports 25, 587, 2525, or 465. Structured message submission through a mail protocol is Operation Invocation, distinct in primitive from the REST APIs. Current.                                                                                                                                                                                                                                                                                           |
| Export API (v1.0)                                                              | Programmatic   | HTTP bulk export                                           | developer/marketing/docs/fundamentals documents a single-purpose Export API v1.0 under a separate base (/export/1.0/) returning streaming bulk export data. Different base and control structure from the Marketing REST API qualify it as a separate Programmatic interface. Current but legacy and single-purpose.                                                                                                                                                                                                                                             |
| Marketing webhooks                                                             | Event          | Service-initiated HTTP callbacks                           | developer/marketing/guides/sync-audience-data-webhooks documents Mailchimp posting audience and account events to a consumer-controlled URL when subscribed events occur (Event Notification). Current.                                                                                                                                                                                                                                                                                                                                                          |
| Transactional webhooks and inbound routing                                     | Event          | Service-initiated HTTP callbacks and inbound email parsing | mandrillapp.com/docs describes real-time event webhooks and receiving, processing, and parsing inbound email delivered to the consumer's endpoint. Service-initiated delivery to a consumer-controlled receiver from the Transactional platform, a separate base and account from Marketing webhooks. Current.                                                                                                                                                                                                                                                   |
| Analytics AI (in-product assistant)                                            | Conversational | Native GenAI assistant                                     | help/use-analytics-ai and solutions/ai-tools describe a conversational assistant built into the account where the user asks plain-language questions about campaigns, automations, audience, and revenue. The primitive is the natural-language message interpreted by Mailchimp, with orchestration internal to the service (Contextual Conversation). Current; part of Intuit Intelligence, portions in beta.                                                                                                                                                  |
| AI assistant connectors (ChatGPT, Claude, Perplexity, Codex, Google Workspace) | Agentic        | Official assistant connectors and ChatGPT app              | solutions/ai-tools states Mailchimp "connects to ChatGPT, Claude, Perplexity, Codex, and Google Workspace" so external assistants can build campaigns grounded in account data, and resources/connect-mailchimp-to-chatgpt documents an official Mailchimp app in the ChatGPT app store. The interface Mailchimp exposes offers capabilities that an external agent discovers and invokes by the user's goal (Capability Discovery and Invocation). Current; connectors available on Standard and Premium plans, US-only for the ChatGPT app at time of writing. |

## Coverage ledger

| Access mechanism                                                               | Disposition                                                                                             |
| ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------- |
| Marketing API (REST v3.0)                                                      | Marketing API (v3.0)                                                                                    |
| Transactional API (Mandrill)                                                   | Transactional API (Mandrill)                                                                            |
| Transactional SMS                                                              | Part of Transactional API (same base and auth)                                                          |
| Transactional SMTP                                                             | Transactional SMTP relay                                                                                |
| Export API v1.0                                                                | Export API (v1.0)                                                                                       |
| Marketing webhooks                                                             | Marketing webhooks                                                                                      |
| Transactional webhooks and inbound email routing                               | Transactional webhooks and inbound routing                                                              |
| Web application                                                                | Web application                                                                                         |
| Mobile app (iOS and Android)                                                   | Mobile app (iOS and Android)                                                                            |
| Desktop client (first-party surface check)                                     | Excluded: no first-party desktop client documented; the full product is the web application             |
| CLI (first-party surface check)                                                | Excluded: no official first-party CLI found; only client libraries and SDKs are provided                |
| TUI (CLI companion check)                                                      | Excluded: not applicable, no first-party CLI or terminal client exists                                  |
| Analytics AI (native assistant)                                                | Analytics AI                                                                                            |
| AI assistant connectors (ChatGPT, Claude, Perplexity, Codex, Google Workspace) | AI assistant connectors                                                                                 |
| Mailchimp app in the ChatGPT app store                                         | Part of AI assistant connectors (the ChatGPT instance of the connector)                                 |
| Google Workspace connector                                                     | Part of AI assistant connectors (see classification notes)                                              |
| "Write with AI" in-editor content generation / Intuit Assist inline tools      | Excluded: an affordance inside the web and mobile Interactive UI, not a separate logical interface      |
| Client libraries and SDKs (including Mobile SDK)                               | Excluded: SDKs and libraries implement interfaces but are not interfaces                                |
| OAuth 2 and API keys                                                           | Excluded: authentication methods, not interfaces                                                        |
| Integrations directory (300+ third-party integrations)                         | Excluded: third-party integrations, not provider-defined interfaces                                     |
| Third-party Mailchimp MCP servers (Insightful-Pipe, Apify, Composio, Porter)   | Excluded: third-party wrappers over the Marketing API, not provider-defined                             |
| Open Commerce (formerly Reaction Commerce), including its GraphQL API          | Excluded: separate open-source, self-hostable commerce product, not the hosted Mailchimp marketing SaaS |

## Channel coverage

| Channel        | Evidence |
| -------------- | -------- |
| Interactive    | Observed |
| Agentic        | Observed |
| Conversational | Observed |
| Event          | Observed |
| Programmatic   | Observed |

## Classification notes

The AI assistant connectors are the one genuine boundary call. Mailchimp's own marketing language frames the ChatGPT app as a "conversational strategy partner," which describes the human's experience inside ChatGPT rather than the interface Mailchimp itself exposes. The classified unit is Mailchimp's connector, whose consumer is an external assistant that discovers and invokes Mailchimp's capabilities by the user's goal. That is the MCP-style boundary case the taxonomy resolves to Agentic. This is distinct from the "conversational assistant with internal tools" carve-out, which applies only when the service runs the assistant and orchestrates internally, as Analytics AI does.

The Google Workspace connector is grouped by Mailchimp alongside the AI assistant connectors but is a productivity suite rather than an assistant, and its exact interaction contract is less clearly documented. It is folded into the same Agentic interface here because it does not change channel coverage; if its contract were shown to differ materially, it would warrant separate treatment.

## Multichannel verdict

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
  "generated_at": "2026-09-23T12:00:00Z",
  "evidence_checked_at": "2026-09-23T12:00:00Z",
  "saas": { "name": "Mailchimp" },
  "interfaces": [
    {
      "name": "Web application",
      "technology": "Browser-based web client",
      "channel": "Interactive",
      "classification_rationale": "Actions are expressed by manipulating views, menus, and forms over persistent account state; help docs point users to the full web version for anything the mobile app cannot do.",
      "provenance": [
        {
          "url": "https://mailchimp.com/help/about-mailchimp-for-ios/",
          "evidence": "States the full version of Mailchimp is accessed in a web browser when a task is unavailable in the mobile app."
        }
      ]
    },
    {
      "name": "Mobile app (iOS and Android)",
      "technology": "Native iOS and Android clients",
      "channel": "Interactive",
      "classification_rationale": "First-party apps with navigation tabs and a Quick Actions menu; the consumer manipulates on-screen affordances of account state.",
      "provenance": [
        {
          "url": "https://mailchimp.com/features/mailchimp-mobile/",
          "evidence": "Documents free iOS and Android apps to manage contacts, build campaigns, and track performance."
        },
        {
          "url": "https://mailchimp.com/help/about-mailchimp-for-android/",
          "evidence": "Describes Home, Audience, Campaigns, and Analytics tabs and a Quick Actions menu."
        }
      ]
    },
    {
      "name": "Marketing API (v3.0)",
      "technology": "REST over HTTPS",
      "channel": "Programmatic",
      "classification_rationale": "REST resources under one datacenter-suffixed base with API key or OAuth 2; the consumer explicitly invokes provider-defined operations.",
      "provenance": [
        {
          "url": "https://mailchimp.com/developer/marketing/docs/fundamentals/",
          "evidence": "Defines the v3.0 REST Marketing API, its base, versioning, and authentication."
        },
        {
          "url": "https://mailchimp.com/developer/marketing/api/",
          "evidence": "Full API reference of campaigns, lists, reports, and other resources."
        }
      ]
    },
    {
      "name": "Transactional API (Mandrill)",
      "technology": "REST over HTTPS",
      "channel": "Programmatic",
      "classification_rationale": "Distinct REST API at a separate base with its own API key covering transactional email and SMS; explicit operation invocation.",
      "provenance": [
        {
          "url": "https://mandrillapp.com/docs/",
          "evidence": "Documents delivering transactional email and SMS via the API, distinct from the Marketing API."
        }
      ]
    },
    {
      "name": "Transactional SMTP relay",
      "technology": "SMTP submission",
      "channel": "Programmatic",
      "classification_rationale": "Structured message submission over SMTP to smtp.mandrillapp.com; operation invocation with a mail-protocol primitive distinct from the REST APIs.",
      "provenance": [
        {
          "url": "https://mailchimp.com/developer/transactional/docs/smtp-integration/",
          "evidence": "Describes sending via SMTP with supported ports and TLS/SSL options."
        }
      ]
    },
    {
      "name": "Export API (v1.0)",
      "technology": "HTTP bulk export",
      "channel": "Programmatic",
      "classification_rationale": "Single-purpose API at a separate base returning streaming bulk export data; different base and control structure from the Marketing REST API.",
      "provenance": [
        {
          "url": "https://mailchimp.com/developer/marketing/docs/fundamentals/",
          "evidence": "States a single-purpose Export API version 1.0 is supported for account export functionality."
        }
      ]
    },
    {
      "name": "Marketing webhooks",
      "technology": "Service-initiated HTTP callbacks",
      "channel": "Event",
      "classification_rationale": "Mailchimp posts subscribed audience and account events to a consumer-controlled URL; event notification initiated by the service.",
      "provenance": [
        {
          "url": "https://mailchimp.com/developer/marketing/guides/sync-audience-data-webhooks/",
          "evidence": "Documents webhook delivery of audience events to a consumer endpoint."
        }
      ]
    },
    {
      "name": "Transactional webhooks and inbound routing",
      "technology": "Service-initiated HTTP callbacks and inbound email parsing",
      "channel": "Event",
      "classification_rationale": "Real-time event webhooks and inbound email parsed and delivered to the consumer's endpoint from the Transactional platform; separate base and account from Marketing webhooks.",
      "provenance": [
        {
          "url": "https://mandrillapp.com/docs/",
          "evidence": "Describes real-time insight webhooks and receiving, processing, and parsing inbound email."
        }
      ]
    },
    {
      "name": "Analytics AI (in-product assistant)",
      "technology": "Native GenAI assistant",
      "channel": "Conversational",
      "classification_rationale": "The user asks plain-language questions and the service interprets the message and responds; tool orchestration is internal to Mailchimp.",
      "provenance": [
        {
          "url": "https://mailchimp.com/help/use-analytics-ai/",
          "evidence": "Describes a conversational assistant built into the account answering plain-language questions about campaigns, audience, and revenue."
        },
        {
          "url": "https://mailchimp.com/solutions/ai-tools/",
          "evidence": "Positions Analytics AI as part of Mailchimp with Intuit Intelligence for plain-language performance insights."
        }
      ]
    },
    {
      "name": "AI assistant connectors (ChatGPT, Claude, Perplexity, Codex, Google Workspace)",
      "technology": "Official assistant connectors and ChatGPT app",
      "channel": "Agentic",
      "classification_rationale": "Mailchimp exposes capabilities that an external assistant discovers and invokes by the user's goal to build campaigns grounded in account data; capability discovery and selection structure the contract.",
      "provenance": [
        {
          "url": "https://mailchimp.com/solutions/ai-tools/",
          "evidence": "States Mailchimp connects to ChatGPT, Claude, Perplexity, Codex, and Google Workspace, with connectors available on Standard and Premium plans."
        },
        {
          "url": "https://mailchimp.com/resources/connect-mailchimp-to-chatgpt/",
          "evidence": "Documents an official Mailchimp app in the ChatGPT app store that exposes Mailchimp data and campaign-building capabilities to the assistant."
        }
      ]
    }
  ],
  "access_mechanism_ledger": [
    {
      "mechanism": "Marketing API (REST v3.0)",
      "disposition": "interface",
      "detail": "Marketing API (v3.0)"
    },
    {
      "mechanism": "Transactional API (Mandrill)",
      "disposition": "interface",
      "detail": "Transactional API (Mandrill)"
    },
    {
      "mechanism": "Transactional SMS",
      "disposition": "interface",
      "detail": "Part of Transactional API (same base and auth)"
    },
    {
      "mechanism": "Transactional SMTP",
      "disposition": "interface",
      "detail": "Transactional SMTP relay"
    },
    {
      "mechanism": "Export API v1.0",
      "disposition": "interface",
      "detail": "Export API (v1.0)"
    },
    {
      "mechanism": "Marketing webhooks",
      "disposition": "interface",
      "detail": "Marketing webhooks"
    },
    {
      "mechanism": "Transactional webhooks and inbound email routing",
      "disposition": "interface",
      "detail": "Transactional webhooks and inbound routing"
    },
    {
      "mechanism": "Web application",
      "disposition": "interface",
      "detail": "Web application"
    },
    {
      "mechanism": "Mobile app (iOS and Android)",
      "disposition": "interface",
      "detail": "Mobile app (iOS and Android)"
    },
    {
      "mechanism": "Desktop client",
      "disposition": "excluded",
      "detail": "No first-party desktop client documented; the full product is the web application"
    },
    {
      "mechanism": "CLI",
      "disposition": "excluded",
      "detail": "No official first-party CLI found; only client libraries and SDKs are provided"
    },
    {
      "mechanism": "TUI",
      "disposition": "excluded",
      "detail": "Not applicable, no first-party CLI or terminal client exists"
    },
    {
      "mechanism": "Analytics AI (native assistant)",
      "disposition": "interface",
      "detail": "Analytics AI"
    },
    {
      "mechanism": "AI assistant connectors (ChatGPT, Claude, Perplexity, Codex, Google Workspace)",
      "disposition": "interface",
      "detail": "AI assistant connectors"
    },
    {
      "mechanism": "Mailchimp app in the ChatGPT app store",
      "disposition": "interface",
      "detail": "Part of AI assistant connectors"
    },
    {
      "mechanism": "Google Workspace connector",
      "disposition": "interface",
      "detail": "Part of AI assistant connectors"
    },
    {
      "mechanism": "Write with AI in-editor generation / Intuit Assist inline tools",
      "disposition": "excluded",
      "detail": "An affordance inside the web and mobile Interactive UI, not a separate logical interface"
    },
    {
      "mechanism": "Client libraries and SDKs (including Mobile SDK)",
      "disposition": "excluded",
      "detail": "SDKs implement interfaces but are not interfaces"
    },
    {
      "mechanism": "OAuth 2 and API keys",
      "disposition": "excluded",
      "detail": "Authentication methods, not interfaces"
    },
    {
      "mechanism": "Integrations directory (300+ third-party integrations)",
      "disposition": "excluded",
      "detail": "Third-party integrations, not provider-defined interfaces"
    },
    {
      "mechanism": "Third-party Mailchimp MCP servers",
      "disposition": "excluded",
      "detail": "Third-party wrappers over the Marketing API, not provider-defined"
    },
    {
      "mechanism": "Open Commerce (Reaction Commerce), including its GraphQL API",
      "disposition": "excluded",
      "detail": "Separate open-source, self-hostable commerce product, not the hosted Mailchimp marketing SaaS"
    }
  ],
  "channel_evidence": {
    "Interactive": "observed",
    "Agentic": "observed",
    "Conversational": "observed",
    "Event": "observed",
    "Programmatic": "observed"
  },
  "number_of_interfaces": 10,
  "multi_interface": true,
  "number_of_channels": 5,
  "multi_channel": true
}
```
