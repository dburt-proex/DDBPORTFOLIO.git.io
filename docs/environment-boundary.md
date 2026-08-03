# Portfolio Environment and Secret Boundary

## Decision

This public repository may document environment-variable names and safe public configuration values, but it must never contain live credentials, access tokens, signing secrets, private database identifiers, session keys, or unpublished operational data.

The canonical visitor-facing portfolio currently runs on ChatGPT Sites. This repository remains the versioned evidence and publishing-governance layer. Environment variables added here therefore define a future-safe integration contract; they do not automatically configure the live ChatGPT Sites deployment.

## What the variables provide

### Public identity and navigation

`PUBLIC_SITE_NAME`, `PUBLIC_SITE_URL`, `PUBLIC_SITE_DESCRIPTION`, and public profile links centralize safe visitor-facing information. A future runtime can use them for metadata, navigation, canonical URLs, contact links, and structured data without repeating values throughout the codebase.

### Feature configuration

`PUBLIC_ENABLE_*` flags provide controlled release switches for public sections such as the Work Log, Governance Lab, case studies, availability banner, service intake, and AI guide. They allow a runtime-enabled build to activate or suppress incomplete features without deleting implementation code.

### Project selection

`PUBLIC_FEATURED_PROJECTS` and `PUBLIC_PRIMARY_PROJECT` define which public repositories receive portfolio prominence. They expose only already-public repository names and support consistent ordering across project cards, case studies, and navigation.

### Availability messaging

`PUBLIC_AVAILABILITY_STATUS` and `PUBLIC_AVAILABILITY_LABEL` let the portfolio change public engagement status without editing multiple pages.

### Private integration placeholders

Private placeholders document the server-side capabilities that may later power email delivery, CAPTCHA verification, GitHub reads, Notion publishing, Airtable intake, AI functionality, sessions, revalidation, and signed webhooks. They remain empty in `.env.example` and must be configured only in an encrypted hosting environment or ignored local file.

## Exposure classification

| Classification | Examples | Repository rule |
| --- | --- | --- |
| Public configuration | Site name, public URLs, public repository names, feature flags | May appear in `.env.example` with safe values |
| Private integration configuration | API keys, access tokens, service-role keys, session secrets | Variable name may be documented; value must remain empty |
| Sensitive operational data | Lead records, unpublished drafts, analytics exports, internal endpoints | Must not be committed or represented as environment defaults |

## Enforcement controls

1. `.gitignore` blocks `.env`, `.env.*`, local overrides, provider state, logs, and build output while explicitly permitting `.env.example`.
2. `.env.example` contains no working credentials.
3. Public variables use the neutral `PUBLIC_` prefix because this repository is currently static and framework-independent.
4. A future Next.js implementation must expose only explicitly approved values through `NEXT_PUBLIC_`; all other variables must be accessed exclusively by server code.
5. Pull requests should fail when a prohibited environment file is tracked or when high-risk credential patterns are introduced.

## Runtime implementation gate

Before any integration becomes active, the implementation must verify:

- the live hosting platform supports encrypted environment variables;
- private values are read only in server-side execution;
- client bundles and generated static files contain no secret values;
- logs redact credentials and personal data;
- permissions use least privilege;
- key rotation and revocation procedures exist;
- failure behavior does not return configuration details to visitors.

## Prohibited examples

Never commit real values for:

- `OPENAI_API_KEY`
- `GITHUB_READ_TOKEN`
- `CONTACT_EMAIL_API_KEY`
- `NOTION_API_TOKEN`
- `AIRTABLE_PERSONAL_ACCESS_TOKEN`
- `SESSION_SECRET`
- `CSRF_SECRET`
- `WEBHOOK_SIGNING_SECRET`
- database connection strings
- provider service-role keys

## Acceptance criteria

- No credential-bearing environment file is tracked.
- `.env.example` contains only public values and empty private placeholders.
- The repository clearly distinguishes the static evidence layer from the live ChatGPT Sites experience.
- Any future runtime integration requires a separate reviewed implementation and deployment configuration.
