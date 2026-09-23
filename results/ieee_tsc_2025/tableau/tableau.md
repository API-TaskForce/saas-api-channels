## SaaS summary

**SaaS:** Tableau (analytics and business intelligence platform, Salesforce). Resolved to the official domains `tableau.com` and `help.tableau.com`, with the developer platform documented at `tableau.com/developer` and the API references under `help.tableau.com/current/api/`.

**Identified logical interfaces:** 12.
**Distinct channels with at least one classified interface:** 5.

## Interface classification table

| Interface                                                               | Channel        | Interaction technology     | Provenance                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| ----------------------------------------------------------------------- | -------------- | -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Tableau web application (Tableau Cloud / Tableau Server browser client) | Interactive    | Web UI                     | `help.tableau.com/.../dev_resources.htm` and the Tableau Agent help confirm a browser authoring and consumption environment where users act on workbooks, dashboards, and projects. Actions are expressed by manipulating presented affordances (views, shelves, menus, filters) of a persistent navigable representation of service state, which is Affordance Manipulation. Current.                                                      |
| Tableau Desktop                                                         | Interactive    | Desktop GUI                | The Tableau Agent FAQ (`.../web_author_einstein_faq.htm`) documents Tableau Agent inside Tableau Desktop, establishing Desktop as a first-party authoring client. A drag-and-drop viz-authoring canvas is Affordance Manipulation. Current.                                                                                                                                                                                                 |
| Tableau Prep Builder                                                    | Interactive    | Desktop GUI                | The Tableau Agent FAQ documents Tableau Agent in Tableau Prep. Prep Builder ships a distinct flow-authoring canvas whose interaction contract differs from Desktop's viz canvas, so it is counted separately, still Affordance Manipulation. Current.                                                                                                                                                                                       |
| Tableau Mobile                                                          | Interactive    | Mobile app                 | The Pulse documentation (`.../pulse_intro.htm`) states Pulse runs on web and mobile, and the extensibility guide references the Tableau Mobile client through Mobile App Bootstrap. A first-party mobile client acting on navigable content is Affordance Manipulation. Current.                                                                                                                                                            |
| Tableau REST API                                                        | Programmatic   | REST over HTTP             | The REST API reference (`.../REST/rest_api_ref.htm`) documents management of sites, users, workbooks, data sources, and flows through structured HTTP requests to provider-defined endpoints, which is Operation Invocation. Current.                                                                                                                                                                                                       |
| VizQL Data Service (VDS) API                                            | Programmatic   | REST over HTTP             | The VDS reference (`.../api/vizql-data-service/en-us/`) provides programmatic querying of published data sources through a structured query payload, a distinct base and contract from the management REST API. It is explicit Operation Invocation. Being marketed for AI agents does not change the paradigm, since consumer type never determines channel. Current.                                                                      |
| Metadata API                                                            | Programmatic   | GraphQL over HTTP          | The Metadata API introduction (`.../api/metadata_api/en-us/`) exposes a GraphQL schema for querying content and lineage. GraphQL query submission against a fixed schema is explicit structured invocation, so Programmatic, not Agentic. Current.                                                                                                                                                                                          |
| tabcmd command-line utility                                             | Programmatic   | CLI                        | The Salesforce developer-platform module lists tabcmd among automation tools. A command-based CLI issuing structured commands to the server is Operation Invocation. Current.                                                                                                                                                                                                                                                               |
| Tableau Services Manager (TSM) administrative interface                 | Programmatic   | CLI and REST API           | The developer-platform module lists TSM for server administration. Its command-line and REST surfaces share one administrative contract distinct from the content REST API, and both express structured invocation, so Programmatic. (TSM also ships a browser admin console, an additional Interactive surface already covered by the Interactive channel.) Applies to Tableau Server. Current.                                            |
| Tableau Webhooks                                                        | Event          | HTTP callbacks             | The Webhooks docs (`.../developer/webhooks/en-us/`) show the service sending an HTTP POST to a consumer-specified destination URL when a subscribed event (for example an extract-refresh failure or workbook creation) occurs. Service-initiated delivery to a consumer-controlled receiver is Event Notification. Current.                                                                                                                |
| Tableau MCP server                                                      | Agentic        | Model Context Protocol     | The official Tableau MCP project (`tableau.github.io/tableau-mcp`) exposes semantically described tools, resources, and prompts that an AI consumer discovers and selects as part of the interaction contract. Under the MCP boundary rule, capability discovery and selection make this Agentic rather than Programmatic. Current, recent.                                                                                                 |
| Tableau Agent / Tableau Pulse natural-language Q&A                      | Conversational | Natural-language assistant | The Tableau Agent pages and Pulse Ask and Discover docs (`.../web_author_einstein.htm`, `.../pulse_ask_discover_qa.htm`) describe a conversational assistant where users express intent through natural-language messages that the service interprets to build vizzes, calculations, and insights. The primitive is the message and tool orchestration is internal, so Conversational. Current, with premium tiers in general availability. |

