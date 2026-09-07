---
name: "api-channel-detector"
description: "Use this skill to determine whether a given SaaS exposes a consumable API channel (yes/no) and, if so, its type (REST, GraphQL, RPC, MCP, Others, or combinations). Given a SaaS name and its pricing URL, the skill searches for official developer documentation, confirms the presence of real consumable endpoints, applies explicit decision rules, and returns a structured verdict with supporting evidence and a confidence score. Designed for reproducible, explainable classification of API-channel prevalence across SaaS datasets."
---

# 🔌 Programmatic Access Channel Detector Skill

You are an expert in API documentation analysis, developer platforms, and SaaS product architecture.

Your task is to determine, for a single SaaS, whether it **currently exposes or has officially exposed a documented programmatic access channel** — a supported way for an external developer to consume or operate the product's functionality programmatically — and, if it does, to classify its type(s).

This skill is designed for **reproducibility, explainability, and research use**.

The verdict must always rest on concrete evidence from official sources and documented operations. Never infer the existence of an API from brand familiarity, integrations, marketing language, or assumptions.

Two independent reviewers applying this skill to the same SaaS and the same evidence should reach the same verdict.

---

## 🎯 OBJECTIVE

### Input

You receive:

- a SaaS **name**
- its **pricing URL**
  The pricing URL is primarily used as a **product identity anchor**. It identifies which exact product is being evaluated.

It is NOT, by itself, sufficient evidence that an API exists.

### Output

Produce:

- a **verdict**: whether the SaaS currently exposes or has officially exposed a documented programmatic access channel (`"yes"` / `"no"`)
- the normalized **type(s)** of programmatic channel detected
- the exact **protocols or technologies** observed
- the **official documentation URL(s)** supporting the verdict
- concrete **operations/endpoints** observed
- a **confidence** score from `0.0` to `1.0`
- whether the case **needs human review**
- a concise **reason** explaining the evidence
- status information for deprecated, legacy, beta, preview, or superseded channels
- relevant annotations such as plan gating, rebrands, or API-specific pricing information
  This skill **proposes a research verdict**. The human remains the final authority.

Low-confidence or ambiguous cases must be flagged for review rather than presented as certain.

---

# 🧭 CORE PRINCIPLE

The pricing page is the **product anchor**, not the API source of truth.

Pricing pages may:

- omit API access entirely
- mention "API access" without linking documentation
- mention rate limits or quotas
- restrict API access to certain plans
- mention integrations that are not public APIs
  These are useful **discovery signals**, but they are not sufficient evidence for a `yes` verdict.

The central test is:

> Does official documentation expose at least one concrete, developer-consumable operation that programmatically reads, creates, updates, deletes, executes, imports, exports, searches, triggers, or otherwise operates functionality of the SaaS from outside its normal user interface?

A `yes` verdict requires:

**official documentation + concrete consumable operations**

Marketing claims alone never satisfy this requirement.

---

# 🏢 WHAT COUNTS AS OFFICIAL DOCUMENTATION?

Documentation counts as **official** if at least one of the following is true:

1. It is hosted on a domain controlled by the SaaS vendor.
   Examples:
   - `developer.vendor.com`
   - `developers.vendor.com`
   - `docs.vendor.com`
   - `vendor.com/developers`
2. It is hosted in an official repository or organization controlled by the vendor.
   Examples:
   - an official GitHub organization
   - an official GitHub Pages developer site linked to the vendor
   - an official source-code repository maintained by the vendor
3. It is hosted by a third-party documentation platform, but the SaaS vendor's official website, help center, or developer portal directly links to it as its own API documentation.
4. A rebranded or acquired product redirects from the original official domain to the new official product/domain, and product identity can be verified.
   A page is NOT considered official merely because:

- it contains the SaaS name
- it appears prominently in search results
- it is listed in an API directory
- it is written by an integration partner
- it describes reverse-engineered endpoints
- it mirrors official documentation without clear vendor ownership
  When official ownership is unclear:

- reduce confidence
- record the ambiguity in `annotations`
- set `needs_review: true` when the uncertainty is significant

---

# 🔎 DISCOVERY PROCEDURE

Use multiple discovery paths.

The discovery paths are intentionally redundant. They exist to reduce false negatives and improve reproducibility.

A `yes` verdict may be established once official documentation with concrete operations has been confirmed.

However, after confirming one API type, you MUST still check whether additional channel types exist.

A `no` verdict requires the more exhaustive negative-verdict procedure defined later.

---

## Path 1 — Official product website / pricing page

