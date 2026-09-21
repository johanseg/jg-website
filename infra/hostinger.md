# Hostinger deployment

Deploy on VPS **789285** (`srv789285`, `168.231.64.60`, Tailscale `doa-box`).
VPS 845316 hosts TSI and is excluded from these deployments.

Coolify manages both static sites behind its existing Traefik proxy. Use the
repository root as the build context so npm workspaces and shared design tokens
are available. Do not use the old single-site `/dist` output.

| Coolify application | Repository / branch | Install | Build | Publish directory |
| --- | --- | --- | --- | --- |
| `johangarcia` | `johanseg/jg-website` / `master` | `npm ci` | `npm run build:johan` | `/apps/johan/dist` |
| `digitaloptimizer-agency` | `johanseg/jg-website` / `master` | `npm ci` | `npm run build:agency` | `/apps/agency/dist` |

Both use Nixpacks, static-site mode, base directory `/`, and container port 80.
Pin each deployment to its full reviewed commit SHA. Validate with `npm ci`,
`npm run check`, `npm run build`, and `git diff --check` before release.

Before replacing either site, retain a Hostinger snapshot, its current image,
and its Coolify configuration. Test the build on an isolated preview route,
then deploy through the existing Coolify application. Verify HTTPS, apex/www
redirects, page assets, mobile layout, and unchanged unrelated containers.
Rollback uses the retained image and prior Coolify configuration; a full VPS
restore is a last resort because it affects unrelated services.

The private `Digital-Optimizer/digitaloptimizer-app` repository is deployed
separately. Its sandbox UI does not implement authentication or persistence.
Every route and asset must be behind a real access gate before public routing.
Never reuse TSI source, data, credentials, or its server for this app.
