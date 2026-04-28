# Aether Edge

Aether Edge is the Cloudflare Workers edge service for the `aether-edge` production deployment.

## Deployment target

- **Cloudflare service:** `aether-edge`
- **Environment:** `production`
- **GitHub repository:** `gugmaae-prog/ae`
- **Default branch:** `main`
- **Cloudflare dashboard:** https://dash.cloudflare.com/b1b843ec85bc39a3a4d370ba4f84f17a/workers/services/view/aether-edge/production

## Git to Cloudflare continuity

Keep GitHub as the source of truth for the worker code and deployment configuration. Cloudflare should deploy from this repository so every production deployment can be traced back to a commit on `main`.

Recommended continuity rules:

1. Commit all Worker source, configuration, and deployment notes to this repository.
2. Connect the Cloudflare Worker `aether-edge` to this GitHub repository.
3. Configure the production environment to deploy from the `main` branch.
4. Confirm Cloudflare build/deploy settings match this repo's Worker entrypoint and configuration.
5. After each deploy, verify the Cloudflare production deployment points to the latest intended Git commit.
6. Keep secrets in Cloudflare environment variables or GitHub repository secrets. Do not commit secrets to Git.

## Expected Worker configuration

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

## Deploy checks

Before treating production as ready, confirm:

- The Cloudflare service is named `aether-edge`.
- The active environment is `production`.
- The production route, custom domain, or workers.dev URL points to the intended Worker.
- The latest production deployment corresponds to the latest intended GitHub commit.
- Required environment variables and bindings exist in Cloudflare.
- GitHub Actions or Cloudflare Git integration is connected to `gugmaae-prog/ae` on branch `main`.

## Manual deployment

If deploying manually with Wrangler:

```bash
npm install
npx wrangler deploy --env production
```

Use this only after confirming the local branch is up to date with `main`.

## Notes

This README is the continuity anchor between GitHub and Cloudflare. Update it whenever the Worker name, environment, branch, route, build command, or deployment process changes.
