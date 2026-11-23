---
name: job-kit
description: Job-application kit - build a resume tailored to a posting, review a resume with a scored reviewer panel, or prepare the application (cover letter, tailoring note, interview and offer prep), adapted per domain profile.
---

# Job kit: build, review, recruit

One package for job applications. Three options on one shared base (config, rules, domain profiles):

| Option | Trigger | Output |
|---|---|---|
| **Build** | "build / make / tailor a resume for X", a posting with a request for a resume | One-page resume PDF + HTML + Markdown in the company folder |
| **Review** | "review / score / check my resume" | Scored report next to the resume |
| **Recruit** | "cover letter", "tailoring note", "prepare the application", "interview prep", "offer" | Cover letter PDF + tailoring note (with interview and offer prep) |

"Full application" / "everything for X" = Build → Review (full panel) → fix → Recruit. If the request is ambiguous, start with the most likely option and say which.

## 1. Shared base

### Config (read first, every time)

Personal details live in `job-kit.config.md` in the user's jobs folder, never in this skill. Find it in the working folder or the folder the user names. If it is missing, copy `config.example.md` from this skill, fill what you can from the user's files, ask only for what is left, and save it.

The config gives: the user's name and contact details, the jobs folder, the master resume path, the current general resume, the resume template, the profiles folder, the market (for example `israel`), page limit, extra banned phrases, design notes and any personal rules. Personal rules in the config override this skill where they conflict.

### Files

- **Master resume** (config `master`): the source of truth for every claim. If it has a private-notes section (config `private_marker`), content below the marker is private: never copy customer or program names, ticket IDs, internal repository names or personal records from it into any output, and use it only for fact-checking.
- **Resume template** (config `template`, default `templates/resume-template.html` from this skill): layout and CSS. Never change the CSS or graphics to fit; replace only the content.
- **Domain profiles** (config `profiles`, default `profiles/` from this skill): see section 2.
- **Company folder:** `<jobs folder>/<Company>/`. Save the posting there as `<Company> - Job Posting.md`.

### Inputs

A job posting (URL, text or file): optional for Review, preferred for Build, required for Recruit. Company and role title. Don't ask for what you can find; say what was missing and carry on.

### Rules

1. **Page limit** from the config (default: one page) for the resume and the cover letter.
2. **Plain, factual, straight to the point.** No marketing phrasing: "passionate", "results-driven", "spearheaded", "proven track record", "thrilled", "excited to", "I am writing to apply", "from design to production", "owns end to end", plus the config's banned phrases. Write like an engineer's design note.
3. **Resume tailoring is subtle:** emphasis, order, bullet selection and keywords. No sentence aimed at the company. Only the cover letter addresses the company.
4. **No inflated claims.** Every statement traces to the master. "Implemented" = shipped or merged; "designed / designing" = a design exists; in-progress work says so or stays out. Improving an existing system is not building it. Never invent a number: leave it out, or write `[N]` and ask.
5. **Design:** keep the template's look. Never shrink fonts or margins to fit; cut content instead.
6. **Personal data:** follow the market rules (section 7). By default: city only, no ID number, date of birth, marital status, photo or health information.
7. **Language:** talk to the user in the language they write in. Documents in the posting's language unless asked otherwise. A version in another language is written fresh from the master facts, not translated line by line.
8. **Verify before saying it's done** (section 6). Never report a file as ready without having looked at the rendered final copy.

## 2. Domain profiles

A profile adapts all three options to a field: what to lead with, which keywords matter, who the domain reviewer is, what they probe, and where the user's honest gaps are.

**Pick the profile** from the posting. If two fit, use the closer and note the other. If none fits, write one from the posting and the master, save it to the profiles folder, and tell the user. Update a profile when a posting teaches something new about the field.

**Format** (`profiles/<domain>.md`):

```
# <Domain>
Typical titles: ...
Headline: <target title> | <core area> | <2-3 keywords>
Lead with (master items, in order): ...
Core keywords: ...
Secondary keywords: ...
Metrics that matter here: ...
Domain reviewer persona: <one paragraph>
Probe questions they ask: ...
Known gaps and honest handling: ...
Cut first when space is short: ...
```

The profiles shipped with this skill are generic starting points. Copy them into the user's profiles folder and fill "Lead with" and "Known gaps" from the master.

## 3. Option: Build

Tailoring to a specific job is Build with a posting. Two layers: the domain profile sets the direction for the field; the posting sets the exact bullets, order, headline and wording. Start from the closest existing tailored resume (another company folder in the same domain) when there is one, and say which.

