# Prompt log

## 2026-10-09

**What I asked:** Build the repository skeleton, tailor AGENTS.md from the baseline and my resume, write CLAUDE.md, .gitignore and this log, and put my resume into RESUME.md without changing what it says. Show every file before I commit anything.

**What was produced:** The directory skeleton with one-line READMEs in empty folders, README.md as a one-line placeholder (none existed), CLAUDE.md, .gitignore, AGENTS.md tailored to marketing and digital analytics, RESUME.md as Markdown, and this entry.

**What was wrong and how it was caught:** My first message ended before the resume text, and the model noticed the gap, built only the parts that did not depend on it, and asked for the resume. The resume then arrived pasted twice; the two copies read as identical in wording and differ only in spacing, so one was used. The resume has no name or contact header, so none was added. The AGENTS.md data-to-never-paste list was inferred from the resume's roles, so I need to read it and edit it to match what I actually handle.

## 2026-10-09 (second entry, same day)

**What I asked:** Add a header to RESUME.md with my name, email address and LinkedIn link.

**What was produced:** A header at the top of RESUME.md: my name as the title, then the email and the LinkedIn link on one line. Nothing else in RESUME.md changed.

**What was wrong and how it was caught:** Nothing wrong that I found. I checked the top of the file and that the rest was unchanged.

## 2026-10-09 (third entry, same day)

**What I asked:** Remove my email address from the RESUME.md header, because the repository is public, and help me create the repository and commit.

**What was produced:** RESUME.md with the header reduced to my name and LinkedIn link, and steps for creating the repository and committing on github.com.

**What was wrong and how it was caught:** Nothing wrong that I found. I checked that the email appears nowhere else in the repository.