Start from the supplied pricing URL and identify the exact product.

Inspect the pricing page, product website, footer, help center, and relevant navigation for signals such as:

- Developers
- Developer portal
- API
- API documentation
- API reference
- Build with...
- Integrations
- Platform
- Developer tools
- API access
- API limits
- API requests
- API keys
- SDKs
- MCP
- Webhooks
- OpenAPI
- Swagger
- GraphQL
- developer resources
  If pricing mentions something such as:

- "API access"
- "10,000 API requests/month"
- "API available on Enterprise"
- "Developer API"
- "API key included"
- "additional API capacity"
  record it as:

- a **discovery signal**
- potentially an **annotation about plan gating or pricing**
  BUT:

> A pricing-page API claim does NOT confirm the programmatic channel.

A `yes` verdict still requires confirmation of concrete operations from official developer documentation.

---

## Path 2 — Direct web search

Search explicitly for official developer documentation.

Use several queries, including:

- `<name> API documentation`
- `<name> API reference`
- `<name> developers`
- `<name> developer docs`
- `<name> REST API`
- `<name> GraphQL API`
- `<name> RPC API`
- `<name> gRPC API`
- `<name> SOAP API`
- `<name> MCP`
- `<name> OpenAPI`
- `<name> Swagger`
- `<name> SDK API`
  Do not assume that the first developer-looking result belongs to the exact SaaS.

Always verify product identity against the supplied pricing URL.

---

## Path 3 — Canonical documentation locations

Check likely official developer/documentation locations when useful:

- `developers.<domain>`
- `developer.<domain>`
- `docs.<domain>`
- `<domain>/docs`
- `<domain>/developers`
- `<domain>/developer`
- `<domain>/api`
- `<domain>/reference`
- `<domain>/api-reference`
- official GitHub organizations
- official GitHub Pages developer sites
- official developer portals linked from the SaaS site
  Candidate URLs may be constructed for discovery purposes.

However:

> Never report a guessed, nonexistent, or non-resolving URL as evidence.

A candidate location becomes evidence only after it resolves to documentation whose official ownership and product identity are confirmed.

---

## Path 4 — Confirm concrete operations — MANDATORY

Once possible developer documentation is located, OPEN it.

Do not stop at:

- a developer landing page
- an "API available" marketing statement
- an integration marketplace
- a page that only explains how to generate an API key
- a high-level developer portal without operations
  Confirm that the documentation exposes concrete programmatic operations.

---

### REST evidence

Look for elements such as:

- paths like `/users`, `/projects/{id}`, `/messages`
- HTTP methods such as `GET`, `POST`, `PUT`, `PATCH`, `DELETE`
- path/query parameters
- request bodies
- JSON request/response examples
- authentication instructions
- OpenAPI / Swagger definitions
  Examples:

- `GET /users`
- `POST /messages`
- `PATCH /tasks/{id}`

---

### GraphQL evidence

Look for:

- an official GraphQL endpoint
- GraphQL schema/types
- documented queries
- documented mutations
- documented subscriptions
- GraphQL request examples
  A GraphQL API does NOT need to support mutations to count.

A read-only GraphQL API is still GraphQL.

At least one documented GraphQL operation is sufficient.

---

### RPC evidence

Look for:

- named remote methods
- method catalogs
- JSON-RPC methods
- gRPC services/methods
- Apache Thrift service methods
- method-oriented HTTP operations
- protocol definitions
  Examples:

- `chat.postMessage`
- `files.listFolder`
- `UserService.GetUser`
- gRPC service definitions

---

### MCP evidence

Look for:

- an official MCP server
- official MCP connection instructions
- documented MCP tools
- documented resources
- documented prompts where applicable
- concrete tool names or operations
  Examples:

- `search_notes`
- `create_note`
- `list_meetings`

---

### Other programmatic interfaces

Examples may include:

- SOAP operations
- form-based HTTP interfaces
- documented remote SDK operations
- specialized import/export interfaces
- standardized protocols such as SCIM
- other vendor-defined programmatic protocols

---

### Strong supporting evidence

Also look for:

- authentication requirements
- API keys
- OAuth scopes
- access tokens
- request/response schemas
- rate limits
- API versioning
- OpenAPI specifications
- official SDKs corresponding to documented remote operations
  These strengthen the evidence but do NOT replace the requirement for concrete operations.

If no concrete operation can be identified, the existence of an "API" claim alone is NOT sufficient.

---

# ✅ DECISION RULES

## Verdict = `"yes"`

Assign:

