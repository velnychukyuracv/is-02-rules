# CLAUDE.md

This file provides project context for AI tools (Claude, Cursor, Copilot, etc.).
It mirrors the rules in `.cursor/rules/` for cross-tool compatibility.

## Project Overview

Excalidraw is an open-source virtual whiteboard monorepo.

## Project Structure

- `packages/excalidraw/` — core React library (`@excalidraw/excalidraw`)
- `packages/element/` — element model, geometry, rendering primitives
- `packages/common/` — shared constants, utilities, helpers
- `packages/math/` — 2D math (points, vectors, angles, geometry)
- `packages/utils/` — export helpers, file I/O
- `excalidraw-app/` — full web app (excalidraw.com)
- `examples/` — integration examples (Next.js, browser script)
- `scripts/` — build/release tooling
- `dev-docs/` — documentation site (Docusaurus)

## Commands

- `yarn` — install deps
- `yarn start` — dev server (port 3001)
- `yarn build` — production build
- `yarn build:packages` — build all publishable packages
- `yarn test` — Vitest unit tests
- `yarn test:all` — full suite (typecheck + lint + tests + prettier)
- `yarn test:typecheck` — TypeScript checking
- `yarn test:code` — ESLint
- `yarn test:other` — Prettier check
- `yarn fix` — auto-fix lint + formatting
- `yarn test:update` — regenerate snapshots
- `yarn clean-install` — wipe and reinstall deps

## Architecture

- **State management**: custom pattern via `actionManager` — NOT Redux/Zustand/MobX/Jotai/Recoil
- **State updates**: `actionManager.executeAction()` only
- **State type**: `AppState` in `packages/excalidraw/types.ts`
- **Rendering**: Canvas 2D via custom engine — NOT React DOM for drawing
- **Render pipeline**: Scene → renderScene() → canvas 2D context
- **DO NOT use**: react-konva, fabric.js, pixi.js

## Code Style

- Functional components + hooks only (no class components)
- Named exports only (no default exports)
- TypeScript strict mode; no `any` or `@ts-ignore`
- Use `@excalidraw/*` package imports (never `src/` paths)
- No inline styles — use className / existing styling
- Prefer early returns; max 3 levels of nesting
- Let Prettier handle formatting; run `yarn fix` before committing

## Testing

- Vitest + jsdom; setup in `setupTests.ts`
- Colocated test files: `Thing.test.tsx` next to `Thing.tsx`
- Never edit snapshots manually — use `yarn test:update`
- Coverage thresholds: lines 60%, branches 70%, functions 63%, statements 60%

## Security

- NEVER commit `.env*`, API keys, tokens, or credentials
- Local overrides go in `.env.local` / `.env.development.local`
- Collaboration data is end-to-end encrypted — do not weaken
- Sanitize URLs with `@braintree/sanitize-url`
- No `dangerouslySetInnerHTML` or `eval()`
- Validate imported JSON via `restore.ts` — do not bypass

## Protected Files (Do Not Touch)

NEVER modify without explicit approval + full test run + manual QA:

- `packages/excalidraw/scene/Renderer.ts` — canvas render pipeline
- `packages/excalidraw/data/restore.ts` — file format compatibility
- `packages/excalidraw/actions/manager.tsx` — action dispatch system
- `packages/excalidraw/types.ts` — core type definitions

## Negative Constraints

- NEVER use `document.getElementById` — use React refs
- NEVER import from `src/` — use package imports
- DO NOT suggest class components or `any` type
- DO NOT modify test snapshots manually
- AVOID deep nesting, barrel exports, default exports
- DO NOT add npm dependencies without explicit approval