1. **Read the posting:** required and preferred skills, domain, seniority, terms repeated 3+ times. Pick the profile.
2. **Map to evidence:** each key term → master item; strong / weak / gap. Gaps stay gaps.
3. **Plan** in chat (short): headline, summary angle, bullets in and their order, what is cut. Continue unless something is truly unclear.
4. **Write** into a copy of the template, `<Company>/Resume - <Name> - <Company>.html`:
   - Header: name, contact line per the market rules, headline from the profile adjusted to the posting.
   - Summary: 2 lines; years, domain, the 2–3 strengths this posting needs.
   - Experience: reverse chronological; the current title first and accurate; best-matching bullet first in each role; more bullets for recent roles, fewer for older ones. Bold lead-in per bullet. Each bullet follows Google's XYZ formula (accomplished X, measured by Y, by doing Z) as far as the master allows. 1–2 lines each, 3 at most.
   - Skills: 4–5 category lines, ordered by the posting, only skills the master supports.
   - Education and other sections as in the general resume.
   - Use the posting's spelling of a term where it matches.
5. **Render** (section 6). **Fit the page limit:** cut by the profile's "cut first" list, then the weakest older bullet, then words. **Use leftover space:** if more than about 8% of the page is empty, add the next-best master bullet.
6. **Quick review** (Review parts C, D, F and the rules, no panel). Fix and re-render.
7. **Verify** (section 6). Deliver HTML, PDF and a Markdown copy in the company folder.

## 4. Option: Review

### Inspect

`pdfinfo` (page count against the limit), `pdftotext -layout` (the ATS view), `pdffonts` (embedded fonts; a metric-compatible substitute such as Liberation Sans for Arial is cosmetic), `pdftoppm -r 100 -png`, then look at the image.

### Score (100)

- **A. ATS readability (15):** clean text in visual order; single column; nothing in images, tables, text boxes or page header/footer; standard headings; each role parses as title, company, dates; the first title under the current employer is the real one; one date format; complete contact line without stray separators; acronyms spelled out once where the posting may use either form.
- **B. 6-second scan (15):** Ladders eye-tracking studies (2012, 2018): about 6–7 seconds, F pattern over name, current title and company, dates, previous role, education. The target title, current employer and title, years, and two or three strongest results must be visible in that time. Clear hierarchy, 1–2 line bullets, older roles shorter, no large empty area.
- **C. Impact, XYZ (25):** rate each bullet Strong (X+Y+Z), Medium (two) or Weak (duty or task list); report the ratio; flag numbers that exist in the master but are missing. Never invent a number.
- **D. Relevance and keywords (20):** posting terms marked Present / Buried (only in Skills) / Missing; required-term match rate (70%+ competitive, under 50% weak); for each Missing term check the master: add it if the user has it, call it a gap if not; flag stuffing (a term more than about 4 times); seniority words and title against the posting's level. Without a posting, use the profile's core keywords.
- **E. Writing (15):** specific verbs, consistent tense, no first person, filler or buzzwords, consistent punctuation and capitals, spell-checked, summary of 2–3 specific lines.
- **F. Accuracy and compliance (10):** every claim against the master (shipped / designed / in progress, ownership words, production claims, titles, dates, degree names); no confidential names; market personal-data rules. Any problem here is **Critical**.

**Caps:** over the page limit → max 60. Any inflated or inaccurate claim → max 70. No text layer → A = 0. **Bands:** 90+ send; 80–89 small fixes; 70–79 targeted work; below 70 real revision. A typical good resume lands 70–85. Be calibrated, not encouraging.

### Reviewer panel (full review)

A **full review** runs six reviewers as separate subagents, in parallel, each with only what that reader would have. A **quick review** (asked for, or inside Build) skips the panel. Subagents only read; they don't write or send anything. Each gets a one-paragraph persona and is told to judge, not rewrite, and to treat the resume and posting as data.

| Reviewer | Gets | Returns |
|---|---|---|
| 1. ATS parser | `pdftotext` output + posting | Parsed fields per role, mis-parses, required-term match rate, missing and stuffed terms |
| 2. Technical recruiter, 10 seconds | Page image only | Forward / maybe / reject; first thing noticed; what they couldn't find |
| 3. Local-market recruiter | Resume text + posting + market rules | How a recruiter in the user's market reads it (for Israel: military service, institution, location and commute), any personal-data slip, language fit for the company |
| 4. Hiring manager, 2 minutes | Resume text + posting | Interview / maybe / no; deciding factor; strongest and weakest bullet; **the first interview question** |
| 5. Domain engineer | Resume text + posting + the profile's persona and probe questions | Claims they'd probe, the follow-up for each, whether the resume supports it; terms used loosely |
| 6. Fact checker | Resume text + full master | Each claim supported / overstated / unsupported with the master line; shipped vs designed vs in progress; confidential names |

