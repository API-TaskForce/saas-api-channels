## SaaS summary

Provider resolved as Atlassian. "Jira" is scoped here to the core Jira Cloud work-management and software product (the unified "Jira", formerly Jira Software plus Jira Work Management). Jira Service Management, Jira Product Discovery, and Jira Align are separate products in the Jira family and are treated as out of scope, with their product-specific surfaces disposed of in the coverage ledger. Official documentation was taken from developer.atlassian.com, support.atlassian.com, and atlassian.com.

Identified logical interfaces: 9. Distinct channels with at least one classified interface: 5.

## Interface classification table

| Interface                       | Channel        | Interaction technology                               | Provenance                                                                                                                                                                                                                                                                                                                                                                                                                    |
| ------------------------------- | -------------- | ---------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Jira web application            | Interactive    | Web UI (browser)                                     | Atlassian's mobile guide contrasts the web surface with mobile, noting the web is where advanced configuration and admin setup happen (atlassian.com/software/jira/guides/mobile-apps/overview). Actions are expressed by manipulating boards, forms, and menus of a persistent navigable representation, so the primitive is affordance manipulation. Current.                                                               |
| Jira mobile app                 | Interactive    | Native iOS and Android clients                       | Atlassian ships first-party iOS and Android apps giving access to boards, backlogs, forms, and approvals (atlassian.com/software/jira/mobile-app; .../guides/mobile-apps/overview). The consumer manipulates presented views and controls of service state, a distinct client surface from web but the same affordance-manipulation primitive. Current.                                                                       |
| Jira Cloud platform REST API    | Programmatic   | REST over HTTP (JSON, API v3)                        | The REST intro states the API lets you interact with Jira programmatically using standard HTTP verbs (developer.atlassian.com/cloud/jira/platform/rest/v3/intro). The consumer explicitly invokes provider-defined operations through structured requests, which is operation invocation. Current, v3 latest.                                                                                                                 |
| Atlassian GraphQL API (Gateway) | Programmatic   | GraphQL over HTTP                                    | The Atlassian platform GraphQL API exposes Jira data such as projects and Jira fields through the GraphQL Gateway, with a distinct endpoint and query primitive from REST (developer.atlassian.com/platform/atlassian-graphql-api/graphql). Separately exposed query and mutation invocation, so a second Programmatic interface. Current.                                                                                    |
| Atlassian CLI (ACLI)            | Programmatic   | Command-line binary (`acli jira`)                    | The official command reference documents `acli jira` subcommands for work items, boards, sprints, filters, and projects, including create, edit, transition, and search (developer.atlassian.com/cloud/acli/reference/commands/jira). Structured commands invoke provider-defined operations, so operation invocation. Current.                                                                                               |
| Incoming email (mail handler)   | Programmatic   | POP, IMAP, or Microsoft Graph mailbox processing     | Jira can be configured to create issues and add comments from inbound email through a mail handler that maps a submitted message to a defined operation (support.atlassian.com/jira-cloud-administration/docs/create-issues-and-comments-from-email). A submitted message invoking a fixed provider-defined operation resembles SMTP submission, so operation invocation rather than conversation. Current.                   |
| Webhooks                        | Event          | User-defined HTTP POST callbacks                     | Jira webhooks are user-defined callbacks that notify a remote endpoint when events occur, removing the need to poll (developer.atlassian.com/server/jira/platform/webhooks; developer.atlassian.com/cloud/jira/platform/integrate-jira-issues-with-your-application). The service initiates the interaction on subscribed events and delivers to a consumer-controlled receiver, which is event notification. Current.        |
| Rovo conversational assistant   | Conversational | Rovo Chat in-product, plus first-party chat surfaces | Rovo Chat is reached from the product top navigation and answers natural-language questions, and Rovo in Jira can create and update work items from chat (support.atlassian.com/rovo/kb/rovo-capabilities-and-features-for-atlassian-cloud; atlassian.com/software/jira/ai). The primitive is the natural-language message interpreted by the service, with tool orchestration internal, so contextual conversation. Current. |
| Atlassian Rovo MCP Server       | Agentic        | Remote MCP endpoint (mcp.atlassian.com)              | The MCP overview describes a server that advertises a small primary tool set and lets clients discover the rest of the catalog on demand through a discover tool (developer.atlassian.com/cloud/rovo-mcp; support.atlassian.com/atlassian-rovo-mcp-server). Capability discovery and selection are part of the interaction contract, which the decision tree resolves to Agentic rather than Programmatic. Current.           |

