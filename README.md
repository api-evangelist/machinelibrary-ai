# Space Frontiers

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Space Frontiers is a Wyoming corporation whose search and AI product, Machine Library (formerly Space Frontiers search, moved to machinelibrary.ai on 2026-09-12), is a full-text retrieval API and hosted MCP server over a corpus the provider describes as multi-billion documents: peer-reviewed papers (CrossRef, PubMed, arXiv), books, USPTO patents, Wikipedia, technical standards, YouTube transcripts, and live Reddit, Telegram and Discord posts. It is built for AI agents doing literature review, fact-checking, citation walking and grounded research synthesis, returning compact reranked hits with canonical source URIs (DOI, arXiv, PMID, ISBN) and token-bounded full text. Three surfaces share one account and API key: a REST API at api.machinelibrary.ai (OpenAPI 3.1, pay-as-you-go), a Streamable-HTTP MCP server at mcp.machinelibrary.ai (OAuth 2.1 with PKCE and RFC 7591 dynamic registration against the issuer api.machinelibrary.ai, scope search, or a Bearer API key), and an A2A agent at machinelibrary.ai/a2a. It also ships a PDF/EPUB/DJVU-to-Markdown recognition API and Stripe-settled prepaid credit packages for agents (ACP checkout, MPP top-up). The company also publishes Hermes, an open-source Rust search engine with a gRPC contract and Python/TypeScript clients.

**Areas:** Research · Scholarly Search · Full-Text Search · Retrieval · RAG · Patents · Documents · OCR · Document Recognition · MCP · A2A · Agent-Native

## Space Frontiers on APIs.io