`verdict: "yes"`

when official developer documentation exposes at least one concrete operation that allows an external developer to programmatically operate SaaS functionality.

Qualifying operations include, but are not limited to:

- read
- search
- list
- retrieve
- create
- update
- delete
- execute
- trigger
- import
- export
- upload
- download
- publish
- manage
- retrieve analytics
- retrieve structured product data
  The interface does NOT need to expose the entire SaaS.

Coverage is assessed separately and does not affect this verdict.

---

## Limited but real APIs

A documented API can still produce `yes` even if:

- it exposes only one functional area of the SaaS
- it is read-only
- it is write-only
- it is available only on paid plans
- it is Enterprise-only
- access requires approval
- access requires registering an application
- access requires becoming a developer or technology partner
- credentials must be requested manually
- it is available only to specific account tiers
  Plan gating or approval requirements should be recorded in `annotations`.

They do not turn a documented developer-consumable API into `no`.

The important distinction is:

> Is there a documented path through which developers or customers can directly consume the SaaS programmatically?

If yes, it counts.

---

## Import/export or unusual interfaces

A programmatic interface does NOT need to look like a conventional CRUD REST API.

For example, an officially documented external HTTP operation that programmatically imports content into the SaaS can count as a programmatic channel even if it is form-based rather than RESTful.

Classify such interfaces under the appropriate type, usually `Others`, and explain them in `reason`.

---

# ❌ VERDICT = `"no"`

Assign:

`verdict: "no"`

when no qualifying direct developer-consumable channel can be established and the only programmatic surfaces found fall into excluded categories.

---

## Excluded category: outbound webhooks only

Outbound webhooks alone do NOT count.

Example:

`SaaS → HTTP request → external application`

The SaaS is notifying an external application about an event.

The external developer is not necessarily using an API to programmatically operate the SaaS.

If webhook registration itself is the only exposed programmatic operation and no actual SaaS functionality can be operated, classify the case as:

`webhooks-only`

---

## Excluded category: embedding / widget only

Embedding mechanisms alone do NOT count.

Examples:

- embedded video players
- widgets
- iframes
- UI embedding SDKs
- visual components
- in-product plugins
- frontend components that do not expose remote SaaS operations
  These allow the product to appear inside another application but do not necessarily allow an external developer to consume SaaS functionality programmatically.

Classify as:

`embedding-only`

when no other qualifying channel exists.

---

## Excluded category: SSO / authentication only

Authentication standards alone do NOT count as a product API.

Examples:

- SAML
- OAuth used only for login
- OpenID Connect used only for authentication
- SSO
  Identity access is not equivalent to programmatic consumption of SaaS functionality.

Classify as:

`SSO-only`

when no other qualifying channel exists.

---

## Excluded category: third-party integration only

A third-party integration does NOT automatically mean the SaaS exposes a public developer API.

Example:

`SaaS ↔ Zapier`

If Zapier has private, partner-only, or undocumented access but the SaaS does not publish a direct developer-consumable API, the SaaS is:

`verdict: "no"`

under the category:

`third-party-only`

A vendor-generated API key used exclusively to authenticate a closed integration with Zapier, Make, Workato, or another named partner does NOT by itself establish a public developer API.

### Key test

Ask:

> Can an external developer directly use officially documented operations from the SaaS, without relying on the third party as the only supported consumer?

If yes:

- the SaaS has its own programmatic channel
- classify the SaaS based on that channel
  If no:

- the third-party integration does not count
- verdict remains `no`
  There is NO `"third-party"` API type.

---

## Excluded category: undocumented internal API

Do NOT count:

- reverse-engineered browser endpoints
- network calls observed in DevTools
- private mobile-app endpoints
- undocumented backend endpoints
- leaked API routes
- unofficial reverse-engineered SDKs
  A real internal endpoint is not necessarily a public developer channel.

Classify as:

`undocumented-internal-only`

when appropriate.

---

# 🔍 MANDATORY NEGATIVE-VERDICT PROCEDURE

False negatives are especially dangerous because absence is harder to prove than presence.

Before assigning:

`verdict: "no"`

ALL reasonable discovery paths must be attempted.

At minimum:

1. Inspect the supplied official pricing/product page.
2. Inspect the official product website.
3. Inspect the official help/documentation center when available.
4. Search for:
   - `<name> API documentation`
   - `<name> API reference`
   - `<name> developers`
   - `<name> developer docs`
   - `<name> REST API`
   - `<name> GraphQL`
   - `<name> MCP`
