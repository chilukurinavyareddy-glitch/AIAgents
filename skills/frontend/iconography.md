# Frontend Skill: Iconography

## Purpose

Ensure UI implementations preserve the project's icon language and do not replace visual icons with placeholder text.

## Rules

- Discover the project's configured icon library before adding UI icons.
- If the project context specifies Font Awesome, use Font Awesome classes consistently.
- Match mockup icon placement, size, tone, and semantic intent where practical.
- Do not expose internal icon labels as visible UI text.
- Do not use text shortcuts such as `S`, `C`, `OK`, `Prev`, `Next`, `Sh`, or `P` when the mockup shows icons.
- Decorative icons must use `aria-hidden="true"`.
- Icon-only buttons must have an accessible label on the parent control.
- Keep icon usage reusable and centralized when the same mapping appears in multiple components.

## QA Checklist

- Icons render in desktop, tablet, and mobile views.
- Icons are not clipped or replaced by missing-font squares.
- Action icons match the action meaning.
- Status/trust icons match the product visual language.
- Placeholder text is not used where an icon is expected.
- Accessibility labels are present for icon-only controls.
