## AI agent commands (project playbook)

This repo is the Excalidraw monorepo and uses **Yarn classic** (`yarn@1.22.22`).

### Commands

- **Install**: `yarn install`
  - **Clean install**: `yarn clean-install`
- **Dev (app)**: `yarn start`
- **Build (app)**: `yarn build`
- **Build (packages)**: `yarn build:packages`
- **Tests**:
  - **Unit/app**: `yarn test`
  - **All**: `yarn test:all`
  - **Typecheck**: `yarn test:typecheck`
  - **Lint**: `yarn test:code`
  - **Prettier check**: `yarn test:other`
- **Fix**:
  - **Prettier write**: `yarn fix:other`
  - **ESLint fix**: `yarn fix:code`
  - **Both**: `yarn fix`

## Project Structure

- `excalidraw-app/` — main web app (excalidraw.com)
- `packages/excalidraw/` — core React library (`@excalidraw/excalidraw`)
- `packages/element/` — element model, geometry, rendering primitives
- `packages/common/` — shared constants, utilities, helpers
- `packages/math/` — 2D math (points, vectors, angles, geometry)
- `packages/utils/` — export helpers, file I/O
- `examples/` — integration examples (Next.js, browser script)
- `scripts/` — build/release tooling
- `dev-docs/` — documentation site (Docusaurus)

## Code Style

- TypeScript throughout; prefer explicit types at module boundaries
- Named exports only (no default exports)
- Functional components + hooks (no class components)
- No `any` or `@ts-ignore` — use proper types or safe narrowing
- Use `@excalidraw/*` package imports (never `src/` paths)
- No inline styles — use className / existing styling patterns
- Keep functions small; avoid deep nesting (max 3 levels)
- Let Prettier handle formatting; run `yarn fix` before committing

## Architecture

- **State management**: custom pattern via `actionManager` — NOT Redux/Zustand/MobX/Jotai/Recoil
- **State updates**: `actionManager.executeAction()` only
- **State type**: `AppState` in `packages/excalidraw/types.ts`
- **Rendering**: Canvas 2D via custom engine — NOT React DOM for drawing
- **Render pipeline**: Scene → renderScene() → canvas 2D context
- **DO NOT use**: react-konva, fabric.js, pixi.js

## Testing

- **Runner**: Vitest with jsdom environment
- **Setup**: `setupTests.ts` (canvas mock, IndexedDB mock, font mock)
- **Run tests**: `yarn test` (unit) / `yarn test:all` (full suite)
- **Snapshots**: never edit manually — regenerate with `yarn test:update`
- **Coverage thresholds**: lines 60%, branches 70%, functions 63%, statements 60%
- **File naming**: colocated `*.test.ts` / `*.test.tsx` next to source

## Security

- NEVER commit `.env*`, API keys, tokens, or credentials
- Put local overrides in `.env.local` / `.env.development.local` (gitignored)
- Collaboration data is end-to-end encrypted — do not weaken encryption
- Sanitize URLs (use `@braintree/sanitize-url`)
- No `dangerouslySetInnerHTML` or `eval()`
- Validate `.excalidraw` JSON via restore.ts — do not bypass

## Guardrails

- NEVER modify `packages/excalidraw/scene/Renderer.ts` without full test run
- NEVER modify `packages/excalidraw/data/restore.ts` without full test run
- NEVER modify `packages/excalidraw/actions/manager.tsx` without full test run
- NEVER modify `packages/excalidraw/types.ts` without full test run
- NEVER add npm dependencies without approval
- Don't commit secrets (`.env*`, keys, tokens)
- Avoid destructive git operations unless explicitly asked (no force push / hard reset)
- Keep diffs minimal; don't reformat unrelated files
- Don't change dependencies unless needed; keep `yarn.lock` consistent