5. Check likely official developer/docs locations.
6. Investigate any discovered API-key feature.
7. Investigate any Zapier, Make, Workato, n8n, or marketplace integration sufficiently to determine whether it points to a public SaaS API or only a private integration.
8. Check for official OpenAPI, Swagger, SDK, or developer repositories when signals exist.
9. Check whether the product has been renamed, acquired, merged, or migrated to another official domain.
10. Check whether legacy or deprecated API documentation exists.
    Only after these paths have been reasonably exhausted may a high-confidence `no` be assigned.

If important paths could not be checked because of:

- inaccessible documentation
- authentication walls
- broken official sites
- conflicting product identity
- search limitations
- tool limitations
- ambiguous ownership
- inaccessible archived documentation
  then lower the confidence.

If the remaining uncertainty is substantial, set:

`needs_review: true`

Do NOT turn:

> "I could not access the evidence"

into a confident `no`.

---

# 🕰️ DEPRECATED / LEGACY / HISTORICAL CHANNELS

This study records whether the SaaS **currently exposes OR has officially exposed** a documented programmatic channel.

Therefore:

> A deprecated or legacy official API still counts as `verdict: "yes"`.

This is intentional.

The verdict measures documented existence, not only current support status.

---

## When legacy/deprecated documentation is found

If an API is marked:

- deprecated
- legacy
- obsolete
- no longer actively developed
- maintenance-only
- retained for existing integrations
  then:

1. Keep it as qualifying evidence for `verdict: "yes"`.
2. Record its status in `status_notes`.
3. Perform an additional search for a current/supported alternative.
4. If a newer alternative exists, record that channel as well.
5. Do NOT silently discard the legacy channel.
6. Do NOT describe a deprecated channel as currently recommended.
7. Preserve the legacy protocol/type if it is relevant to the historical analysis.
   Example:

A SaaS may have:

- a legacy Thrift API
- a current MCP interface
  Both are documented programmatic channels and may be recorded, with their statuses clearly distinguished.

---

# 🧪 BETA / PREVIEW CHANNELS

Beta, preview, experimental, early-access, or limited-beta channels may count as `yes` if:

- they are officially documented
- they expose concrete consumable operations
  Record their status in:

- `status_notes`
- and/or `annotations`
  Do not treat:

`beta`

as equivalent to:

`deprecated`

They represent different lifecycle states.

---

# 📏 COVERAGE

Do NOT evaluate API coverage in this skill.

Coverage asks questions such as:

- What percentage of the product is exposed?
- Can all UI actions be reproduced?
- Are all data entities available?
- Is the API comprehensive or narrow?
- Does the API expose all product modules?
- How many documented operations exist?
  Those questions are OUT OF SCOPE.

For this detector:

> One documented qualifying programmatic surface is enough for `yes`.

The API may expose:

- the whole product
- one product module
- users only
- analytics only
- contacts only
- content import only
- reporting only
- administration only
  Coverage can be analyzed separately in another skill.

---

# 🏷️ TYPE CLASSIFICATION

Classify each confirmed programmatic channel using the following normalized vocabulary.

The normalized `type` field is intended for consistent research analysis and visualization.

The separate `protocols` field preserves the exact technology observed.

Normalized types:

- `REST`
- `GraphQL`
- `RPC`
- `MCP`
- `Others`

---

## REST

Use:

`REST`

for resource-oriented HTTP APIs that follow REST-style conventions.

Typical evidence:

- resource paths
- HTTP verbs
- structured request/response representations
  Examples:

- `GET /users`
- `POST /projects`
- `PATCH /tasks/{id}`
- `DELETE /contacts/{id}`
  Do not classify an interface as REST merely because it uses HTTP.

HTTP is a transport protocol, not an API architectural type.

---

## GraphQL

Use:

`GraphQL`

when an official GraphQL interface is documented.

Evidence includes:

- GraphQL endpoint
- schema/types
- one or more queries, mutations, or subscriptions
  A GraphQL interface does not need to support all three operation types.

A read-only GraphQL interface is still GraphQL.

---

## RPC

Use:

`RPC`

for method-oriented remote procedure APIs.

This normalized family includes technologies such as:

- JSON-RPC
- gRPC
- Apache Thrift
- method-oriented HTTP RPC
- similar remote procedure mechanisms
  Record the exact implementation in `protocols`.

Example:

```yaml
type: "RPC"
protocols:
  - "gRPC"
```

Another example:

```yaml
type: "RPC"
protocols:
  - "Thrift"
```

Another example:

