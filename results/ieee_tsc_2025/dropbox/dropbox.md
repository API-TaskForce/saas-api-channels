## Resumen del SaaS

- **Servicio:** Dropbox (almacenamiento, sincronización y compartición de archivos)
- **Interfaces lógicas identificadas:** 6
- **Canales distintos con al menos una interfaz clasificada:** 3

## Tabla de clasificación de interfaces

| Interfaz                                         | Canal        | Tecnología de interacción                                                                                        | Procedencia                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| ------------------------------------------------ | ------------ | ---------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Aplicación web                                   | Interactive  | Cliente web de primera parte (dropbox.com)                                                                       | El pie de la documentación oficial enlaza "Dropbox Web" (dropbox.com) como cliente del servicio. El usuario expresa acciones manipulando vistas, controles y menús sobre una representación navegable del estado de archivos. Regla 1 del árbol: manipulación de affordances. Fuente vigente.                                                                                                                                                      |
| Aplicación de escritorio                         | Interactive  | Cliente GUI de escritorio para Windows, macOS y Linux (dropbox.com/desktop)                                      | Enlace oficial "Desktop app" en el pie de la documentación de desarrollador. Misma paradigma de manipulación de affordances sobre un cliente GUI persistente. Una sola interfaz lógica a través de plataformas por compartir el mismo contrato de interacción. Fuente vigente.                                                                                                                                                                     |
| Aplicación móvil                                 | Interactive  | Cliente móvil de primera parte iOS/Android (dropbox.com/mobile)                                                  | Enlace oficial "Mobile app". Interacción por manipulación de affordances en pantallas móviles. Regla 1. Fuente vigente.                                                                                                                                                                                                                                                                                                                            |
| Dropbox API (HTTP/RPC v2)                        | Programmatic | API HTTP con endpoints RPC, de contenido y de subida, bajo OAuth 2.0 (docs.dropboxapi.com)                       | La documentación oficial describe una API para que los desarrolladores trabajen con archivos en Dropbox, con funciones como búsqueda de texto completo, miniaturas y compartición. El consumidor invoca explícitamente operaciones definidas por el proveedor mediante solicitudes estructuradas. Regla 5: invocación de operaciones. Un solo conjunto de operaciones bajo una misma base y autenticación, por tanto una interfaz. Fuente vigente. |
| CLI de escritorio para Linux (comando `dropbox`) | Programmatic | Interfaz de línea de comandos que controla el demonio de escritorio (help.dropbox.com/installs/linux-commands)   | El centro de ayuda oficial documenta que la aplicación de escritorio de Dropbox puede controlarse con la interfaz de línea de comandos (CLI) de Linux, con comandos como `start`, `stop`, `status`, `ls` y `sharelink`. El consumidor invoca comandos estructurados definidos por el proveedor. Regla 5: invocación de operaciones basada en comandos, sin TUI navegable. Fuente vigente.                                                          |
| Webhooks                                         | Event        | Notificaciones HTTP salientes hacia una URI receptora registrada (docs.dropboxapi.com/dropbox-api/docs/webhooks) | La guía oficial indica que Dropbox envía una solicitud HTTP a la URI registrada cada vez que hay un cambio en las cuentas conectadas a la app. El servicio inicia la interacción ante eventos y la entrega a un receptor controlado por el consumidor. Regla 4: notificación de eventos. Fuente vigente.                                                                                                                                           |

## Registro de cobertura

