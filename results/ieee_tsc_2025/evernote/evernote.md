## SaaS summary

**Evernote** (Evernote Corporation, operated by Bending Spoons). Official domain evernote.com, developer portal dev.evernote.com, help center help.evernote.com.

Identified logical interfaces: **8**. Distinct channels with at least one classified interface: **5**.

## Interface classification table

| Interface                                   | Channel        | Interaction technology                                        | Provenance                                                                                                                                                                                                                                                                                                                                                                                                         |
| ------------------------------------------- | -------------- | ------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Evernote GUI clients (web, desktop, mobile) | Interactive    | Web app, Windows/macOS desktop apps, iOS/Android apps         | The official download page ships first-party clients for Windows, Mac, iOS, and Android plus the web app. Actions are expressed by manipulating views, menus, and forms over a persistent, navigable representation of the note collection. Affordance Manipulation → Interactive. Current.                                                                                                                        |
| Web Clipper                                 | Interactive    | Browser extension (Chrome, Safari, Firefox, Edge)             | Evernote Web Clipper is a first-party browser extension, published by Evernote Corporation, that saves web pages, articles, and screenshots directly to the account. The consumer manipulates capture affordances (clip type, notebook, tags, annotations). Affordance Manipulation → Interactive. Current.                                                                                                        |
| AI Assistant                                | Conversational | In-app chat drawer (LLM-backed, built with OpenAI)            | The AI Assistant is opened from a button in the desktop and web app that expands a chat drawer; the consumer interacts through natural-language messages and the assistant reads, searches, and works with notes on their behalf. The primitive is the message and tool orchestration is internal to the service, so by the natural-language-assistant boundary case this is Conversational, not Agentic. Current. |
| Evernote MCP server                         | Agentic        | Model Context Protocol server (provider-hosted)               | Evernote hosts an MCP server that acts as a secure gateway between the account and external AI tools, exposing Read and Create capabilities that AI agents discover and invoke, available to all paid users. Capability discovery and selection structure the interaction contract, so by the MCP boundary case this is Agentic, not Programmatic. Current (help article updated August 2026).                     |
| Cloud API (EDAM)                            | Programmatic   | Thrift-based RPC over HTTPS (NoteStore, UserStore), OAuth     | When an application accesses the Cloud API it speaks directly to the Evernote web service to act on a single user's account, across supported languages including Objective-C, Java, PHP, Ruby, Python, and others. The consumer explicitly invokes provider-defined operations through structured calls. Operation Invocation → Programmatic. See freshness note below.                                           |
| Local API                                   | Programmatic   | Command lines (Windows), AppleScript (Mac), Intents (Android) | The Local API lets an application call the local Evernote clients, with authentication and security handled by the local application, using command lines on Windows, AppleScript on Mac, and Intents on Android. Provider-defined operations invoked through structured commands against a different base (the local client) and a different auth model. Operation Invocation → Programmatic.                     |
| Email-to-Evernote                           | Programmatic   | Inbound email to a unique @m.evernote.com address             | Each account has a unique Evernote email address; forwarding or sending an email to it creates a new note, and subject-line commands such as @notebook, #tag, and !reminder direct the note. The consumer submits a structured message to a provider-defined address to invoke note creation, analogous to SMTP submission. Operation Invocation → Programmatic. Current.                                          |
| Webhooks                                    | Event          | HTTP callbacks to a consumer-controlled URL                   | A webhook is registered by contacting Evernote developer support with the customer key, the URL the webhook will call, and a note filter, after which the service calls that URL. The service initiates the interaction when subscribed note events occur and delivers to a receiver the consumer controls. Event Notification → Event. Current.                                                                   |

## Coverage ledger table

| Access mechanism                                          | Disposition                                                                                                                    |
| --------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| Web app                                                   | Evernote GUI clients (Interactive)                                                                                             |
| Desktop app (Windows, macOS)                              | Evernote GUI clients (Interactive)                                                                                             |
| Mobile app (iOS, Android)                                 | Evernote GUI clients (Interactive)                                                                                             |
| Web Clipper (browser extension)                           | Web Clipper (Interactive)                                                                                                      |
| AI Assistant (chat)                                       | AI Assistant (Conversational)                                                                                                  |
| MCP server                                                | Evernote MCP server (Agentic)                                                                                                  |
| Cloud API                                                 | Cloud API (Programmatic)                                                                                                       |
| Local API                                                 | Local API (Programmatic)                                                                                                       |
| Email-to-Evernote (inbound email)                         | Email-to-Evernote (Programmatic)                                                                                               |
| Webhooks                                                  | Webhooks (Event)                                                                                                               |
| CLI                                                       | Excluded: no first-party command-line client documented                                                                        |
| TUI                                                       | Excluded: no first-party TUI (no CLI to carry one)                                                                             |
| Terminal client                                           | Excluded: none shipped                                                                                                         |
| GraphQL API                                               | Excluded: no official evidence; the public API is Thrift-based (EDAM)                                                          |
| SDKs (iOS, Android, Python, Java, and others)             | Excluded: client libraries that implement the Cloud API, not interfaces                                                        |
| Semantic Search, AI Meeting Notes                         | Excluded: features surfaced inside the GUI and AI Assistant, not separate access interfaces (feature coverage is out of scope) |
| Third-party integrations (Zapier, Pipedream, and similar) | Excluded: built on the Cloud API; not provider-defined interfaces                                                              |

