# AI Development Skills

Reusable Codex skills for writing cleaner, more maintainable, secure, and
accessible software.

Each skill provides focused instructions and supporting references that Codex
loads when the task matches the skill's purpose. Use them independently or
combine them when a change spans multiple concerns.

## Available skills

| Skill | Use it for | Main focus |
| --- | --- | --- |
| [`clean-code`](clean-code/SKILL.md) | Designing, implementing, or refactoring code in any language | Readability, meaningful names, small functions, DRY, KISS, and YAGNI |
| [`de-slop-code`](de-slop/de-slop-code/SKILL.md) | Reorganizing oversized or tightly coupled production code | Cohesive, feature-oriented components with behavior preserved |
| [`de-slop-tests`](de-slop/de-slop-tests/SKILL.md) | Splitting and reorganizing oversized test suites | Maintainable test structure with coverage and assertions preserved |
| [`better-ui`](ui/better-ui/SKILL.md) | Designing, reviewing, or refactoring user interfaces | Visual hierarchy, consistency, forms, and WCAG 2.1 AA accessibility |
| [`sec-ops`](sec-ops/SKILL.md) | Designing, implementing, or reviewing security-sensitive software | Secure-by-design practices, threat modeling, OWASP risks, and practical mitigations |

`de-slop-code` changes production-code structure and leaves tests alone.
`de-slop-tests` changes test structure and never modifies production code.

## Install for Codex

Clone the repository and link the skills you want into
`~/.codex/skills`:

```bash
git clone https://github.com/yorevs/ai-dev-skills.git
cd ai-dev-skills

mkdir -p ~/.codex/skills

ln -s "$PWD/clean-code" ~/.codex/skills/clean-code
ln -s "$PWD/de-slop/de-slop-code" ~/.codex/skills/de-slop-code
ln -s "$PWD/de-slop/de-slop-tests" ~/.codex/skills/de-slop-tests
ln -s "$PWD/ui/better-ui" ~/.codex/skills/better-ui
ln -s "$PWD/sec-ops" ~/.codex/skills/sec-ops
```

The links keep installed skills synchronized with the repository. After
pulling an update, Codex uses the updated instructions without another
installation step.

Open a new Codex turn after linking a skill. If it is not discovered, restart
Codex.

### Install a single skill

From the repository root, create only the link you need:

```bash
ln -s "$PWD/sec-ops" ~/.codex/skills/sec-ops
```

The command intentionally fails when a file or link already exists at the
destination, avoiding accidental replacement.

## Usage

Codex can select a skill automatically from its description. You can also
request one explicitly by name:

```text
Use $clean-code to refactor this module without changing its behavior.

Use $de-slop-code to split this service into cohesive feature components.

Use $de-slop-tests to reorganize this test suite without changing production code.

Use $better-ui to review this form for hierarchy, consistency, and accessibility.

Use $sec-ops to audit this API and classify each finding by severity.
```

Skills can be combined when their responsibilities overlap:

```text
Use $clean-code and $sec-ops to refactor this authentication flow while
preserving behavior and improving its security posture.
```

## Repository structure

```text
ai-dev-skills/
├── clean-code/
│   ├── SKILL.md
│   └── references/
├── de-slop/
│   ├── de-slop-code/
│   │   ├── SKILL.md
│   │   └── references/
│   └── de-slop-tests/
│       ├── SKILL.md
│       └── references/
├── sec-ops/
│   ├── SKILL.md
│   └── references/
└── ui/
    └── better-ui/
        ├── SKILL.md
        └── references/
```

Every skill has a `SKILL.md` containing:

- YAML frontmatter with the skill name and trigger description.
- The workflow and rules Codex follows after the skill is selected.
- Links to supporting material under `references/`, when needed.

## Contributing

Keep each skill focused on one responsibility, make its trigger description
specific, and place detailed examples or domain guidance in `references/`
instead of expanding `SKILL.md` unnecessarily.

When changing an existing skill, preserve its stated boundaries and verify
that every referenced file exists before opening a pull request.
