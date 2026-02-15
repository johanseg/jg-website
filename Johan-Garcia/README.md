# Johan Garcia Website (Astro)

Personal website built with Astro.

## Local Development

```bash
npm install
npm run dev
```

## Build

```bash
npm run build
```

Output is generated in `dist/`.

## Auto Deploy to Hostinger VPS

This repo includes a GitHub Actions workflow that builds and deploys `dist/` to a Hostinger VPS over SSH:

- Workflow: `/Users/johan/AI/cursor/johangarcia.com/.github/workflows/deploy-hostinger.yml`
- Setup guide: `/Users/johan/AI/cursor/johangarcia.com/Johan-Garcia/docs/DEPLOY_HOSTINGER.md`
