# Vue Nuxt Frontend Conventions

Use this reference when the task needs deeper guidance than the main `SKILL.md` should carry.

## Folder And App Structure

Prefer a structure that makes ownership obvious and keeps shared pieces intentional.

For many Nuxt applications, a shape like this is reasonable:

```text
app.vue
components/
composables/
layouts/
middleware/
pages/
plugins/
server/
  api/
stores/
utils/
```

If the repository already uses a coherent feature-based or domain-based structure, preserve it unless there is a strong reason to improve it.

## Component And Composable Design

- Keep components focused on one level of responsibility.
- Prefer smaller composable pieces over giant configuration-heavy components.
- Separate presentational concerns from data loading or orchestration concerns when that improves clarity.
- Use composables for repeated logic, not just to move lines around.
- Keep composable inputs and outputs explicit and stable.

## State And Data Flow

- Keep local UI state close to the component that owns it.
- Use `useAsyncData` or `useFetch` deliberately based on lifecycle and SSR needs.
- Keep server state separate from transient UI state.
- Use Pinia only when state is genuinely shared across distant parts of the app or needs app-wide coordination.
- Model asynchronous states explicitly: loading, empty, error, success.

## SSR And Hydration Safety

- Avoid reading browser-only globals during SSR render paths.
- Keep client-only behavior behind the right lifecycle or client guards.
- Prevent hydration mismatches by ensuring server and client output stay consistent for initial render.
- Be cautious with time-dependent, random, or viewport-dependent rendering during SSR.
- Choose server routes versus client fetches intentionally based on security, latency, and ownership.

## Accessibility

- Prefer semantic HTML elements before adding ARIA.
- Ensure interactive elements are keyboard reachable and visibly focusable.
- Use labels, descriptions, and roles only where they materially improve assistive technology support.
- Avoid click-only interactions that exclude keyboard or screen-reader users.
- Treat color contrast, motion sensitivity, and screen size adaptability as requirements, not polish.

## SEO And Metadata

- Use Nuxt metadata APIs intentionally for titles, descriptions, and social previews.
- Add Open Graph, canonical URLs, structured data, and sitemap support when the page or app benefits from discoverability.
- Make SSR-visible content meaningful for marketing or crawlable pages.
- Do not overfit SEO patterns to authenticated or purely internal application surfaces.

## Performance

- Optimize bundle size, hydration cost, and rendering only when it matters.
- Prefer clear rendering boundaries and simple state ownership before micro-optimizing.
- Defer heavy client-only behavior when the user experience benefits.
- Be careful with global plugins or middleware that run on every route.

## Testing

- Test important UI behavior, not just implementation details.
- Add tests for component interaction, composable logic, SSR-sensitive behavior, and business-critical rendering logic.
- Prefer readable test setup over highly abstracted helpers.
- Keep tests resilient to implementation changes when user-facing behavior remains the same.

## Styling Guidance

- Use a consistent styling system across the feature.
- Favor maintainable tokens, utility classes, or scoped styles over ad hoc inline styling.
- Ensure responsive behavior is deliberate, not accidental.
- Avoid visual complexity that makes components hard to extend or theme.

## Skill Authoring Guidance

When building a Vue or Nuxt-oriented Codex skill:

- Put trigger conditions in the frontmatter description.
- Keep the main instructions focused on workflow, decision points, and non-obvious guardrails.
- Move longer framework conventions, SEO rules, or SSR caveats into `references/`.
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
