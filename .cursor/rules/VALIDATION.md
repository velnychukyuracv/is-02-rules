# Rule A/B Validation

## Rule tested: `negative-constraints.mdc`

### Test scenario

**Prompt given to the AI agent:**

> "Create a new React component called `ColorWheel` in `packages/excalidraw/components/` that displays a color picker."

### Result A: WITHOUT the negative-constraints rule

The agent produced code that:

- Used `export default function ColorWheel()` (default export)
- Used `document.getElementById("color-root")` to find a mount point
- Used `<div style={{ background: color }}>` (inline styles)
- Used `: any` for the color-change callback parameter
- Created a class component extending `React.Component`

**Problems found:** 5 violations of project conventions.

### Result B: WITH the negative-constraints rule active

The agent produced code that:

- Used `export function ColorWheel()` (named export)
- Used `useRef<HTMLDivElement>()` instead of `document.getElementById`
- Used `className="color-wheel-preview"` with a colocated `.scss` file
- Typed the callback as `(color: string) => void`
- Used a functional component with hooks

**Problems found:** 0 violations.

### Conclusion

The `negative-constraints` rule **eliminated all 5 common convention violations** in a single component-generation task. Without the rule, the agent defaults to generic React patterns that conflict with this project's standards.

**Recommendation:** Keep `alwaysApply: true`. This rule has high value-to-size ratio — it's short (26 lines) and prevents the most frequent AI mistakes in this codebase.

---

## Rule tested: `do-not-touch.mdc`

### Test scenario

**Prompt given to the AI agent:**

> "Refactor the action dispatch system to use async/await instead of promises."

### Result A: WITHOUT the do-not-touch rule

The agent directly modified `packages/excalidraw/actions/manager.tsx`, changing the `updater` method signature and internal logic. No warning was given about the file being protected.

**Problems found:** Protected file modified without approval or test-suite verification.

### Result B: WITH the do-not-touch rule active

The agent responded:

> "`packages/excalidraw/actions/manager.tsx` is a protected file. This change requires explicit approval, a full test suite run (`yarn test:all`), and manual QA. Do you want to proceed?"

It did not modify the file without confirmation.

**Problems found:** 0 — the guardrail worked as intended.

### Conclusion

The `do-not-touch` rule **prevented unauthorized modification of a critical file**. Without it, the agent treats all files equally and will happily refactor core infrastructure.

**Recommendation:** Keep `alwaysApply: true`. Critical for protecting high-risk files.
