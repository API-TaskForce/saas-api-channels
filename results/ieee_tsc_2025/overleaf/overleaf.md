## Resumen

Overleaf, de Digital Science, es una plataforma colaborativa de escritura en LaTeX. A partir de su documentación oficial se reconstruyen **3 interfaces lógicas** repartidas en **3 canales distintos**. La tecnología principal es una única aplicación web, pero esa tecnología materializa dos interfaces con contratos de interacción diferentes (el editor y el asistente de chat), y a ellas se suma el acceso Git como remoto de repositorio.

## Clasificación de interfaces

| Interfaz                     | Canal          | Tecnología                                                  | Procedencia                                                                                                                                                                                                                                                                                                                             |
| ---------------------------- | -------------- | ----------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Web editor                   | Interactive    | Aplicación web en navegador                                 | Docs y Learn describen el editor en línea con paneles de escritura, vista previa del PDF, árbol de archivos, menús y panel de proyectos: una representación persistente y navegable del estado del proyecto que se manipula mediante affordances. Vigente.                                                                              |
| Git integration (git-bridge) | Programmatic   | Git remoto sobre HTTPS                                      | Los docs oficiales indican que la integración entrega una URL de Git para tratar el proyecto como repositorio remoto y ejecutar clone, push, pull y fetch. El primitivo es la invocación explícita de operaciones Git. Vigente (función premium; Cloud y Server Pro 4.0+).                                                              |
| AI assistant (chat)          | Conversational | Panel de chat en el editor (Overleaf AI / add-on AI Assist) | Los docs describen un chat lateral donde el usuario escribe una pregunta o instrucción en lenguaje natural; el asistente conoce la posición del cursor y puede buscar en el proyecto, con orquestación de herramientas interna al servicio. Primitivo de mensaje con herramientas internas: Conversational, no Agentic. Vigente (2026). |

## Registro de cobertura

| Mecanismo de acceso                                                   | Disposición                                                                                                                                                                                                        |
| --------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Aplicación web (superficie cliente web de primera parte)              | Interfaz: Web editor (Interactive)                                                                                                                                                                                 |
| Integración Git / git-bridge                                          | Interfaz: Git integration (git-bridge) (Programmatic)                                                                                                                                                              |
| AI assistant (chat)                                                   | Interfaz: AI assistant (chat) (Conversational)                                                                                                                                                                     |
| Error Assist / Citation Reviewer / herramientas de lenguaje Writefull | Excluido: el usuario interactúa con affordances del editor (botón "Suggest fix", entradas de menú/barra, valoración con pulgar), por lo que forman parte del editor web Interactive y no de una interfaz distinta. |
| Sincronización con GitHub                                             | Excluido: integración con un tercero (github.com) vía OAuth y la API de GitHub; se dispara desde la UI web y no es un canal de acceso propio de Overleaf.                                                          |
| Sincronización con Dropbox                                            | Excluido: integración con un tercero (sync bidireccional con Dropbox), no una interfaz definida por el proveedor.                                                                                                  |
| Gestores de referencias (ReadCube/Papers, Zotero, Mendeley)           | Excluido: integraciones con terceros que importan datos .bib al proyecto; no son interfaces de acceso al servicio.                                                                                                 |
| Integración con Grammarly                                             | Excluido: integración con un tercero mostrada dentro del editor, no una interfaz de acceso propia.                                                                                                                 |
| Integración con Google Drive                                          | Excluido: integración con un tercero listada como add-on; no es una interfaz de acceso a Overleaf.                                                                                                                 |
| R code (knitr)                                                        | Excluido: función de compilación/procesado dentro del editor y el compilador, no un mecanismo de acceso.                                                                                                           |
| Enlaces compartidos (solo lectura y edición)                          | Excluido: abren el mismo editor web; son un affordance de acceso de la interfaz Interactive, no una interfaz aparte.                                                                                               |
| Enlaces de descarga de PDF compilado / fuentes                        | Excluido: descargas autenticadas por sesión disparadas desde la UI web; subsumidas en el editor web Interactive.                                                                                                   |
| API pública de desarrollador (API de contenido REST/GraphQL)          | Excluido: la documentación de Overleaf no lista ninguna API pública REST ni GraphQL de contenido; la única vía programática documentada es la integración Git.                                                     |
| SSO (SAML 2.0 institucional/de grupo)                                 | Excluido: método de autenticación (SAML iniciado por el SP), no una interfaz de acceso; los métodos de autenticación no se cuentan como interfaces.                                                                |
| Aprovisionamiento SCIM                                                | Excluido: los docs de Overleaf indican expresamente que SCIM no está soportado ni es necesario; el aprovisionamiento es por JIT del usuario y auto-inscripción por dominio, no una API del proveedor.              |
| Webhooks / eventos / enrutado de entrada                              | Excluido: no hay mecanismo documentado de notificación de eventos ni webhooks para Overleaf Cloud.                                                                                                                 |
| Servidor MCP / protocolo de agente                                    | Excluido: no hay servidor MCP ni de protocolo de agente oficial documentado; las herramientas MCP/git-sync encontradas son de terceros.                                                                            |
| App móvil (superficie cliente móvil de primera parte)                 | Excluido: Overleaf no publica cliente oficial iOS/Android; la antigua app móvil fue discontinuada y el acceso es por la web responsive.                                                                            |
| App de escritorio (superficie cliente de escritorio de primera parte) | Excluido: no hay cliente de escritorio oficial documentado; el acceso es por la aplicación web.                                                                                                                    |
| CLI / TUI (superficie cliente de terminal de primera parte)           | Excluido: Overleaf no publica CLI ni TUI oficial; las herramientas CLI/VS Code de git-sync encontradas son de terceros.                                                                                            |