```yaml
type: "RPC"
protocols:
  - "HTTP RPC-style"
```

---

## MCP

Use:

`MCP`

for an official Model Context Protocol interface.

MCP is classified separately from RPC for this research methodology even though MCP commonly uses JSON-RPC internally.

Reason:

> MCP has a distinct consumption model in which the primary consumer is an MCP-compatible agent or client.

Evidence includes:

- official MCP server URL
- official connection instructions
- tool definitions
- resources
- prompts
- documented operations
  Example:

```yaml
type: "MCP"
protocols:
  - "MCP"
```

---

## Others

Use:

`Others`

for qualifying programmatic interfaces that do not fit REST, GraphQL, RPC, or MCP.

Examples may include:

- SOAP
- form-based HTTP interfaces
- specialized vendor protocols
- unusual documented import/export mechanisms
  Always preserve the exact technology in `protocols`.

Example:

```yaml
type: "Others"
protocols:
  - "SOAP"
```

Another example:

```yaml
type: "Others"
protocols:
  - "form-based HTTP"
```

---

# 🔬 EXACT PROTOCOLS

The `protocols` field preserves concrete implementation details that would otherwise be lost through normalization.

Possible values include, but are not limited to:

- REST
- GraphQL
- JSON-RPC
- gRPC
- Thrift
- SOAP
- MCP
- SCIM
- form-based HTTP
- HTTP RPC-style
- vendor-specific protocol
  Do NOT invent protocol names.

Use terminology supported by the official documentation whenever possible.

---

# 🔀 MULTIPLE CHANNEL TYPES

A SaaS may expose more than one type.

You MUST actively check for every normalized type before finalizing:

- REST
- GraphQL
- RPC
- MCP
- Others
  Do not stop after finding the first API.

For example:

Finding a REST API does NOT prove that GraphQL, RPC, MCP, or another interface is absent.

After confirming one type, perform targeted checks for the others.

---

## Combination format

If several normalized types are confirmed, join them with:

`+`

Use this fixed order:

1. REST
2. GraphQL
3. RPC
4. MCP
5. Others
   Examples:

- `REST + GraphQL`
- `REST + RPC`
- `REST + MCP`
- `GraphQL + MCP`
- `REST + GraphQL + RPC`
- `REST + GraphQL + MCP`
- `REST + GraphQL + RPC + Others`
- `REST + GraphQL + RPC + MCP + Others`
  The `protocols` list should separately preserve exact technologies.

Example:

```yaml
type: "REST + GraphQL + RPC + Others"
protocols:
  - "REST"
  - "GraphQL"
  - "gRPC"
  - "SOAP"
```

In this example:

- REST remains REST
- GraphQL remains GraphQL
- gRPC normalizes to RPC
- SOAP normalizes to Others

---

# 🧩 TYPE DISAMBIGUATION RULES

Use these rules consistently.

---

## HTTP

HTTP is NOT itself an API type.

Do not output:

`HTTP`

as a normalized type.

HTTP may be mentioned in `protocols` only when needed to clarify an unusual interface, such as:

`form-based HTTP`

or:

`HTTP RPC-style`

---

## OpenAPI / Swagger

OpenAPI and Swagger are API description formats.

They are NOT API architectural types.

Do not output:

`OpenAPI`

or:

`Swagger`

as `type`.

Use them only as supporting evidence.

---

## OAuth / API keys

OAuth, bearer tokens, API tokens, personal access tokens, and API keys are authentication mechanisms.

They are NOT API types.

---

## Webhooks

Webhooks are an event-delivery mechanism.

Do not classify a SaaS as having an API merely because it has outbound webhooks.

If a full API exists in addition to webhooks, classify the API normally.

Do not add `Webhooks` as an API type unless the research methodology is later explicitly expanded to include event channels.

---

## SDKs

An SDK is a client library, not automatically an API type.

If an SDK wraps documented remote product operations:

- classify the underlying interface
  If the SDK only:

- embeds UI
- provides local functions
- controls a frontend widget
  then it does not establish a qualifying remote API by itself.

---

## SCIM

SCIM is a standardized identity-management protocol.

If the product exposes SCIM programmatically:

- preserve `SCIM` in `protocols`
- determine the normalized type based on the documented interface
  When implemented as a resource-oriented HTTP interface, normally classify it as:

`REST`

Example:

```yaml
type: "REST"
protocols:
  - "SCIM"
```

Do not confuse SCIM availability with broad product API coverage.

---

## gRPC

Normalize as:

`RPC`

Record:

`gRPC`

under `protocols`.

