# Interface classification table

| Interface                                            | Channel        | Interaction technology                                                                                | Provenance                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| ---------------------------------------------------- | -------------- | ----------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Microsoft 365 web client                             | Interactive    | Web apps at m365.cloud.microsoft / office.com (Word, Excel, PowerPoint, Outlook, OneDrive on the web) | microsoft.com product pages document free and subscription web versions of the apps. Actions are expressed by manipulating views, menus and forms of a navigable representation of documents and mailboxes, so decision-tree step 1 (Affordance Manipulation) resolves it as Interactive. Current/GA.                                                                                                                                                                         |
| Microsoft 365 desktop client                         | Interactive    | Windows and macOS desktop apps installed via Click-to-Run                                             | The Office applications service description confirms first-party desktop apps on Windows and Mac. Same Affordance-Manipulation paradigm on a distinct client surface. Current/GA.                                                                                                                                                                                                                                                                                             |
| Microsoft 365 mobile client                          | Interactive    | iOS and Android apps (unified Microsoft 365 app plus per-app clients)                                 | microsoft.com and support.microsoft.com document iOS/Android apps for Word, Excel, PowerPoint, Outlook, OneDrive. Distinct first-party mobile surface, same Interactive paradigm. Current/GA (stable builds dated 2026).                                                                                                                                                                                                                                                      |
| Microsoft Graph REST API                             | Programmatic   | REST/OData over HTTPS at graph.microsoft.com (v1.0 and beta)                                          | The Graph overview and API reference describe explicit invocation of provider-defined operations against resources such as `me`, `messages`, `drive`, `sites`. The consumer constructs and issues structured requests, matching Operation Invocation. Current/GA.                                                                                                                                                                                                             |
| Exchange Online administrative PowerShell            | Programmatic   | PowerShell cmdlets via the ExchangeOnlineManagement module (Connect-ExchangeOnline)                   | The Connect to Exchange Online PowerShell doc describes a command-based cmdlet interface with its own REST-backed connection, endpoint and auth, distinct from Graph. Explicit command invocation, so Programmatic. Current/GA.                                                                                                                                                                                                                                               |
| Internet mail protocols (SMTP submission, IMAP, POP) | Programmatic   | Authenticated SMTP client submission, IMAP4, POP3 with OAuth 2.0                                      | The authenticated client SMTP submission and IMAP/POP/SMTP OAuth docs confirm first-party protocol endpoints for sending and retrieving mail from Exchange Online mailboxes. Structured protocol operations against provider-defined endpoints, so Programmatic. Current (OAuth supported; basic auth retired).                                                                                                                                                               |
| Microsoft Graph change notifications                 | Event          | Subscriptions delivered via webhooks, Azure Event Hubs, or Azure Event Grid                           | The change-notifications docs describe the service initiating delivery to a consumer-controlled `notificationUrl` or event channel when a subscribed resource changes. The service pushes on events to a receiver the consumer controls, matching Event Notification. Current/GA.                                                                                                                                                                                             |
| Microsoft 365 Copilot                                | Conversational | In-app and standalone natural-language assistant                                                      | Product pages and the declarative-agent docs present Copilot as a natural-language assistant; the consumer expresses intent through messages and Copilot orchestrates tools, plugins and MCP internally. The primitive is the message, so Conversational (see the assistant-with-internal-tools boundary case). Current/GA.                                                                                                                                                   |
| Microsoft MCP Server for Enterprise                  | Agentic        | First-party MCP endpoint at mcp.svc.cloud.microsoft/enterprise exposing discoverable Graph tools      | The Graph MCP Server overview describes an MCP endpoint whose tools (`microsoft_graph_suggest_queries`, `microsoft_graph_get`, `microsoft_graph_list_properties`) are discovered and selected as part of the interaction contract (`tools/list`, `tools/call`). Capability discovery and selection are part of the contract, so Agentic (MCP boundary case), not Programmatic. **Preview**, currently scoped to Microsoft Entra identity/directory read-only data over Graph. |

# Coverage ledger table