| Mecanismo de acceso                                       | Disposición                                                                                                                                               |
| --------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Referencia de la API HTTP                                 | Interfaz: Dropbox API (HTTP/RPC v2)                                                                                                                       |
| Webhooks                                                  | Interfaz: Webhooks                                                                                                                                        |
| CLI de Linux (`dropbox`)                                  | Interfaz: CLI de escritorio para Linux                                                                                                                    |
| Cliente web (superficie de primera parte)                 | Interfaz: Aplicación web                                                                                                                                  |
| Cliente móvil (superficie de primera parte)               | Interfaz: Aplicación móvil                                                                                                                                |
| Cliente de escritorio (superficie de primera parte)       | Interfaz: Aplicación de escritorio                                                                                                                        |
| Superficie de terminal/TUI                                | Excluido: la CLI de Linux es solo por comandos; no se documenta una TUI persistente y navegable                                                           |
| `dbxcli` (CLI en la organización GitHub de Dropbox)       | Excluido: envoltorio cliente sobre la API HTTP, declarado explícitamente como "no un producto Dropbox formalmente soportado"                              |
| Componentes prediseñados (Chooser, Saver, Embedder)       | Excluido: widgets de integración incrustables para desarrolladores, no canales de acceso autónomos; si se contaran serían Interactive, canal ya observado |
| Extensions                                                | Excluido: punto de extensión para lanzar apps de terceros desde un archivo; forma parte de la UI web/escritorio, no es un canal distinto                  |
| SDKs (Swift, Objective-C, Python, .NET, Java, JavaScript) | Excluido: bibliotecas cliente, no son interfaces                                                                                                          |
| Servidor MCP de la documentación                          | Excluido: da acceso de IA a la documentación de la API, no al servicio Dropbox                                                                            |
| Asistente "Ask AI" incrustado en los docs                 | Excluido: asistente de ayuda sobre la documentación, no un canal de acceso al servicio                                                                    |
| Índice de integraciones (app-integrations)                | Excluido: integraciones de terceros, no mecanismos de acceso de primera parte                                                                             |
| Dropbox Dash                                              | Excluido: producto separado (dash.dropbox.com), fuera del alcance del servicio central                                                                    |
| Dropbox Sign                                              | Excluido: producto separado (antes HelloSign), fuera del alcance del servicio central                                                                     |

## Cobertura de canales

| Canal          | Evidencia               |
| -------------- | ----------------------- |
| Interactive    | Observado               |
| Agentic        | Sin evidencia observada |
| Conversational | Sin evidencia observada |
| Event          | Observado               |
| Programmatic   | Observado               |

## Notas de clasificación

La CLI de Linux controla el demonio de escritorio local en lugar de llamar directamente a la nube, pero eso no cambia el paradigma: sigue siendo invocación de operaciones mediante comandos estructurados, por lo que es Programmatic y una interfaz distinta de la API HTTP (difieren en base, autenticación y primitiva). Los canales Agentic y Conversational aparecen en productos hermanos (Dash, con búsqueda y preguntas en lenguaje natural), no en el servicio central analizado aquí; su ausencia dentro de este alcance no implica que Dropbox como compañía no los ofrezca.

## Veredicto multicanal

