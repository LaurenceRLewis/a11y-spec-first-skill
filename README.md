# Spec-First Coding

**A prompt instruction file for AI coding assistants that enforces specification-grounded responses for web accessibility and front-end code.**

Authored by [Laurence Lewis](https://github.com/laurencelewis) — Accessibility Senior Specialist.

---

## The Problem

AI coding assistants often generate HTML, CSS, ARIA, and JavaScript from training-data recall alone. Specifications change. Browser behaviour diverges from older spec versions. ARIA patterns documented in training data may be superseded by WAI-ARIA 1.2 or 1.3. The result is plausible-sounding code that fails WCAG conformance or contradicts the current normative specification.

This instruction file forces the AI to identify and cite the governing specification for every technology it references — before writing a single line of code.

---

## What It Does

When active, the AI must:

1. List every technology involved in the response (HTML, ARIA, CSS, etc.)
2. Map each to its canonical specification using the built-in Authority Table
3. Output a structured `SPEC:` citation block before any code or guidance
4. Apply the specification normatively in the response
5. Flag anything that is a Working Draft, has known AT support gaps, or conflicts with another specification

### Example output

```
SPEC: WAI-ARIA 1.2
Section: 6.6.11 — dialog (role)
Claim: A dialog element must have an accessible name provided via aria-label or aria-labelledby.
Source: https://www.w3.org/TR/wai-aria-1.2/#dialog

SPEC: HTML Living Standard
Section: The dialog element
Claim: The native <dialog> element carries an implicit role of "dialog" and does not require an explicit ARIA role attribute.
Source: https://html.spec.whatwg.org/multipage/interactive-elements.html#the-dialog-element
```

---

## Covered Specifications

### Accessibility

- WCAG 2.2 (W3C Recommendation)
- WCAG 3.0 (W3C Working Draft)
- WAI-ARIA 1.2 (W3C Recommendation)
- WAI-ARIA 1.3 (First Public Working Draft — informational reference only)
- ARIA Authoring Practices Guide (APG)
- ARIA in HTML
- Accessible Name and Description Computation 1.2
- Core Accessibility API Mappings 1.2
- HTML Accessibility API Mappings

### HTML

- HTML Living Standard (WHATWG) — including Popover API, Dialog, Forms, Custom Elements, Focus Management

### CSS

- CSS Anchor Positioning Level 1
- CSS Cascade Level 5
- CSS Custom Properties Level 1
- CSS Grid Layout Level 2
- CSS Flexible Box Layout Level 1
- CSS Color Level 4
- CSS Color Adjustment Level 1 (forced colors, prefers-color-scheme)
- CSS Media Queries Level 5 (prefers-reduced-motion)
- CSS Selectors Level 4 (:focus-visible)
- CSS Transitions Level 1

### JavaScript / TypeScript / Browser APIs

- ECMAScript 2024 (ECMA-262)
- TypeScript Handbook
- DOM Living Standard (WHATWG)
- Intersection Observer, MutationObserver, Resize Observer

### SCSS / Sass

- Sass Documentation (language and @use / @forward module system)

---

## Installation

### Claude (claude.ai)

1. Download `spec-first-coding.skill` from [Releases](../../releases).
2. In Claude, open **Settings** and navigate to **Skills**.
3. Upload the `.skill` file.
4. The instruction set will activate automatically for any conversation involving the covered technologies.

### GitHub Copilot (VS Code)

1. Copy the contents of `spec-first-coding/SKILL.md` into a file named `.github/copilot-instructions.md` at the root of your repository.
2. Copilot will apply the instructions to all chat and inline suggestions within that repository.

Reference: [GitHub Copilot — repository custom instructions](https://docs.github.com/en/copilot/customizing-copilot/adding-repository-custom-instructions-for-github-copilot)

### GitHub Copilot (organisation-wide)

1. In your GitHub organisation settings, navigate to **Copilot** and then **Policies**.
2. Add the contents of `SKILL.md` as a custom instruction set applied to all repositories.

### Other LLMs (ChatGPT, Gemini, Mistral, etc.)

The `SKILL.md` file is plain Markdown. It can be used as a system prompt or pasted at the start of any conversation:

1. Open `spec-first-coding/SKILL.md`.
2. Copy the full contents.
3. Paste as the system prompt (if your interface supports it) or as the first message in the conversation before asking your question.

For persistent use, most LLM platforms that support custom instructions (e.g. ChatGPT's **Custom Instructions** feature) allow you to paste the content of `SKILL.md` directly into the system instruction field.

---

## Repository Structure

```
wcag-spec-first-coding-skill/
├── README.md
├── LICENSE
└── spec-first-coding/
    └── SKILL.md          # The instruction file — works as a Claude skill or plain system prompt
```

---

## Contributing

Contributions are welcome. If a specification URL has changed, a new W3C Recommendation has been published, or a technology is missing from the Authority Table, please open an issue or submit a pull request.

When contributing, please include:
- The specification name and version
- The canonical URL
- The technology or topic it governs

---

## Versioning

This project follows [Semantic Versioning](https://semver.org/):
- **MAJOR** version for breaking changes to the instruction format or workflow
- **MINOR** version for new specifications or authority table entries
- **PATCH** version for URL corrections and clarifications

---

## License

MIT License. See [LICENSE](./LICENSE) for details.

You are free to use, adapt, and redistribute this instruction file in personal and commercial projects, including embedding it in your own tooling, repositories, or AI assistant configurations.

---

## Author

**Laurence Lewis** — Accessibility Senior Specialist

Feedback and issues welcome via [GitHub Issues](../../issues).