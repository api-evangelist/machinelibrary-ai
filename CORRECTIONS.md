# Profile refresh — September 26, 2026

This correction uses publicly reachable Machine Library sources. No credentials,
paid searches, payment settlement or authenticated MCP introspection were used.
The independently generated files under `kin/` are unchanged.

- Refresh the combined and recognition OpenAPI descriptions from their served JSON.
  OAuth authorization code with PKCE and scope `search`, recognition authentication,
  OpenAPI 3.1 nullability and application error/retry schemas are now present.
- Refresh OAuth, API catalog, authentication/install guides and llms.txt snapshots.
- Describe all seven hosted `machinelibrary_*` tools and compatibility aliases.
  Separate hosted capabilities from the standalone Python package's versions and
  schemas. Exact hosted tool schemas require authenticated `tools/list`.
- Publish scope entries using `scope`, with scheme and flow metadata, instead of
  relying only on `name`. The old source listed one scope while the generated page
  displayed zero.
- Replace the custom rate-limit wrapper with the API Commons rate-limit list schema.
  The three entries are documented gateway limits per source IP at each replica,
  not purchased account quotas. Additional capacity limits may apply.
- Add operations, changelog, status, security.txt and datasets links; correct related
  lifecycle, error, authentication and security narratives. The status page provides
  bounded endpoint checks, not independent uptime or incident-history monitoring.
- Qualify corpus records versus full-text availability and searchable coverage.
- Retain dates on unrelated historical probes and observations; this is not a fresh
  compliance audit or an authenticated runtime verification.

## Primary sources

- https://machinelibrary.ai/openapi.json
- https://api.machinelibrary.ai/v1/recognitions/docs/openapi.json
- https://api.machinelibrary.ai/.well-known/oauth-authorization-server
- https://mcp.machinelibrary.ai/.well-known/oauth-protected-resource
- https://machinelibrary.ai/.well-known/api-catalog
- https://machinelibrary.ai/.well-known/mcp/server-card.json
- https://machinelibrary.ai/.well-known/security.txt
- https://machinelibrary.ai/install.md
- https://api.machinelibrary.ai/auth.md
- https://machinelibrary.ai/mcp
- https://machinelibrary.ai/docs/api/operations
- https://machinelibrary.ai/changelog
- https://machinelibrary.ai/status
- https://machinelibrary.ai/datasets

## Validation

Both OpenAPI documents validate and their parsed YAML matches the fetched JSON.
The rate-limit artifact validates against API Commons' published JSON Schema.
All YAML and JSON files parse; the seven tool names, REST operation bindings, and
OAuth scope agree across the corrected artifacts.

## Catalog rebuild needed

Please re-ingest the corrected artifacts and rescore using current evidence.
On September 26, the live provider page showed 50.3/100, scored September 25
(rubric 0.23.0), but descriptions and derived scope data still used older snapshots.

The directory also needs these generated-page corrections:

1. The provider's MCP card links to
   https://apis.io/servers/machinelibrary-ai/space-frontiers-mcp-server/ (404).
   The separate API detail page works. Rebuild the server route and incoming link
   with the current product title, preserving an appropriate redirect if needed.
2. The provider header shows two APIs while its introduction and list show four.
   Recompute from one definition, or label distinct counts clearly.
3. Rebuild scopes and rate limits from the corrected structures. Scope `search`
   must appear; three documented gateway limits should replace the empty display.

No target rating is requested, and no unrelated features or compliance claims
have been added to improve a score.
