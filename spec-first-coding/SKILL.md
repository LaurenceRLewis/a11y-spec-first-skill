---
name: spec-first-coding
description: >
  MANDATORY: Read this skill before writing, reviewing, or advising on ANY code involving
  TypeScript, JavaScript, HTML, CSS, SCSS, ARIA, SVG, or web APIs — including snippets,
  components, audits, patterns, and copy-edit responses. Also triggers for any WCAG success
  criterion discussion, AT behaviour question, browser API investigation (Popover, Dialog,
  Anchor Positioning, etc.), or accessibility specification reference. This skill ensures
  Claude consults the correct, current specification before responding — never training-data
  recall alone. Non-negotiable.
metadata:
  author: Laurence Lewis
  version: "1.0"
---

# Spec-First Coding

## Purpose

This skill prevents specification hallucination. Before providing any code, guidance, or
audit output involving the technologies listed below, Claude MUST identify the governing
specification for each relevant technology and surface the normative reference. Claude must
never rely solely on training-data recall for specification details.

---

## Anti-Hallucination Rules (Read First — Override Everything Else)

### Rule 1: No spec recall from memory alone

If a response involves a behaviour, attribute, property, value, pattern, or requirement
governed by a published specification, Claude MUST:

1. Identify the specification and the relevant section or criterion.
2. State it explicitly in the response before providing code or guidance.
3. If web search is available, fetch the current specification to confirm the detail.

Do not paraphrase specifications from training memory as if they are current fact. Training
data has a cutoff; specifications are updated. When in doubt, flag the uncertainty and
recommend the user verify against the live specification.

### Rule 2: Proof-of-spec

For every normative claim, output a spec citation in this format before the code or
guidance:

```
SPEC: [Specification name and version]
Section: [Section number or heading]
Claim: [One-sentence plain-language summary of the normative rule being applied]
Source: [URL — use the canonical URL from the AUTHORITY TABLE below]
```

Multiple specs may apply to a single response. Output one block per specification.

### Rule 3: Conflict between specs

If two specifications appear to conflict (e.g. HTML spec and ARIA spec disagree on an
attribute), surface both, state the conflict plainly, and recommend the more conservative
or user-agent-tested option. Do not silently pick one.

### Rule 4: Version awareness

Always state the specification version being referenced. If the user's context implies a
version constraint (e.g. targeting WCAG 2.1 for a contract, using a specific browser API
at a known support threshold), apply that version and note it.

---

## Authority Table

This table maps each technology to its canonical specification source. Always cite from
these sources. If a URL has changed or a newer version supersedes the one listed, note the
discrepancy and use the current URL.

### Accessibility Standards

| Technology / Topic | Specification | Canonical URL |
|---|---|---|
| WCAG conformance requirements | WCAG 2.2 (W3C Recommendation) | https://www.w3.org/TR/WCAG22/ |
| WCAG 3.0 (draft) | W3C Working Draft | https://www.w3.org/TR/wcag-3.0/ |
| ARIA roles, states, properties | WAI-ARIA 1.2 (W3C Recommendation) | https://www.w3.org/TR/wai-aria-1.2/ |
| ARIA 1.3 (First Public Working Draft — not a Recommendation, do not cite as normative) | WAI-ARIA 1.3 Working Draft | https://www.w3.org/TR/wai-aria-1.3/ |
| ARIA authoring patterns | ARIA Authoring Practices Guide (APG) | https://www.w3.org/WAI/ARIA/apg/ |
| ARIA in HTML mapping | ARIA in HTML | https://www.w3.org/TR/html-aria/ |
| Accessible name computation | Accessible Name and Description Computation 1.2 | https://www.w3.org/TR/accname-1.2/ |
| Role to platform mapping | Core AAM 1.2 | https://www.w3.org/TR/core-aam-1.2/ |
| HTML AAM | HTML AAM | https://www.w3.org/TR/html-aam/ |

### HTML

| Technology / Topic | Specification | Canonical URL |
|---|---|---|
| HTML elements, attributes, semantics | HTML Living Standard (WHATWG) | https://html.spec.whatwg.org/multipage/ |
| Popover API | HTML Living Standard — Popover | https://html.spec.whatwg.org/multipage/popover.html |
| Dialog element | HTML Living Standard — Dialog | https://html.spec.whatwg.org/multipage/interactive-elements.html#the-dialog-element |
| Forms | HTML Living Standard — Forms | https://html.spec.whatwg.org/multipage/forms.html |
| Custom elements | HTML Living Standard — Custom elements | https://html.spec.whatwg.org/multipage/custom-elements.html |

### CSS

| Technology / Topic | Specification | Canonical URL |
|---|---|---|
| CSS Anchor Positioning | CSS Anchor Positioning Level 1 (W3C WD) | https://www.w3.org/TR/css-anchor-position-1/ |
| CSS cascade and specificity | CSS Cascading and Inheritance Level 5 | https://www.w3.org/TR/css-cascade-5/ |
| CSS custom properties | CSS Custom Properties Level 1 | https://www.w3.org/TR/css-variables-1/ |
| CSS Grid | CSS Grid Layout Level 2 | https://www.w3.org/TR/css-grid-2/ |
| CSS Flexbox | CSS Flexible Box Layout Level 1 | https://www.w3.org/TR/css-flexbox-1/ |
| CSS Color | CSS Color Level 4 | https://www.w3.org/TR/css-color-4/ |
| Forced colors / prefers-color-scheme | CSS Color Adjustment Level 1 | https://www.w3.org/TR/css-color-adjust-1/ |
| prefers-reduced-motion | CSS Media Queries Level 5 | https://www.w3.org/TR/mediaqueries-5/ |
| :focus-visible | CSS Selectors Level 4 | https://www.w3.org/TR/selectors-4/ |
| CSS Transitions | CSS Transitions Level 1 | https://www.w3.org/TR/css-transitions-1/ |

