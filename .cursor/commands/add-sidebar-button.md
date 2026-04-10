---
description: "Add a new button to the sidebar menu"
---

Add a new button to the sidebar menu with these requirements:

- Button name/label: $ARGUMENTS
- Location: `packages/excalidraw/components/` (sidebar area)
- Follow existing sidebar button patterns in the codebase

Steps:

1. Find existing sidebar buttons by searching `packages/excalidraw/components/` for sidebar-related components
2. Create a new functional component for the button following project conventions:
   - Named export (not default)
   - Props interface: `{Name}ButtonProps`
   - Use className for styling (no inline styles)
3. Register the button in the sidebar component where other buttons are rendered
4. Add an action in `packages/excalidraw/actions/` if the button triggers a state change (use actionManager pattern)
5. Add i18n key in `packages/excalidraw/locales/en.json` for the button label
6. Create a colocated test file `{Name}Button.test.tsx`
7. Run `yarn test:typecheck` and `yarn test` to verify

Constraints (from .cursor/rules/):

- Do NOT use default exports
- Do NOT use inline styles
- Do NOT use `any` type
- Do NOT modify protected files without approval
- State changes go through actionManager only