`Multichannel` (3 paradigmas distintos: Interactive, Programmatic, Event)

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
  "generated_at": "2026-09-23T00:00:00Z",
  "evidence_checked_at": "2026-09-23T00:00:00Z",
  "saas": {
    "name": "Dropbox"
  },
  "interfaces": [
    {
      "name": "Web application",
      "technology": "First-party web client (dropbox.com)",
      "channel": "Interactive",
      "classification_rationale": "Actions are expressed by manipulating views, controls and menus over a persistent, navigable representation of file state.",
      "provenance": [
        {
          "url": "https://www.dropbox.com/",
          "evidence": "Official developer documentation footer links Dropbox Web as the service client."
        }
      ]
    },
    {
      "name": "Desktop application",
      "technology": "First-party desktop GUI client for Windows, macOS and Linux",
      "channel": "Interactive",
      "classification_rationale": "Persistent GUI client whose interaction is affordance manipulation; one logical interface across platforms sharing the same contract.",
      "provenance": [
        {
          "url": "https://www.dropbox.com/desktop",
          "evidence": "Official 'Desktop app' link on the developer documentation."
        }
      ]
    },
    {
      "name": "Mobile application",
      "technology": "First-party iOS/Android client",
      "channel": "Interactive",
      "classification_rationale": "Interaction through affordance manipulation on mobile screens.",
      "provenance": [
        {
          "url": "https://www.dropbox.com/mobile",
          "evidence": "Official 'Mobile app' link on the developer documentation."
        }
      ]
    },
    {
      "name": "Dropbox API (HTTP/RPC v2)",
      "technology": "HTTP API with RPC, content and upload endpoints under OAuth 2.0",
      "channel": "Programmatic",
      "classification_rationale": "The consumer explicitly invokes provider-defined operations through structured HTTP requests; one interface across resource groups under a shared base and auth.",
      "provenance": [
        {
          "url": "https://docs.dropboxapi.com/dropbox-api/docs/get-started/welcome",
          "evidence": "Official docs describe an API for developers to work with files, including full-text search, thumbnails and sharing."
        }
      ]
    },
    {
      "name": "Linux desktop CLI (dropbox command)",
      "technology": "Command-line interface controlling the desktop daemon",
      "channel": "Programmatic",
      "classification_rationale": "Consumer invokes provider-defined structured commands (start, stop, status, ls, sharelink); command-based, no navigable TUI.",
      "provenance": [
        {
          "url": "https://help.dropbox.com/installs/linux-commands",
          "evidence": "Official help center documents that the desktop app can be controlled with the Linux CLI and lists its commands."
        }
      ]
    },
    {
      "name": "Webhooks",
      "technology": "Outbound HTTP notifications to a registered receiver URI",
      "channel": "Event",
      "classification_rationale": "The service initiates an HTTP request to a consumer-controlled URI whenever files in connected accounts change.",
      "provenance": [
        {
          "url": "https://docs.dropboxapi.com/dropbox-api/docs/webhooks",
          "evidence": "Official webhooks guide: Dropbox sends an HTTP request to the registered URI on every change in connected accounts."
        }
      ]
    }
  ],
  "access_mechanism_ledger": [
    {
      "mechanism": "HTTP API reference",
      "disposition": "interface",
      "detail": "Dropbox API (HTTP/RPC v2)"
    },
    {
      "mechanism": "Webhooks",
      "disposition": "interface",
      "detail": "Webhooks"
    },
    {
      "mechanism": "Linux CLI (dropbox command)",
      "disposition": "interface",
      "detail": "Linux desktop CLI (dropbox command)"
    },
    {
      "mechanism": "Web client (first-party surface)",
      "disposition": "interface",
      "detail": "Web application"
    },
    {
      "mechanism": "Mobile client (first-party surface)",
      "disposition": "interface",
      "detail": "Mobile application"
    },
    {
      "mechanism": "Desktop client (first-party surface)",
      "disposition": "interface",
      "detail": "Desktop application"
    },
    {
      "mechanism": "Terminal/TUI surface",
      "disposition": "excluded",
      "detail": "Linux CLI is command-based only; no persistent navigable TUI documented."
    },
    {
      "mechanism": "dbxcli (Dropbox GitHub org CLI)",
      "disposition": "excluded",
      "detail": "Client wrapper over the HTTP API, explicitly stated to be not a formally supported Dropbox product."
    },
    {
      "mechanism": "Pre-built Components (Chooser, Saver, Embedder)",
      "disposition": "excluded",
      "detail": "Embeddable developer integration widgets, not standalone access channels; would be Interactive if counted, a channel already observed."
    },
    {
      "mechanism": "Extensions",
      "disposition": "excluded",
      "detail": "Extension point to launch third-party apps from a file; part of the web/desktop UI, not a distinct access channel."
    },
    {
      "mechanism": "SDKs (Swift, Objective-C, Python, .NET, Java, JavaScript)",
      "disposition": "excluded",
      "detail": "Client libraries, not interfaces."
    },
    {
      "mechanism": "Documentation MCP server",
      "disposition": "excluded",
      "detail": "Provides AI access to the API documentation, not to the Dropbox service."
    },
    {
      "mechanism": "Docs embedded 'Ask AI' assistant",
      "disposition": "excluded",
      "detail": "Documentation help assistant, not a service access channel."
    },
    {
      "mechanism": "Integrations index (app-integrations)",
      "disposition": "excluded",
      "detail": "Third-party integrations, not first-party access mechanisms."
    },
    {
      "mechanism": "Dropbox Dash",
      "disposition": "excluded",
      "detail": "Separate product (dash.dropbox.com), out of scope for the core Dropbox service."
    },
    {
      "mechanism": "Dropbox Sign",
      "disposition": "excluded",
      "detail": "Separate product (formerly HelloSign), out of scope for the core Dropbox service."
    }
  ],
  "channel_evidence": {
    "Interactive": "observed",
    "Agentic": "no_evidence_observed",
    "Conversational": "no_evidence_observed",
    "Event": "observed",
    "Programmatic": "observed"
  },
  "number_of_interfaces": 6,
  "multi_interface": true,
  "number_of_channels": 3,
  "multi_channel": true
}
```