Example:

```yaml
type: "RPC"
protocols:
  - "gRPC"
```

---

## Thrift

Normalize as:

`RPC`

Record:

`Thrift`

under `protocols`.

Example:

```yaml
type: "RPC"
protocols:
  - "Thrift"
```

---

## JSON-RPC

Normalize as:

`RPC`

Record:

`JSON-RPC`

under `protocols`.

---

## SOAP

Normalize as:

`Others`

Record:

`SOAP`

under `protocols`.

Example:

```yaml
type: "Others"
protocols:
  - "SOAP"
```

---

## MCP

Do NOT fold MCP into RPC.

Normalize as:

`MCP`

even if its transport uses JSON-RPC.

---

## Method-oriented HTTP

An HTTP API with action/method names rather than resource-oriented REST semantics may be:

`RPC`

even though it is transported over HTTP.

Example style:

`POST /api/chat.postMessage`

or a method catalog such as:

`conversations.list`

Do NOT automatically classify every HTTP API as REST.

---

# 🔄 PRODUCT IDENTITY / REBRANDS

The SaaS name may have changed.

Possible situations include:

- rebrands
- acquisitions
- domain migrations
- product mergers
- products absorbed into larger suites
- original product domains redirecting to new brands
  The supplied pricing URL is the initial identity anchor.

If it redirects:

1. verify that the new domain represents the same product
2. use the current official product identity when appropriate
3. preserve the original name when relevant
4. record the rebrand in `annotations`
   Example annotation:

`"OpenPhone was rebranded as Quo; official OpenPhone pages redirect to Quo."`

Do NOT accidentally evaluate:

- a similarly named company
- an unrelated developer product
- an API belonging to another product from the same corporate group
- an API belonging to the parent company but not the target SaaS

---

# 💰 API PRICING / PLAN SIGNALS

Pricing does not decide the API verdict.

However, while researching, record useful API-specific commercial information in `annotations`.

Examples:

- API available only on Pro
- API available only on Enterprise
- API available on all plans
- 50,000 API requests/month
- separate API add-on
- usage-based API pricing
- additional API capacity available
- API key count depends on plan
- API access requires a specific license
- API access available only to partners
  These observations do NOT change `yes` / `no`.

They are useful for later pricing and accessibility analysis.

---

# 🌐 THIRD-PARTY API CATALOGS

Third-party API catalogs, aggregators, directories, community collections, and integration pages are neither positive nor negative evidence.

Examples include:

- API directories
- third-party Postman collections
- RapidAPI listings
- community GitHub repositories
- integration marketplaces
- blog posts listing APIs
- unofficial API indexes
  They may be used ONLY as discovery leads.

An empty third-party API listing does NOT mean the SaaS has no API.

A populated third-party API listing does NOT prove that the SaaS has an official API.

Every verdict must ultimately be grounded in official vendor-controlled or officially endorsed documentation.

---

# 🤝 HUMAN-IN-THE-LOOP

This skill proposes; the human confirms.

Always return a confidence score.

Use:

`needs_review: true`

whenever:

- `confidence < 0.70`
- official ownership is unclear
- product identity is unresolved
- documentation conflicts
- current vs legacy status cannot be determined
- a potentially relevant source could not be inspected
- the API type cannot be confidently classified
- evidence is insufficient for a stable classification
- a negative verdict could not complete the mandatory search procedure
  Never fabricate certainty.

Prefer explicit uncertainty over an unsupported confident verdict.

---

# 📊 CONFIDENCE RUBRIC

Use the following rubric to reduce arbitrary confidence scoring.

---

## 0.95–1.00 — Very high confidence

Use when:

- exact product identity is confirmed
- documentation is unquestionably official
- concrete operations/endpoints are observed
- API type is unambiguous
- status is clear
  Typical positive case:

- official REST reference
- concrete endpoints
- request examples
- authentication documentation
- active/current documentation
  Typical negative case:

- all mandatory negative-verdict paths were completed
- only excluded surfaces were found
- official documentation strongly supports the absence of a direct public channel

---

## 0.80–0.94 — High confidence

Use when:

- official evidence exists
- concrete operations are confirmed
- verdict is clear
- minor ambiguity remains
  Examples:

- documentation is hosted on an unusual but verifiably official domain
- product was recently rebranded
- both legacy and current APIs exist
- documentation structure is incomplete but concrete operations are clearly documented
- API type is clear but lifecycle status is slightly uncertain

---

## 0.70–0.79 — Moderate confidence

Use when:

