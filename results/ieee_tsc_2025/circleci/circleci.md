## SaaS summary

CircleCI is a cloud continuous integration and delivery platform operated by CircleCI, Inc. (circleci.com). Working from its official documentation and developer portal, I identified **nine provider-defined logical interfaces** spread across **four distinct access channels**.

## Interface classification table

| Interface                            | Channel      | Interaction technology                  | Provenance                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| ------------------------------------ | ------------ | --------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Web application (app.circleci.com)   | Interactive  | Web UI                                  | The web app presents a navigable representation of pipelines, workflows, jobs, project and org settings that users act on through views, menus, buttons and forms. Actions are expressed by manipulating those affordances, which is Affordance Manipulation. Source: circleci.com/docs "Intro to the CircleCI web app" and app.circleci.com. Current.                                                                                                                 |
| VS Code extension (Pipeline Manager) | Interactive  | IDE extension panel                     | A first-party client that renders a persistent pipelines panel and status bar inside the editor. Users view and act on pipelines, workflows and jobs through tree items, hover actions and panel controls (rerun, cancel, approve, SSH). This is Affordance Manipulation on a distinct client surface. The bundled Config Helper is a local language-server aid and not a separate service interface. Source: circleci.com/docs "VS Code extension overview". Current. |
| REST API v2                          | Programmatic | HTTP REST API                           | The consumer explicitly invokes provider-defined operations over a single base and token auth. No capability discovery structures the contract, so it is Operation Invocation. Source: circleci.com/docs/api/v2. Current.                                                                                                                                                                                                                                              |
| CircleCI CLI (command interface)     | Programmatic | Command-line binary                     | Commands invoke provider-defined operations (run, config, orb, context, policy) and a `circleci api` passthrough. The CLI is documented as behaving correctly in non-TTY contexts and exposes commands and interactive prompts, not a persistent navigable dashboard, so no TUI interface exists. Command invocation is Operation Invocation. Source: circleci.com/docs "The CircleCI CLI" and cli.circleci.com. Current.                                              |
| Custom webhook triggers (inbound)    | Programmatic | Inbound webhook endpoint                | An external caller triggers a pipeline by sending a structured POST to a trigger URL with a secret. The consumer initiates and invokes a defined operation, which is Operation Invocation, on an endpoint and auth model distinct from the REST API. It is not Event, because the service does not initiate. Source: circleci.com/docs "Custom webhooks". Current.                                                                                                     |
| Outbound webhooks                    | Event        | Outbound webhook delivery               | CircleCI initiates delivery when subscribed pipeline, workflow and job events occur, sending an HTTP POST to a consumer-registered receiver URL. This is Event Notification. Source: circleci.com/docs "Outbound Webhooks". Current.                                                                                                                                                                                                                                   |
| Hosted MCP server                    | Agentic      | Model Context Protocol (hosted)         | A CircleCI-hosted MCP server at mcp.circleci.com/v1/mcp exposes a curated set of semantically described CI tools that an assistant discovers and selects by goal. Capability discovery and selection are part of the contract, which is the MCP boundary case resolving to Agentic. Source: circleci.com/docs "CircleCI MCP overview". Current.                                                                                                                        |
| CircleCI CLI MCP                     | Agentic      | Model Context Protocol (local, via CLI) | A local MCP server built into the CLI that exposes the full CLI surface as discoverable MCP tools, authenticated by the local CLI session. Same technology as the CLI command interface but a different contract based on capability discovery, so Agentic. Source: circleci.com/docs "Connecting to the CircleCI CLI MCP". Current.                                                                                                                                   |
| Docs MCP server                      | Agentic      | Model Context Protocol (docs)           | A provider-defined MCP server exposing documentation-retrieval tools that an assistant discovers and calls. Agentic in paradigm, scoped to documentation rather than run state. Source: circleci.com/docs "Connecting to the CircleCI Docs MCP Server". Current.                                                                                                                                                                                                       |

## Coverage ledger