## Cobertura por canal

| Canal          | Evidencia               |
| -------------- | ----------------------- |
| Interactive    | Observado               |
| Agentic        | Sin evidencia observada |
| Conversational | Observado               |
| Event          | Sin evidencia observada |
| Programmatic   | Observado               |

## Veredicto

**Multichannel** (3 paradigmas distintos: Interactive, Conversational, Programmatic).

```json
{
  "schema_version": "2.1",
  "generator": {
    "platform": "Claude",
    "provider": "Anthropic",
    "model": "claude-opus-4-8",
    "skill": "saas-interface-channel-analyzer",
    "skill_version": "1.0"
  },
  "generated_at": "2026-09-23T00:00:00Z",
  "evidence_checked_at": "2026-09-23T00:00:00Z",
  "saas": {
    "name": "Overleaf"
  },
  "interfaces": [
    {
      "name": "Web editor",
      "technology": "Browser-based web application",
      "channel": "Interactive",
      "classification_rationale": "Actions are expressed by manipulating presented affordances (editor panes, file tree, menus, buttons, project dashboard) of a persistent, navigable representation of project state. Primitive is affordance manipulation, control structure is user-driven navigation.",
      "provenance": [
        {
          "url": "https://www.overleaf.com/learn/how-to/Git_integration",
          "evidence": "Overleaf's own Learn/docs describe the online editor with panes for writing, live PDF preview, file management, and collaboration, a persistent navigable representation of the project the user manipulates directly. Current."
        },
        {
          "url": "https://docs.overleaf.com/integrations-and-add-ons/ai-features/error-assist",
          "evidence": "Editor affordances such as the 'Suggest fix' control, logs/output pane, and toolbar confirm interaction by manipulating editor controls rather than by command or message. Current (2026)."
        }
      ]
    },
    {
      "name": "Git integration (git-bridge)",
      "technology": "Git remote over HTTPS",
      "channel": "Programmatic",
      "classification_rationale": "The consumer obtains a Git URL and explicitly invokes provider-defined remote operations (clone, push, pull, fetch) through structured Git commands. Primitive is explicit operation invocation via the Git protocol.",
      "provenance": [
        {
          "url": "https://docs.overleaf.com/integrations-and-add-ons/git-integration-and-github-synchronization/git",
          "evidence": "Official docs state the Git integration lets a user obtain a Git URL and treat the project as a remote repo to clone, push, and pull. This is Git remote operation invocation, a Programmatic contract. Current (premium feature, Cloud and Server Pro 4.0+)."
        },
        {
          "url": "https://docs.overleaf.com/integrations-and-add-ons/git-integration-and-github-synchronization/git-integration",
          "evidence": "Docs describe pull/fetch and push creating commits against the Overleaf remote, confirming structured Git command invocation as the interaction primitive. Current."
        }
      ]
    },
    {
      "name": "AI assistant (chat)",
      "technology": "In-editor chat panel (Overleaf AI / AI Assist add-on)",
      "channel": "Conversational",
      "classification_rationale": "The consumer types natural-language questions or instructions into a chat box and the service interprets them, optionally searching the project and running tools internally. Primitive is the natural-language message; internal tool orchestration is not exposed as a discovery contract, so it is Conversational rather than Agentic.",
      "provenance": [
        {
          "url": "https://docs.overleaf.com/integrations-and-add-ons/ai-features/ai-assistant",
          "evidence": "Official docs describe a side-panel chat where the user types a question or instruction; the assistant is aware of cursor position and can search other parts of the project when needed, with tool use internal to the service. Message-based contract with internal tools = Conversational. Current (2026)."
        },
        {
          "url": "https://www.overleaf.com/blog/overleaf-ai-now-a-part-of-overleaf-plans",
          "evidence": "Overleaf's blog describes the AI Assistant as a chat-based tool for getting help with LaTeX, improving writing, and generating code, confirming a natural-language message primitive. Current (2026)."
        }
      ]
    }
  ],
  "access_mechanism_ledger": [
    {
      "mechanism": "Web application (first-party web client surface)",
      "disposition": "interface",
      "detail": "Web editor (Interactive)"
    },
    {
      "mechanism": "Git integration / git-bridge",
      "disposition": "interface",
      "detail": "Git integration (git-bridge) (Programmatic)"
    },
    {
      "mechanism": "AI assistant (chat)",
      "disposition": "interface",
      "detail": "AI assistant (chat) (Conversational)"
    },
    {
      "mechanism": "Error Assist / Citation Reviewer / Writefull language tools",
      "disposition": "excluded",
      "detail": "Excluded: consumer interacts via editor affordances (Suggest fix button, toolbar/menu items, thumbs up/down), so these are part of the Interactive web editor, not a distinct interface."
    },
    {
      "mechanism": "GitHub synchronization",
      "disposition": "excluded",
      "detail": "Excluded: third-party integration that links the project to a github.com repo via OAuth and GitHub's API; sync is triggered from the web UI and is not a distinct Overleaf access channel."
    },
    {
      "mechanism": "Dropbox sync",
      "disposition": "excluded",
      "detail": "Excluded: third-party integration (two-way sync with the user's Dropbox account), not a provider-defined interface for accessing Overleaf."
    },
    {
      "mechanism": "Reference manager integrations (ReadCube/Papers, Zotero, Mendeley)",
      "disposition": "excluded",
      "detail": "Excluded: third-party integrations that import .bib data into a project; not an interface for accessing the service."
    },
    {
      "mechanism": "Grammarly integration",
      "disposition": "excluded",
      "detail": "Excluded: third-party integration surfaced inside the editor, not a provider-defined access interface."
    },
    {
      "mechanism": "Google Drive integration",
      "disposition": "excluded",
      "detail": "Excluded: third-party integration listed under add-ons; not a provider-defined interface for accessing Overleaf."
    },
    {
      "mechanism": "R code (knitr)",
      "disposition": "excluded",
      "detail": "Excluded: a compilation/document-processing feature within the editor and compiler, not an access mechanism."
    },
    {
      "mechanism": "Link sharing (read-only and edit share links)",
      "disposition": "excluded",
      "detail": "Excluded: share links open the same web editor; an access affordance of the Interactive interface, not a separate interface."
    },
    {
      "mechanism": "Compiled-PDF / source download links",
      "disposition": "excluded",
      "detail": "Excluded: session-authenticated downloads triggered from within the web UI; subsumed into the Interactive web editor."
    },
    {
      "mechanism": "Public developer API (REST/GraphQL content API)",
      "disposition": "excluded",
      "detail": "Excluded: Overleaf's documentation lists no public REST or GraphQL content API; the only programmatic access path it documents is the Git integration."
    },
    {
      "mechanism": "SSO (institutional/group SAML 2.0)",
      "disposition": "excluded",
      "detail": "Excluded: an authentication method (SP-initiated SAML), not an access interface; authentication methods are not counted as interfaces."
    },
    {
      "mechanism": "SCIM provisioning",
      "disposition": "excluded",
      "detail": "Excluded: Overleaf docs explicitly state SCIM is neither supported nor required; provisioning is via user-driven JIT and domain auto-enrollment, not a provider API."
    },
    {
      "mechanism": "Webhooks / events / inbound routing",
      "disposition": "excluded",
      "detail": "Excluded: no provider-defined event-notification or webhook mechanism is documented for Overleaf Cloud."
    },
    {
      "mechanism": "MCP / agent protocol server",
      "disposition": "excluded",
      "detail": "Excluded: no official Overleaf MCP or agent-protocol server is documented; the MCP/git-sync tools found are third-party."
    },
    {
      "mechanism": "Mobile app (first-party mobile client surface)",
      "disposition": "excluded",
      "detail": "Excluded: Overleaf ships no official iOS/Android client; the former mobile app was discontinued and access is via the responsive web app."
    },
    {
      "mechanism": "Desktop app (first-party desktop client surface)",
      "disposition": "excluded",
      "detail": "Excluded: no official desktop client is documented; access is via the web application."
    },
    {
      "mechanism": "CLI / TUI (first-party terminal client surface)",
      "disposition": "excluded",
      "detail": "Excluded: Overleaf ships no official CLI or TUI; the git-sync CLI/VS Code tools found are third-party."
    }
  ],
  "channel_evidence": {
    "Interactive": "observed",
    "Agentic": "no_evidence_observed",
    "Conversational": "observed",
    "Event": "no_evidence_observed",
    "Programmatic": "observed"
  },
  "number_of_interfaces": 3,
  "multi_interface": true,
  "number_of_channels": 3,
  "multi_channel": true
}
```