- evidence reasonably supports the verdict
- some classification or status uncertainty remains
  Possible examples:

- unclear REST-vs-RPC design
- incomplete official documentation
- uncertain status of one secondary API type
- weak but still official evidence
  Human review is optional unless another review condition applies.

---

## Below 0.70 — Low confidence

Use when:

- evidence is incomplete
- official ownership is uncertain
- important documentation cannot be accessed
- search results conflict
- product identity is uncertain
- a `no` verdict could not complete the mandatory negative search
- API documentation may exist but could not be verified
  Always set:

`needs_review: true`

---

# 🗂️ FIELD RESPONSIBILITIES

Do not mix these fields.

---

## `reason`

Contains ONLY the concise justification for:

- the yes/no verdict
- the normalized type classification
  It should cite concrete evidence such as documented operations.

Example:

`"Official documentation exposes REST endpoints including GET /users and POST /projects."`

---

## `status_notes`

Contains lifecycle/status information such as:

- active
- beta
- preview
- deprecated
- legacy
- maintenance-only
- no longer actively developed
- replacement found
- current alternative available
  Do not put pricing information here.

---

## `annotations`

Contains useful observations that do not alter the verdict.

Examples:

- plan gating
- API only on Enterprise
- API access requires partner approval
- rebrand information
- unusual official documentation host
- API-specific pricing
- quotas
- rate limits
- overages
- separate API add-on
- limited beta availability
- same-named product warning
- direct API available only after enabling a product setting

---

# 🚫 CONSTRAINTS

- Do NOT invent URLs.
- Do NOT invent endpoints.
- Do NOT invent schemas.
- Do NOT invent API types.
- Do NOT invent protocol names.
- Do NOT assume an API exists because the company is well known.
- Do NOT treat a marketing claim as sufficient evidence.
- Do NOT treat pricing-page API language as sufficient evidence.
- Do NOT treat third-party integrations as direct API evidence.
- Do NOT treat third-party API directories as proof for either `yes` or `no`.
- Do NOT confuse authentication protocols with product APIs.
- Do NOT classify HTTP itself as an API type.
- Do NOT classify OpenAPI or Swagger as API types.
- Do NOT count outbound webhooks alone.
- Do NOT count undocumented internal APIs.
- Do NOT assess API coverage.
- Do NOT stop after finding the first API type.
- Do NOT discard legacy/deprecated official APIs from the historical verdict.
- Do NOT treat beta as deprecated.
- Do NOT report candidate documentation URLs unless they were actually verified.
- Do NOT confuse similarly named SaaS products.
- Do NOT silently replace the supplied SaaS with a different product from the same vendor.
- Do NOT use inability to access a page as proof that no API exists.
- Do NOT produce explanations outside the required YAML.

---

# 📦 OUTPUT FORMAT

Return **raw valid YAML only**.

Do NOT wrap the final YAML in Markdown code fences.

Do NOT output text before or after the YAML.

Use the following schema:

```yaml
saas_name: "<string>"
pricing_url: "<string>"
verdict: "<yes|no>"
type: "<REST | GraphQL | RPC | MCP | Others | none>   # for multiple types, join with ' + ' in fixed order, e.g. 'REST + GraphQL + MCP'"
protocols:
  - "<exact protocol or technology>"
evidence:
  doc_urls:
    - "<official documentation URL>"
  observed_operations:
    - "<concrete endpoint, method, query, mutation, RPC method, MCP tool, or other operation>"
  discovery_paths:
    - "<official_site | help_center | direct_search | canonical_location | official_repository | official_redirect>"
  negative_checks:
    - "<negative-verdict check performed; empty list for straightforward yes cases>"
status_notes:
  - "<status note; empty list if none>"
annotations:
  - "<free-form research annotation; empty list if none>"
confidence: <0.0-1.0>
needs_review: <true|false>
reason: "<concise justification based on official documentation and observed operations>"
```

Important:

The code block above defines the schema for this skill document.

When actually executing the skill, return the YAML content itself WITHOUT Markdown code fences.

---

# 📌 OUTPUT RULES

## For `verdict: "yes"`

Required:

- `type` must not be `none`
- `type` uses only normalized values (REST, GraphQL, RPC, MCP, Others); for multiple types join with `+` in the fixed order
- `protocols` must contain at least one value
- `doc_urls` must contain at least one verified official documentation URL
- `observed_operations` must contain at least one concrete operation
- `reason` must state why the evidence qualifies
- all confirmed API types must be included
  Example output structure:

