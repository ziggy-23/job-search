---
name: tailor-cv
description: Tailor Ziggy's CV to one specific job posting by selecting the best 4-5 bullets per role from his experience bank, mirroring the posting's language honestly, and drafting a short cover note and recruiter message. Use when asked to tailor, adapt, or prepare an application for a specific job.
---

# Tailor CV to a posting

Problem being solved: Ziggy has 100+ things he has done per role but a CV fits only 4-5 bullets per role.
The job of this skill is choosing the right ones, in the posting's language, without inventing anything.

## Inputs
- The job posting (URL or pasted text). Fetch it if only a URL is given.
- `data/experience-bank.md` (the master list of everything he has done). If it is thin, ask Ziggy targeted
  questions to fill it before tailoring, one role at a time.

## Steps
0. **Apply the canonical rules** at the top of `data/experience-bank.md` before anything else: SEA Expo wording and numbers, MA dates (2024-2026, or 2024-2027 only for Spanish internships needing a three-way agreement), never include Idiomes Manhattan or British Time outside language-teaching roles, database size (2,261 exact, 2,250+ on a CV), and never present the tools-guide example numbers as Ziggy's own.
1. **Decode the posting.** List the 6-8 things this employer most wants (skills, outcomes, tools, traits).
   Separate must-haves from nice-to-haves. Note keywords to mirror (exact wording matters for ATS filters).
2. **Match.** For each CV role, score every bank bullet against the list. Pick the best 4-5 (fewer for older roles).
   Prefer bullets with a number, a named client/institution, and a clear outcome.
3. **Rewrite.** Rework each chosen bullet as: strong verb + what + how/tool + measurable result, using the
   posting's vocabulary where it is true. Max ~20 words. No filler adjectives.
4. **Honesty check (hard rule).** Every claim must be something Ziggy actually did or can defend in an interview.
   Reframing and emphasis are fine. Invented tools, titles, metrics or dates are not. If a must-have is a
   real gap, do not fake it: put it in a "gaps and how to bridge them" list with a 2-week plan and a
   truthful line for the interview ("I haven't used X in a job, but I did Y which is the same skill").
5. **Headline and summary.** Write a 2-3 line profile that fits this posting specifically.
6. **Skills line.** Reorder so the posting's must-haves come first (only ones he has).
7. **Extras (offer, don't force):** a 120-word cover note, a 60-word message to the recruiter (from the
   report's contact), and 5 likely interview questions with answer angles from the bank.
8. Save outputs to `results/applications/<company>-<role>/` as markdown. If a LaTeX or Word CV is wanted,
   ask for the template first; the user has a separate resume-kit workflow for that.

## Rules
- Never send anything. Drafts only. Ziggy sends.
- Keep the CV to what the reader sees in 10 seconds: the top third must say why he fits this job.
- Spanish or French postings: write the CV and note in that language unless told otherwise.