| Access mechanism                                              | Disposition                                                                                                                                                                               |
| ------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Web app (office.com / m365.cloud.microsoft)                   | Interface: Microsoft 365 web client (Interactive)                                                                                                                                         |
| Desktop app (Windows/macOS Click-to-Run)                      | Interface: Microsoft 365 desktop client (Interactive)                                                                                                                                     |
| Mobile app (iOS/Android)                                      | Interface: Microsoft 365 mobile client (Interactive)                                                                                                                                      |
| Terminal / TUI surface                                        | Excluded: no first-party persistent navigable TUI. First-party terminal access is command-based only (PowerShell, mgc), already classified as Programmatic.                               |
| API / API reference (Microsoft Graph)                         | Interface: Microsoft Graph REST API (Programmatic)                                                                                                                                        |
| CLI (Exchange Online PowerShell and other M365 admin modules) | Interface: Exchange Online administrative PowerShell (Programmatic). Teams and SharePoint Online Management Shell share the cmdlet paradigm and are treated within this interface family. |
| SMTP / relay, IMAP, POP                                       | Interface: Internet mail protocols (Programmatic)                                                                                                                                         |
| Webhooks / events / change notifications                      | Interface: Microsoft Graph change notifications (Event)                                                                                                                                   |
| Conversational / chat / AI assistant                          | Interface: Microsoft 365 Copilot (Conversational)                                                                                                                                         |
| MCP / agent / protocol                                        | Interface: Microsoft MCP Server for Enterprise (Agentic)                                                                                                                                  |
| Microsoft Graph SDKs and Microsoft Graph PowerShell SDK       | Excluded: client libraries/SDKs and a wrapper over Graph REST; the "do not count" rule bars SDKs and wrappers.                                                                            |
| Microsoft Graph CLI (mgc)                                     | Excluded: first-party but a thin command wrapper over the Graph REST API, not a distinct interaction contract.                                                                            |
| CLI for Microsoft 365 (m365)                                  | Excluded: community/open-source project, not a provider-defined Microsoft interface.                                                                                                      |
| Graph Explorer                                                | Excluded: first-party developer testing tool that builds and issues Graph API requests; its operations are the Graph REST API's, not a separate service interface.                        |
| Third-party integrations index / connectors                   | Excluded: third-party integrations and Graph connectors ingest external data; they are not first-party access interfaces to the service.                                                  |

# Channel coverage table

| Channel        | Evidence |
| -------------- | -------- |
| Interactive    | Observed |
| Agentic        | Observed |
| Conversational | Observed |
| Event          | Observed |
| Programmatic   | Observed |

# Classification notes

The three Interactive entries follow the first-party client-surface checklist: web, desktop and mobile each ship a first-party client and are counted as separate Interactive interfaces on the same Affordance-Manipulation paradigm.

The Agentic classification rests on a preview interface. The Microsoft MCP Server for Enterprise is a genuine first-party MCP endpoint over the Graph platform, but at the evidence date its tools are limited to Microsoft Entra identity and directory read-only scenarios. It is included because it exposes M365 platform (Graph) capabilities through MCP capability discovery, which is the defining test for Agentic. A stricter analyst who scopes Microsoft 365 to the productivity suite alone, excluding the identity layer, could set this interface aside pending broader-scope GA; that choice would remove the only Agentic evidence and drop the count to four channels. The distinction is noted rather than hidden.

Copilot is Conversational rather than Agentic even though it invokes MCP tools and API plugins. Per the assistant-with-internal-tools boundary case, that orchestration is internal to the service and is not part of the consumer-facing contract, which is natural-language messaging. The MCP extensibility is the reverse direction from the Agentic interface above: Copilot acts as an MCP client consuming tools, whereas the Enterprise MCP Server acts as an MCP server exposing tools.

The internet mail protocols (SMTP submission, IMAP, POP) are grouped as one Programmatic interface family sharing the mail-protocol paradigm against Exchange Online mailboxes. A stricter split by protocol and port would yield more Programmatic entries without changing the channel or the multichannel verdict.

# Multichannel verdict