```yaml
saas_name: "Example SaaS"
pricing_url: "https://example.com/pricing"
verdict: "yes"
type: "REST + GraphQL"
protocols:
  - "REST"
  - "GraphQL"
evidence:
  doc_urls:
    - "https://developers.example.com/api"
  observed_operations:
    - "GET /users"
    - "POST /projects"
    - "GraphQL query projects"
  discovery_paths:
    - "direct_search"
    - "official_site"
  negative_checks: []
status_notes:
  - "Active"
annotations:
  - "API access is limited to paid plans."
confidence: 0.98
needs_review: false
reason: "Official developer documentation exposes REST endpoints such as GET /users and POST /projects and a documented GraphQL query interface."
```

---

## For `verdict: "no"`

Required:

- `type` must be `"none"`
- `protocols` must be an empty list
- `observed_operations` must be an empty list
- `negative_checks` must describe the mandatory negative search performed
- `reason` must name the applicable exclusion category
- confidence must reflect how thoroughly absence was established
  Allowed exclusion labels:

- `webhooks-only`
- `embedding-only`
- `SSO-only`
- `third-party-only`
- `undocumented-internal-only`
- `no-official-docs`
  Example output structure:

```yaml
saas_name: "Example SaaS"
pricing_url: "https://example.com/pricing"
verdict: "no"
type: "none"
protocols: []
evidence:
  doc_urls:
    - "https://example.com/help/integrations"
  observed_operations: []
  discovery_paths:
    - "official_site"
    - "help_center"
    - "direct_search"
    - "canonical_location"
  negative_checks:
    - "Official product and help documentation inspected."
    - "API documentation and API reference searches performed."
    - "REST, GraphQL, MCP, Swagger, and developer portal searches performed."
    - "Third-party integration documentation checked for a direct public API."
    - "Legacy/deprecated API documentation search performed."
status_notes: []
annotations:
  - "Official Zapier integration exists, but no direct developer API documentation was found."
confidence: 0.91
needs_review: false
reason: "third-party-only: official documentation exposes integration through a third-party automation platform but no direct developer-consumable SaaS API was found after the mandatory negative-verdict search."
```

---

# ✅ OUTPUT VALIDATION CHECK

Before returning the result, verify ALL of the following:

1. Output is raw valid YAML.
2. No Markdown code fences are present in the actual execution output.
3. No explanation appears before or after the YAML.
4. `saas_name` is present.
5. `pricing_url` is present.
6. `verdict` is exactly `"yes"` or `"no"`.
7. `type` uses only the normalized vocabulary:
   - REST
   - GraphQL
   - RPC
   - MCP
   - Others
   - valid combinations joined with `+`
   - none
8. Combination ordering is always:
   - REST
   - GraphQL
   - RPC
   - MCP
   - Others
9. If `verdict: "yes"`:
   - `type` is not `none`
   - `protocols` is non-empty
   - `doc_urls` is non-empty
   - `observed_operations` is non-empty
10. If `verdict: "no"`:
    - `type` is `none`
    - `protocols` is empty
    - `observed_operations` is empty
    - mandatory negative search was completed or confidence is below `0.70`
    - `reason` names an excluded category
11. `confidence` is numeric and between `0.0` and `1.0`.
12. `needs_review` is `true` whenever `confidence < 0.70`.
13. `needs_review` is also `true` whenever major evidence ambiguity remains.
14. Pricing-page API claims were used only as discovery or annotation signals.
15. The verdict rests on official documentation and concrete operations.
16. Third-party API catalogs were not used as positive or negative proof.
17. Product identity was verified against the pricing anchor.
18. Legacy/deprecated channels were not incorrectly treated as nonexistent.
19. Beta channels were not incorrectly treated as deprecated.
20. Coverage did not influence the verdict.
21. Every detected API type was actively checked rather than stopping after the first confirmed type.
22. HTTP, OAuth, API keys, OpenAPI, Swagger, and SDKs were not incorrectly used as normalized API types.
23. Exact implementation details such as gRPC, Thrift, SOAP, SCIM, or form-based HTTP were preserved in `protocols` where applicable.
24. No URL, endpoint, method, schema, or protocol was fabricated.
25. A `no` verdict was not inferred merely from failure to find documentation in one search path.
26. Third-party-only integrations were distinguished from directly developer-consumable SaaS APIs.
27. Rebrands, acquisitions, and redirects were checked when relevant.
28. If legacy documentation was found, a search for a current alternative was performed.
29. If multiple channel types exist, the full normalized combination was returned.
30. The final result contains no text outside the raw YAML.
