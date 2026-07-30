---
name: better-ui
description: Use when designing, coding, refactoring, or, updating UI code of ANY language. This guide is to analyze, write, and refactor code adhering strictly to established clean ui design principles.
---

# Better UI Skill

The goal of this skill is to adhere to clean ui design principles to evaluate, design, and refactor user interfaces by applying objective, logic-driven UI principles and accessibility guidelines. You prioritize clarity, accessibility, consistent interaction patterns, and visual harmony over purely subjective aesthetic choices.

See:

  - `references/example-1.png`
  - `references/example-2.png`

---

# Core UI Design Principles to Enforce

## Page elements, fonts, colors, styles, ...

### 1. Structure, Spacing & Layout
- **Use Space to Group Related Elements:** Group information using proximity, continuous alignment, and common containers. Avoid clutter—rely on white space rather than heavy borders or background containers to establish relationships.
- **Left-Align Text for Readability:** Align body text to the left to align with natural F-shaped scanning patterns (LTR languages). Avoid center-aligning long paragraphs or justifying text.
- **Maintain Comfortable Line Heights:** Set body text line height to at least 1.5 (150%) to prevent line-skipping and improve readability.


### 2. Visual Hierarchy & Simplicity
- **Create a Clear Order of Importance:** Guide the user's eye by varying size, contrast, weight, and depth. The primary call-to-action (CTA) must always be the most prominent element on the screen.
- **Pass the Squint / Blur Test:** Crucial actions and primary information must remain recognizable even when the screen is blurred or viewed from a distance.
- **Remove Unnecessary Styles:** Strip away gratuitous borders, heavy drop shadows, redundant containers, and decorative background shapes to reduce cognitive load.
- **Follow the KISS & YAGNI Principles:** Keep layouts simple and avoid adding speculative UI elements, extra controls, or decorative visual noise that doesn't serve a clear user goal.


### 3. Typography & Text Standards
- **Use a Single Sans-Serif Typeface:** Prefer neutral, highly legible sans-serif typefaces (e.g., Inter, Roboto) over complex serif or display fonts for user interfaces.
- **Choose Typefaces with Tall x-Height:** Select typefaces with larger lowercase letters and generous letter-spacing to maintain legibility at small sizes.
- **Limit Font Weights:** Restrict the type system primarily to `Regular` and `Bold` (or `Semi-Bold`). Avoid using ultra-light, thin, or black font weights for body text or functional labels.
- **Limit Uppercase:** Use sentence case by default. Reserve uppercase strictly for very short labels or badges, as standard word shapes improve reading speed.
- **Avoid Pure Black Text:** Use dark grey (e.g., `#1E1E1E` or `#2C2C2C`) on light backgrounds instead of `#000000` to prevent harsh contrast and eye strain.


### 4. Color, Contrast & Accessibility (WCAG 2.1 AA)
- **Use Color Purposefully:** Apply brand and primary colors deliberately—primarily to signal interactive elements (links, active buttons). Keep non-interactive elements neutral to avoid false affordances.
- **Maintain Interface Element Contrast (3:1 Minimum):** Form fields, icons, button boundaries, and graphical controls must maintain at least a 3:1 contrast ratio against their background.
- **Maintain Text Contrast (4.5:1 Minimum):** Small text (18px and under) requires at least a 4.5:1 contrast ratio. Large text (above 18px bold / 24px regular) requires at least 3:1.
- **Never Rely on Color Alone:** Always pair color indicators with secondary cues (e.g., text labels, icons, or underlines for links) to support color-blind users.

### 5. Consistency & Functional Affordance
- **Maintain Visual & Interaction Consistency:** Ensure icons, button shapes, and control styles are visually uniform across the entire app (e.g., consistent icon stroke weight, fill rules, and corner radii).
- **Match Visual Design to Functionality:** Elements that look similar must behave similarly. Non-interactive elements (e.g., informational badges or static icons) should never share button styling, interactive colors, or hover cues.

Here is a summarized list of key form design hints based on Andrew Coyle's article:

## Forms

* **Use a single column:** Multi-column layouts disrupt vertical momentum. Single-column forms are easier to scan and complete faster.
* **Top-align labels:** Top-aligned labels lead to faster completion rates and scale better on mobile screens. *(Exception: Left-align labels for dense, data-heavy forms where scanning inputs side-by-side helps reduce overall page height).*
* **Group labels closely with their inputs:** Keep a label and its corresponding field close together, and leave clear spacing between separate fields to avoid confusion.
* **Group related fields logically:** Break long forms into logical sections or batches so they don't feel overwhelming.

### Options & Selections

* **Show all options if 5 or fewer:** Avoid drop-down menus for small sets of options (use radio buttons or checkboxes instead). Use drop-downs for 6+ options, and add contextual search if there are more than 25.
* **Stack checkboxes and radio buttons vertically:** Vertical stacking makes options much faster and easier to scan than horizontal arrangements.

### Labels & Microcopy

* **Don't use placeholder text as labels:** Placeholders fade when users type, which causes usability issues. Keep labels visible above the field.
* **Avoid ALL CAPS:** Title case or sentence case is much easier to read and scan than uppercase text.
* **Mark optional fields instead of required ones:** Drop the required asterisk (`*`) and explicitly label the few fields that are "(optional)".
* **Make CTAs descriptive:** Use specific, intent-driven button text (e.g., "Create Account") rather than generic words like "Submit".
* **Keep basic helper text visible:** Avoid hiding essential instructions behind tooltips; show basic helper text directly on screen.

### Validation & Inputs

* **Specify errors inline:** Show errors directly next to the field where they occurred, accompanied by a clear explanation.
* **Validate after completion:** Trigger inline validation *after* the user finishes typing or leaves the field (unless real-time feedback actively helps during input, such as password strength or character counts).
* **Match field length to expected input:** Adjust the input field width to match the length of expected answers (e.g., zip codes, phone numbers).

### General Best Practices

* **Differentiate actions:** Clearly distinguish the primary action from secondary options (or eliminate secondary options altogether).
* **Omit unnecessary fields:** Always ask if a field can be excluded, postponed, or inferred automatically.
* **Automate data entry where possible:** Leverage autofill, location data, biometrics, OCR, or conversational interfaces to reduce manual typing.
* **Symmetry is beauty:** Keep elements consistently aligned and the same size whenever possible. Use 1rem for margins by default unless otherwise specified.

---


# Execution Workflow

When reviewing, critiquing, or generating UI layouts or code (HTML/Tailwind/CSS, React, Figma specs):

1. **Audit & Diagnostics:** Evaluate the interface against the principles above. Identify specific usability and visual smells (e.g., low contrast, crowded spacing, non-interactive elements styled like buttons, missing visual hierarchy).
2. **Refactored Solution:** Provide the improved UI layout, Tailwind CSS code, or detailed design specs.
3. **Design Rationale:** Explain the key changes, explicitly linking each modification back to the specific UI principle or WCAG requirement applied.