**Multichannel** (5 distinct paradigms observed).

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
  "saas": { "name": "Microsoft 365" },
  "interfaces": [
    {
      "name": "Microsoft 365 web client",
      "technology": "Web apps at m365.cloud.microsoft / office.com",
      "channel": "Interactive",
      "classification_rationale": "Actions are expressed by manipulating views, menus and forms of a navigable representation of documents and mailboxes (Affordance Manipulation).",
      "provenance": [
        {
          "url": "https://www.microsoft.com/en-us/microsoft-365/free-office-online-for-the-web",
          "evidence": "First-party web versions of Word, Excel, PowerPoint, Outlook, OneDrive."
        }
      ]
    },
    {
      "name": "Microsoft 365 desktop client",
      "technology": "Windows and macOS desktop apps (Click-to-Run)",
      "channel": "Interactive",
      "classification_rationale": "First-party desktop apps whose actions are affordance manipulation of a navigable UI; distinct client surface, same Interactive paradigm.",
      "provenance": [
        {
          "url": "https://learn.microsoft.com/en-us/office365/servicedescriptions/office-applications-service-description/office-applications-service-description",
          "evidence": "Office desktop apps installed on Windows and Mac via Click-to-Run."
        }
      ]
    },
    {
      "name": "Microsoft 365 mobile client",
      "technology": "iOS and Android apps",
      "channel": "Interactive",
      "classification_rationale": "First-party mobile apps; Affordance Manipulation on a distinct mobile surface.",
      "provenance": [
        {
          "url": "https://support.microsoft.com/en-us/office/foundations-experiences/microsoft-365-mobile-apps",
          "evidence": "iOS and Android versions of Word, Excel, PowerPoint, OneDrive, Outlook."
        }
      ]
    },
    {
      "name": "Microsoft Graph REST API",
      "technology": "REST/OData over HTTPS (graph.microsoft.com v1.0 and beta)",
      "channel": "Programmatic",
      "classification_rationale": "Consumer explicitly invokes provider-defined operations against resources via structured HTTP requests (Operation Invocation).",
      "provenance": [
        {
          "url": "https://learn.microsoft.com/en-us/graph/use-the-api",
          "evidence": "Structured {HTTP method} https://graph.microsoft.com/{version}/{resource} request pattern over M365 data."
        },
        {
          "url": "https://learn.microsoft.com/en-us/graph/overview",
          "evidence": "Microsoft Graph is the unified REST API for Microsoft 365 services."
        }
      ]
    },
    {
      "name": "Exchange Online administrative PowerShell",
      "technology": "PowerShell cmdlets via ExchangeOnlineManagement module",
      "channel": "Programmatic",
      "classification_rationale": "Explicit command invocation through cmdlets over a distinct Exchange endpoint and auth, separate primitive from Graph REST.",
      "provenance": [
        {
          "url": "https://learn.microsoft.com/en-us/powershell/exchange/connect-to-exchange-online-powershell?view=exchange-ps",
          "evidence": "First-party command-line cmdlet interface with its own REST-backed connection to Exchange Online."
        }
      ]
    },
    {
      "name": "Internet mail protocols (SMTP submission, IMAP, POP)",
      "technology": "Authenticated SMTP, IMAP4, POP3 with OAuth 2.0",
      "channel": "Programmatic",
      "classification_rationale": "Structured protocol operations to send and retrieve mail against provider-defined Exchange Online endpoints (Operation Invocation).",
      "provenance": [
        {
          "url": "https://learn.microsoft.com/en-us/exchange/clients-and-mobile-in-exchange-online/authenticated-client-smtp-submission",
          "evidence": "Authenticated SMTP client submission for Office 365 / Microsoft 365 mailboxes."
        },
        {
          "url": "https://learn.microsoft.com/en-us/exchange/client-developer/legacy-protocols/how-to-authenticate-an-imap-pop-smtp-application-by-using-oauth",
          "evidence": "OAuth support for IMAP, POP and SMTP for Microsoft 365 users."
        }
      ]
    },
    {
      "name": "Microsoft Graph change notifications",
      "technology": "Subscriptions delivered via webhooks, Azure Event Hubs, or Azure Event Grid",
      "channel": "Event",
      "classification_rationale": "The service initiates delivery to a consumer-controlled receiver when a subscribed resource changes (Event Notification), not consumer-invoked.",
      "provenance": [
        {
          "url": "https://learn.microsoft.com/en-us/graph/change-notifications-overview",
          "evidence": "Applications subscribe and receive service-initiated notifications via webhooks, Event Hubs, or Event Grid."
        },
        {
          "url": "https://learn.microsoft.com/en-us/graph/change-notifications-delivery-webhooks",
          "evidence": "Graph POSTs change notifications to the consumer's notificationUrl endpoint."
        }
      ]
    },
    {
      "name": "Microsoft 365 Copilot",
      "technology": "In-app and standalone natural-language assistant",
      "channel": "Conversational",
      "classification_rationale": "The consumer expresses intent through natural-language messages; tool, plugin and MCP orchestration is internal to the service (Contextual Conversation), matching the assistant-with-internal-tools boundary case.",
      "provenance": [
        {
          "url": "https://learn.microsoft.com/en-us/microsoft-365-copilot/extensibility/overview-api-plugins",
          "evidence": "Declarative agents let users ask in natural language; Copilot reasons over and invokes tools internally."
        },
        {
          "url": "https://www.microsoft.com/en-us/microsoft-365",
          "evidence": "Copilot presented as an AI assistant across the Microsoft 365 apps."
        }
      ]
    },
    {
      "name": "Microsoft MCP Server for Enterprise",
      "technology": "First-party MCP endpoint (mcp.svc.cloud.microsoft/enterprise), preview",
      "channel": "Agentic",
      "classification_rationale": "Exposes semantically described Graph tools that agents discover and select via tools/list and tools/call as part of the interaction contract (Capability Discovery and Invocation), the MCP boundary case for Agentic rather than Programmatic.",
      "provenance": [
        {
          "url": "https://learn.microsoft.com/en-us/graph/mcp-server/overview",
          "evidence": "First-party MCP endpoint exposing microsoft_graph_suggest_queries, microsoft_graph_get, microsoft_graph_list_properties for agent discovery and invocation. Preview; currently Entra identity read-only over Graph."
        }
      ]
    }
  ],
  "access_mechanism_ledger": [
    {
      "mechanism": "Web app (office.com / m365.cloud.microsoft)",
      "disposition": "interface",
      "detail": "Microsoft 365 web client (Interactive)"
    },
    {
      "mechanism": "Desktop app (Windows/macOS Click-to-Run)",
      "disposition": "interface",
      "detail": "Microsoft 365 desktop client (Interactive)"
    },
    {
      "mechanism": "Mobile app (iOS/Android)",
      "disposition": "interface",
      "detail": "Microsoft 365 mobile client (Interactive)"
    },
    {
      "mechanism": "Terminal / TUI surface",
      "disposition": "excluded",
      "detail": "No first-party persistent navigable TUI; terminal access is command-based only (already classified as Programmatic)."
    },
    {
      "mechanism": "API / API reference (Microsoft Graph)",
      "disposition": "interface",
      "detail": "Microsoft Graph REST API (Programmatic)"
    },
    {
      "mechanism": "CLI (Exchange Online and M365 admin PowerShell)",
      "disposition": "interface",
      "detail": "Exchange Online administrative PowerShell (Programmatic); Teams and SharePoint Online Management Shell share the cmdlet paradigm within this family."
    },
    {
      "mechanism": "SMTP / IMAP / POP",
      "disposition": "interface",
      "detail": "Internet mail protocols (Programmatic)"
    },
    {
      "mechanism": "Webhooks / change notifications",
      "disposition": "interface",
      "detail": "Microsoft Graph change notifications (Event)"
    },
    {
      "mechanism": "Conversational / AI assistant",
      "disposition": "interface",
      "detail": "Microsoft 365 Copilot (Conversational)"
    },
    {
      "mechanism": "MCP / agent / protocol",
      "disposition": "interface",
      "detail": "Microsoft MCP Server for Enterprise (Agentic)"
    },
    {
      "mechanism": "Microsoft Graph SDKs and Graph PowerShell SDK",
      "disposition": "excluded",
      "detail": "SDKs/client libraries and a wrapper over Graph REST; barred by the do-not-count rule."
    },
    {
      "mechanism": "Microsoft Graph CLI (mgc)",
      "disposition": "excluded",
      "detail": "First-party but a thin command wrapper over the Graph REST API, not a distinct contract."
    },
    {
      "mechanism": "CLI for Microsoft 365 (m365)",
      "disposition": "excluded",
      "detail": "Community/open-source project, not a provider-defined Microsoft interface."
    },
    {
      "mechanism": "Graph Explorer",
      "disposition": "excluded",
      "detail": "First-party developer testing tool that issues Graph API requests; operations belong to the Graph REST API."
    },
    {
      "mechanism": "Third-party integrations index / Graph connectors",
      "disposition": "excluded",
      "detail": "External integrations and data ingestion, not first-party access interfaces to the service."
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
