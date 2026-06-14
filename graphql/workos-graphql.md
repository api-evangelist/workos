# WorkOS GraphQL Schema

## Overview

WorkOS exposes a **REST-only** public API (`https://api.workos.com`). This directory contains a **conceptual GraphQL schema** (`workos-schema.graphql`) derived from WorkOS's published REST types, their OpenAPI 3.1.1 specification at [github.com/workos/openapi-spec](https://github.com/workos/openapi-spec), and the public reference documentation at [workos.com/docs/reference](https://workos.com/docs/reference).

The schema is not a live GraphQL endpoint. It models WorkOS's domain objects in SDL to support tooling, documentation generation, and client code generation.

## Source Material

| Source | URL |
|---|---|
| REST API Reference | https://workos.com/docs/reference |
| OpenAPI Specification | https://github.com/workos/openapi-spec |
| Client Libraries | https://workos.com/docs/reference/client-libraries |
| GitHub Organization | https://github.com/workos |

## Types Modelled

### Identity & Users

| Type | Description |
|---|---|
| `User` | An AuthKit-managed user identity with email verification, MFA, and session state. |
| `DirectoryUser` | A SCIM-synced directory user from an enterprise Identity Provider. |
| `DirectoryGroup` | A SCIM-synced group or role from an enterprise Identity Provider. |
| `Profile` | A normalized SSO profile returned after a successful SAML or OIDC authentication. |

### Organizations

| Type | Description |
|---|---|
| `Organization` | A WorkOS Organization grouping connections, directories, users, and domains. |
| `OrganizationDomain` | A domain attached to an Organization; verified via DNS TXT record or manual upload. |

### SSO

| Type | Description |
|---|---|
| `Connection` | An SSO connection linking an Organization to an Identity Provider (SAML or OIDC). |
| `SAMLConnection` | SAML-specific metadata: IdP entity ID, SSO URL, metadata URL, SP ACS URL. |
| `OIDCConnection` | OIDC-specific metadata: client ID, discovery endpoint, redirect URI. |

### Directory Sync

| Type | Description |
|---|---|
| `DirectorySync` | A SCIM 2.0 directory sync connection to an HR or IdP system. |

### MFA

| Type | Description |
|---|---|
| `AuthFactor` | An enrolled authentication factor (TOTP app) for a User. |
| `AuthChallenge` | A one-time MFA challenge issued against an enrolled factor. |
| `TotpFactor` | TOTP-specific enrollment data: QR code, secret, URI. |
| `Password` | Password credential metadata for a User (no hash is exposed via the API). |

### Admin Portal

| Type | Description |
|---|---|
| `Portal` | A time-limited, white-label Admin Portal URL for an Organization's IT admin. |

### Audit Logs

| Type | Description |
|---|---|
| `AuditLogEvent` | A single structured audit event with actor, targets, action, and context. |
| `AuditLogExport` | An in-progress or completed CSV export of filtered audit log events. |
| `AuditLogActor` | The entity (user, system, API key) that performed the audited action. |
| `AuditLogTarget` | The resource(s) affected by the audited action. |
| `AuditLogContext` | IP address and user agent context captured at event occurrence. |

### Events & Webhooks

| Type | Description |
|---|---|
| `Event` | A WorkOS platform event, available via the Events polling API. |
| `Webhook` | A configured webhook endpoint receiving platform events via HTTP POST. |

### Environment

| Type | Description |
|---|---|
| `Environment` | A WorkOS environment (test / production) with its client ID and redirect URIs. |

## Schema Design Notes

- **Pagination** follows WorkOS's cursor-based list style: `before` / `after` cursors with a `limit` parameter, mirroring the `ListMetadata` shape in the REST API.
- **`ConnectionType`** enum covers all 34+ identity provider integrations documented by WorkOS (Okta, Azure, Google, PingFederate, etc.).
- **`DirectoryType`** enum covers all SCIM and directory providers (Azure SCIM, Okta SCIM, Google Workspace, Workday, BambooHR, etc.).
- **`EventType`** enum covers the complete set of webhook-deliverable platform events across authentication, SSO, Directory Sync, and Organization lifecycle.
- The `JSON` scalar is used for `rawAttributes` and `metadata` fields where WorkOS returns provider-specific data with no fixed schema.
- MFA enrollment and challenge flows are modelled as mutations, matching the POST/PUT REST endpoints.
- Audit Log ingestion (`createAuditLogEvent`) supports the structured actor/target/context envelope WorkOS requires, plus an optional idempotency key.

## Types Count

19 named object/enum types:

1. `Connection`
2. `DirectorySync`
3. `User`
4. `DirectoryGroup`
5. `Profile`
6. `Organization`
7. `OrganizationDomain`
8. `Portal`
9. `AuditLogEvent`
10. `AuditLogExport`
11. `SAMLConnection`
12. `OIDCConnection`
13. `Password`
14. `AuthFactor`
15. `AuthChallenge`
16. `Event`
17. `Webhook`
18. `Environment`
19. `DirectoryUser`