### JavaScript / TypeScript / Browser APIs

| Technology / Topic | Specification | Canonical URL |
|---|---|---|
| ECMAScript (JS/TS target) | ECMAScript 2024 (ECMA-262) | https://tc39.es/ecma262/ |
| TypeScript language | TypeScript Handbook (non-normative reference) | https://www.typescriptlang.org/docs/handbook/ |
| DOM API | DOM Living Standard (WHATWG) | https://dom.spec.whatwg.org/ |
| Focus management (focus, blur, focusin) | HTML Living Standard — Focus | https://html.spec.whatwg.org/multipage/interaction.html#focus-management |
| IntersectionObserver | Intersection Observer (W3C WD) | https://www.w3.org/TR/intersection-observer/ |
| MutationObserver | DOM Living Standard — MutationObserver | https://dom.spec.whatwg.org/#mutationobserver |
| ResizeObserver | Resize Observer (W3C WD) | https://www.w3.org/TR/resize-observer/ |

### SCSS / Sass

| Technology / Topic | Specification | Canonical URL |
|---|---|---|
| Sass language and syntax | Sass Documentation | https://sass-lang.com/documentation/ |
| @use / @forward module system | Sass — @use | https://sass-lang.com/documentation/at-rules/use/ |

---

## Workflow

### Step 1: Identify the technologies involved

Before writing a single line of code or guidance, list every technology and topic the
response will address. Example: "This involves: HTML dialog element, ARIA aria-modal,
CSS focus-visible, WAI-ARIA 1.2 dialog role."

### Step 2: Map to specifications

For each technology, identify the governing specification using the Authority Table. If
the technology is not in the table, state this and recommend the user supply the
relevant specification or use web search to locate it.

### Step 3: Output spec citations

Output one SPEC block per specification before the code or guidance. See Rule 2 above.

### Step 4: Apply the specification normatively

Write code or guidance that directly reflects the cited specification. Do not
deviate from normative requirements without flagging the deviation and the reason.

### Step 5: Flag spec gaps and uncertainties

If a behaviour is:
- implementation-defined (varies by browser or AT)
- not yet stable (Working Draft, Candidate Recommendation)
- known to have AT support gaps

State this explicitly alongside the citation. Example:

```
SPEC NOTE: CSS Anchor Positioning is a W3C Working Draft as of this response.
Browser support is partial. Verify current support at https://caniuse.com/css-anchor-positioning
before shipping.
```

---

## WCAG Success Criterion Quick Reference

When referencing a WCAG success criterion, always include:

- The criterion number and short name (e.g. "1.4.13 Content on Hover or Focus")
- The level (A, AA, or AAA)
- The conformance requirement in plain language
- A link to the criterion in WCAG 2.2: `https://www.w3.org/TR/WCAG22/#[fragment]`

Common criterion fragments for accessibility work:

| SC | Name | Fragment |
|---|---|---|
| 1.1.1 | Non-text Content | non-text-content |
| 1.3.1 | Info and Relationships | info-and-relationships |
| 1.4.1 | Use of Color | use-of-color |
| 1.4.3 | Contrast (Minimum) | contrast-minimum |
| 1.4.4 | Resize Text | resize-text |
| 1.4.10 | Reflow | reflow |
| 1.4.11 | Non-text Contrast | non-text-contrast |
| 1.4.12 | Text Spacing | text-spacing |
| 1.4.13 | Content on Hover or Focus | content-on-hover-or-focus |
| 2.1.1 | Keyboard | keyboard |
| 2.1.2 | No Keyboard Trap | no-keyboard-trap |
| 2.4.3 | Focus Order | focus-order |
| 2.4.7 | Focus Visible | focus-visible |
| 2.4.11 | Focus Appearance | focus-appearance |
| 2.5.3 | Label in Name | label-in-name |
| 3.1.1 | Language of Page | language-of-page |
| 3.2.2 | On Input | on-input |
| 3.3.1 | Error Identification | error-identification |
| 3.3.2 | Labels or Instructions | labels-or-instructions |
| 4.1.2 | Name, Role, Value | name-role-value |
| 4.1.3 | Status Messages | status-messages |

---

## Scope

This skill applies to all of the following request types:

- Writing new HTML, CSS, SCSS, TypeScript, or JavaScript
- Reviewing or auditing existing code
- Answering questions about ARIA attributes, roles, states, or properties
- Answering questions about WCAG success criteria
- Investigating native browser API behaviour (Popover, Dialog, Anchor Positioning, etc.)
- Advising on AT (assistive technology) behaviour
- Comparing implementation approaches for accessibility
- Correcting or improving existing code for accessibility conformance

---

## Critical Rules Summary

1. Never cite a specification detail from memory alone without flagging the version and
   recommending verification against the live source.
2. Always output a SPEC block before code or guidance.
3. Always include the specification version.
4. Always flag Working Drafts and Candidate Recommendations as not yet stable.
5. Always flag known AT support gaps alongside the spec citation.
6. If two specs conflict, surface both and state the conflict.
7. If a technology is not in the Authority Table, say so — do not invent a source.