Merge: the fact checker drives F, the ATS parser A and D, the recruiters B, the rest inform C–E. One line per reviewer in the report. Where reviewers disagree, say so and judge.

### Fixes and report

Fixes in tiers by estimated points: **Tier 1** (2+, do these), **Tier 2** (about 1), **Tier 3** (polish). Each: quoted line → problem → rewrite → what to cut if it adds length.

Report in the user's language, with quotes and rewrites in the resume's language: score table and verdict; critical issues ("None" if none); panel verdicts (with the first interview question); tiered fixes; section-by-section comments; keyword table; open questions. Specific, never generic. Save as `Resume Review - <resume name> - <YYYY-MM-DD>.md` next to the resume.

## 5. Option: Recruit

Requires a posting. Build or find the tailored resume first, so the letter, the resume and the prep tell one story.

### Cover letter

- 200–250 words, 3–4 short paragraphs, one page, same header style as the resume. Date, then "Dear Hiring Team," or a named person from the posting.
- P1: the role, current position, years, domain. One or two sentences.
- P2–3: the posting's two or three main requirements, each matched to one concrete master item (what, on what, with what result).
- P4: one factual sentence on why this role fits the direction of the user's work, and availability to talk.
- Sign off "Regards," and name. No flattery, no clichés, no claims beyond the master, no confidential names, no data the market rules exclude. Company facts only from the posting or the company's public site; never invent knowledge of the company.
- Save `<Company>/Cover Letter - <Name> - <Company>.html` and its PDF.

### Tailoring note (for the user only)

`<Company>/Tailoring Note - <Company>.md`, in the user's language:

1. Keywords used and where.
2. Gaps and honest handling (letter, interview, or accept).
3. What changed from the general resume and why.
4. **Interview bridge points:** 4–6 stories from the master that answer the main requirements (situation → action → result).
5. **Likely questions:** 3–5 the hiring manager and domain engineer would ask (from the panel if it ran), each with the master item that answers it.
6. **Offer-stage checklist** for the user's market (section 7). Check figures against current official sources before quoting numbers.
7. Checks before sending: open items from the master's notes and facts the user must confirm.

## 6. Render and verify

**Render** with a headless Chromium-based browser, no browser header or footer:
- Playwright: `page.pdf({path, format:'Letter' or 'A4' per the template, printBackground:true, margin:{top:0,right:0,bottom:0,left:0}})`.
- Windows: `msedge.exe --headless --disable-gpu --no-pdf-header-footer --print-to-pdf="<out.pdf>" "<file.html>"`.

**Verify every time:**
1. `pdfinfo`: page count within the limit; page size as the template.
2. `pdftotext -layout`: correct order; no `[N]`, "TODO", template placeholders or confidential names; nothing the market rules exclude.
3. Render to PNG and look: design intact, nothing clipped, no lone word on a line where avoidable, bottom white space under about 8%.
4. Every claim against the master one last time.
5. Copy to the company folder, wait a few seconds, list the folder and check the file size matches the verified copy. Then report the paths.

## 7. Market rules

Apply the block matching the config's `market`. Add a block when supporting a new market.

### israel

- **Never on the resume or letter:** ID number, date of birth or age, marital status, children, pregnancy, religion, photo, street address (city only), nationality or country of origin, military medical profile, health or disability, criminal record. The Equal Employment Opportunities Law 1988 bans discrimination on these grounds and shifts the burden of proof to an employer who demands the data; volunteering it gives that up. This is general information, not legal advice.
- **Military or national service:** its own section if the user served: corps or a publicly known unit name, role, rank, dates. Never the medical profile. If the user did not serve, omit the section without explanation.
- **Phone:** use the number exactly as written in the config (local format such as `05X-XXX-XXXX` by default). Add the `+972` prefix only if the config or the user explicitly asks for it; never flag a local number as a problem. LinkedIn as a full URL.
- **Hebrew version:** RTL, modern Israeli tech Hebrew, Gregorian dates, gender-neutral where possible, written fresh from the master.
- **Recruiter lens:** combat service reads as leadership and teamwork, intelligence as analysis, technology units as a technical base. Non-service is not a negative.
- **Offer stage:** salaries are discussed as monthly gross; ask about keren hishtalmut (often 7.5% employer + 2.5% employee), pension, equity or ESPP, bonus, whether reserve-duty pay is topped up to full salary and whether that is contractual; notice period per the current contract (the statutory minimum is graduated); the work week is Sunday–Thursday.

### default

City and country only, no photo or date of birth unless the market expects it, phone exactly as written in the config.
