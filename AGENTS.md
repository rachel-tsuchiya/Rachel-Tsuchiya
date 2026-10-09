# AI conventions

## About this repository
Rachel Tsuchiya's public GitHub portfolio for a graduate business course. My field is marketing, with a digital analytics focus: web and social performance analysis, market and competitive research, audience segmentation, and customer journey mapping.
Canonical file: AGENTS.md. CLAUDE.md points here.

## Where things are
- capabilities/<capability>/  a capability, with its spec and model
- docs/briefs/          written BEFORE work: scope + hypothesis
- docs/decisions/       written AFTER work: recommendations
- analysis/             findings and figures
- data/                 sourced inputs, with provenance

## Naming
- The directory matters most. A file in the wrong folder is harder to find. If you are not certain which folder a file belongs in, ask me
  before you write it — do not choose for me.
- Graded files use the exact filename the stage brief gives — lowercase,
  hyphens, no spaces. Dated documents are YYYY-MM-DD-slug-type.md (no name — the repo is yours);
  the stage page says so when they do.
- Slugs name the engagement, never the week, the course, or the assignment
  number.
- Never invent a path or a filename. I will give you the exact one.

## How I work
- Explain concepts fully and walk the worked example. Do not hand me conclusions.
- Explain analytics and statistics concepts in marketing terms (funnels, segments, conversion, engagement), and show the arithmetic step by step.
- Critique my reasoning directly. I would rather be corrected than agreed with.
- When you are uncertain, say so and say what would resolve it.

## What you may and may not draft
- You MAY explain, critique, debug, quiz me, and draft mechanical files.
- You MAY NOT write my briefs, analyses, memos, or reflections.
- You MAY review my README.md bio but never draft it.
- Every statistic or figure you give me is a draft until I verify it against a source.

## Documentation
When work changes, update the document that describes it in the same commit.
A capability's README names the engagements that exercised it — keep that current.

## Scope
Do the work I asked for. If you notice something worth doing that I did not ask
for, tell me instead of doing it.

## Commits
Descriptive messages: what changed and why. Never "update" or "stuff".

## Prompt log
At the end of every session that changed a file, append one entry to prompt-log.md: the date, what I asked, what you produced, what was wrong and how it was caught. Never backfill earlier sessions and never edit a past entry.

## Never include
No credentials, no API keys, no personal data about anyone, no licensed or
copyrighted material. If I paste something that fits that description, stop and
tell me rather than committing it.

## Never paste into a model (from my work)
This list also governs what goes in the repository. If it would not be safe in a public repo, it does not go in a chat window.
- Servco Pacific: Google Analytics 4, Microsoft Clarity, or Databricks exports, session recordings, or customer-level data; Google Business Profile account access; non-public competitive analyses, audience segments, journey maps, or campaign plans.
- Becker Communications: client performance metrics from email, Google, or social platforms; the Excel reports and quarterly client presentations; unreleased sponsorship or event-partnership research.
- Sprout Social or any other platform: logins, tokens, account exports, or private message and audience data.
- CINO: guest names, contact details, reservations, seating charts, and guest complaints or reviews tied to an identifiable person.
- American Marketing Association: member rosters and contact details, mock-interview participant information, corporate partner contacts, and chapter financial records.
- Kaulukoa Volleyball Institute: names, ages, or contact details of players (who are minors) or their parents.
- Anything covered by an employer's confidentiality agreement, whatever the source. When in doubt, use made-up or heavily aggregated data and tell me you did.

## Mistakes to avoid (append to this list)
Record errors here as they happen, so the same one does not repeat.
- (empty — add the first one when it happens)
