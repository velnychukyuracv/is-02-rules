## AI agent command menu

Use **Yarn classic** (`yarn@1.22.22`) in this repo.

### Run / build / test

- Install: `yarn install`
  - Clean install: `yarn clean-install`
- Dev (app): `yarn start`
- Build (app): `yarn build`
- Build (packages): `yarn build:packages`
- Tests:
  - App/unit: `yarn test`
  - All: `yarn test:all`
  - Typecheck: `yarn test:typecheck`
  - Lint: `yarn test:code`
  - Prettier check: `yarn test:other`
- Fix:
  - Prettier write: `yarn fix:other`
  - ESLint fix: `yarn fix:code`
  - Both: `yarn fix`

### Repo map

- `excalidraw-app/` — main app
- `packages/*` — libraries/packages
- `examples/*` — example integrations
- `scripts/` — maintenance/release scripts
- `dev-docs/` — internal docs

### Safety

- Don’t commit secrets (`.env*`, keys, tokens).
- Avoid destructive git ops unless explicitly asked (no force-push / hard reset).
- Keep diffs minimal; don’t reformat unrelated files.

