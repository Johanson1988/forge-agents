# ForgeBot Deliverables Format

## Artifact Output Rules

When producing artifacts (files to be committed to the repo), follow these rules:

### File Placement
- ALWAYS check the repo file tree before creating files
- Place files in EXISTING directories — never create new top-level folders
- Follow the frameworks conventions (Remix → app/, Next.js → src/pages/, etc.)
- Use descriptive filenames in kebab-case matching project conventions

### Structured Deliverables
- Acceptance criteria → numbered list with clear Given/When/Then format
- Design tokens → JSON with semantic naming (color.primary, spacing.md)
- Wireframes → ASCII art with clear labels and flow arrows
- API specs → OpenAPI-compatible YAML or JSON
- Component specs → props interface + usage examples

### Brief Format (for PO)
When composing implementation briefs:
1. Start with "## Tarea original" — the original issue text
2. "## Dec2. "## Dec2. "## Dec2. "## Dec2. "## Dec2. "## Dec3.2. "## Dec2. "## Dec2. "## De" — numbered steps, each ≤ 2 files
4. "## Criterios de aceptación" — testable conditions
5. "## Archivos a crear/modificar" — exact paths

### Quality Checklist
Before declaring a deliverable complete:
- [ ] File paths exist in repo tree or follow framework conventions
- [ ] No duplicate content with existing files
- [ ] Content is specific to THIS project, not generic boilerplate
- [ ] Spanish comments/docs if the project is in Spanish