## Coverage ledger table

| Access mechanism                                                                     | Disposition                                                                                                                                                                                                                 |
| ------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Web client (first-party, web surface)                                                | Jira web application (Interactive)                                                                                                                                                                                          |
| Mobile client (first-party, mobile surface)                                          | Jira mobile app (Interactive)                                                                                                                                                                                               |
| Desktop client (first-party, desktop surface)                                        | Excluded: no current first-party desktop client. Atlassian's Jira for Mac shipped in 2019 and was retired in February 2022; no Windows client exists, and the feature request JRACLOUD-78044 remains at Gathering Interest. |
| CLI (first-party, terminal surface)                                                  | Atlassian CLI / ACLI (Programmatic)                                                                                                                                                                                         |
| CLI persistent TUI dashboard                                                         | Excluded: ACLI is command-based; no official persistent navigable TUI observed in the command reference.                                                                                                                    |
| REST API                                                                             | Jira Cloud platform REST API (Programmatic)                                                                                                                                                                                 |
| GraphQL API                                                                          | Atlassian GraphQL API (Programmatic)                                                                                                                                                                                        |
| Webhooks / events                                                                    | Webhooks (Event)                                                                                                                                                                                                            |
| Incoming email / mail handler                                                        | Incoming email (Programmatic)                                                                                                                                                                                               |
| Conversational / AI assistant (Rovo Chat)                                            | Rovo conversational assistant (Conversational)                                                                                                                                                                              |
| First-party chat integrations (@Jira in Teams and Slack)                             | Rovo conversational assistant (Conversational): the natural-language message primitive is the same paradigm surfaced in a chat host, not a separate contract.                                                               |
| MCP / agent protocol (Rovo MCP Server)                                               | Atlassian Rovo MCP Server (Agentic)                                                                                                                                                                                         |
| Atlassian Agent2Agent (A2A) Gateway                                                  | Excluded: cross-product Rovo platform gateway for external agents to delegate goals, not a core-Jira-specific interface; if counted its paradigm would be Agentic, already represented by the MCP server.                   |
| Connect and Forge app frameworks                                                     | Excluded: app-development and extension frameworks that consume the REST and GraphQL APIs; not access interfaces in their own right.                                                                                        |
| SDKs and client libraries (for example atlassian-python-api, Jira REST Java Client)  | Excluded: wrappers over the REST API, not interfaces.                                                                                                                                                                       |
| JQL                                                                                  | Excluded: a query language used within other interfaces, not a standalone access mechanism.                                                                                                                                 |
| Jira Service Management portal and email channel, Jira Product Discovery, Jira Align | Excluded: separate products in the Jira family, out of scope for core Jira.                                                                                                                                                 |

## Channel coverage table

| Channel        | Evidence |
| -------------- | -------- |
| Interactive    | Observed |
| Agentic        | Observed |
| Conversational | Observed |
| Event          | Observed |
| Programmatic   | Observed |

## Classification notes

The incoming-email interface was placed in Programmatic rather than Conversational because the mail handler maps a submitted message to a fixed, provider-defined operation (create issue or add comment) rather than interpreting free natural language into arbitrary actions. The Rovo MCP Server was placed in Agentic rather than Programmatic under the MCP boundary rule, since capability discovery and selection form part of its contract. The first-party Teams and Slack chat integrations were folded into the Conversational interface rather than counted separately, because they share the natural-language-message primitive and control structure.

## Multichannel verdict