| Access mechanism                                                                      | Disposition                                                                                                                                                    |
| ------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Web application                                                                       | Web application (Interactive)                                                                                                                                  |
| VS Code extension                                                                     | VS Code extension Pipeline Manager (Interactive)                                                                                                               |
| REST API v2                                                                           | REST API v2 (Programmatic)                                                                                                                                     |
| CircleCI CLI (commands)                                                               | CircleCI CLI command interface (Programmatic)                                                                                                                  |
| CLI TUI dashboard                                                                     | Excluded: the CLI exposes commands and interactive prompts only; no persistent navigable TUI is documented                                                     |
| Custom webhooks (inbound)                                                             | Custom webhook triggers (Programmatic)                                                                                                                         |
| Outbound webhooks                                                                     | Outbound webhooks (Event)                                                                                                                                      |
| Hosted MCP server                                                                     | Hosted MCP server (Agentic)                                                                                                                                    |
| CLI MCP                                                                               | CircleCI CLI MCP (Agentic)                                                                                                                                     |
| Docs MCP server                                                                       | Docs MCP server (Agentic)                                                                                                                                      |
| Mobile app                                                                            | Excluded: no first-party mobile client observed; mobile material concerns building and deploying customer apps as CI targets, not a CircleCI management client |
| Desktop app                                                                           | Excluded: no first-party desktop client; CircleCI Server is self-hosted backend infrastructure, not a desktop client surface                                   |
| Environment CLI                                                                       | Excluded from separate count: legacy in-job test-splitting utility, command-based (Programmatic) paradigm, adds no new channel                                 |
| Chunk CLI                                                                             | Excluded from separate count: Beta specialized command-line tool, command-based (Programmatic) paradigm, adds no new channel                                   |
| In-app AI features / Intelligent summaries                                            | Excluded: AI augmentation rendered inside the web app, not a standalone access interface                                                                       |
| Docs "Ask AI" widget                                                                  | Excluded: documentation-site question-and-answer helper in the docs front end; its MCP form is already captured as the Docs MCP                                |
| CircleCI Agent Skills                                                                 | Excluded: agent skill definitions and guidance, not a service access interface                                                                                 |
| Config SDK / Orb development kit / YAML language server                               | Excluded: SDKs, dev kits and libraries, not interfaces                                                                                                         |
| Third-party integrations (Slack, Jira, Datadog, New Relic, Sumo Logic, OpenTelemetry) | Excluded: third-party integrations, not provider-defined interfaces                                                                                            |
| Public GraphQL API                                                                    | Excluded: none observed; the public API surface is REST (API v2)                                                                                               |

## Channel coverage

| Channel        | Evidence             |
| -------------- | -------------------- |
| Interactive    | Observed             |
| Agentic        | Observed             |
| Conversational | No evidence observed |
| Event          | Observed             |
| Programmatic   | Observed             |

## Classification notes

The three MCP servers are enumerated separately because their interaction contracts genuinely differ in base, authentication and scope: the hosted server is a remote HTTPS endpoint with OAuth2 or personal-token auth and a curated tool set, the CLI MCP is a local process authenticated by the CLI session that exposes the entire CLI, and the Docs MCP is scoped to documentation retrieval. All three share the Agentic paradigm, so they contribute one channel.

Conversational is recorded as not observed. The natural-language experience CircleCI advertises is delivered by the client assistant (Cursor, Claude, and similar), while CircleCI's own contract is the MCP tool surface, which is Agentic. CircleCI does not expose a message-based interface that it interprets itself, so no Conversational interface is asserted. Absence of evidence is not treated as evidence of absence.

## Multichannel verdict

