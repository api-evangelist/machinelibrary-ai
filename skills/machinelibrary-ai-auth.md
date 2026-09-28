---
name: machinelibrary-ai-auth
description: Guide for authenticating agents and users to Machine Library via OAuth 2.1, PKCE, and service_auth flows, including discovery, registration, token handling, and revocation.
method: generated
generated: '2026-09-19'
---

# auth.md

Machine Library, the search and AI product by Space Frontiers Company, supports agentic registration for its read-only research search
and document-retrieval service. The MCP resource is
https://mcp.machinelibrary.ai and the authorization server is
https://api.spacefrontiers.org. The available scope is `search`.

Machine Library uses the existing Space Frontiers account database and OAuth issuer.
The original `https://mcp.spacefrontiers.org` resource remains supported; use
the resource URL advertised by the endpoint you connect to.

Agents can use OAuth 2.1 with PKCE or the user-claimed `service_auth` flow below.
Never ask a user to share a password, session cookie, API key, authorization
code, access token, refresh token, claim token, or identity assertion in chat.

## 1. Discover

Fetch these documents before authenticating. Their structured values are the
source of truth:

```text
GET https://mcp.machinelibrary.ai/.well-known/oauth-protected-resource
GET https://api.spacefrontiers.org/.well-known/oauth-authorization-server
```

The Protected Resource Metadata identifies the resource, authorization server,
supported scope, and bearer method. The Authorization Server Metadata contains
the standard OAuth endpoints and an `agent_auth` object with:

- `skill`: this guide
- `identity_endpoint`: start `service_auth` registration
- `claim_endpoint`: start a new claim attempt when supported
- `claim_complete_uri`: authenticated browser approval endpoint
- `revocation_uri`: revoke an issued access token
- `identity_types_supported`: `service_auth`
- `credential_types_supported`: `access_token`

## 2. Pick a method

- If the client can receive a browser OAuth callback, prefer OAuth 2.1
  authorization code with PKCE as described in section 7.
- If the client cannot receive a callback but knows the user's Machine Library
  account email, use `service_auth`.
- Anonymous registration and external identity assertions are not accepted.

`service_auth` does not grant access until the user signs in with the matching,
verified email and explicitly approves the request.

## 3. Register with `service_auth`

Ask the user which Machine Library account email to use. The email is only a
login hint; it is not proof of identity.

```http
POST https://api.spacefrontiers.org/v2/agent/identity
Content-Type: application/json

{"type":"service_auth","login_hint":"user@example.com"}
```

A successful response has this shape. Values shown in angle brackets are
placeholders:

```json
{
  "registration_id": "<registration ID>",
  "registration_type": "service_auth",
  "claim_url": "https://api.spacefrontiers.org/v2/agent/identity/claim",
  "claim_token": "<secret claim token>",
  "claim_token_expires": "<RFC 3339 timestamp>",
  "post_claim_scopes": ["search"],
  "claim": {
    "user_code": "123456",
    "expires_in": 900,
    "verification_uri": "https://machinelibrary.ai/agent/claim?claim_attempt_token=<secret>",
    "interval": 5
  }
}
```

Store `claim_token` as a secret. Show the user only `claim.verification_uri` and
the six-digit `claim.user_code` together. Do not email the code.

## 4. User claim and approval

The user opens `claim.verification_uri`, signs in to Machine Library with the
requested verified email, confirms that the displayed code matches
`claim.user_code`, and approves or denies the request. The browser submits that
decision to the authenticated `claim_complete_uri`; the agent must not call that
endpoint or handle the user's session.

While the user decides, poll the OAuth token endpoint no faster than the
returned `claim.interval`:

```http
POST https://api.spacefrontiers.org/v2/oauth/token
Content-Type: application/x-www-form-urlencoded

grant_type=urn%3Aworkos%3Aagent-auth%3Agrant-type%3Aclaim&claim_token=<claim token>
```

- Continue polling on `authorization_pending`.
- Increase the polling interval on `slow_down`.
- Stop on `access_denied` or `expired_token`.

After approval, the token response contains a one-hour `access_token` and a
service-signed `identity_assertion`:

```json
{
  "access_token": "<secret bearer token>",
  "token_type": "Bearer",
  "expires_in": 3600,
  "scope": "search",
  "identity_assertion": "<secret signed assertion>"
}
```

## 5. Use and renew the credential

Send the access token only to the configured MCP resource:

```http
Authorization: Bearer <access token>
```

When the access token expires, exchange the still-active service-signed
identity assertion at the discovered token endpoint:

```http
POST https://api.spacefrontiers.org/v2/oauth/token
Content-Type: application/x-www-form-urlencoded

grant_type=urn%3Aietf%3Aparams%3Aoauth%3Agrant-type%3Ajwt-bearer&assertion=<identity assertion>
```

## 6. Revoke and recover

Revoke an access token when it is no longer needed:

```http
POST https://api.spacefrontiers.org/v2/oauth/revoke
Content-Type: application/x-www-form-urlencoded

token=<access token>&token_type_hint=access_token
```

Access-token revocation ends that token. The active identity assertion can mint
a replacement until the agent connection itself is revoked or expires. On a
`401`, discard the rejected credential, fetch both discovery documents again,
and restart registration if necessary.

## 7. Browser OAuth for MCP clients

Clients that can receive a callback should prefer OAuth authorization code with
PKCE. Register a public client using RFC 7591:

```http
POST https://api.spacefrontiers.org/v2/oauth/register
Content-Type: application/json

{
  "client_name": "Research agent",
  "redirect_uris": ["https://agent.example.com/oauth/callback"],
  "token_endpoint_auth_method": "none",
  "grant_types": ["authorization_code", "refresh_token"],
  "response_types": ["code"],
  "scope": "search"
}
```

Use PKCE with `S256`, request only `search`, and set the OAuth resource to
https://mcp.machinelibrary.ai. The user signs in and approves access in the
browser. Use the discovered token and revocation endpoints for token exchange,
refresh, and revocation.

## Scope and policies

- `search`: search the corpus and retrieve research documents using the user's
  account credits.
- Pricing: https://machinelibrary.ai/pricing
- Privacy: https://machinelibrary.ai/privacy
- Terms: https://machinelibrary.ai/terms-of-service
- Integration help: https://machinelibrary.ai/contacts