## Coverage ledger table

| Access mechanism                              | Disposition                                                                                                                                                 |
| --------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Web browser client (Cloud / Server)           | Interface: Tableau web application                                                                                                                          |
| Desktop client                                | Interfaces: Tableau Desktop; Tableau Prep Builder                                                                                                           |
| Mobile client                                 | Interface: Tableau Mobile                                                                                                                                   |
| Terminal / CLI                                | Interfaces: tabcmd; TSM (CLI portion)                                                                                                                       |
| TUI dashboard                                 | Excluded: no persistent navigable text UI is documented for tabcmd or TSM; their prompts are command arguments, not a TUI.                                  |
| REST API                                      | Interface: Tableau REST API                                                                                                                                 |
| VizQL Data Service                            | Interface: VDS API                                                                                                                                          |
| Metadata API (GraphQL)                        | Interface: Metadata API                                                                                                                                     |
| Pulse API                                     | Excluded: subsumed into the Tableau REST API (same base and auth).                                                                                          |
| TSM (Services Manager)                        | Interface: TSM administrative interface (Programmatic); its browser admin console is an Interactive surface already represented by the Interactive channel. |
| Webhooks / events                             | Interface: Tableau Webhooks                                                                                                                                 |
| Conversational / AI assistant                 | Interface: Tableau Agent / Pulse Q&A                                                                                                                        |
| MCP / agent protocol                          | Interface: Tableau MCP server                                                                                                                               |
| Email subscriptions (scheduled delivery)      | Excluded: an end-user notification feature delivering to inboxes on a schedule, not a developer-consumer-controlled event receiver.                         |
| SMTP / relay                                  | Excluded: no inbound SMTP submission interface is documented.                                                                                               |
| Embedding API (JavaScript API)                | Excluded: a client library that embeds and controls the existing Interactive web viz within a host page, not a distinct provider interaction contract.      |
| Dashboard Extensions API / Viz Extensions API | Excluded: an extensibility SDK for building add-ons that run inside Tableau, not an external access mechanism.                                              |
| Analytics Extensions API                      | Excluded: outbound integration in which Tableau calls external analytics services, not a way to access Tableau.                                             |
| TabPy                                         | Excluded: an external analytics service Tableau invokes, not a Tableau access interface.                                                                    |
| Hyper API                                     | Excluded: a client library for creating and editing local `.hyper` extract files, not a service access interface.                                           |
| Connector SDK / Web Data Connector SDK        | Excluded: SDKs for building data connectors.                                                                                                                |
| Tableau Server Client (TSC)                   | Excluded: a Python client library wrapping the REST API.                                                                                                    |
| Mobile App Bootstrap                          | Excluded: an open-source sample app, not a provider interface.                                                                                              |
| Connected Apps (direct trust / OAuth)         | Excluded: an authentication and authorization mechanism.                                                                                                    |
| Postman Collection                            | Excluded: a request collection for the REST API, not an interface.                                                                                          |
| Tableau Exchange (integrations index)         | Excluded: a third-party marketplace, not a provider interface.                                                                                              |
| Tableau Public                                | Excluded: a variant offering that exposes the same web and desktop interfaces already classified.                                                           |