Multichannel (5 distinct paradigms).

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
    "name": "Jira"
  },
  "interfaces": [
    {
      "name": "Jira web application",
      "technology": "Web UI (browser)",
      "channel": "Interactive",
      "classification_rationale": "Actions are expressed by manipulating boards, forms, menus, and views of a persistent navigable representation of service state, which is affordance manipulation.",
      "provenance": [
        {
          "url": "https://www.atlassian.com/software/jira/guides/mobile-apps/overview",
          "evidence": "Distinguishes the Jira web surface as the place for advanced configuration and admin setup, confirming a first-party web client."
        }
      ]
    },
    {
      "name": "Jira mobile app",
      "technology": "Native iOS and Android clients",
      "channel": "Interactive",
      "classification_rationale": "A first-party mobile client where the consumer manipulates presented views and controls; a distinct surface from web but the same affordance-manipulation primitive.",
      "provenance": [
        {
          "url": "https://www.atlassian.com/software/jira/mobile-app",
          "evidence": "Official iOS and Android app for accessing projects, boards, and updates."
        },
        {
          "url": "https://www.atlassian.com/software/jira/guides/mobile-apps/overview",
          "evidence": "Describes mobile access to boards, backlogs, approvals, and forms."
        }
      ]
    },
    {
      "name": "Jira Cloud platform REST API",
      "technology": "REST over HTTP (JSON, API v3)",
      "channel": "Programmatic",
      "classification_rationale": "The consumer explicitly invokes provider-defined operations through structured HTTP requests, which is operation invocation.",
      "provenance": [
        {
          "url": "https://developer.atlassian.com/cloud/jira/platform/rest/v3/intro/",
          "evidence": "States the REST API lets you interact with Jira programmatically using standard HTTP methods."
        }
      ]
    },
    {
      "name": "Atlassian GraphQL API (Gateway)",
      "technology": "GraphQL over HTTP",
      "channel": "Programmatic",
      "classification_rationale": "Separately exposed query and mutation invocation over a distinct endpoint and primitive from REST; still explicit operation invocation.",
      "provenance": [
        {
          "url": "https://developer.atlassian.com/platform/atlassian-graphql-api/graphql/",
          "evidence": "Exposes Jira data such as projects and Jira fields through the Atlassian GraphQL Gateway."
        }
      ]
    },
    {
      "name": "Atlassian CLI (ACLI)",
      "technology": "Command-line binary (acli jira)",
      "channel": "Programmatic",
      "classification_rationale": "Structured terminal commands invoke provider-defined operations on work items, boards, and sprints, which is operation invocation.",
      "provenance": [
        {
          "url": "https://developer.atlassian.com/cloud/acli/reference/commands/jira/",
          "evidence": "Documents acli jira subcommands including workitem create, edit, transition, and search."
        }
      ]
    },
    {
      "name": "Incoming email (mail handler)",
      "technology": "POP, IMAP, or Microsoft Graph mailbox processing",
      "channel": "Programmatic",
      "classification_rationale": "A submitted email message maps to a fixed provider-defined operation (create issue or add comment), resembling SMTP submission rather than natural-language conversation.",
      "provenance": [
        {
          "url": "https://support.atlassian.com/jira-cloud-administration/docs/create-issues-and-comments-from-email/",
          "evidence": "Jira scans a configured mailbox and creates work items or comments from received email via a mail handler."
        }
      ]
    },
    {
      "name": "Webhooks",
      "technology": "User-defined HTTP POST callbacks",
      "channel": "Event",
      "classification_rationale": "The service initiates the interaction on subscribed events and delivers to a consumer-controlled receiver, which is event notification.",
      "provenance": [
        {
          "url": "https://developer.atlassian.com/server/jira/platform/webhooks/",
          "evidence": "Webhooks are user-defined callbacks that push notifications to a remote endpoint when Jira events occur."
        },
        {
          "url": "https://developer.atlassian.com/cloud/jira/platform/integrate-jira-issues-with-your-application",
          "evidence": "Lists REST APIs and webhooks as the Jira Cloud product integration mechanisms."
        }
      ]
    },
    {
      "name": "Rovo conversational assistant",
      "technology": "Rovo Chat in-product, plus first-party chat surfaces",
      "channel": "Conversational",
      "classification_rationale": "The primitive is the natural-language message interpreted by the service, with tool orchestration internal to the service, which is contextual conversation.",
      "provenance": [
        {
          "url": "https://support.atlassian.com/rovo/kb/rovo-capabilities-and-features-for-atlassian-cloud/",
          "evidence": "Rovo Chat is reached from the product top navigation and answers natural-language queries."
        },
        {
          "url": "https://www.atlassian.com/software/jira/ai",
          "evidence": "Rovo in Jira creates and updates work items from chat."
        }
      ]
    },
    {
      "name": "Atlassian Rovo MCP Server",
      "technology": "Remote MCP endpoint (mcp.atlassian.com)",
      "channel": "Agentic",
      "classification_rationale": "The server advertises primary tools and lets clients discover the rest of the catalog on demand, so capability discovery and selection are part of the contract, resolving to Agentic under the MCP boundary rule.",
      "provenance": [
        {
          "url": "https://developer.atlassian.com/cloud/rovo-mcp/",
          "evidence": "Describes discovery of the tool catalog on demand through a discover tool over an OAuth-authorized MCP endpoint."
        },
        {
          "url": "https://support.atlassian.com/atlassian-rovo-mcp-server/docs/getting-started-with-the-atlassian-remote-mcp-server/",
          "evidence": "Official remote MCP server through which AI clients select and run Jira actions with the user's permissions."
        }
      ]
    }
  ],
  "access_mechanism_ledger": [
    {
      "mechanism": "Web client (first-party, web surface)",
      "disposition": "interface",
      "detail": "Jira web application"
    },
    {
      "mechanism": "Mobile client (first-party, mobile surface)",
      "disposition": "interface",
      "detail": "Jira mobile app"
    },
    {
      "mechanism": "Desktop client (first-party, desktop surface)",
      "disposition": "excluded",
      "detail": "No current first-party desktop client; Jira for Mac was retired in Feb 2022 and no Windows client exists (JRACLOUD-78044 at Gathering Interest)."
    },
    {
      "mechanism": "CLI (first-party, terminal surface)",
      "disposition": "interface",
      "detail": "Atlassian CLI (ACLI)"
    },
    {
      "mechanism": "CLI persistent TUI dashboard",
      "disposition": "excluded",
      "detail": "ACLI is command-based; no official persistent navigable TUI observed."
    },
    {
      "mechanism": "REST API",
      "disposition": "interface",
      "detail": "Jira Cloud platform REST API"
    },
    {
      "mechanism": "GraphQL API",
      "disposition": "interface",
      "detail": "Atlassian GraphQL API (Gateway)"
    },
    {
      "mechanism": "Webhooks / events",
      "disposition": "interface",
      "detail": "Webhooks"
    },
    {
      "mechanism": "Incoming email / mail handler",
      "disposition": "interface",
      "detail": "Incoming email (mail handler)"
    },
    {
      "mechanism": "Conversational / AI assistant (Rovo Chat)",
      "disposition": "interface",
      "detail": "Rovo conversational assistant"
    },
    {
      "mechanism": "First-party chat integrations (@Jira in Teams and Slack)",
      "disposition": "interface",
      "detail": "Folded into Rovo conversational assistant (same natural-language-message paradigm)."
    },
    {
      "mechanism": "MCP / agent protocol (Rovo MCP Server)",
      "disposition": "interface",
      "detail": "Atlassian Rovo MCP Server"
    },
    {
      "mechanism": "Atlassian Agent2Agent (A2A) Gateway",
      "disposition": "excluded",
      "detail": "Cross-product Rovo platform gateway, not a core-Jira-specific interface; its paradigm (Agentic) is already represented by the MCP server."
    },
    {
      "mechanism": "Connect and Forge app frameworks",
      "disposition": "excluded",
      "detail": "App-development and extension frameworks that consume the REST and GraphQL APIs; not access interfaces themselves."
    },
    {
      "mechanism": "SDKs and client libraries",
      "disposition": "excluded",
      "detail": "Wrappers over the REST API, not interfaces."
    },
    {
      "mechanism": "JQL",
      "disposition": "excluded",
      "detail": "A query language used within other interfaces, not a standalone access mechanism."
    },
    {
      "mechanism": "JSM portal and email channel, Jira Product Discovery, Jira Align",
      "disposition": "excluded",
      "detail": "Separate products in the Jira family, out of scope for core Jira."
    }
  ],
  "channel_evidence": {
    "Interactive": "observed",
    "Agentic": "observed",
    "Conversational": "observed",
    "Event": "observed",
    "Programmatic": "observed"
  },
  "number_of_interfaces": 9,
  "multi_interface": true,
  "number_of_channels": 5,
  "multi_channel": true
}
```