Everything profiled for Space Frontiers is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/machinelibrary-ai/](https://apis.io/providers/machinelibrary-ai/)** — or go straight to one of the APIs or properties below.

### APIs (9)

- [Machine Library MCP Server](https://apis.io/apis/machinelibrary-ai/machine-library-mcp-server/) — Hosted Streamable-HTTP MCP server at https://mcp.machinelibrary.ai (legacy https://mcp.spacefrontiers.org still served) exposing nine machinelibrary_*…
- [Machine Library A2A Agent](https://apis.io/apis/machinelibrary-ai/machine-library-a2a-agent/) — A2A (protocolVersion 0.3.0) research and commerce agent at https://machinelibrary.ai/a2a over JSON-RPC: grounded research answers with citation artifacts,…
- [Hermes Search Engine gRPC API](https://apis.io/apis/machinelibrary-ai/hermes-search-engine-grpc-api/) — Self-hosted, MIT-licensed Rust search engine published by Space Frontiers (github.com/SpaceFrontiers/hermes) with a published protobuf wire contract:…
- [Space Frontiers Documents API](https://apis.io/apis/machinelibrary-ai/machinelibrary-ai-documents-api/) — Fetch documents by ID or canonical URI.
- [Space Frontiers Payments API](https://apis.io/apis/machinelibrary-ai/machinelibrary-ai-payments-api/) — The Payments API from Space Frontiers — 1 operation(s) for payments.
- [Space Frontiers Raw document downloads API](https://apis.io/apis/machinelibrary-ai/machinelibrary-ai-raw-document-downloads-api/) — Authenticated, feature-gated streaming of PDF, EPUB, and DJVU library originals.
- [Space Frontiers Recognition API](https://apis.io/apis/machinelibrary-ai/machinelibrary-ai-recognition-api/) — Document recognition: PDF, EPUB, and DJVU to structured Markdown with quality reports.
- [Space Frontiers Search API](https://apis.io/apis/machinelibrary-ai/machinelibrary-ai-search-api/) — Ranked retrieval and document similarity.
- [Space Frontiers Conversations API](https://apis.io/apis/machinelibrary-ai/machinelibrary-ai-conversations-api/) — Retrieval-augmented conversation workflows.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [Machine Library](https://apis.io/servers/machinelibrary-ai/org-spacefrontiers-search/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Machinelibrary Ai Agentic Access](https://apis.io/agentic-access/machinelibrary-ai/machinelibrary-ai-agentic-access/)

#### JSON Schema (12)

The data models the API reads and writes.

- [AgentCommentSubmission](https://apis.io/schemas/machinelibrary-ai/machinelibrary-ai-agent-comment-submission/)
- [ByUriResponse](https://apis.io/schemas/machinelibrary-ai/machinelibrary-ai-by-uri-response/)
- [ConversationRequest](https://apis.io/schemas/machinelibrary-ai/machinelibrary-ai-conversation-request/)
- [ConversationResponse](https://apis.io/schemas/machinelibrary-ai/machinelibrary-ai-conversation-response/)
- [FeedbackAccepted](https://apis.io/schemas/machinelibrary-ai/machinelibrary-ai-feedback-accepted/)
- [RecognitionJobStatus](https://apis.io/schemas/machinelibrary-ai/machinelibrary-ai-recognition-job-status/)
- [RecognitionSubmission](https://apis.io/schemas/machinelibrary-ai/machinelibrary-ai-recognition-submission/)
- [SearchFeedback](https://apis.io/schemas/machinelibrary-ai/machinelibrary-ai-search-feedback/)
- [SearchRequestV2](https://apis.io/schemas/machinelibrary-ai/machinelibrary-ai-search-request-v2/)
- [SimilarRequestV2](https://apis.io/schemas/machinelibrary-ai/machinelibrary-ai-similar-request-v2/)
- [V2DocumentResponse](https://apis.io/schemas/machinelibrary-ai/machinelibrary-ai-v2-document-response/)
- [V2SearchResponse](https://apis.io/schemas/machinelibrary-ai/machinelibrary-ai-v2-search-response/)

#### JSON-LD (1)

Linked-data contexts for the provider's vocabulary.

- [Machinelibrary Ai Context](https://apis.io/jsonld/machinelibrary-ai/machinelibrary-ai-context/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Machinelibrary Ai Openapi Overlay](https://apis.io/overlays/machinelibrary-ai/machinelibrary-ai-openapi-overlay/)

#### Governance rules (1)

Spectral rulesets for the provider's contracts.

- [Space Frontiers API Rules](https://apis.io/rules/machinelibrary-ai/machinelibrary-ai-rules/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Machinelibrary Ai Authentication](https://apis.io/security/machinelibrary-ai/machinelibrary-ai-authentication/)
- [Machinelibrary Ai Domain Security](https://apis.io/security/machinelibrary-ai/machinelibrary-ai-domain-security/)
- [Machinelibrary Ai Vulnerability Disclosure](https://apis.io/security/machinelibrary-ai/machinelibrary-ai-vulnerability-disclosure/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Machinelibrary Ai Scopes](https://apis.io/scopes/machinelibrary-ai/machinelibrary-ai-scopes/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Machinelibrary Ai Plans Pricing](https://apis.io/plans/machinelibrary-ai/machinelibrary-ai-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Machinelibrary Ai Rate Limits](https://apis.io/rate-limits/machinelibrary-ai/machinelibrary-ai-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://machinelibrary.ai/)
- [Documentation](https://machinelibrary.ai/docs/api)
- [Getting started](https://machinelibrary.ai/docs/api)
- [API reference](https://machinelibrary.ai/docs/api/reference)
- [Pricing](https://machinelibrary.ai/pricing)
- [Sign up](https://machinelibrary.ai/auth/signup)
- [Support](https://machinelibrary.ai/contacts)
- [Changelog](https://machinelibrary.ai/changelog)
- [Terms of service](https://machinelibrary.ai/terms-of-service)
- [Privacy policy](https://machinelibrary.ai/privacy)
- [GitHub](https://github.com/SpaceFrontiers)
- [Status](https://machinelibrary.ai/status)

## API Evangelist rating

**Kin Score 63.4** — strong · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 77.5 |
| Contract quality | 67.6 |
| Contract governance | 35.6 |
| Operational transparency | 52.6 |
| Developer ergonomics | 59.5 |
| Access clarity | 65.8 |

**Agent readiness 68.9** — agent-ready (gated down from agent-native)

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | — |
| MCP Server | documented (partial credit) |
| Auth Clarity | served (partial credit) |
| Idempotency | documented (partial credit) |
| Error Semantics | verified |
| OpenAPI Examples | verified |
| Rate Limit Signal | verified |
| Event Surface Described | — |
| Agent Skills | yes |
| Well Known Catalog | yes |
| Consent Identity | — |
| Agent Card | conformant |
| Dry Run Mode | — |
| Delegated Identity | served (partial credit) |
| Protected Resource Metadata | verified |
| Dynamic Client Registration | yes |
| Agentic Commerce | — |
| Pagination Ratio | na |
| Operation Distinctiveness | distinct |

**Regulatory alignment 40.2** — Education & Research

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/machinelibrary-ai/](https://apis.io/providers/machinelibrary-ai/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Space Frontiers: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/machinelibrary-ai/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
