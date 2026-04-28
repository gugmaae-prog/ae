# Aether Edge

Aether Edge is the Cloudflare Workers deployment for the Aether interface and edge runtime.

## Project Links

- **Cloudflare Worker:** `aether-edge`
- **Environment:** `production`
- **GitHub Repository:** `https://github.com/gugmaae-prog/ae/`
- **Default branch:** `main`
- **Cloudflare dashboard:** https://dash.cloudflare.com/b1b843ec85bc39a3a4d370ba4f84f17a/workers/services/view/aether-edge/production
- **Supabase Project:** `entity`
- **Supabase Ref:** `ypkfganbwdvcjrcxygta`
- **Supabase Region:** `ap-southeast-1`
- **Supabase Status:** `ACTIVE_HEALTHY`
- **Postgres:** `17.6.1.063`

## Deployment Continuity

Production should maintain continuity across:

1. GitHub source repository
2. Cloudflare Workers production service
3. Supabase backend project
4. Environment variables and secrets
5. Worker routes or custom domains
6. Frontend artifact versioning

The continuity rule is:

```text
main branch = production source of truth
Cloudflare production = deployed from main
Supabase ref = ypkfganbwdvcjrcxygta
```

Every production deployment should be traceable to one Git commit on `main`.

## Cloudflare Worker

Worker service:

```text
aether-edge
```

Production environment:

```text
production
```

Expected deployment flow:

```text
GitHub repo -> Cloudflare Worker build/deploy -> production Worker
```

Cloudflare should deploy from this repository so every production deployment can be traced back to a commit on `main`.

Recommended continuity rules:

1. Commit all Worker source, configuration, and deployment notes to this repository.
2. Connect the Cloudflare Worker `aether-edge` to this GitHub repository.
3. Configure the production environment to deploy from the `main` branch.
4. Confirm Cloudflare build/deploy settings match this repo's Worker entrypoint and configuration.
5. After each deploy, verify the Cloudflare production deployment points to the latest intended Git commit.
6. Keep secrets in Cloudflare environment variables or GitHub repository secrets. Do not commit secrets to Git.

## Supabase

Connected Supabase project:

```text
Project name: entity
Project ref: ypkfganbwdvcjrcxygta
Status: ACTIVE_HEALTHY
Region: ap-southeast-1
Database: PostgreSQL 17.6.1.063
```

Supabase URL:

```text
https://ypkfganbwdvcjrcxygta.supabase.co
```

## Required Environment Variables

Set these in Cloudflare Workers production secrets/settings:

```text
SUPABASE_URL=https://ypkfganbwdvcjrcxygta.supabase.co
SUPABASE_ANON_KEY=...
SUPABASE_SERVICE_ROLE_KEY=...
```

Do not commit service role keys, private API keys, tokens, or production secrets to GitHub.

## Expected Worker Configuration

A typical Cloudflare Workers project should include:

```text
wrangler.toml or wrangler.jsonc
src/index.ts or src/index.js
package.json
README.md
```

For `aether-edge`, make sure `wrangler.toml` or `wrangler.jsonc` uses the correct service name:

```toml
name = "aether-edge"
main = "src/index.ts"
compatibility_date = "2026-04-28"
```

Adjust `main` if the Worker entrypoint is different.

## Deployment Checklist

Before marking production as complete, confirm:

- [x] `README.md` exists in the root of the GitHub repo.
- [ ] Cloudflare Worker service is named `aether-edge`.
- [ ] Production environment is selected in Cloudflare.
- [ ] Worker routes or custom domain are attached correctly.
- [ ] Supabase project ref is `ypkfganbwdvcjrcxygta`.
- [ ] Supabase project status is healthy.
- [ ] Cloudflare production secrets match the Supabase project.
- [ ] GitHub repository contains the latest Aether source or artifact.
- [ ] Cloudflare deployment is connected to the correct GitHub repo.
- [ ] Latest production Worker deployment was triggered from the correct branch.
- [ ] The live app loads successfully.
- [ ] No old Worker, old repo, or old Supabase project is referenced.

## Manual Deployment

Install dependencies:

```bash
npm install
```

Authenticate Wrangler if needed:

```bash
wrangler login
```

Deploy to production:

```bash
npx wrangler deploy --env production
```

Use manual deployment only after confirming the local branch is up to date with `main`.

## GitHub Setup

Recommended branch:

```text
main
```

Recommended continuity rule:

```text
main branch = production source of truth
Cloudflare production = deployed from main
Supabase ref = ypkfganbwdvcjrcxygta
```

## Notes

This README is the continuity anchor between GitHub, Cloudflare, and Supabase. Update it whenever the Worker name, environment, branch, route, build command, Supabase project, secrets, or deployment process changes.
