## SaaS summary

**Figma** (Figma, Inc.; official domain figma.com, developer portal developers.figma.com). This analysis identifies **9 logical interfaces** spread across **5 distinct access channels**.

## Interface classification table

| Interface                  | Channel        | Interaction technology                                        | Provenance                                                                                                                                                                                                                                                                                                                                                                                                       |
| -------------------------- | -------------- | ------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Figma design editor (GUI)  | Interactive    | Web app + macOS/Windows desktop app                           | figma.com/downloads and the desktop-app guide confirm a first-party client on web and desktop; the desktop app "gives you access to the same features and functionality as using Figma in a browser," so both surfaces share one affordance-manipulation contract (canvas, panels, menus over persistent file state). Current.                                                                                   |
| Figma mobile app           | Interactive    | iOS and Android first-party app                               | Official App Store / Google Play listings describe viewing files, commenting, playing prototypes, and live mirroring. Distinct touch-oriented control structure from the desktop editor but the same paradigm: actions expressed by manipulating presented affordances. Current.                                                                                                                                 |
| REST API                   | Programmatic   | HTTPS REST, base `https://api.figma.com`, PAT/OAuth2          | REST API docs: the consumer explicitly invokes provider-defined operations (files, comments, variables, components, dev resources) via structured HTTP requests. Operation Invocation. Current.                                                                                                                                                                                                                  |
| Plugin API                 | Programmatic   | In-editor JavaScript/HTML API                                 | Plugin docs: plugins invoke provider-defined imperative operations against the open document's scene graph (create/read/edit nodes, variables, images). Primitive is the explicit operation call; control is caller-driven. Current.                                                                                                                                                                             |
| Widget API                 | Programmatic   | In-editor declarative TypeScript/JSX API                      | Widget docs: a distinct contract from the Plugin API (declarative React-like components with `useSyncedState`, multiplayer canvas state) but still explicit invocation of provider-defined operations/components. Split from Plugin API on genuinely different primitive and control structure; both Programmatic. Current.                                                                                      |
| Code Connect CLI           | Programmatic   | Command-line tool (`figma connect …`)                         | Code Connect docs: a first-party CLI whose own command contract publishes component-to-code mappings; the consumer invokes provider-defined commands. Operation Invocation. (The "Code Connect in Figma UI" form is not a separate interface — see ledger.) Current.                                                                                                                                             |
| Webhooks V2                | Event          | Provider-initiated HTTP callbacks to a subscriber endpoint    | Webhooks docs: the service initiates delivery when subscribed events fire (on files, projects, or teams) to a consumer-controlled receiver URL. Event Notification, not an API that merely returns event data. Current.                                                                                                                                                                                          |
| Figma MCP Server           | Agentic        | Model Context Protocol server (remote hosted + local desktop) | MCP Server docs: "a standardized interface for AI agents," exposing semantically described, discoverable/selectable tools (`get_design_context`, `get_screenshot`, `get_metadata`, `get_variable_defs`, write-to-canvas). Capability Discovery and Invocation is part of the contract → Agentic (the MCP boundary case), not Programmatic. Current (recently GA'd from beta).                                    |
| Figma Make (AI chat/agent) | Conversational | In-product natural-language chat agent                        | Figma Make docs: "Through conversation, you can ideate, iterate, and improve your apps"; the surface centers on an "AI chat, where you can prompt the model," with tool orchestration internal to the service. Primitive is the message → Conversational (the assistant-with-internal-tools boundary case), not Agentic. The auxiliary edit panel is a secondary affordance, not the defining contract. Current. |

## Coverage ledger

| Access mechanism                                                             | Disposition                                                                                                                                                   |
| ---------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Web client (first-party surface)                                             | Interface: Figma design editor (GUI)                                                                                                                          |
| Desktop client — macOS/Windows (first-party surface)                         | Interface: Figma design editor (GUI) — same contract as web                                                                                                   |
| Mobile client — iOS/Android (first-party surface)                            | Interface: Figma mobile app                                                                                                                                   |
| Terminal client (first-party surface)                                        | Interface: Code Connect CLI (command-based; **no persistent navigable TUI** is documented, so no Interactive interface arises from the terminal)              |
| REST API                                                                     | Interface: REST API                                                                                                                                           |
| Plugin API                                                                   | Interface: Plugin API                                                                                                                                         |
| Widget API                                                                   | Interface: Widget API                                                                                                                                         |
| Code Connect (CLI form)                                                      | Interface: Code Connect CLI                                                                                                                                   |
| Code Connect (in Figma UI form)                                              | Excluded: a feature accessed through the web editor's affordances, not a separate interaction contract                                                        |
| Webhooks V2                                                                  | Interface: Webhooks V2                                                                                                                                        |
| Figma MCP Server (remote + local)                                            | Interface: Figma MCP Server (one interface; same protocol/tools on both hosts)                                                                                |
| Figma Make                                                                   | Interface: Figma Make (conversational)                                                                                                                        |
| Embeds / Embed Kit / Embed API                                               | Excluded: the embedded viewer is the web Interactive interface delivered via iframe; the Embed Kit and Embed API are SDKs/JS control surfaces, not interfaces |
| Figma Sites                                                                  | Excluded: a website-publishing feature within the editor, not a distinct access mechanism                                                                     |
| GitHub App / GitHub integration                                              | Excluded: third-party integration supporting Code Connect UI                                                                                                  |
| SDKs / client libraries (e.g. figma-api, Embed Kit JS)                       | Excluded: SDKs/wrappers                                                                                                                                       |
| OAuth2 / Personal Access Tokens                                              | Excluded: authentication methods                                                                                                                              |
| FigmaAgent font installer                                                    | Excluded: background localhost helper with "no interface to open"; supports the desktop app, not an access channel                                            |
| Figma Mirror / device preview                                                | Excluded: a feature of the mobile app                                                                                                                         |
| FigJam / Figma Slides / Figma Draw / Dev Mode / Figma AI (first draft, etc.) | Excluded: products and modes surfaced within the Interactive editor, not separate interaction contracts                                                       |

## Channel coverage table

| Channel        | Evidence                                                      |
| -------------- | ------------------------------------------------------------- |
| Interactive    | Observed (design editor GUI; mobile app)                      |
| Agentic        | Observed (MCP Server)                                         |
| Conversational | Observed (Figma Make)                                         |
| Event          | Observed (Webhooks V2)                                        |
| Programmatic   | Observed (REST API; Plugin API; Widget API; Code Connect CLI) |

## Classification notes

Two boundary calls drive the AI-era classifications. The MCP Server is **Agentic** rather than Programmatic because discovery and selection of semantically described tools is part of its contract. Figma Make is **Conversational** rather than Agentic because the consumer-facing primitive is the natural-language message and tool orchestration is internal to the service. The Plugin API and Widget API are kept as two interfaces (both Programmatic) because their contracts genuinely differ — imperative scene-graph mutation versus declarative, state-synced canvas components — not because of any channel difference.

## Multichannel verdict

**Multichannel** — 5 distinct paradigms observed.

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
  "generated_at": "2026-09-22T00:00:00Z",
  "evidence_checked_at": "2026-09-22T00:00:00Z",
  "saas": { "name": "Figma" },
  "interfaces": [
    {
      "name": "Figma design editor (GUI)",
      "technology": "Web app and macOS/Windows desktop app",
      "channel": "Interactive",
      "classification_rationale": "Actions are expressed by manipulating presented affordances (canvas, panels, menus) over a persistent, navigable representation of file state; web and desktop share one contract.",
      "provenance": [
        {
          "url": "https://www.figma.com/downloads/",
          "evidence": "First-party desktop clients for macOS and Windows plus the web app."
        },
        {
          "url": "https://help.figma.com/hc/en-us/articles/5601429983767-Guide-to-the-Figma-desktop-app",
          "evidence": "Desktop app provides the same features and functionality as the browser editor."
        }
      ]
    },
    {
      "name": "Figma mobile app",
      "technology": "iOS and Android first-party app",
      "channel": "Interactive",
      "classification_rationale": "A touch-oriented client for viewing, commenting, playing prototypes, and mirroring; actions are expressed by manipulating on-screen affordances of file state.",
      "provenance": [
        {
          "url": "https://apps.apple.com/us/app/figma/id1152747299",
          "evidence": "Official mobile app: access Figma Design/Make/Slides/FigJam files, comment, play prototypes, mirror designs."
        }
      ]
    },
    {
      "name": "REST API",
      "technology": "HTTPS REST API, base https://api.figma.com, PAT/OAuth2",
      "channel": "Programmatic",
      "classification_rationale": "The consumer explicitly invokes provider-defined operations over files, comments, variables, components, and dev resources via structured HTTP requests.",
      "provenance": [
        {
          "url": "https://developers.figma.com/docs/rest-api/",
          "evidence": "REST API for accessing files, components, variables, comments; PAT/OAuth2; base https://api.figma.com."
        }
      ]
    },
    {
      "name": "Plugin API",
      "technology": "In-editor JavaScript/HTML API",
      "channel": "Programmatic",
      "classification_rationale": "Plugins invoke provider-defined imperative operations against the open document's scene graph; primitive is the explicit operation call.",
      "provenance": [
        {
          "url": "https://developers.figma.com/docs/plugins/",
          "evidence": "Editor extensions that read and write the open file via a JavaScript API."
        }
      ]
    },
    {
      "name": "Widget API",
      "technology": "In-editor declarative TypeScript/JSX API",
      "channel": "Programmatic",
      "classification_rationale": "Explicit invocation of provider-defined operations/components with a declarative, state-synced contract distinct from the imperative Plugin API; still Operation Invocation.",
      "provenance": [
        {
          "url": "https://developers.figma.com/docs/widgets/",
          "evidence": "Interactive on-canvas widgets built with a React-like declarative API and synced multiplayer state."
        }
      ]
    },
    {
      "name": "Code Connect CLI",
      "technology": "Command-line tool (figma connect ...)",
      "channel": "Programmatic",
      "classification_rationale": "A first-party CLI whose own command contract publishes component-to-code mappings; the consumer invokes provider-defined commands.",
      "provenance": [
        {
          "url": "https://developers.figma.com/docs/code-connect/quickstart-guide/",
          "evidence": "Code Connect CLI maps and publishes code components to design components; distinct command surface from REST."
        }
      ]
    },
    {
      "name": "Webhooks V2",
      "technology": "Provider-initiated HTTP callbacks to a subscriber endpoint",
      "channel": "Event",
      "classification_rationale": "The service initiates delivery when subscribed events fire on files, projects, or teams, to a consumer-controlled receiver URL.",
      "provenance": [
        {
          "url": "https://developers.figma.com/docs/rest-api/webhooks/",
          "evidence": "Subscribe to real-time events for files, projects, and teams; payloads delivered to a registered endpoint."
        }
      ]
    },
    {
      "name": "Figma MCP Server",
      "technology": "Model Context Protocol server (remote hosted and local desktop)",
      "channel": "Agentic",
      "classification_rationale": "A standardized interface exposing semantically described, discoverable and selectable tools (get_design_context, get_metadata, get_variable_defs, write-to-canvas); discovery/selection is part of the contract.",
      "provenance": [
        {
          "url": "https://developers.figma.com/docs/figma-mcp-server/",
          "evidence": "MCP server as a standardized interface for AI agents to interact with Figma, with discoverable tools; remote and local hosting."
        }
      ]
    },
    {
      "name": "Figma Make",
      "technology": "In-product natural-language chat agent",
      "channel": "Conversational",
      "classification_rationale": "The consumer expresses actions through natural-language messages ('through conversation') interpreted by the service; tool orchestration is internal, so Conversational rather than Agentic.",
      "provenance": [
        {
          "url": "https://help.figma.com/hc/en-us/articles/31304412302231-Explore-Figma-Make",
          "evidence": "AI-driven prompt-to-app tool; 'through conversation you can ideate, iterate, and improve'; interface centers on an AI chat."
        }
      ]
    }
  ],
  "access_mechanism_ledger": [
    {
      "mechanism": "Web client (first-party surface)",
      "disposition": "interface",
      "detail": "Figma design editor (GUI)"
    },
    {
      "mechanism": "Desktop client macOS/Windows (first-party surface)",
      "disposition": "interface",
      "detail": "Figma design editor (GUI) — same contract as web"
    },
    {
      "mechanism": "Mobile client iOS/Android (first-party surface)",
      "disposition": "interface",
      "detail": "Figma mobile app"
    },
    {
      "mechanism": "Terminal client (first-party surface)",
      "disposition": "interface",
      "detail": "Code Connect CLI; no persistent navigable TUI documented, so no Interactive interface from the terminal"
    },
    {
      "mechanism": "REST API",
      "disposition": "interface",
      "detail": "REST API"
    },
    {
      "mechanism": "Plugin API",
      "disposition": "interface",
      "detail": "Plugin API"
    },
    {
      "mechanism": "Widget API",
      "disposition": "interface",
      "detail": "Widget API"
    },
    {
      "mechanism": "Code Connect (CLI form)",
      "disposition": "interface",
      "detail": "Code Connect CLI"
    },
    {
      "mechanism": "Code Connect (in Figma UI form)",
      "disposition": "excluded",
      "detail": "Feature accessed through the web editor's affordances, not a separate interaction contract"
    },
    {
      "mechanism": "Webhooks V2",
      "disposition": "interface",
      "detail": "Webhooks V2"
    },
    {
      "mechanism": "Figma MCP Server (remote + local)",
      "disposition": "interface",
      "detail": "Figma MCP Server (one interface across both hosts)"
    },
    {
      "mechanism": "Figma Make",
      "disposition": "interface",
      "detail": "Figma Make"
    },
    {
      "mechanism": "Embeds / Embed Kit / Embed API",
      "disposition": "excluded",
      "detail": "Embedded viewer is the web Interactive interface via iframe; Embed Kit/Embed API are SDKs"
    },
    {
      "mechanism": "Figma Sites",
      "disposition": "excluded",
      "detail": "Website-publishing feature within the editor, not a distinct access mechanism"
    },
    {
      "mechanism": "GitHub App / GitHub integration",
      "disposition": "excluded",
      "detail": "Third-party integration supporting Code Connect UI"
    },
    {
      "mechanism": "SDKs / client libraries",
      "disposition": "excluded",
      "detail": "SDKs/wrappers, not interfaces"
    },
    {
      "mechanism": "OAuth2 / Personal Access Tokens",
      "disposition": "excluded",
      "detail": "Authentication methods"
    },
    {
      "mechanism": "FigmaAgent font installer",
      "disposition": "excluded",
      "detail": "Background localhost helper with no interface; supports the desktop app"
    },
    {
      "mechanism": "Figma Mirror / device preview",
      "disposition": "excluded",
      "detail": "Feature of the mobile app"
    },
    {
      "mechanism": "FigJam / Figma Slides / Figma Draw / Dev Mode / Figma AI features",
      "disposition": "excluded",
      "detail": "Products and modes surfaced within the Interactive editor, not separate contracts"
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
