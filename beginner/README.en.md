# dev-practices · Beginner Edition

A "development mentor" Skill for **complete beginners with zero coding experience**. It is not a dry specification to read on your own, but an AI mentor who **walks you through building a project one step at a time and explains every development rule in plain language**.

## The Problem It Solves

Many beginners want to build a website or an app but get stuck: they don't know where to start, the jargon is confusing, copying tutorials doesn't build understanding, and nothing sticks afterward. With this edition, an AI mentor guides you as you **build a real project with your own hands while genuinely learning development knowledge and rules**.

## How It Works (Core Principles)

1. **One step at a time**: each step is explained, then you do it yourself and confirm before moving on — never an information dump.
2. **Plain language and real-life analogies**: every term is introduced with an everyday analogy (the frontend is a restaurant's dining room, the backend is the kitchen, a Git commit is a game save point).
3. **Code explained line by line**: every piece of code comes with a plain explanation of what each line does, so you copy with understanding.
4. **Learning by doing**: each step ends with a short summary of the key points, tied directly to hands-on work.
5. **A project document as you go**: maintain `PROJECT_JOURNAL.md` from day one, then turn it into a complete project development experience document at the end.
6. **Encouraging debugging**: errors are part of learning; the mentor reads error messages with you, locates the cause, and fixes it together.

## The Guided Path (12 Steps)

0. Before you start: understand software development and prepare your tools
1. Decide what to build: requirements and the feature list
2. Design before coding: pages and data
3. Set up the project: install the environment and initialize
4. Learn to save your work: Git basics
5. Your first frontend page
6. Your first backend API
7. Connecting frontend and backend
8. Checking your own code: testing basics
9. Getting a second pair of eyes: code review basics
10. Making it accessible to everyone: deployment
11. Review and summary: completing the project document

## Default Stack and Sample Project

- Sample project: a **to-do list website** (add, view, mark done, delete).
- Frontend: HTML + CSS + JavaScript (learn the fundamentals first).
- Backend: Node.js + Express.
- Database: SQLite (the whole database is a single file — zero configuration).
- Tools: VS Code, Git / GitHub, and a free hosting platform.

You only need one language (JavaScript) to go full stack, which is ideal for beginners; the mentor also adapts to whatever project you choose.

## Directory Structure

```
beginner/
├── SKILL.md                       # Main entry for mentor mode (role, principles, per-step structure, red lines)
├── README.md                      # Introduction in Chinese
├── README.en.md                   # This file (English)
├── glossary.md                    # Plain-language glossary (Chinese–English)
├── project-journal-template.md    # Project journal template (filled in as you build)
├── guide/                         # 12 step-by-step guides (explanations, actions, checks, key points, journal prompts)
└── checkpoints/
    └── step-checkpoints.md        # Minimal completion check for each step
```

## Quick Start

1. Have the AI load `SKILL.md` in this directory (or install the entire `beginner/` folder as a Skill).
2. Simply tell the AI: "I have no coding experience and want to build a project from scratch. Please guide me step by step."
3. Tell your mentor what you'd like to build (or start with the to-do list example), then follow each step.
4. In step 0, create your `PROJECT_JOURNAL.md` and start recording the journey.

## What You'll Take Away

- A full-stack project you built yourself and can deploy online.
- A genuine understanding of the complete software development lifecycle and its basic rules.
- A project document capturing the whole experience, ready to use as a portfolio piece.

## Relationship to the Standard Edition

The `dev-practices` edition at the repository root (SKILL.md + rules/ + checklists/) is a concise, executable team standard for experienced developers. This `beginner/` edition is for newcomers and emphasizes teaching and guidance. Once you've worked through the beginner edition, the standard edition becomes your everyday reference.

## License

MIT; see the LICENSE file at the repository root.
