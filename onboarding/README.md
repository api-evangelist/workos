# Programmatic API Onboarding — WorkOS

A single-file, zero-dependency Node.js (18+) CLI that reproduces SoundCloud's
`sc-api-auth.mjs` pattern for WorkOS: register an application / obtain credentials
programmatically instead of clicking through a dashboard, so agents and developers
can onboard at the command line.

- Script: [`workos-api-auth.mjs`](workos-api-auth.mjs)
- Run `node workos-api-auth.mjs --help` for usage and the required environment variables.
- Story / rationale: https://apievangelist.com/2026/08/03/workos-dashboard-key-then-agents-run/

Part of the API Evangelist "Programmatic API Onboarding for the Agentic Moment" series.
