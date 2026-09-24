## SaaS summary

Trustmary (Trustmary Group Oy, trustmary.com) is a review and testimonial collection, management, and display platform. From official sources I identified **four logical interfaces** spanning **three distinct access channels**.

## Interface classification table

| Interface                                 | Channel      | Interaction technology                                        | Provenance                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| ----------------------------------------- | ------------ | ------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Web management application                | Interactive  | Authenticated web app (browser)                               | Help Center articles direct users to operate the app UI directly (for example navigating to Settings and the Developers tab to create API keys, building surveys, configuring widgets, viewing reports). The product pages describe collecting, managing, and showcasing reviews through this console. Actions are expressed by manipulating presented controls over a persistent, navigable representation of account state, which is Affordance Manipulation. Current.                             |
| Respondent-facing survey and widget forms | Interactive  | Embedded/hosted JavaScript widgets and survey forms (browser) | The Widgets category and the "Protect Widget Forms with Google reCAPTCHA" article document public forms rendered on customer sites or via hosted links, distributed through embed, URL, QR code, email, and SMS. Respondents complete branded surveys and leave reviews by manipulating form affordances, with conditional logic driving a navigable flow. This is a distinct contract from the console (public, unauthenticated, different base), same paradigm (Affordance Manipulation). Current. |
| Integration REST API                      | Programmatic | HTTP/JSON REST API at `api.trustmary.io/v1`                   | The API Authentication article establishes API-key auth and a `/v1/test` endpoint; resource articles (Contacts, Reviews, Surveys, Review connections, Contact lists, EU Data Act Data Transition) share one base, one auth, and JSON request bodies. The consumer explicitly invokes provider-defined operations through structured requests, which is Operation Invocation. Current.                                                                                                                |
| Survey answer webhooks                    | Event        | Outbound HTTP webhooks                                        | The "Survey answer webhooks (developers)" article describes pushing events to a consumer endpoint, and the Zapier/Make "Watch New Completed Answer" triggers are backed by these webhooks. Trustmary initiates the interaction when a survey answer is completed and delivers it to a consumer-controlled receiver, which is Event Notification, not an ordinary API returning event data. Current.                                                                                                  |

## Coverage ledger

| Access mechanism                                                                                              | Disposition                                                                                                                                                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Web app (first-party web surface)                                                                             | Web management application (Interactive)                                                                                                                                                                                                                                                                       |
| Embedded widgets / survey and feedback forms                                                                  | Respondent-facing survey and widget forms (Interactive)                                                                                                                                                                                                                                                        |
| Integration API (`api.trustmary.io/v1`)                                                                       | Integration REST API (Programmatic)                                                                                                                                                                                                                                                                            |
| Survey answer webhooks                                                                                        | Survey answer webhooks (Event)                                                                                                                                                                                                                                                                                 |
| Mobile client (first-party mobile surface)                                                                    | Excluded: no native first-party app observed in official sources or app stores. Third-party listings marking Android/iPhone/iPad support reflect the responsive web app being browser-accessible, not a native client.                                                                                         |
| Desktop client (first-party desktop surface)                                                                  | Excluded: no native desktop client documented.                                                                                                                                                                                                                                                                 |
| CLI (first-party terminal surface)                                                                            | Excluded: no command-line interface documented.                                                                                                                                                                                                                                                                |
| TUI                                                                                                           | Excluded: no CLI exists, so no navigable terminal interface.                                                                                                                                                                                                                                                   |
| Conversational / in-product AI assistant                                                                      | Excluded: the "AI analyses" feature summarizes feedback into themes (internal analytics) and the "AI-optimised profile" is content read by external AI models. Neither is a provider-defined natural-language access interface. The Help Center "Chat with us" is Crisp support chat, not a product interface. |
| MCP / agent protocol                                                                                          | Excluded: no agent-protocol or capability-discovery interface documented.                                                                                                                                                                                                                                      |
| Zapier / Make / native integrations (HubSpot, Pipedrive, QuickBooks, Google Sheets, WooCommerce, CMS plugins) | Excluded: third-party integrations built on the REST API and webhooks, not separate provider-defined interfaces.                                                                                                                                                                                               |
| Email / SMS / QR / URL survey distribution                                                                    | Excluded: outbound distribution mechanisms for surveys. The resulting respondent interaction is the survey-forms interface already counted.                                                                                                                                                                    |
| SDKs / client libraries                                                                                       | Excluded: not counted as interfaces per rule; none prominently documented in any case.                                                                                                                                                                                                                         |

## Channel coverage table

| Channel        | Evidence             |
| -------------- | -------------------- |
| Interactive    | Observed             |
| Agentic        | No evidence observed |
| Conversational | No evidence observed |
| Event          | Observed             |
| Programmatic   | Observed             |

## Multichannel verdict

