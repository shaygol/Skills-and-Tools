# job-kit

A Claude skill for job applications. One package, three options:

- **Build:** a resume tailored to a job posting, from your master resume, in your own design, fitted to your page limit.
- **Review:** a 100-point score (ATS readability, 6-second scan, XYZ impact, keyword match, writing, accuracy) and, for a full review, a panel of six reviewers run as subagents: ATS parser, technical recruiter, local-market recruiter, hiring manager, domain engineer and fact checker.
- **Recruit:** a short cover letter and a private tailoring note with keywords, gaps, interview stories, likely questions and an offer-stage checklist.

Every claim is checked against your master resume. The skill never invents numbers and keeps shipped, designed and in-progress work apart.

## Layout

| Path | What it is |
|---|---|
| `SKILL.md` | The skill |
| `config.example.md` | Template for your personal config |
| `templates/resume-template.html` | One-page resume design with placeholder content |
| `profiles/` | Generic domain profiles (networking, embedded, systems C/C++, AI infrastructure) |

## Setup

1. Install the skill: copy this folder into your skills directory (for Claude Code, `~/.claude/skills/job-kit/`), or upload it as a skill in Claude.
2. In your jobs folder, create `job-kit.config.md` from `config.example.md`.
3. Write a master resume: every fact you might use, in Markdown. Optional private notes go below the marker line set in the config.
4. Copy `profiles/` into your jobs folder and fill in "Lead with" and "Known gaps" for the fields you apply to.
5. Optional: copy `templates/resume-template.html` and adjust the design once.

Then ask, for example: "Build a resume for this posting", "Review my resume", or "Prepare the application for Company X".

## Requirements

- poppler-utils (`pdfinfo`, `pdftotext`, `pdffonts`, `pdftoppm`) for checks.
- A headless Chromium (Playwright, Chrome or Edge) to render HTML to PDF.

## Markets

Market rules live in `SKILL.md` section 7. `israel` covers personal data that stays off a CV, the military-service section, Hebrew versions and offer-stage items.

The legal notes are general information, not legal advice.