## Channel coverage table

| Channel        | Evidence |
| -------------- | -------- |
| Interactive    | Observed |
| Agentic        | Observed |
| Conversational | Observed |
| Event          | Observed |
| Programmatic   | Observed |

## Multichannel verdict

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
  "generated_at": "2026-09-23T00:00:00Z",
  "evidence_checked_at": "2026-09-23T00:00:00Z",
  "saas": {
    "name": "Tableau"
  },
  "interfaces": [
    {
      "name": "Tableau web application (Cloud / Server browser client)",
      "technology": "Web UI",
      "channel": "Interactive",
      "classification_rationale": "Actions are expressed by manipulating presented affordances (views, shelves, menus, filters) of a persistent, navigable representation of workbooks, dashboards, and projects.",
      "provenance": [
        {
          "url": "https://help.tableau.com/current/online/en-us/dev_resources.htm",
          "evidence": "Developer resources overview confirming the browser-based Tableau Cloud/Server environment."
        },
        {
          "url": "https://help.tableau.com/current/online/en-us/web_author_einstein_faq.htm",
          "evidence": "References Tableau Cloud and Server web authoring as an interactive environment."
        }
      ]
    },
    {
      "name": "Tableau Desktop",
      "technology": "Desktop GUI",
      "channel": "Interactive",
      "classification_rationale": "A first-party desktop viz-authoring client whose drag-and-drop canvas is a navigable representation acted on through affordance manipulation.",
      "provenance": [
        {
          "url": "https://help.tableau.com/current/online/en-us/web_author_einstein_faq.htm",
          "evidence": "Documents Tableau Agent inside Tableau Desktop, establishing Desktop as a first-party client."
        }
      ]
    },
    {
      "name": "Tableau Prep Builder",
      "technology": "Desktop GUI",
      "channel": "Interactive",
      "classification_rationale": "A first-party desktop flow-authoring client with a distinct canvas contract from Desktop, still acted on through affordance manipulation.",
      "provenance": [
        {
          "url": "https://help.tableau.com/current/online/en-us/web_author_einstein_faq.htm",
          "evidence": "References Tableau Agent in Tableau Prep, establishing Prep Builder as a distinct authoring surface."
        }
      ]
    },
    {
      "name": "Tableau Mobile",
      "technology": "Mobile app",
      "channel": "Interactive",
      "classification_rationale": "A first-party mobile client for consuming and navigating content, which is affordance manipulation of service state.",
      "provenance": [
        {
          "url": "https://help.tableau.com/current/online/en-us/pulse_intro.htm",
          "evidence": "States Pulse is available on web and mobile."
        },
        {
          "url": "https://help.tableau.com/current/blueprint/en-us/bp_extensibility.htm",
          "evidence": "References the Tableau Mobile client via Mobile App Bootstrap."
        }
      ]
    },
    {
      "name": "Tableau REST API",
      "technology": "REST over HTTP",
      "channel": "Programmatic",
      "classification_rationale": "The consumer explicitly invokes provider-defined endpoints for sites, users, workbooks, data sources, and flows through structured HTTP requests.",
      "provenance": [
        {
          "url": "https://help.tableau.com/current/api/rest_api/en-us/REST/rest_api_ref.htm",
          "evidence": "Full endpoint reference for managing Tableau resources programmatically over HTTP."
        }
      ]
    },
    {
      "name": "VizQL Data Service (VDS) API",
      "technology": "REST over HTTP",
      "channel": "Programmatic",
      "classification_rationale": "Programmatic querying of published data sources through a structured query payload; explicit operation invocation on a distinct base from the management REST API. AI-agent framing does not change the paradigm.",
      "provenance": [
        {
          "url": "https://help.tableau.com/current/api/vizql-data-service/en-us/index.html",
          "evidence": "Documents programmatic query access to published data sources (headless BI)."
        }
      ]
    },
    {
      "name": "Metadata API",
      "technology": "GraphQL over HTTP",
      "channel": "Programmatic",
      "classification_rationale": "GraphQL queries submitted against a fixed metadata schema are explicit structured invocation, not capability discovery as a contract.",
      "provenance": [
        {
          "url": "https://help.tableau.com/current/api/metadata_api/en-us/index.html",
          "evidence": "Documents a GraphQL API for querying content metadata and lineage."
        }
      ]
    },
    {
      "name": "tabcmd command-line utility",
      "technology": "CLI",
      "channel": "Programmatic",
      "classification_rationale": "A command-based CLI issuing structured commands to the server, which is operation invocation.",
      "provenance": [
        {
          "url": "https://trailhead.salesforce.com/content/learn/modules/tableau-developer-platform/get-started-with-the-tableau-developer-platform",
          "evidence": "Official platform module lists tabcmd among automation and integration tools."
        }
      ]
    },
    {
      "name": "Tableau Services Manager (TSM) administrative interface",
      "technology": "CLI and REST API",
      "channel": "Programmatic",
      "classification_rationale": "Server administration via structured commands and requests over a base and auth distinct from the content REST API; both surfaces are operation invocation. Its browser admin console is a separate Interactive surface already covered by the Interactive channel.",
      "provenance": [
        {
          "url": "https://trailhead.salesforce.com/content/learn/modules/tableau-developer-platform/get-started-with-the-tableau-developer-platform",
          "evidence": "Official platform module lists TSM among automation and integration tooling for Tableau Server."
        }
      ]
    },
    {
      "name": "Tableau Webhooks",
      "technology": "HTTP callbacks",
      "channel": "Event",
      "classification_rationale": "The service initiates an HTTP POST to a consumer-specified destination URL when a subscribed event occurs, which is event notification to a consumer-controlled receiver.",
      "provenance": [
        {
          "url": "https://help.tableau.com/current/developer/webhooks/en-us/docs/webhooks-get-started.html",
          "evidence": "Describes event-triggered HTTP POST with JSON payload to a configured destination URL."
        }
      ]
    },
    {
      "name": "Tableau MCP server",
      "technology": "Model Context Protocol",
      "channel": "Agentic",
      "classification_rationale": "Exposes semantically described tools, resources, and prompts that the consumer discovers and selects as part of the interaction contract, which is the defining feature of the Agentic paradigm under the MCP boundary rule.",
      "provenance": [
        {
          "url": "https://tableau.github.io/tableau-mcp/docs/intro",
          "evidence": "Official Tableau MCP project exposing discoverable tools over VDS, Metadata, and Pulse APIs for AI applications."
        }
      ]
    },
    {
      "name": "Tableau Agent / Tableau Pulse natural-language Q&A",
      "technology": "Natural-language assistant",
      "channel": "Conversational",
      "classification_rationale": "The consumer expresses intent through natural-language messages the service interprets to build vizzes, calculations, and insights, with tool orchestration internal to the service.",
      "provenance": [
        {
          "url": "https://help.tableau.com/current/online/en-us/web_author_einstein.htm",
          "evidence": "Describes typing natural-language questions to a conversational assistant that creates and iterates on vizzes."
        },
        {
          "url": "https://help.tableau.com/current/online/en-us/pulse_ask_discover_qa.htm",
          "evidence": "Documents asking questions in natural language in Pulse to explore metrics."
        }
      ]
    }
  ],
  "access_mechanism_ledger": [
    {
      "mechanism": "Web browser client (Cloud / Server)",
      "disposition": "interface",
      "detail": "Tableau web application"
    },
    {
      "mechanism": "Desktop client",
      "disposition": "interface",
      "detail": "Tableau Desktop; Tableau Prep Builder"
    },
    {
      "mechanism": "Mobile client",
      "disposition": "interface",
      "detail": "Tableau Mobile"
    },
    {
      "mechanism": "Terminal / CLI",
      "disposition": "interface",
      "detail": "tabcmd; TSM (CLI portion)"
    },
    {
      "mechanism": "TUI dashboard",
      "disposition": "excluded",
      "detail": "No persistent navigable text UI documented; CLI prompts are command arguments, not a TUI."
    },
    {
      "mechanism": "REST API",
      "disposition": "interface",
      "detail": "Tableau REST API"
    },
    {
      "mechanism": "VizQL Data Service",
      "disposition": "interface",
      "detail": "VDS API"
    },
    {
      "mechanism": "Metadata API (GraphQL)",
      "disposition": "interface",
      "detail": "Metadata API"
    },
    {
      "mechanism": "Pulse API",
      "disposition": "excluded",
      "detail": "Subsumed into the Tableau REST API (same base and auth)."
    },
    {
      "mechanism": "Tableau Services Manager (TSM)",
      "disposition": "interface",
      "detail": "TSM administrative interface; its admin console is an Interactive surface already covered by the Interactive channel."
    },
    {
      "mechanism": "Webhooks / events",
      "disposition": "interface",
      "detail": "Tableau Webhooks"
    },
    {
      "mechanism": "Conversational / AI assistant",
      "disposition": "interface",
      "detail": "Tableau Agent / Pulse Q&A"
    },
    {
      "mechanism": "MCP / agent protocol",
      "disposition": "interface",
      "detail": "Tableau MCP server"
    },
    {
      "mechanism": "Email subscriptions (scheduled delivery)",
      "disposition": "excluded",
      "detail": "End-user notification feature delivering to inboxes on a schedule, not a consumer-controlled event receiver."
    },
    {
      "mechanism": "SMTP / relay",
      "disposition": "excluded",
      "detail": "No inbound SMTP submission interface documented."
    },
    {
      "mechanism": "Embedding API (JavaScript API)",
      "disposition": "excluded",
      "detail": "Client library that embeds and controls the existing Interactive web viz, not a distinct provider contract."
    },
    {
      "mechanism": "Dashboard Extensions API / Viz Extensions API",
      "disposition": "excluded",
      "detail": "Extensibility SDK for add-ons running inside Tableau, not an external access mechanism."
    },
    {
      "mechanism": "Analytics Extensions API",
      "disposition": "excluded",
      "detail": "Outbound integration in which Tableau calls external analytics services."
    },
    {
      "mechanism": "TabPy",
      "disposition": "excluded",
      "detail": "External analytics service Tableau invokes, not a Tableau access interface."
    },
    {
      "mechanism": "Hyper API",
      "disposition": "excluded",
      "detail": "Client library for local .hyper extract files, not a service access interface."
    },
    {
      "mechanism": "Connector SDK / Web Data Connector SDK",
      "disposition": "excluded",
      "detail": "SDKs for building data connectors."
    },
    {
      "mechanism": "Tableau Server Client (TSC)",
      "disposition": "excluded",
      "detail": "Python client library wrapping the REST API."
    },
    {
      "mechanism": "Mobile App Bootstrap",
      "disposition": "excluded",
      "detail": "Open-source sample app, not a provider interface."
    },
    {
      "mechanism": "Connected Apps (direct trust / OAuth)",
      "disposition": "excluded",
      "detail": "Authentication and authorization mechanism."
    },
    {
      "mechanism": "Postman Collection",
      "disposition": "excluded",
      "detail": "Request collection for the REST API, not an interface."
    },
    {
      "mechanism": "Tableau Exchange (integrations index)",
      "disposition": "excluded",
      "detail": "Third-party marketplace, not a provider interface."
    },
    {
      "mechanism": "Tableau Public",
      "disposition": "excluded",
      "detail": "Variant offering exposing the same web and desktop interfaces already classified."
    }
  ],
  "channel_evidence": {
    "Interactive": "observed",
    "Agentic": "observed",
    "Conversational": "observed",
    "Event": "observed",
    "Programmatic": "observed"
  },
  "number_of_interfaces": 12,
  "multi_interface": true,
  "number_of_channels": 5,
  "multi_channel": true
}
```
