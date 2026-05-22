# WorkOS (workos)

WorkOS is the "Enterprise Ready" identity platform for B2B SaaS. It provides AuthKit user management, enterprise SSO (SAML/OIDC), Directory Sync (SCIM 2.0), Multi-Factor Authentication, Audit Logs, an Admin Portal for IT admins, Fine-Grained Authorization (FGA, formerly Warrant), Radar bot/fraud protection, and a growing suite of agent-oriented surfaces — Pipes (session-scoped, human-approved agent credentials), MCP Auth (with RFC 8707 Resource Indicators), and the `auth.md` open protocol for agent service registration.

> "Your app, Enterprise Ready." — workos.com

**Index:** [apis.yml](https://raw.githubusercontent.com/api-evangelist/workos/refs/heads/main/apis.yml)

**Run:** [Capabilities Using Naftiko](https://github.com/naftiko/fleet?utm_source=api-evangelist&utm_medium=readme&utm_campaign=company-api-evangelist&utm_content=repo)

## Tags

Authentication, Identity Provider, SSO, SAML, OIDC, SCIM, Directory Sync, Authorization, FGA, Audit Logs, MFA, B2B SaaS, Agents, MCP

## Timestamps

- **Created:** 2026-03-25
- **Modified:** 2026-05-22

## APIs

### WorkOS REST API

The official WorkOS REST API at `https://api.workos.com` — 172 operations across 41 tag groups in the published OpenAPI 3.1.1 spec. Covers:

- **AuthKit / User Management** — users, organizations, organization memberships, invitations, sessions, JWT templates, redirect URIs, CORS origins, data providers, magic auth, MFA enrollment and challenges, authorized applications, user feature flags.
- **Enterprise SSO** — authorization URLs, profile/token exchange, connections, organization domains.
- **Directory Sync** — directories, directory users, directory groups.
- **Audit Logs** — schema definition, event emission, SIEM streaming.
- **Authorization (FGA / Warrant)** — relation checks, queries, permissions.
- **Operational** — applications, application client secrets, API keys, organization API keys, webhooks, events, feature flags, feature flag targets, Admin Portal, widgets, WorkOS Connect.
- **Agent surfaces** — Pipes (provider-scoped agent credentials).
- **Trust and abuse** — Radar bot/fraud checks.

**Human URL:** [https://workos.com](https://workos.com)
**Base URL:** `https://api.workos.com` (staging: `https://api.workos-test.com`)

### Properties

- [Documentation](https://workos.com/docs)
- [API Reference](https://workos.com/docs/reference)
- [Upstream OpenAPI](https://github.com/workos/openapi-spec)
- [Local OpenAPI](openapi/workos-openapi.yml)
- [Changelog](https://workos.com/changelog)
- [Status Page](https://status.workos.com)
- [Pricing](https://workos.com/pricing)
- [Rate Limits](https://workos.com/docs/reference/rate-limits)
- [Plans (API Commons)](plans/workos-plans-pricing.yml)
- [Capabilities](capabilities/shared/workos.yaml)

## Artifacts

| Type | Count | Path |
|---|---|---|
| OpenAPI specs | 1 | [openapi/](openapi/) |
| Spectral rulesets | 1 | [rules/](rules/) |
| Naftiko shared capabilities | 1 | [capabilities/shared/](capabilities/shared/) |
| Naftiko workflow capabilities | 3 | [capabilities/](capabilities/) |
| JSON Schemas | 6 | [json-schema/](json-schema/) |
| JSON Structures | 3 | [json-structure/](json-structure/) |
| JSON-LD context | 1 | [json-ld/](json-ld/) |
| Operation examples | 13 | [examples/](examples/) |
| Vocabulary | 1 | [vocabulary/](vocabulary/) |
| API Commons Plans | 1 | [plans/](plans/) |
| API Commons Rate Limits | 1 | [rate-limits/](rate-limits/) |
| FinOps mapping | 1 | [finops/](finops/) |

## Capability Workflows

- **[B2B Enterprise Onboarding](capabilities/b2b-enterprise-onboarding.yaml)** — Create org → generate Admin Portal link → poll for active SSO connection → confirm directory is linked → confirm users are syncing.
- **[Agent-Scoped Authentication](capabilities/agent-scoped-authentication.yaml)** — Authenticate human → mint Pipe credential for AI agent → validate API key → check FGA → emit audit event. The full WorkOS agent-auth narrative captured as one composable workflow.
- **[Audit Everything to SIEM](capabilities/audit-everything-to-siem.yaml)** — Define schema, emit events, stream to SIEM, query for replay.

## Pricing snapshot (USD/month)

| Product | Pricing |
|---|---|
| AuthKit | Free up to 1M MAU, then $2,500/mo per additional 1M |
| Single Sign-On | $125 → $50 per connection (tiered 1–15 → 101–200), 201+ custom |
| Directory Sync | Same tier curve as SSO |
| Audit Logs | $125 per SIEM destination + $99 per 1M events retained |
| Radar | First 1,000 checks free, then $100 per 50K checks |
| Custom Domain | $99 |
| Scale Support | $1,000 (Enterprise: custom) |

## Rate limits

- **REST API (default):** 600 req/min per org
- **Auth endpoints:** 60 req/min per org
- **Directory Sync:** 10 events/sec per directory
- **Throttled response:** HTTP 429 with `Retry-After`

## Agent and MCP angle

WorkOS has positioned itself early as the "enterprise readiness" layer for AI agents. The picture across the GitHub org plus recent changelog and blog entries:

- **Pipes** — Session-scoped, human-approved credentials a host can issue to an agent to call third-party APIs. The reference MCP server is at [`workos/pipes-mcp`](https://github.com/workos/pipes-mcp); the API tag is `pipes`.
- **MCP Auth + Resource Indicators** — Per-server access scoping using RFC 8707. Released May 13, 2026 per the changelog.
- **User-scoped API keys** — Released May 19, 2026 so organizations can issue keys bound to individual users (the credential agents present).
- **`auth.md`** — Open protocol letting agents register for services on behalf of users via a Markdown file at a domain.
- **MCP Night** — WorkOS's recurring agent-mode event and storefront (`mcp.shop`).

## SDKs and AuthKit integrations

Official SDKs: [Node](https://github.com/workos/workos-node) · [Python](https://github.com/workos/workos-python) · [Ruby](https://github.com/workos/workos-ruby) · [Go](https://github.com/workos/workos-go) · [PHP](https://github.com/workos/workos-php) · [.NET](https://github.com/workos/workos-dotnet) · [Kotlin](https://github.com/workos/workos-kotlin) · [Rust](https://github.com/workos/workos-rust) (new — May 2026) · [Elixir](https://github.com/workos/workos-elixir) · [Laravel](https://github.com/workos/workos-php-laravel)

AuthKit framework libraries: [Next.js](https://github.com/workos/authkit-nextjs) · [React](https://github.com/workos/authkit-react) · [Remix](https://github.com/workos/authkit-remix) · [React Router](https://github.com/workos/authkit-react-router) · [SvelteKit](https://github.com/workos/authkit-sveltekit) · [TanStack Start](https://github.com/workos/authkit-tanstack-start) · [Vanilla JS](https://github.com/workos/authkit-js) · [XMCP](https://github.com/workos/authkit-xmcp)

CLI: [workos/cli](https://github.com/workos/cli) — AI-powered AuthKit integration wizard. [Homebrew Tap](https://github.com/workos/homebrew-tap). [GitHub Action](https://github.com/workos/cli-action).

Toolchain: [oagen](https://github.com/workos/oagen) — WorkOS's own framework for building OpenAPI-driven SDK generators.

## Maintainers

- **Kin Lane** — kin@apievangelist.com