`Multichannel` (4 distinct paradigms: Interactive, Programmatic, Event, Agentic)

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
  "saas": { "name": "CircleCI" },
  "interfaces": [
    {
      "name": "Web application",
      "technology": "Web UI (app.circleci.com)",
      "channel": "Interactive",
      "classification_rationale": "Users act on a persistent, navigable representation of pipelines, jobs and settings by manipulating views, menus, buttons and forms, which is Affordance Manipulation.",
      "provenance": [
        {
          "url": "https://circleci.com/docs/guides/about-circleci/introduction-to-the-circleci-web-app/",
          "evidence": "Official overview of the CircleCI web application and its navigable pipeline, workflow and settings views."
        }
      ]
    },
    {
      "name": "VS Code extension (Pipeline Manager)",
      "technology": "IDE extension panel",
      "channel": "Interactive",
      "classification_rationale": "A first-party editor client renders a persistent pipelines panel and status bar whose tree items, hover actions and controls the user manipulates to view and act on runs.",
      "provenance": [
        {
          "url": "https://circleci.com/docs/guides/toolkit/vs-code-extension-overview/",
          "evidence": "Documents the Pipeline Manager panel, status bar and per-item actions (rerun, cancel, approve, SSH) inside VS Code."
        }
      ]
    },
    {
      "name": "REST API v2",
      "technology": "HTTP REST API",
      "channel": "Programmatic",
      "classification_rationale": "The consumer explicitly invokes provider-defined operations over one base and token auth, with no capability discovery in the contract, which is Operation Invocation.",
      "provenance": [
        {
          "url": "https://circleci.com/docs/api/v2/index.html",
          "evidence": "Official API v2 reference describing resources and operations for pipelines, workflows, jobs, contexts, webhooks and more."
        }
      ]
    },
    {
      "name": "CircleCI CLI (command interface)",
      "technology": "Command-line binary",
      "channel": "Programmatic",
      "classification_rationale": "Commands invoke defined operations and a direct api passthrough. It exposes commands and prompts but no persistent navigable dashboard, so it is Operation Invocation, not Interactive.",
      "provenance": [
        {
          "url": "https://circleci.com/docs/guides/toolkit/circleci-cli/",
          "evidence": "Official CLI documentation; the CLI is documented to run correctly in non-TTY contexts and exposes command groups such as run, config, orb, context and policy."
        }
      ]
    },
    {
      "name": "Custom webhook triggers (inbound)",
      "technology": "Inbound webhook endpoint",
      "channel": "Programmatic",
      "classification_rationale": "An external caller triggers a pipeline by POSTing a structured request with a secret to a distinct trigger endpoint. The consumer initiates and invokes an operation, which is Operation Invocation, not service-initiated Event.",
      "provenance": [
        {
          "url": "https://circleci.com/docs/guides/orchestrate/custom-webhooks/",
          "evidence": "Describes inbound custom webhooks that let any service trigger a pipeline via a POST to a trigger URL with a secret."
        }
      ]
    },
    {
      "name": "Outbound webhooks",
      "technology": "Outbound webhook delivery",
      "channel": "Event",
      "classification_rationale": "CircleCI initiates an HTTP POST to a consumer-registered receiver when subscribed pipeline, workflow or job events occur, which is Event Notification.",
      "provenance": [
        {
          "url": "https://circleci.com/docs/guides/integration/outbound-webhooks/",
          "evidence": "Documents service-initiated webhook delivery to a registered receiver URL on platform events."
        }
      ]
    },
    {
      "name": "Hosted MCP server",
      "technology": "Model Context Protocol (hosted)",
      "channel": "Agentic",
      "classification_rationale": "A hosted MCP server exposes semantically described CI tools that an assistant discovers and selects by goal; capability discovery and selection structure the contract, the MCP boundary case resolving to Agentic.",
      "provenance": [
        {
          "url": "https://circleci.com/docs/guides/toolkit/circleci-mcp-overview/",
          "evidence": "Describes the hosted MCP server at mcp.circleci.com/v1/mcp with a curated tool set an assistant selects from."
        }
      ]
    },
    {
      "name": "CircleCI CLI MCP",
      "technology": "Model Context Protocol (local, via CLI)",
      "channel": "Agentic",
      "classification_rationale": "A local MCP server built into the CLI exposes the full CLI as discoverable MCP tools under the local CLI session, a distinct capability-discovery contract on the same technology as the CLI.",
      "provenance": [
        {
          "url": "https://circleci.com/docs/guides/toolkit/circleci-mcp-overview/",
          "evidence": "Documents the CLI MCP, built into the CircleCI CLI, exposing the entire CLI as tools to AI assistants."
        }
      ]
    },
    {
      "name": "Docs MCP server",
      "technology": "Model Context Protocol (docs)",
      "channel": "Agentic",
      "classification_rationale": "A provider-defined MCP server exposes documentation-retrieval tools an assistant discovers and calls; Agentic in paradigm, scoped to documentation.",
      "provenance": [
        {
          "url": "https://circleci.com/docs/guides/toolkit/connecting-to-a-docs-mcp-server/",
          "evidence": "Official page for connecting to the CircleCI Docs MCP server."
        }
      ]
    }
  ],
  "access_mechanism_ledger": [
    {
      "mechanism": "Web application",
      "disposition": "interface",
      "detail": "Web application (Interactive)"
    },
    {
      "mechanism": "VS Code extension",
      "disposition": "interface",
      "detail": "VS Code extension Pipeline Manager (Interactive)"
    },
    {
      "mechanism": "REST API v2",
      "disposition": "interface",
      "detail": "REST API v2 (Programmatic)"
    },
    {
      "mechanism": "CircleCI CLI (commands)",
      "disposition": "interface",
      "detail": "CircleCI CLI command interface (Programmatic)"
    },
    {
      "mechanism": "CLI TUI dashboard",
      "disposition": "excluded",
      "detail": "No persistent navigable TUI documented; the CLI exposes commands and prompts only"
    },
    {
      "mechanism": "Custom webhooks (inbound)",
      "disposition": "interface",
      "detail": "Custom webhook triggers (Programmatic)"
    },
    {
      "mechanism": "Outbound webhooks",
      "disposition": "interface",
      "detail": "Outbound webhooks (Event)"
    },
    {
      "mechanism": "Hosted MCP server",
      "disposition": "interface",
      "detail": "Hosted MCP server (Agentic)"
    },
    {
      "mechanism": "CLI MCP",
      "disposition": "interface",
      "detail": "CircleCI CLI MCP (Agentic)"
    },
    {
      "mechanism": "Docs MCP server",
      "disposition": "interface",
      "detail": "Docs MCP server (Agentic)"
    },
    {
      "mechanism": "Mobile app",
      "disposition": "excluded",
      "detail": "No first-party mobile client; mobile material concerns building customer apps as CI targets"
    },
    {
      "mechanism": "Desktop app",
      "disposition": "excluded",
      "detail": "No first-party desktop client; CircleCI Server is self-hosted backend infrastructure"
    },
    {
      "mechanism": "Environment CLI",
      "disposition": "excluded",
      "detail": "Legacy in-job test-splitting utility; command-based Programmatic paradigm, adds no new channel"
    },
    {
      "mechanism": "Chunk CLI",
      "disposition": "excluded",
      "detail": "Beta specialized command-line tool; command-based Programmatic paradigm, adds no new channel"
    },
    {
      "mechanism": "In-app AI features / Intelligent summaries",
      "disposition": "excluded",
      "detail": "AI augmentation inside the web app, not a standalone access interface"
    },
    {
      "mechanism": "Docs Ask AI widget",
      "disposition": "excluded",
      "detail": "Documentation-site Q&A helper; its MCP form is captured as the Docs MCP"
    },
    {
      "mechanism": "CircleCI Agent Skills",
      "disposition": "excluded",
      "detail": "Agent skill definitions and guidance, not an access interface"
    },
    {
      "mechanism": "Config SDK / Orb development kit / YAML language server",
      "disposition": "excluded",
      "detail": "SDKs, dev kits and libraries, not interfaces"
    },
    {
      "mechanism": "Third-party integrations (Slack, Jira, Datadog, New Relic, Sumo Logic, OpenTelemetry)",
      "disposition": "excluded",
      "detail": "Third-party integrations, not provider-defined interfaces"
    },
    {
      "mechanism": "Public GraphQL API",
      "disposition": "excluded",
      "detail": "None observed; the public API surface is REST (API v2)"
    }
  ],
  "channel_evidence": {
    "Interactive": "observed",
    "Agentic": "observed",
    "Conversational": "no_evidence_observed",
    "Event": "observed",
    "Programmatic": "observed"
  },
  "number_of_interfaces": 9,
  "multi_interface": true,
  "number_of_channels": 4,
  "multi_channel": true
}
```
