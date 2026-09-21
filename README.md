# Digital Optimizer Web

Shared Astro monorepo for Johan Garcia and Digital Optimizer Agency.

## Applications

| App | Production domain | Build output |
| --- | --- | --- |
| `@digital-optimizer/johan` | `johangarcia.com` | `apps/johan/dist` |
| `@digital-optimizer/agency` | `digitaloptimizer.agency` | `apps/agency/dist` |

## Commands

```bash
npm install
npm run check
npm run build
npm run dev:johan
npm run dev:agency
```

Both sites share design tokens from `packages/design-system/tokens.css` while retaining distinct visual identities and messaging.