## Channel coverage table

| Channel        | Evidence |
| -------------- | -------- |
| Interactive    | Observed |
| Agentic        | Observed |
| Conversational | Observed |
| Event          | Observed |
| Programmatic   | Observed |

## Classification notes

The Cloud API remains documented and operational at dev.evernote.com, but present-day access is gated: new developer keys are issued only after a manual review of a submitted request rather than self-serve, so the interface is current though its onboarding is restricted. This affects availability, not the classification.

Two boundary cases sit close together and were resolved by contract. The AI Assistant is Conversational because the consumer-facing primitive is the natural-language message and the assistant's use of search, note creation, tagging, and web lookup is orchestrated internally. The MCP server is Agentic because capability discovery and selection (its Read and Create tools) are part of the interaction contract that external agents consume.

Web Clipper is counted as a second Interactive interface, distinct from the main GUI, on the basis of a genuinely different capture-overlay control structure. A reviewer who folded it into the GUI client family would report seven interfaces rather than eight, with no change to channel coverage or the verdict.

## Multichannel verdict

**Multichannel** (5 distinct paradigms observed).

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
  "saas": { "name": "Evernote" },
  "interfaces": [
    {
      "name": "Evernote GUI clients (web, desktop, mobile)",
      "technology": "Web app, Windows/macOS desktop apps, iOS/Android apps",
      "channel": "Interactive",
      "classification_rationale": "Actions are expressed by manipulating views, menus, and forms over a persistent, navigable representation of the note collection. Affordance Manipulation.",
      "provenance": [
        {
          "url": "https://evernote.com/download",
          "evidence": "First-party clients for Windows, Mac, iOS, Android and the web app."
        },
        {
          "url": "https://evernote.com/features/ai-features",
          "evidence": "Confirms first-party Desktop and Web clients as the interactive surface."
        }
      ]
    },
    {
      "name": "Web Clipper",
      "technology": "Browser extension (Chrome, Safari, Firefox, Edge)",
      "channel": "Interactive",
      "classification_rationale": "First-party browser-extension capture surface; the consumer manipulates capture affordances (clip type, notebook, tags, annotations). Affordance Manipulation.",
      "provenance": [
        {
          "url": "https://evernote.com/features/webclipper",
          "evidence": "Web Clipper integrates with the account and is compatible with all major browsers."
        },
        {
          "url": "https://evernote.com/web-clipper/web-clipper-for-desktop",
          "evidence": "Provider page describing the first-party clipper client."
        }
      ]
    },
    {
      "name": "AI Assistant",
      "technology": "In-app chat drawer (LLM-backed, built with OpenAI)",
      "channel": "Conversational",
      "classification_rationale": "The consumer interacts through natural-language messages; the assistant's search, creation, tagging, and web lookup are orchestrated internally and are not part of the consumer-facing contract. Contextual Conversation.",
      "provenance": [
        {
          "url": "https://help.evernote.com/hc/en-us/articles/46319409880211-AI-Assistant",
          "evidence": "Chat drawer opened from a button in the desktop and web app; assistant reads, searches, and works with the user's notes."
        },
        {
          "url": "https://evernote.com/features/ai-features",
          "evidence": "AI Assistant responds to a simple request and retrieves content directly from the chat window."
        }
      ]
    },
    {
      "name": "Evernote MCP server",
      "technology": "Model Context Protocol server (provider-hosted)",
      "channel": "Agentic",
      "classification_rationale": "Provider-hosted gateway exposing Read and Create capabilities that external AI agents discover and invoke; capability discovery and selection structure the contract. MCP boundary case resolves to Agentic.",
      "provenance": [
        {
          "url": "https://help.evernote.com/hc/en-us/articles/51596325640339-Evernote-MCP-Model-Context-Protocol",
          "evidence": "Evernote hosts an MCP server acting as a secure gateway with Read and Create capabilities, available to all paid users; updated August 2026."
        }
      ]
    },
    {
      "name": "Cloud API (EDAM)",
      "technology": "Thrift-based RPC over HTTPS (NoteStore, UserStore), OAuth",
      "channel": "Programmatic",
      "classification_rationale": "The consumer explicitly invokes provider-defined operations against the Evernote web service through structured RPC calls. Operation Invocation.",
      "provenance": [
        {
          "url": "https://dev.evernote.com/documentation/",
          "evidence": "The Cloud API speaks directly to the Evernote web service to act on a single user's account; new key issuance is gated behind manual review."
        },
        {
          "url": "https://dev.evernote.com/doc/",
          "evidence": "API Reference generated from Evernote source describes the core API types and functions."
        }
      ]
    },
    {
      "name": "Local API",
      "technology": "Command lines (Windows), AppleScript (Mac), Intents (Android)",
      "channel": "Programmatic",
      "classification_rationale": "Provider-defined operations on the local client invoked through structured commands, with a different base and auth model than the Cloud API. Operation Invocation.",
      "provenance": [
        {
          "url": "https://dev.evernote.com/documentation/local/",
          "evidence": "Calls the local clients using command lines on Windows, AppleScript on Mac, and Intents on Android, with security handled by the local application."
        }
      ]
    },
    {
      "name": "Email-to-Evernote",
      "technology": "Inbound email to a unique @m.evernote.com address",
      "channel": "Programmatic",
      "classification_rationale": "The consumer submits a structured message to a provider-defined address to invoke note creation, with subject-line commands directing notebook, tags, and reminders. Operation Invocation, analogous to SMTP submission.",
      "provenance": [
        {
          "url": "https://help.evernote.com/hc/en-us/articles/209005347-Save-emails-into-Evernote",
          "evidence": "Forwarding an email to the unique Evernote address creates a note; subject-line commands specify notebook, tags, and reminders."
        },
        {
          "url": "https://help.evernote.com/hc/en-us/articles/360050995914-Find-your-Evernote-email-address",
          "evidence": "Each account has an automatically generated unique incoming email address."
        }
      ]
    },
    {
      "name": "Webhooks",
      "technology": "HTTP callbacks to a consumer-controlled URL",
      "channel": "Event",
      "classification_rationale": "The service initiates a call to a consumer-controlled URL when subscribed note events occur, filtered by a note filter. Event Notification.",
      "provenance": [
        {
          "url": "https://dev.evernote.com/support/faq.php",
          "evidence": "A webhook is registered with the customer key, target URL, and a note filter; the service then calls that URL on matching note events."
        }
      ]
    }
  ],
  "access_mechanism_ledger": [
    {
      "mechanism": "Web app",
      "disposition": "interface",
      "detail": "Evernote GUI clients (Interactive)"
    },
    {
      "mechanism": "Desktop app (Windows, macOS)",
      "disposition": "interface",
      "detail": "Evernote GUI clients (Interactive)"
    },
    {
      "mechanism": "Mobile app (iOS, Android)",
      "disposition": "interface",
      "detail": "Evernote GUI clients (Interactive)"
    },
    {
      "mechanism": "Web Clipper (browser extension)",
      "disposition": "interface",
      "detail": "Web Clipper (Interactive)"
    },
    {
      "mechanism": "AI Assistant (chat)",
      "disposition": "interface",
      "detail": "AI Assistant (Conversational)"
    },
    {
      "mechanism": "MCP server",
      "disposition": "interface",
      "detail": "Evernote MCP server (Agentic)"
    },
    {
      "mechanism": "Cloud API",
      "disposition": "interface",
      "detail": "Cloud API (Programmatic)"
    },
    {
      "mechanism": "Local API",
      "disposition": "interface",
      "detail": "Local API (Programmatic)"
    },
    {
      "mechanism": "Email-to-Evernote",
      "disposition": "interface",
      "detail": "Email-to-Evernote (Programmatic)"
    },
    {
      "mechanism": "Webhooks",
      "disposition": "interface",
      "detail": "Webhooks (Event)"
    },
    {
      "mechanism": "CLI",
      "disposition": "excluded",
      "detail": "No first-party command-line client documented."
    },
    {
      "mechanism": "TUI",
      "disposition": "excluded",
      "detail": "No first-party TUI; no CLI to carry one."
    },
    {
      "mechanism": "Terminal client",
      "disposition": "excluded",
      "detail": "No terminal client shipped."
    },
    {
      "mechanism": "GraphQL API",
      "disposition": "excluded",
      "detail": "No official evidence; the public API is Thrift-based (EDAM)."
    },
    {
      "mechanism": "SDKs (iOS, Android, Python, Java, and others)",
      "disposition": "excluded",
      "detail": "Client libraries that implement the Cloud API, not interfaces."
    },
    {
      "mechanism": "Semantic Search, AI Meeting Notes",
      "disposition": "excluded",
      "detail": "Features inside the GUI and AI Assistant, not separate access interfaces."
    },
    {
      "mechanism": "Third-party integrations (Zapier, Pipedream, and similar)",
      "disposition": "excluded",
      "detail": "Built on the Cloud API; not provider-defined interfaces."
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
