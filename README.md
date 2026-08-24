# Fillmore

Drafts job applications. Takes the monotony out of retyping the same name, address, and education
on every form, and puts the effort where it counts — which resume to send, and how the free-text
questions get answered.

**It does not submit anything on its own.** Every application is drafted as an editable file
first. You read it, edit it, and approve it. Then it gets typed into the form.

## Setup

Requires Node (installed via `brew install node`).

```bash
npm install -g @playwright/cli@latest
```

Then create your private files from the templates. All four live in gitignored paths:

```bash
mkdir -p profile resumes
cp profile.example.yaml       profile/profile.yaml
cp answers.example.yaml       profile/answers.yaml
cp voice.example.md           profile/voice.md
cp resumes.index.example.yaml resumes/index.yaml
```

Fill them in, drop your resume PDFs into `resumes/`, and describe each one in `resumes/index.yaml`
so the right version gets picked per posting.

`profile/voice.md` matters more than it looks. It holds samples of your actual writing, which is
what keeps drafted answers from sounding like every other application in the pile.

## Use

Paste a job URL and ask to apply. What happens:

1. **Intake** — scrapes the posting, checks `log.md` so you don't apply twice.
2. **Resume** — recommends one with reasoning, and always asks whether you'd rather supply a more
   tailored version.
3. **Recon** — inventories every field on every page. Nothing typed yet.
4. **Draft** — writes `review.md`: every field, the question, the proposed value, plus drafted
   free-text answers and a list of anything needing your hands.
5. **You review** — edit `review.md` directly. Still nothing typed.
6. **Fill** — uploads the resume first (ATS parsers prefill from it, badly), then fills your
   approved values and verifies each one landed.
7. **Submit gate** — screenshot, then it asks. Default is that you click Submit yourself.

## What it won't do

Some of this is principle, some is hard limitation. Either way these come back to you:

- Creating accounts or entering passwords — Workday needs one per employer
- CAPTCHAs
- SSN, driver's license, passport, bank details, signatures
- Submitting without your explicit approval, per application
- **Claiming anything not in your profile or resume.** You're the one who has to defend it in the
  interview.
- Guessing at EEO questions — those default to "prefer not to answer" unless you set otherwise
- **LinkedIn Easy Apply** — automating it violates their ToS and risks your account

Blockers get collected into one list in `review.md` rather than interrupting you field by field.

## Supported platforms

Greenhouse, Lever, and Ashby work best — clean forms, often no login. Workday, iCIMS, and Taleo
work but involve more handoffs (accounts, timeouts, CAPTCHAs).

## Layout

```
profile/     your data          — gitignored
resumes/     PDFs + index.yaml  — gitignored
applications/<date>-<company>-<role>/
             posting.md, review.md, status.md — gitignored
log.md       master tracker     — gitignored
```

Git tracks only the tooling and the example templates. Nothing personal is ever committed —
`review.md` contains your address and phone as literal field values, so it's excluded along with
everything else.

See `CLAUDE.md` for the full operating rules.
