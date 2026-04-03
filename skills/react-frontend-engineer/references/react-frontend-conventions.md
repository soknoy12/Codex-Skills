# React Frontend Conventions

Use this reference when the task needs deeper guidance than the main `SKILL.md` should carry.

## Folder And Component Structure

Prefer a structure that makes ownership obvious and keeps shared pieces intentional.

For many React applications, a shape like this is reasonable:

```text
src/
  app/
  components/
  features/
  hooks/
  lib/
  services/
  styles/
  test/
```

If the repository already uses a coherent feature-based or route-based structure, preserve it unless there is a strong reason to improve it.

## Component Design

- Keep components focused on one level of responsibility.
- Prefer smaller composable components over giant configuration-heavy ones.
- Separate presentational concerns from data-fetching or orchestration concerns when that improves clarity.
- Avoid prop surfaces that try to solve every future variation.
- Extract hooks for repeated stateful behavior, not just to move lines around.

## State And Data Flow

- Keep local UI state close to the component that owns it.
- Keep server state separate from transient UI state.
- Model asynchronous states explicitly: loading, empty, error, success.
- Use shared state only when multiple distant parts of the tree truly need coordination.
- Keep data fetching boundaries clear and easy to test.

## Accessibility

- Prefer semantic HTML elements before adding ARIA.
- Ensure interactive elements are keyboard reachable and visibly focusable.
- Use labels, descriptions, and roles only where they materially improve assistive technology support.
- Avoid div-based buttons and links unless there is a compelling reason.
- Treat color contrast, motion sensitivity, and screen size adaptability as product requirements, not polish.

## Performance

- Optimize obvious hot paths, expensive lists, or repeated renders when they matter.
- Do not add `memo`, `useMemo`, or `useCallback` reflexively; use them when they solve a real rendering or identity problem.
- Prefer stable component boundaries and simple state ownership before micro-optimizing.
- Defer expensive calculations or rendering work only when the user experience benefits.

## Testing

- Test important UI behavior, not just implementation details.
- Add tests for state transitions, key interactions, accessibility-sensitive behavior, and business-critical rendering logic.
- Prefer readable test setup over highly abstracted helpers.
- Keep tests resilient to implementation changes when behavior remains the same.

## Styling Guidance

- Use a consistent styling system across the feature.
- Favor maintainable tokens, utility classes, or scoped styles over ad hoc inline styling.
- Ensure responsive behavior is deliberate, not accidental.
- Avoid visual complexity that makes components hard to extend or theme.

## Skill Authoring Guidance

When building a frontend-oriented Codex skill:

- Put trigger conditions in the frontmatter description.
- Keep the main instructions focused on workflow, decision points, and non-obvious guardrails.
- Move longer UI system rules, design-system conventions, or framework variants into `references/`.
- Add scripts only for deterministic generation, validation, or transformation that materially improves repeatability.
- Remove template clutter before packaging.

## Output Expectations

When the user wants generated deliverables rather than direct repository edits, prefer:

1. Short implementation plan
2. Skill or feature name
3. Folder structure
4. Complete contents or created artifacts
5. Validation and packaging notes
6. Follow-up improvements