`Multichannel` (3 distinct paradigms: Interactive, Programmatic, Event).

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
  "generated_at": "2026-09-24T12:00:00Z",
  "evidence_checked_at": "2026-09-24T12:00:00Z",
  "saas": {
    "name": "Trustmary"
  },
  "interfaces": [
    {
      "name": "Web management application",
      "technology": "Authenticated web application (browser)",
      "channel": "Interactive",
      "classification_rationale": "Users operate a persistent, navigable representation of account state (surveys, reviews, widgets, reports, settings) by manipulating presented controls, which is Affordance Manipulation.",
      "provenance": [
        {
          "url": "https://help.trustmary.com/en/article/api-authentication-developers-11uji38/",
          "evidence": "Instructs users to navigate the app to Settings and the Developers tab to create API keys, evidencing a navigable management console."
        },
        {
          "url": "https://trustmary.com/integrations/",
          "evidence": "Describes managing collection, reviews, and social proof in one place through the Trustmary app."
        }
      ]
    },
    {
      "name": "Respondent-facing survey and widget forms",
      "technology": "Embedded/hosted JavaScript widgets and survey forms (browser)",
      "channel": "Interactive",
      "classification_rationale": "Respondents complete branded surveys and leave reviews by manipulating form affordances in a navigable, conditional flow. Public and unauthenticated, a genuinely different base and auth from the console, but the same Affordance Manipulation paradigm.",
      "provenance": [
        {
          "url": "https://help.trustmary.com/en/article/protect-widget-forms-with-google-recaptcha-ysx7sq/",
          "evidence": "Documents widget forms that record genuine user interactions/submissions, protected by reCAPTCHA."
        },
        {
          "url": "https://help.trustmary.com/en/category/widgets-1sekyvc/",
          "evidence": "Widgets category establishing embedded, respondent-facing form and display surfaces distributed via embed, URL, QR, email, and SMS."
        }
      ]
    },
    {
      "name": "Integration REST API",
      "technology": "HTTP/JSON REST API (api.trustmary.io/v1)",
      "channel": "Programmatic",
      "classification_rationale": "The consumer explicitly invokes provider-defined operations over contacts, reviews, surveys, review connections, and lists through structured JSON requests under one base and one API-key auth, which is Operation Invocation.",
      "provenance": [
        {
          "url": "https://help.trustmary.com/en/article/api-authentication-developers-11uji38/",
          "evidence": "Establishes API-key authentication and a testable endpoint at https://api.trustmary.io/v1/test."
        },
        {
          "url": "https://help.trustmary.com/en/article/reviews-developers-1xp19l3/",
          "evidence": "Defines API resource objects and operations (reviews) invoked via structured requests, part of the single REST surface."
        }
      ]
    },
    {
      "name": "Survey answer webhooks",
      "technology": "Outbound HTTP webhooks",
      "channel": "Event",
      "classification_rationale": "The service initiates the interaction on the survey-answer-completed event and delivers it to a consumer-controlled receiver endpoint, which is Event Notification rather than an ordinary API returning event data.",
      "provenance": [
        {
          "url": "https://help.trustmary.com/en/article/survey-answer-webhooks-developers-1oq7d8y/",
          "evidence": "Describes webhooks as a method of pushing events to the consumer's endpoint."
        }
      ]
    }
  ],
  "access_mechanism_ledger": [
    {
      "mechanism": "Web app (first-party web surface)",
      "disposition": "interface",
      "detail": "Web management application"
    },
    {
      "mechanism": "Embedded widgets / survey and feedback forms",
      "disposition": "interface",
      "detail": "Respondent-facing survey and widget forms"
    },
    {
      "mechanism": "Integration API (api.trustmary.io/v1)",
      "disposition": "interface",
      "detail": "Integration REST API"
    },
    {
      "mechanism": "Survey answer webhooks",
      "disposition": "interface",
      "detail": "Survey answer webhooks"
    },
    {
      "mechanism": "Mobile client (first-party mobile surface)",
      "disposition": "excluded",
      "detail": "No native first-party app in official sources or app stores; third-party device-support claims reflect the responsive web app, not a native client."
    },
    {
      "mechanism": "Desktop client (first-party desktop surface)",
      "disposition": "excluded",
      "detail": "No native desktop client documented."
    },
    {
      "mechanism": "CLI (first-party terminal surface)",
      "disposition": "excluded",
      "detail": "No command-line interface documented."
    },
    {
      "mechanism": "TUI",
      "disposition": "excluded",
      "detail": "No CLI exists, so no navigable terminal interface."
    },
    {
      "mechanism": "Conversational / in-product AI assistant",
      "disposition": "excluded",
      "detail": "AI analyses is internal analytics and the AI-optimised profile is content read by external AI; neither is a provider-defined NL access interface. Help Center chat is third-party support (Crisp)."
    },
    {
      "mechanism": "MCP / agent protocol",
      "disposition": "excluded",
      "detail": "No agent-protocol or capability-discovery interface documented."
    },
    {
      "mechanism": "Zapier / Make / native integrations",
      "disposition": "excluded",
      "detail": "Third-party integrations built on the REST API and webhooks, not separate provider-defined interfaces."
    },
    {
      "mechanism": "Email / SMS / QR / URL survey distribution",
      "disposition": "excluded",
      "detail": "Outbound distribution mechanisms; the resulting respondent interaction is the survey-forms interface already counted."
    },
    {
      "mechanism": "SDKs / client libraries",
      "disposition": "excluded",
      "detail": "Not counted as interfaces per rule; none prominently documented."
    }
  ],
  "channel_evidence": {
    "Interactive": "observed",
    "Agentic": "no_evidence_observed",
    "Conversational": "no_evidence_observed",
    "Event": "observed",
    "Programmatic": "observed"
  },
  "number_of_interfaces": 4,
  "multi_interface": true,
  "number_of_channels": 3,
  "multi_channel": true
}
```
