# dev-practices

A full-lifecycle development standard for teams (frontend · backend), distributed as a Skill for both engineering teams and AI coding assistants to follow. The repository contains **two editions**: a standard edition for experienced developers and a mentor edition for complete beginners.

## What's Inside

### 1. Standard Edition (repository root)

- **SKILL.md**: the main Skill entry (description, usage, red lines, file index).
- **rules/**: executable rules organized by development stage (process, architecture, Git, structure, environment, frontend, backend, database, review, testing, CI/CD, docs, security, AI assistance, observability, collaboration — 16 files).
- **checklists/**: ready-to-use checklists (new project, local self-check, PR review, DoD, release — 5 files).

### 2. Beginner Edition (beginner/)

A "development mentor" for people with zero coding experience: one step at a time, plain-language explanations, code explained line by line, and learning by doing — while guiding learners to keep a project journal and finish with a project development experience document. See [`beginner/README.en.md`](beginner/README.en.md).

```
beginner/
├── SKILL.md                    # Main entry for mentor mode
├── guide/                      # 12 step-by-step guides
├── checkpoints/                # Per-step completion checks
├── glossary.md                 # Plain-language glossary
└── project-journal-template.md # Project journal template
```

## Which Edition Should I Use?

| Your situation | Recommended edition |
| --- | --- |
| Experienced developer needing a team standard and quick references | Standard edition (root) |
| Complete beginner who wants step-by-step guidance while learning by doing | Beginner edition (beginner/) |

## How to Use

- Install as a Skill: place the relevant folder in your agent's skill root directory, or reference its `SKILL.md` directly.
- As a team standard: organize team documentation around `rules/` and `checklists/`, and maintain it over iterations.
- For beginner learning: load `beginner/SKILL.md`, tell the AI what you want to build, and follow each step.

## Sources

Compiled with reference to public engineering practices, as attribution:

- Google Engineering Practices (code review)
- elsewhencode/project-guidelines (project-wide best practices)
- Microsoft Code-with Engineering Playbook (engineering fundamentals and checklists)
- CISA Development Guide (engineering toolchain and security)
- Microsoft REST API Guidelines (API design)
- Conventional Commits (commit message conventions)
- OWASP Top 10 (web security baseline)
- Google Core Web Vitals (frontend performance metrics)

## Documentation Languages

- Chinese: README.md, beginner/README.md
- English: this file (README.en.md), beginner/README.en.md

## License

Released under the MIT License (see [LICENSE](LICENSE)).
